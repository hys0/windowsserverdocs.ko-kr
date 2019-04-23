---
title: 가상 컴퓨터 리소스 컨트롤
description: VM CPU 그룹 사용
keywords: windows 10, Hyper-V
author: allenma
ms.date: 06/18/2018
ms.topic: article
ms.prod: windows-10-hyperv
ms.service: windows-10-hyperv
ms.assetid: cc7bb88e-ae75-4a54-9fb4-fc7c14964d67
ms.openlocfilehash: 7c4ddf3e5d2ff58eef844c50960327c27a3e0a3d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854764"
---
>적용 대상: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

# <a name="virtual-machine-resource-controls"></a>가상 컴퓨터 리소스 컨트롤

이 문서에서는 가상 머신에 대 한 Hyper-v 리소스 및 격리 컨트롤에 설명 합니다.  에서는 사용 하는 가상 머신 CPU 그룹 또는 "CPU 그룹"으로, 이러한 기능은 Windows Server 2016에서 도입 되었습니다.  CPU 그룹에는 Hyper-v 관리자를 관리 하 고 게스트 가상 머신에서 호스트의 CPU 리소스를 할당할 수 있습니다.  CPU 그룹을 사용 하 여 Hyper-v 관리자가 수행할 수 있습니다.

* 가상화 호스트의 총 CPU 리소스를 그룹 전체에서 공유의 다른 할당 각 그룹을 사용 하 여 가상 머신의 그룹을 만듭니다. 이 통해 다양 한 유형의 Vm에 대 한 서비스 클래스를 구현 하려면 호스트 관리자입니다.

* 특정 그룹에 CPU 리소스 한도 설정 합니다. 이 그룹 "cap" 호스트에 대 한 상한 값은 해당 그룹에 대 한 서비스의 원하는 클래스를 효과적으로 적용 전체 그룹을 사용할 수 있는 CPU 리소스를 설정 합니다.

* 호스트 시스템의 프로세서의 특정 집합에만 실행 되도록 CPU 그룹을 제한 합니다. 서로 다른 CPU 그룹에 속한 Vm을 격리 데 수 수 있습니다.

## <a name="managing-cpu-groups"></a>CPU 그룹 관리

CPU 그룹 HCS를 Hyper-v 호스트 계산 서비스를 통해 관리 됩니다. HCS, 해당 발생에 대 한 훌륭한 설명을 HCS Api에 대 한 링크는 Microsoft Virtualization 팀 블로그 게시에서 사용 가능한 [호스트 계산 서비스 (HCS) 소개](https://blogs.technet.microsoft.com/virtualization/2017/01/27/introducing-the-host-compute-service-hcs/)합니다.

>[!NOTE] 
>HCS만 CPU 그룹; 만들기 및 관리를 사용할 수 있습니다. Hyper-v 관리자 애플릿의 WMI 및 PowerShell 관리 인터페이스 CPU 그룹을 지원 하지 않습니다.

명령줄을 제공 하는 Microsoft 유틸리티, cpugroups.exe에 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?linkid=865968) CPU 그룹을 관리 하는 HCS 인터페이스를 사용 하는 합니다.  이 유틸리티는 호스트의 CPU 토폴로지를 표시할 수도 있습니다.

## <a name="how-cpu-groups-work"></a>CPU 작업을 그룹화 하는 방법

CPU 그룹 호스트 계산 리소스 할당 계산된 CPU 그룹 한도 사용 하 여 Hyper-v 하이퍼바이저에 의해 적용 됩니다. CPU 그룹 단면이 CPU 그룹에 대 한 총 CPU 용량과의 비율입니다. 그룹 cap 값 그룹 클래스나 우선 순위 수준 할당에 따라 달라 집니다. 계산된 그룹 cap "CPU 시간의 가치가 LP's 수"로 생각할 수 있습니다. 이 그룹 예산 이므로 자체에 대 한 전체 그룹의 CPU 할당을 사용할 수 있습니다만 활성 상태 였던 단일 VM에서 공유 됩니다.

CPU 그룹 한도 G로 계산 됩니다 = *n* x *C*여기서:

    *G* is the amount of host LP we'd like to assign to the group
    *n* is the total number of logical processors (LPs) in the group
    *C* is the maximum CPU allocation — that is, the class of service desired for the group, expressed as a percentage of the system’s total compute capacity

예를 들어 4 개의 논리 프로세서 (LPs) 및 50% 캡을 사용 하 여 구성 된 CPU 그룹을 것이 좋습니다.

    G = n * C
    G = 4 * 50%
    G = 2 LP's worth of CPU time for the entire group

이 예제에서는 CPU 그룹 G CPU 시간의 가치가 2 LP's 할당 됩니다.  

가상 컴퓨터 또는 그룹에 바인딩된 가상 프로세서 수에 관계 없이 및 상태에 관계 없이 그룹 제한에 적용 됩니다 (예를 들어, 종료 또는 시작) CPU 그룹에 할당 된 가상 머신의. 따라서 동일한 CPU 그룹에 바인딩된 각 VM 그룹의 총 CPU 할당의 분수를 받게 됩니다 하 고 CPU 그룹에 연결 하는 Vm 수를 사용 하 여이 변경 됩니다. 따라서 Vm 바인딩된 하거나 CPU 그룹에서 Vm을 바인딩 해제 하면 전반적인 CPU 그룹 cap 재조정 고 원하는 결과 VM 당 한도 유지 관리를 설정 합니다. VM 호스트의 관리자 또는 가상화 관리 소프트웨어 계층은 원하는 VM CPU 리소스 할당을 위해 필요에 따라 그룹 cap를 관리 하는 일을 담당 합니다.

## <a name="example-classes-of-service"></a>서비스의 예제에서는 클래스

몇 가지 간단한 예제를 살펴보겠습니다. 시작 하려면 Hyper-v 호스트 관리자는 게스트 Vm에 대 한 서비스의 두 계층을 지원 하려는 가정 합니다.

1. 저사양 "C" 계층입니다. 전체 호스트의 계산 리소스의 10%가이 계층을 제공 해 드리겠습니다.

1. 중급 "B" 계층입니다. 이 계층 전체 호스트의 계산 리소스의 50%를 할당 됩니다.

이 시점에서 예제에서에서는 어설션 다른 CPU 리소스 제어 개별 VM caps 등 사용 중인 가중치를 예약 합니다.
그러나 앞으로 살펴보겠지만 잠시 후 개별 VM 대문자는 중요 합니다.

단순성을 가정 하겠습니다 각 VM에 1 VP, 있고 호스트가 8 LPs 합니다. 빈 호스트를 사용 하 여 시작 하겠습니다.

"B" 계층을 만들려면 호스트 adminstartor 그룹 cap을 50%로 설정 합니다.

    G = n * C
    G = 8 * 50%
    G = 4 LP's worth of CPU time for the entire group

호스트 관리자는 단일 "B" 계층 VM을 추가합니다.
이 시점에서 "B" 계층도 VM에서에서 사용할 수 최대 호스트의 CPU 또는 4 LPs에 해당 하는 것이 좋습니다 50% 예제 시스템.

이제 관리자는 두 번째 계층 B "VM을 추가합니다. CPU 그룹의 할당-모든 Vm 간에 균일 하 게 분할 됩니다. 50%, 25% 각각 또는 가치가 2 LPs 계산 시간에 해당 하는 그룹 B의 총 수의 절반을 각 VM 이제 가져옵니다 하므로 그룹 B에는 총 2 개의 Vm에 답변이 있습니다.

## <a name="setting-cpu-caps-on-individual-vms"></a>개별 Vm에 CPU 제한을 설정

한 그룹도 외에도 각 VM에는 개별 VM "cap" 있을 수도 있습니다. CPU 한도, 두께 및 예약을 비롯 하 여 VM 당 CPU 리소스 컨트롤 소개 된 이후로 하이퍼-V 포함 되었습니다.
그룹 cap과 함께 사용할 경우 VM 캡을 그룹에 사용할 수 있는 CPU 리소스 하는 경우에 각 VP 얻을 수 있는 CPU의 최대 크기를 지정 합니다.

예를 들어 호스트 관리자는 "C" Vm에서 10 %VM 캡을 배치할 볼 수 있습니다.
따라서 대부분의 "C" VPs 유휴 상태인 경우에 각 VP 되지 않다가 10% 이상입니다.
VM 제한 없이 "C" Vm 선택적으로 해당 계층에서 허용 하는 수준 외에도 성능을 달성할 수 있습니다.

## <a name="isolating-vm-groups-to-specific-host-processors"></a>특정 호스트 프로세서 격리 VM 그룹

Hyper-v 호스트 관리자는 VM에 계산 리소스를 전용으로 사용할 수 있는 기능을 수도 있습니다.
예를 들어 관리자는 프리미엄 제공 하려고 한다고 가정 "는" 100%는 클래스 끝에 있는 VM.
또한 일정 가장 낮은 대기 시간 요구 및 지터 가능 합니다; 이러한 프리미엄 Vm 즉, 이러한 있습니다 취소 예약 하지 다른 VM에서.
이 분리를 위해 CPU 그룹 특정 LP 선호도 매핑을 사용 하 여 구성할 수도 있습니다.

예를 들어 "A" VM을이 예제의 호스트에 맞게 관리자 새 CPU 그룹을 만들고 호스트의 LPs의 하위 집합으로 그룹의 프로세서 선호도 설정 합니다.
그룹 B와 C 나머지 LPs 규 됩니다.
관리자가 되는 경우가 모든 LPs에 단독으로 액세스 하는 동안 아마도 더 낮은 계층 그룹 B 그룹 A의 단일 그룹에 VM을 만들 수 및 C는 나머지 LPs를 공유 합니다.

## <a name="segregating-root-vps-from-guest-vps"></a>루트 VPs 게스트 VPs에서 분리

기본적으로 Hyper-v에서 각 기본 실제 LP 루트 VP 만들어집니다.
이러한 루트 VPs 시스템과 LPs 엄격 하 게 매핑된 1:1 되며 마이그레이션하지-는 동일한 실제 LP에 항상 실행 하는 각 루트 VP, 합니다.
게스트 VPs 모든 사용 가능한 LP에서 실행 되 고 루트 VPs와 실행을 공유 하는 합니다.

그러나 것이 좋습니다 완전히 별도 루트 VP 활동 게스트 VPs에서.
VM을 프리미엄 "A" 계층 구현 예제를 것이 좋습니다.
"A" VM의 VPs 들은 가장 짧을 대기 시간 및 "지터" 또는 예약 변형 되도록 하고자 LPs 전용된 집합에서 실행 하 고 루트 이러한 LPs에서 실행 되지 않도록 합니다.

OS 파티션 하 나와 함께 전체 시스템 논리 프로세서의 하위 집합에서 실행 중인 호스트를 제한 하는 "minroot" 구성의 조합을 사용 하 여 수행할 수 있습니다 또는 자세히 CPU 그룹을 설정 합니다.

나머지 LPs로 설정 하는 하나 이상의 CPU 그룹을 사용 하 여 특정 LPs에는 호스트 파티션에 대 한 제한에 가상화 호스트를 구성할 수 있습니다.
이런 방식으로 루트 및 게스트 파티션 전용된 CPU 리소스에 대해 실행할 수 및 CPU 공유 완전히 격리 됩니다.

"Minroot" 구성에 대 한 자세한 내용은 참조 하세요. [Hyper-v 호스트 CPU 리소스 관리](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-minroot-2016)합니다.

## <a name="using-the-cpugroups-tool"></a>CpuGroups 도구를 사용 하 여

CpuGroups 도구를 사용 하는 방법의 몇 가지 예를 살펴보겠습니다.

>[!NOTE] 
>CpuGroups 도구에 대 한 명령줄 매개 변수는 공백으로 구분 기호로 사용 하 여 전달 됩니다. 이상 '/' 또는 '-' 문자는 원하는 명령줄 스위치를 진행 해야 합니다.

### <a name="discovering-the-cpu-topology"></a>CPU 토폴로지 검색

아래와 같이 LP 인덱스는 LP 속한 패키지 및 핵심 Id, 루트 VP 인덱스 NUMA 노드를 포함 하 여 현재 시스템에 대 한 정보를 반환 합니다 CpuGroups는 GetCpuTopology 사용 하 여 실행 합니다.

다음 예제에서는 CPU 소켓을 사용 하 여 시스템 및 NUMA 노드에서 총 32 LPs 및 다중 스레딩을 사용 하도록 설정 및 Minroot 8 루트 VPs, 각 NUMA 노드에서 4 사용 하 여 사용 하도록 구성 합니다.
루트 VPs 있는 LPs가는 RootVpIndex > = 0; LPs-1의 RootVpIndex 사용 하 여 루트 파티션에 사용할 수 없는 하 하지만, 하이퍼바이저에서 계속 관리 됩니다 하 고, 기타 구성 설정에서 허용 된 대로 게스트 VPs 실행 됩니다.

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

### <a name="example-2--print-all-cpu-groups-on-the-host"></a>예제 2 – 호스트에서 모든 CPU 그룹 인쇄

여기에서 현재 호스트, 해당 GroupId, 그룹의 CPU 한도 및 해당 그룹에 할당 된 LPs의 인덱스에 있는 모든 CPU 그룹이 나열 됩니다.

유효한 CPU cap 값은 범위 [0, 65536] 하 고 이러한 값 백분율에서 그룹 cap express (예: 32768 = 50%).

```console
C:\vm\tools>CpuGroups.exe GetGroups

CpuGroupId                          CpuCap  LpIndexes
------------------------------------ ------ --------
36AB08CB-3A76-4B38-992E-000000000002 32768  4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536  24,25,26,27,28,29,30,31
```

### <a name="example-3--print-a-single-cpu-group"></a>예제 3 – 인쇄 단일 CPU 그룹

이 예에서는에서는 GroupId 필터로 사용 하 여 단일 CPU 그룹 쿼리 합니다.

```console
C:\vm\tools>CpuGroups.exe GetGroups /GroupId:36AB08CB-3A76-4B38-992E-000000000003
CpuGroupId                          CpuCap   LpIndexes
------------------------------------ ------ ----------
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
```

### <a name="example-4--create-a-new-cpu-group"></a>예 4-새 CPU 그룹 만들기

여기에서 그룹에 할당 하려면 그룹 ID 및 LPs 집합이 지정 하 여 새 CPU 그룹을 만듭니다.

```console
C:\vm\tools>CpuGroups.exe CreateGroup /GroupId:36AB08CB-3A76-4B38-992E-000000000001 /GroupAffinity:0,1,16,17
```

이제이 새로 추가 된 그룹을 표시 합니다.

```console
C:\vm\tools>CpuGroups.exe GetGroups
CpuGroupId                          CpuCap LpIndexes
------------------------------------ ------ ---------
36AB08CB-3A76-4B38-992E-000000000001 65536 0,1,16,17
36AB08CB-3A76-4B38-992E-000000000002 32768 4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536 12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536 24,25,26,27,28,29,30,31
```

### <a name="example-5--set-the-cpu-group-cap-to-50"></a>예 5-CPU 그룹 cap를 50%로 설정

여기서 CPU 그룹 한도 50%로 설정 합니다.

```console
C:\vm\tools>CpuGroups.exe SetGroupProperty /GroupId:36AB08CB-3A76-4B38-992E-000000000001 /CpuCap:32768
```

이제 방금 업데이트 그룹을 표시 하 여이 설정을 확인 합니다.

```console
C:\vm\tools>CpuGroups.exe GetGroups /GroupId:36AB08CB-3A76-4B38-992E-000000000001

CpuGroupId                          CpuCap LpIndexes
------------------------------------ ------ ---------
36AB08CB-3A76-4B38-992E-000000000001 32768 0,1,16,17
```

### <a name="example-6--print-cpu-group-ids-for-all-vms-on-the-host"></a>예 6-호스트의 모든 Vm에 대 한 인쇄 CPU 그룹 id

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

CPU 그룹에서 VM을 제거 하려면 VM의 CpuGroupId NULL guid로 설정 합니다. 이 CPU 그룹에서 VM을 바인딩 해제합니다.

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

### <a name="example-8--bind-a-vm-to-an-existing-cpu-group"></a>예제 8 – 기존 CPU 그룹에 VM을 바인딩합니다.

여기에 기존 CPU 그룹에 VM을 추가 하겠습니다.
모든 기존 CPU 그룹에 VM을 바인딩할 수 해야 또는 CPU 그룹 id 설정 실패는 note 합니다.

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:36AB08CB-3A76-4B38-992E-000000000001
```

이제 VM G1 원하는 CPU 그룹에 있는 경우를 확인 합니다.

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

### <a name="example-9--print-all-vms-grouped-by-cpu-group-id"></a>예제 9 – 인쇄 CPU 그룹 id 별로 그룹화 된 모든 Vm

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

### <a name="example-10--print-all-vms-for-a-single-cpu-group"></a>예제 10 – 인쇄 단일 CPU 그룹에 대 한 모든 Vm

```console
C:\vm\tools>CpuGroups.exe GetGroupVms /GroupId:36ab08cb-3a76-4b38-992e-000000000002

CpuGroupId                           VmName                                VmId
------------------------------------ ------ ------------------------------------
36ab08cb-3a76-4b38-992e-000000000002     G2 4ABCFC2F-6C22-498C-BB38-7151CE678758
36ab08cb-3a76-4b38-992e-000000000002     G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200
```

### <a name="example-11--attempting-to-delete-a-non-empty-cpu-group"></a>예 11-비어 있지 않은 CPU 그룹을 삭제 하려고 합니다.

만 CPU 그룹을 빈-CPU 그룹 없이 Vm을 연결 하는,-삭제할 수 있습니다.
비어 있지 않은 CPU 그룹을 삭제 하려는 시도 실패 합니다.

```console
C:\vm\tools>CpuGroups.exe DeleteGroup /GroupId:36ab08cb-3a76-4b38-992e-000000000001
(null)
Failed with error 0xc0350070
```

### <a name="example-12--unbind-the-only-vm-from-a-cpu-group-and-delete-the-group"></a>예 – 12 CPU 그룹에서 유일한 VM 임을 바인딩 해제 하 고 그룹 삭제

이 예제에서는에서는 몇 가지 명령을 사용 하 여 CPU 그룹을 검사, 해당 그룹에 속하는 단일 VM을 제거 하 고 그룹을 삭제 합니다.

첫째,이 그룹의 Vm 열거 합니다.

```console
C:\vm\tools>CpuGroups.exe GetGroupVms /GroupId:36AB08CB-3A76-4B38-992E-000000000001
CpuGroupId                           VmName                                VmId
------------------------------------ ------ ------------------------------------
36AB08CB-3A76-4B38-992E-000000000001     G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC
```

만 단일 VM을 G1, 이름이이 그룹에 속해 있는지 볼 수 있습니다.
VM의 그룹 ID를 NULL로 설정 하 여이 그룹에서 G1 VM을 제거 하겠습니다.

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:00000000-0000-0000-0000-000000000000
```

및이 변경 내용을 확인 하는 중...

```console
C:\vm\tools>CpuGroups.exe GetVmGroup /VmName:g1
VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 00000000-0000-0000-0000-000000000000
```

그룹을 선택 하지 않으면 했으므로 안전 하 게 삭제할 수 했습니다.

```console
C:\vm\tools>CpuGroups.exe DeleteGroup /GroupId:36ab08cb-3a76-4b38-992e-000000000001
```

고 우리의 그룹이 삭제 되었는지 확인 합니다.

```console
C:\vm\tools>CpuGroups.exe GetGroups
CpuGroupId                          CpuCap                     LpIndexes
------------------------------------ ------ -----------------------------
36AB08CB-3A76-4B38-992E-000000000002 32768  4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536 24,25,26,27,28,29,30,31
```

### <a name="example-13--bind-a-vm-back-to-its-original-cpu-group"></a>예제 13-VM을 원래 CPU 그룹에 다시 바인딩

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
