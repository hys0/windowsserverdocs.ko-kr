---
title: 가상 컴퓨터 리소스 컨트롤
description: VM CPU 그룹 사용
author: allenma
ms.date: 06/18/2018
ms.topic: article
ms.prod: windows-server
ms.service: windows-10-hyperv
ms.assetid: cc7bb88e-ae75-4a54-9fb4-fc7c14964d67
ms.openlocfilehash: ebb5f9a0ca9c50a5e5357e3dd2c755095da98d11
ms.sourcegitcommit: 32f810c5429804c384d788c680afac427976e351
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83203534"
---
# <a name="virtual-machine-resource-controls"></a>가상 컴퓨터 리소스 컨트롤

> 적용 대상: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

이 문서에서는 가상 컴퓨터에 대 한 Hyper-v 리소스 및 격리 컨트롤을 설명 합니다.  가상 컴퓨터 CPU 그룹 또는 "CPU 그룹"을 지칭 하는 이러한 기능은 Windows Server 2016에서 도입 되었습니다.  Hyper-v 관리자는 CPU 그룹을 사용 하 여 게스트 가상 컴퓨터에서 호스트의 CPU 리소스를 보다 효율적으로 관리 하 고 할당할 수 있습니다.  Hyper-v 관리자는 CPU 그룹을 사용 하 여 다음을 수행할 수 있습니다.

* 각 그룹이 전체 그룹에서 공유 되는 가상화 호스트의 총 CPU 리소스에 대해 서로 다른 할당을 갖는 가상 컴퓨터 그룹을 만듭니다. 이를 통해 호스트 관리자는 다양 한 유형의 Vm에 대 한 서비스 클래스를 구현할 수 있습니다.

* 특정 그룹에 대 한 CPU 리소스 제한을 설정 합니다. 이 "그룹 캡"은 전체 그룹이 소비할 수 있는 호스트 CPU 리소스의 상한을 설정 하 여 해당 그룹에 대해 원하는 서비스 클래스를 효과적으로 적용 합니다.

* 특정 호스트 시스템 프로세서 집합 에서만 실행 되도록 CPU 그룹을 제한 합니다. 이는 서로 다른 CPU 그룹에 속하는 Vm을 격리 하는 데 사용할 수 있습니다.

## <a name="managing-cpu-groups"></a>CPU 그룹 관리

CPU 그룹은 Hyper-v 호스트 계산 서비스 또는 HCS를 통해 관리 됩니다. HCS, genesis, HCS Api에 대 한 링크 등에 대 한 유용한 설명은 [HCS (호스트 계산 서비스)를 소개](https://blogs.technet.microsoft.com/virtualization/2017/01/27/introducing-the-host-compute-service-hcs/)하는 게시의 Microsoft 가상화 팀 블로그에서 확인할 수 있습니다.

>[!NOTE]
>HCS만 CPU 그룹을 만들고 관리 하는 데 사용할 수 있습니다. Hyper-v 관리자 애플릿, WMI 및 PowerShell 관리 인터페이스는 CPU 그룹을 지원 하지 않습니다.

Microsoft에서는 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?linkid=865968) 에서 HCS 인터페이스를 사용 하 여 CPU 그룹을 관리 하는 명령줄 유틸리티인 cpugroups를 제공 합니다.  이 유틸리티는 호스트의 CPU 토폴로지를 표시할 수도 있습니다.

## <a name="how-cpu-groups-work"></a>CPU 그룹의 작동 방식

CPU 그룹 전체의 호스트 계산 리소스 할당은 CPU 그룹의 계산을 통해 Hyper-v 하이퍼바이저에 의해 적용 됩니다. Cpu 그룹 캡은 CPU 그룹의 총 CPU 용량 중 일부입니다. 그룹의 상한 값은 그룹 클래스 또는 할당 된 우선 순위 수준에 따라 달라 집니다. 계산 된 그룹 캡은 "많은 LP의 CPU 시간"으로 간주할 수 있습니다. 이 그룹 예산은 공유 되므로 단일 VM만 활성 상태 이면 전체 그룹의 CPU 할당을 사용할 수 있습니다.

CPU 그룹 캡은 G = *n* x *C*로 계산 됩니다. 여기서는 다음과 같습니다.

    *G* is the amount of host LP we'd like to assign to the group
    *n* is the total number of logical processors (LPs) in the group
    *C* is the maximum CPU allocation — that is, the class of service desired for the group, expressed as a percentage of the system's total compute capacity

예를 들어 LPs (4 개의 논리적 프로세서)로 구성 된 CPU 그룹 및 50%의 캡을 가정 합니다.

    G = n * C
    G = 4 * 50%
    G = 2 LP's worth of CPU time for the entire group

이 예제에서 CPU 그룹 G에는 두 가지 LP의 CPU 시간이 할당 됩니다.

그룹에 바인딩된 가상 컴퓨터 또는 가상 프로세서의 수에 관계 없이 그룹에 적용 되는 것은 CPU 그룹에 할당 된 가상 컴퓨터의 상태 (예: 종료 또는 시작 됨)에 관계 없이 적용 됩니다. 따라서 동일한 CPU 그룹에 바인딩된 각 VM은 그룹의 총 CPU 할당에 대 한 분수를 수신 하며,이는 CPU 그룹에 바인딩된 Vm 수에 따라 변경 됩니다. 따라서 Vm이 CPU 그룹에서 바인딩되거나 바인딩되지 않은 Vm 인 경우 전체 CPU 그룹 캡은 다시 조정 해야 하며, 그에 따라 발생 하는 VM 당 cap를 유지 관리 하도록 설정 해야 합니다. VM 호스트 관리자 또는 가상화 관리 소프트웨어 계층은 원하는 VM 별 CPU 리소스 할당을 얻기 위해 필요에 따라 그룹을 관리 하는 일을 담당 합니다.

## <a name="example-classes-of-service"></a>서비스의 예제 클래스

몇 가지 간단한 예제를 살펴보겠습니다. 먼저 Hyper-v 호스트 관리자가 게스트 Vm에 대 한 두 가지 서비스 계층을 지원 한다고 가정 합니다.

1. 낮은 종료 "C" 계층입니다. 전체 호스트의 계산 리소스의 10%를이 계층에 제공 합니다.

1. 중간 범위의 "B" 계층입니다. 이 계층에는 전체 호스트의 계산 리소스의 50%가 할당 됩니다.

이 시점에서는 개별 VM cap, 가중치 및 예약과 같은 다른 CPU 리소스 컨트롤이 사용 되지 않음을 어설션 합니다.
그러나 나중에 약간 볼 수 있으므로 개별 VM cap가 중요 합니다.

간단한 설명을 위해 각 VM에는 1 개의 VP가 있고 호스트에는 8 LPs가 있다고 가정해 보겠습니다. 빈 호스트로 시작 합니다.

"B" 계층을 만들려면 호스트 adminstartor에서 그룹 캡을 50%로 설정 합니다.

    G = n * C
    G = 8 * 50%
    G = 4 LP's worth of CPU time for the entire group

호스트 관리자가 단일 "B" 계층 VM을 추가 합니다.
이 시점에서 "B" 계층 VM은 호스트의 CPU 중 최대 50%를 사용할 수 있으며, 예제 시스템에서 4 LPs와 동일 합니다.

이제 관리자가 두 번째 "계층 B" VM을 추가 합니다. CPU 그룹의 할당은 모든 Vm 간에 균등 하 게 분할 됩니다. 그룹 B에는 총 2 개의 Vm이 있으므로 각 VM은 이제 그룹 B의 절반을 각각 50%, 25%의 절반 또는 계산 시간의 2 개에 해당 하는 값으로 가져옵니다.

## <a name="setting-cpu-caps-on-individual-vms"></a>개별 Vm에서 CPU Cap 설정

그룹 단면 외에도 각 VM에는 개별 "VM 캡"이 있을 수 있습니다. CPU 캡, 무게 및 reserve를 비롯 한 VM 별 CPU 리소스 제어는 도입 이후 Hyper-v의 일부입니다.
그룹 캡과 함께 사용할 경우 VM 캡은 각 VP에서 사용할 수 있는 CPU 리소스가 있는 경우에도 각 VP에서 얻을 수 있는 최대 CPU 크기를 지정 합니다.

예를 들어 호스트 관리자는 "C" Vm에 10% VM cap를 추가 하려고 할 수 있습니다.
이렇게 하면 대부분의 "C" VPs 유휴 상태인 경우에도 각 VP는 10%를 초과 하지 않을 수 있습니다.
VM 캡이 없으면 "C" Vm이 계층에서 허용 하는 수준 이상으로 성능을 대해 선택적으로 수 있습니다.

## <a name="isolating-vm-groups-to-specific-host-processors"></a>VM 그룹을 특정 호스트 프로세서로 격리

Hyper-v 호스트 관리자는 VM에 계산 리소스를 전용으로 사용할 수도 있습니다.
예를 들어 관리자가 100%의 클래스 캡이 포함 된 프리미엄 "A" VM을 제공 하려고 한다고 가정 합니다.
이러한 프리미엄 Vm에는 가장 낮은 예약 대기 시간 및 지터도 필요 합니다. 즉, 다른 VM에서 예약 되지 않은 것일 수 있습니다.
이러한 분리를 위해 특정 LP 선호도 매핑을 사용 하 여 CPU 그룹을 구성할 수도 있습니다.

예를 들어이 예제에서 호스트의 "A" VM에 맞게 관리자는 새 CPU 그룹을 만들고 그룹의 프로세서 선호도를 호스트의 LPs 하위 집합으로 설정 합니다.
그룹 B와 C는 나머지 LPs로 선호도가 설정 됩니다.
관리자는 그룹 A에서 단일 VM을 만들 수 있습니다. 그러면 그룹 a의 모든 LPs에 단독으로 액세스할 수 있으며,이 경우에는 더 낮은 계층 그룹인 B와 C가 나머지 LPs를 공유 합니다.

## <a name="segregating-root-vps-from-guest-vps"></a>게스트 VPs에서 Root VPs 분리

기본적으로 Hyper-v는 각 기본 물리적 LP에 루트 VP를 만듭니다.
이러한 루트 VPs는 시스템 LPs를 사용 하 여 엄격히 1:1 매핑되고, 마이그레이션하지 않습니다. 즉, 각 루트 VP는 항상 동일한 물리적 LP에서 실행 됩니다.
게스트 VPs는 사용 가능한 모든 LP에서 실행 될 수 있으며 루트 VPs를 사용 하 여 실행을 공유 합니다.

그러나 게스트 VPs의 루트 VP 작업을 완전히 분리 하는 것이 좋을 수 있습니다.
프리미엄 "A" 계층 VM을 구현 하는 위의 예를 살펴보겠습니다.
"A" VM의 VPs가 가능한 가장 낮은 대기 시간 및 "지터" 또는 일정 변형을 갖도록 하려면 LPs의 전용 집합에서 실행 하 여 루트가 이러한 LPs에서 실행 되지 않도록 합니다.

이는 "minroot" 구성의 조합을 사용 하 여 수행할 수 있습니다 .이 구성에서는 호스트 OS 파티션이 전체 시스템 논리 프로세서의 하위 집합에서 실행 되도록 제한 하 고 하나 이상의 선호도가 설정 CPU 그룹과 함께 실행 됩니다.

하나 이상의 CPU 그룹이 나머지 LPs로 선호도가 설정 호스트 파티션을 특정 LPs로 제한 하도록 가상화 호스트를 구성할 수 있습니다.
이러한 방식으로 루트 및 게스트 파티션은 CPU 공유 없이 전용 CPU 리소스에서 실행 되 고 완전히 격리 될 수 있습니다.

"Minroot" 구성에 대 한 자세한 내용은 [Hyper-v 호스트 CPU 리소스 관리](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-minroot-2016)를 참조 하세요.

## <a name="using-the-cpugroups-tool"></a>CpuGroups 도구 사용

CpuGroups 도구를 사용 하는 방법에 대 한 몇 가지 예를 살펴보겠습니다.

>[!NOTE]
>CpuGroups 도구에 대 한 명령줄 매개 변수는 공백으로만 공백을 사용 하 여 전달 됩니다. '/' 또는 '-' 문자는 원하는 명령줄 스위치를 진행 하지 않습니다.

### <a name="discovering-the-cpu-topology"></a>CPU 토폴로지 검색

GetCpuTopology를 사용 하 여 CpuGroups를 실행 하면 아래와 같이 LP 인덱스, LP가 속한 NUMA 노드, 패키지 및 핵심 Id 및 루트 VP 인덱스를 비롯 하 여 현재 시스템에 대 한 정보가 반환 됩니다.

다음 예에서는 CPU 소켓과 2 개, 총 32 LPs 및 다중 스레딩을 사용 하는 시스템을 보여 주며, 각 NUMA 노드에서 4 개의 루트 VPs 4 개의 Minroot를 사용 하도록 구성 합니다.
Root VPs가 있는 LPs에 RootVpIndex >= 0;이 (가) 있습니다. RootVpIndex가-1 인 LPs는 루트 파티션에서 사용할 수 없지만 하이퍼바이저에서 계속 관리 되며 다른 구성 설정에서 허용 하는 대로 게스트 VPs을 실행 합니다.

```console
C:\vm\tools>CpuGroups.exe GetCpuTopology

LpIndex NodeNumber PackageId CoreId RootVpIndex
------- ---------- --------- ------ -----------
      0          0         0      0           0
      1          0         0      0           1
      2          0         0      1           2
      3          0         0      1           3
      4          0         0      2          -1
      5          0         0      2          -1
      6          0         0      3          -1
      7          0         0      3          -1
      8          0         0      4          -1
      9          0         0      4          -1
     10          0         0      5          -1
     11          0         0      5          -1
     12          0         0      6          -1
     13          0         0      6          -1
     14          0         0      7          -1
     15          0         0      7          -1
     16          1         1     16           4
     17          1         1     16           5
     18          1         1     17           6
     19          1         1     17           7
     20          1         1     18          -1
     21          1         1     18          -1
     22          1         1     19          -1
     23          1         1     19          -1
     24          1         1     20          -1
     25          1         1     20          -1
     26          1         1     21          -1
     27          1         1     21          -1
     28          1         1     22          -1
     29          1         1     22          -1
     30          1         1     23          -1
     31          1         1     23          -1
```

### <a name="example-2--print-all-cpu-groups-on-the-host"></a>예 2 – 호스트의 모든 CPU 그룹 인쇄

여기에는 현재 호스트의 모든 CPU 그룹, 해당 GroupId, 그룹의 CPU 상한 및 해당 그룹에 할당 된 LPs의 인덱스 나열 됩니다.

유효한 CPU 캡 값은 [0, 65536] 범위에 있으며, 이러한 값은 그룹 끝을 백분율 (예: 32768 = 50%)로 표현 합니다.

```console
C:\vm\tools>CpuGroups.exe GetGroups

CpuGroupId                          CpuCap  LpIndexes
------------------------------------ ------ --------
36AB08CB-3A76-4B38-992E-000000000002 32768  4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536  24,25,26,27,28,29,30,31
```

### <a name="example-3--print-a-single-cpu-group"></a>예제 3 – 단일 CPU 그룹 인쇄

이 예제에서는 GroupId를 필터로 사용 하 여 단일 CPU 그룹을 쿼리 합니다.

```console
C:\vm\tools>CpuGroups.exe GetGroups /GroupId:36AB08CB-3A76-4B38-992E-000000000003
CpuGroupId                          CpuCap   LpIndexes
------------------------------------ ------ ----------
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
```

### <a name="example-4--create-a-new-cpu-group"></a>예제 4 – 새 CPU 그룹 만들기

여기에서는 그룹에 할당할 LPs 집합 및 그룹 ID를 지정 하 여 새 CPU 그룹을 만듭니다.

```console
C:\vm\tools>CpuGroups.exe CreateGroup /GroupId:36AB08CB-3A76-4B38-992E-000000000001 /GroupAffinity:0,1,16,17
```

이제 새로 추가 된 그룹을 표시 합니다.

```console
C:\vm\tools>CpuGroups.exe GetGroups
CpuGroupId                          CpuCap LpIndexes
------------------------------------ ------ ---------
36AB08CB-3A76-4B38-992E-000000000001 65536 0,1,16,17
36AB08CB-3A76-4B38-992E-000000000002 32768 4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536 12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536 24,25,26,27,28,29,30,31
```

### <a name="example-5--set-the-cpu-group-cap-to-50"></a>예 5-CPU 그룹 캡을 50%로 설정

여기서는 CPU 그룹 캡을 50%로 설정 합니다.

```console
C:\vm\tools>CpuGroups.exe SetGroupProperty /GroupId:36AB08CB-3A76-4B38-992E-000000000001 /CpuCap:32768
```

이제 방금 업데이트 한 그룹을 표시 하 여 설정을 확인 하겠습니다.

```console
C:\vm\tools>CpuGroups.exe GetGroups /GroupId:36AB08CB-3A76-4B38-992E-000000000001

CpuGroupId                          CpuCap LpIndexes
------------------------------------ ------ ---------
36AB08CB-3A76-4B38-992E-000000000001 32768 0,1,16,17
```

### <a name="example-6--print-cpu-group-ids-for-all-vms-on-the-host"></a>예 6 – 호스트의 모든 Vm에 대 한 CPU 그룹 id 인쇄

```console
C:\vm\tools>CpuGroups.exe GetVmGroup

VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G2 4ABCFC2F-6C22-498C-BB38-7151CE678758 36ab08cb-3a76-4b38-992e-000000000002
    P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC 36ab08cb-3a76-4b38-992e-000000000003
    P2 A593D93A-3A5F-48AB-8862-A4350E3459E8 36ab08cb-3a76-4b38-992e-000000000004
    G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200 36ab08cb-3a76-4b38-992e-000000000002
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 36ab08cb-3a76-4b38-992e-000000000002
```

### <a name="example-7--unbind-a-vm-from-the-cpu-group"></a>예 7-CPU 그룹에서 VM 바인딩 해제

CPU 그룹에서 VM을 제거 하려면 VM의 CpuGroupId을 NULL GUID로 설정 합니다. 그러면 CPU 그룹에서 VM을 바인딩 해제 합니다.

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:00000000-0000-0000-0000-000000000000

C:\vm\tools>CpuGroups.exe GetVmGroup
VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G2 4ABCFC2F-6C22-498C-BB38-7151CE678758 36ab08cb-3a76-4b38-992e-000000000002
    P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC 36ab08cb-3a76-4b38-992e-000000000003
    P2 A593D93A-3A5F-48AB-8862-A4350E3459E8 36ab08cb-3a76-4b38-992e-000000000004
    G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200 36ab08cb-3a76-4b38-992e-000000000002
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 00000000-0000-0000-0000-000000000000
```

### <a name="example-8--bind-a-vm-to-an-existing-cpu-group"></a>예제 8 – VM을 기존 CPU 그룹에 바인딩

여기서는 기존 CPU 그룹에 VM을 추가 합니다.
VM은 기존 CPU 그룹에 바인딩되어야 합니다. 그렇지 않으면 CPU 그룹 id가 설정 되지 않습니다.

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:36AB08CB-3A76-4B38-992E-000000000001
```

이제 VM G1이 원하는 CPU 그룹에 있는지 확인 합니다.

```console
C:\vm\tools>CpuGroups.exe GetVmGroup
VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G2 4ABCFC2F-6C22-498C-BB38-7151CE678758 36ab08cb-3a76-4b38-992e-000000000002
    P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC 36ab08cb-3a76-4b38-992e-000000000003
    P2 A593D93A-3A5F-48AB-8862-A4350E3459E8 36ab08cb-3a76-4b38-992e-000000000004
    G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200 36ab08cb-3a76-4b38-992e-000000000002
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 36AB08CB-3A76-4B38-992E-000000000001
```

### <a name="example-9--print-all-vms-grouped-by-cpu-group-id"></a>예 9 – CPU 그룹 id 별로 그룹화 된 모든 Vm 인쇄

```console
C:\vm\tools>CpuGroups.exe GetGroupVms
CpuGroupId                           VmName                                 VmId
------------------------------------ ------ ------------------------------------
36AB08CB-3A76-4B38-992E-000000000001     G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC
36ab08cb-3a76-4b38-992e-000000000002     G2 4ABCFC2F-6C22-498C-BB38-7151CE678758
36ab08cb-3a76-4b38-992e-000000000002     G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200
36ab08cb-3a76-4b38-992e-000000000003     P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC
36ab08cb-3a76-4b38-992e-000000000004     P2 A593D93A-3A5F-48AB-8862-A4350E3459E8
```

### <a name="example-10--print-all-vms-for-a-single-cpu-group"></a>예 10 – 단일 CPU 그룹에 대 한 모든 Vm 인쇄

```console
C:\vm\tools>CpuGroups.exe GetGroupVms /GroupId:36ab08cb-3a76-4b38-992e-000000000002

CpuGroupId                           VmName                                VmId
------------------------------------ ------ ------------------------------------
36ab08cb-3a76-4b38-992e-000000000002     G2 4ABCFC2F-6C22-498C-BB38-7151CE678758
36ab08cb-3a76-4b38-992e-000000000002     G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200
```

### <a name="example-11--attempting-to-delete-a-non-empty-cpu-group"></a>예 11 – 비어 있지 않은 CPU 그룹 삭제 시도

비어 있는 CPU 그룹 (즉, 바인딩된 Vm이 없는 CPU 그룹)만 삭제할 수 있습니다.
비어 있지 않은 CPU 그룹을 삭제 하려고 하면 실패 합니다.

```console
C:\vm\tools>CpuGroups.exe DeleteGroup /GroupId:36ab08cb-3a76-4b38-992e-000000000001
(null)
Failed with error 0xc0350070
```

### <a name="example-12--unbind-the-only-vm-from-a-cpu-group-and-delete-the-group"></a>예 12 – CPU 그룹에서 VM의 바인딩을 해제 하 고 그룹을 삭제 합니다.

이 예제에서는 여러 명령을 사용 하 여 CPU 그룹을 검사 하 고 해당 그룹에 속한 단일 VM을 제거한 다음 그룹을 삭제 합니다.

먼저 그룹에서 Vm을 열거 하겠습니다.

```console
C:\vm\tools>CpuGroups.exe GetGroupVms /GroupId:36AB08CB-3A76-4B38-992E-000000000001
CpuGroupId                           VmName                                VmId
------------------------------------ ------ ------------------------------------
36AB08CB-3A76-4B38-992E-000000000001     G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC
```

G1 이라는 단일 VM만이 그룹에 속합니다.
VM의 그룹 ID를 NULL로 설정 하 여 그룹에서 G1 VM을 제거 하겠습니다.

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:00000000-0000-0000-0000-000000000000
```

그리고 변경 내용을 확인 합니다.

```console
C:\vm\tools>CpuGroups.exe GetVmGroup /VmName:g1
VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 00000000-0000-0000-0000-000000000000
```

이제 그룹이 비어 있으므로 안전 하 게 삭제할 수 있습니다.

```console
C:\vm\tools>CpuGroups.exe DeleteGroup /GroupId:36ab08cb-3a76-4b38-992e-000000000001
```

그리고 그룹이 사라졌는지 확인 합니다.

```console
C:\vm\tools>CpuGroups.exe GetGroups
CpuGroupId                          CpuCap                     LpIndexes
------------------------------------ ------ -----------------------------
36AB08CB-3A76-4B38-992E-000000000002 32768  4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536 24,25,26,27,28,29,30,31
```

### <a name="example-13--bind-a-vm-back-to-its-original-cpu-group"></a>예제 13 – VM을 원래 CPU 그룹에 다시 바인딩

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:36AB08CB-3A76-4B38-992E-000000000002

C:\vm\tools>CpuGroups.exe GetGroupVms
CpuGroupId VmName VmId
------------------------------------ -------------------------------- ------------------------------------
36ab08cb-3a76-4b38-992e-000000000002 G2 4ABCFC2F-6C22-498C-BB38-7151CE678758
36ab08cb-3a76-4b38-992e-000000000002 G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200
36AB08CB-3A76-4B38-992E-000000000002 G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC
36ab08cb-3a76-4b38-992e-000000000003 P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC
36ab08cb-3a76-4b38-992e-000000000004 P2 A593D93A-3A5F-48AB-8862-A4350E3459E8
```
