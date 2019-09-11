---
title: Hyper-v 하이퍼바이저 스케줄러 형식 이해 및 사용
description: Hyper-v의 스케줄러 모드 사용에 대 한 정보를 Hyper-v 호스트 관리자에 게 제공 합니다.
author: allenma
ms.author: allenma
ms.date: 08/14/2018
ms.topic: article
ms.prod: windows-server-hyper-v
ms.technology: virtualization
ms.localizationpriority: low
ms.assetid: 6cb13f84-cb50-4e60-a685-54f67c9146be
ms.openlocfilehash: c7c2de8354d067faf0dcf1787c3e178421e2ac03
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70872033"
---
# <a name="managing-hyper-v-hypervisor-scheduler-types"></a>Hyper-v 하이퍼바이저 스케줄러 형식 관리

>적용 대상: Windows 10, Windows Server 2016, Windows Server, 버전 1709, Windows Server, 버전 1803, Windows Server 2019

이 문서에서는 Windows Server 2016에 처음 도입 된 가상 프로세서 예약 논리의 새로운 모드에 대해 설명 합니다. 이러한 모드 또는 스케줄러 형식은 Hyper-v 하이퍼바이저가 게스트 가상 프로세서에서 작업을 할당 하 고 관리 하는 방법을 결정 합니다. Hyper-v 호스트 관리자는 게스트 Vm (가상 컴퓨터)에 가장 적합 한 하이퍼바이저 스케줄러 유형을 선택 하 고 예약 논리를 활용 하도록 Vm을 구성할 수 있습니다.

>[!NOTE]
>이 문서에 설명 된 하이퍼바이저 scheduler 기능을 사용 하려면 업데이트가 필요 합니다. 자세한 내용은 [필수 업데이트](#required-updates)를 참조 하세요.

## <a name="background"></a>배경

Hyper-v 가상 프로세서 예약의 기반이 되는 논리 및 제어에 대해 설명 하기 전에이 문서에 설명 된 기본 개념을 검토 하는 것이 좋습니다.

### <a name="understanding-smt"></a>SMT 이해

동시 다중 스레딩 (SMT)은 최신 프로세서 디자인에서 사용 되는 기술로, 개별 독립 실행 스레드에서 프로세서의 리소스를 공유할 수 있도록 합니다. SMT는 일반적으로 가능한 경우 계산을 병렬화 하 여 대부분의 워크 로드에 대 한 적절 한 성능 향상을 제공 합니다. 공유 프로세서 리소스가 발생 합니다.
SMT를 지 원하는 프로세서는 Intel 및 AMD 둘 다에서 사용할 수 있습니다. Intel은 intel 하이퍼 스레딩 기술 또는 Intel HT로 제공 되는 SMT 서비스를 나타냅니다.

이 문서의 목적상, Hyper-v에서 사용 되는 SMT 및 사용 방법에 대 한 설명은 Intel 및 AMD 시스템에 동일 하 게 적용 됩니다.

* Intel HT 기술에 대 한 자세한 내용은 [Intel 하이퍼 스레딩 기술](https://www.intel.com/content/www/us/en/architecture-and-technology/hyper-threading/hyper-threading-technology.html) (영문)을 참조 하십시오.

* AMD SMT에 대 한 자세한 내용은 ["Zen" 핵심 아키텍처](https://www.amd.com/en/technologies/zen-core) 를 참조 하세요.

## <a name="understanding-how-hyper-v-virtualizes-processors"></a>Hyper-v에서 프로세서를 가상화 하는 방법 이해

하이퍼바이저 스케줄러 유형을 고려 하기 전에 Hyper-v 아키텍처를 이해 하는 것도 유용 합니다. [Hyper-v 기술 개요](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-technology-overview)에서 일반적인 요약을 확인할 수 있습니다. 다음은이 문서에 대 한 중요 한 개념입니다.

* Hyper-v는 하이퍼바이저의 제어에서 계산 리소스를 할당 및 공유 하는 가상 컴퓨터 파티션을 만들고 관리 합니다. 파티션은 모든 게스트 가상 머신과 게스트 Vm과 루트 파티션 간에 강력한 격리 경계를 제공 합니다.

* 루트 파티션은 게스트 가상 컴퓨터 보다 고유한 속성과 훨씬 더 많은 권한을가지고 있지만 가상 컴퓨터 파티션입니다. 루트 파티션은 모든 게스트 가상 컴퓨터를 제어 하는 관리 서비스를 제공 하 고, 게스트에 대 한 가상 장치 지원을 제공 하 고, 게스트 가상 컴퓨터의 모든 장치 i/o를 관리 합니다. 루트 파티션에서 응용 프로그램 워크 로드를 실행 하지 않는 것이 좋습니다.

* 루트 파티션의 각 가상 프로세서 (VP)는 1:1를 기본 논리적 프로세서 (LP)에 매핑합니다. 호스트 VP는 항상 동일한 기본 LP에서 실행 됩니다. 루트 파티션의 VPs는 마이그레이션하지 않습니다.

* 기본적으로 호스트 VPs 실행 되는 LPs는 게스트 VPs 실행할 수도 있습니다.

* 하이퍼바이저는 사용 가능한 모든 논리 프로세서에서 실행 되도록 게스트 VP를 예약할 수 있습니다. 하이퍼바이저 스케줄러는 임시 캐시 집약성, NUMA 토폴로지 및 게스트 VP를 예약할 때 많은 다른 요인을 고려 하는 반면 궁극적으로 모든 호스트 LP에 대해 VP를 예약할 수 있습니다.

## <a name="hypervisor-scheduler-types"></a>하이퍼바이저 스케줄러 형식

Windows Server 2016부터 Hyper-v 하이퍼바이저는 기본 논리 프로세서에서 하이퍼바이저가 가상 프로세서를 예약 하는 방법을 결정 하는 여러 가지 스케줄러 논리 모드를 지원 합니다. 이러한 스케줄러 유형은 다음과 같습니다.

- [클래식, 양호 공유 스케줄러](#the-classic-scheduler)
- [핵심 스케줄러](#the-core-scheduler)
- [루트 스케줄러](#the-root-scheduler)

### <a name="the-classic-scheduler"></a>클래식 스케줄러

클래식 스케줄러는 Windows Server 2016 Hyper-v를 포함 하 여 처음부터 모든 버전의 Windows Hyper-v 하이퍼바이저에 대 한 기본값입니다. 클래식 스케줄러는 게스트 가상 프로세서에 대해 공평 하 게 공유 되 고 선점형 라운드 로빈 예약 모델을 제공 합니다.

클래식 스케줄러 형식은 사설 클라우드, 호스팅 공급자 등에 대해 기존의 Hyper-v 사용에 가장 적합 합니다. 성능 특징을 잘 이해 하 고 VPs에 대 한 과도 한 구독, 여러 다른 유형의 Vm 및 워크 로드를 동시에 실행 하는 등 광범위 한 가상화 시나리오를 지원 하도록 최적화 되어 있으며, 더 큰 확장성을 실행 합니다. 성능 Vm-제한 없이 Hyper-v의 전체 기능 집합을 지원 합니다.

### <a name="the-core-scheduler"></a>핵심 스케줄러

하이퍼바이저 코어 스케줄러는 Windows Server 2016 및 Windows 10 버전 1607에 도입 된 클래식 스케줄러 논리의 새로운 대안입니다. 핵심 스케줄러는 게스트 워크 로드 격리를 위한 강력한 보안 경계를 제공 하 고, SMT 지원 가상화 호스트에서 실행 되는 Vm 내부의 워크 로드에 대 한 성능 가변성을 줄입니다. 핵심 스케줄러를 사용 하면 동일한 SMT 지원 가상화 호스트에서 smt 및 비 SMT 가상 컴퓨터를 동시에 실행할 수 있습니다.

핵심 스케줄러는 가상화 호스트의 SMT 토폴로지를 활용 하 고 필요에 따라 호스트를 게스트 가상 컴퓨터에 표시 하 고, 동일한 가상 컴퓨터에서 SMT 논리적 프로세서 그룹으로의 게스트 가상 프로세서 그룹을 예약 합니다. 이는 대칭적으로 수행 되므로 LPs가 2 그룹에 있는 경우 VPs가 2 그룹으로 예약 되 고 코어는 Vm 간에 공유 되지 않습니다.
SMT를 사용 하지 않고 가상 컴퓨터에 대 한 VP가 예약 된 경우 해당 부사장은 실행 될 때 전체 코어를 사용 합니다.

핵심 스케줄러의 전체 결과는 다음과 같습니다.

* 게스트 VPs는 기본 실제 코어 쌍에서 실행 되도록 제한 되므로 VM을 프로세서 코어 경계로 분리 하 여 악의적인 Vm의 side-by-side 채널 스누핑 공격에 대 한 취약성을 줄일 수 있습니다.

* 처리량의 가변성은 크게 줄어듭니다.

* VPs 그룹 중 하나만 실행할 수 있는 경우 코어의 명령 스트림 중 하나만 유휴 상태를 유지 하 고 나머지는 유휴 상태로 유지 되기 때문에 성능이 저하 될 수 있습니다.

* 게스트 가상 머신에서 실행 되는 OS 및 응용 프로그램은 SMT 동작 및 프로그래밍 인터페이스 (Api)를 활용 하 여 가상화 되지 않은 실행 시와 마찬가지로 smt 스레드 간에 작업을 제어 하 고 배포할 수 있습니다.

* 게스트 워크 로드 격리-게스트 VPs에 대 한 강력한 보안 경계는 보조 채널 스누핑 공격에 대 한 취약성을 줄이기 위해 기본 실제 코어 쌍에서 실행 되도록 제한 됩니다.

핵심 스케줄러는 기본적으로 Windows Server 2019부터 사용 됩니다. Windows Server 2016에서 핵심 스케줄러는 선택 사항이 며 Hyper-v 호스트 관리자가 명시적으로 사용 하도록 설정 해야 하며 클래식 스케줄러는 기본값입니다.

#### <a name="core-scheduler-behavior-with-host-smt-disabled"></a>호스트 SMT를 사용 하지 않는 핵심 scheduler 동작

하이퍼바이저가 핵심 스케줄러 유형을 사용 하도록 구성 되었지만 SMT 기능이 사용 하지 않도록 설정 되었거나 가상화 호스트에 없는 경우 하이퍼바이저는 하이퍼바이저 스케줄러 유형 설정에 관계 없이 클래식 스케줄러 동작을 사용 합니다.

### <a name="the-root-scheduler"></a>루트 스케줄러

루트 스케줄러는 Windows 10 버전 1803에서 도입 되었습니다. 루트 스케줄러 형식이 사용 되는 경우 하이퍼바이저는 루트 파티션에 대 한 작업 예약을 제어으로 넘깁니다 합니다. 루트 파티션의 OS 인스턴스에 있는 NT scheduler는 시스템 LPs에 작업을 예약 하는 모든 측면을 관리 합니다.

루트 스케줄러는 WDAG (Windows Defender Application Guard)에서 사용 되는 것 처럼 강력한 워크 로드 격리를 제공 하기 위해 유틸리티 파티션을 지원 하기 위한 고유한 요구 사항을 해결 합니다. 이 시나리오에서 루트 OS에 대 한 일정 책임은 몇 가지 이점을 제공 합니다. 예를 들어 컨테이너 시나리오에 적용 되는 CPU 리소스 제어를 유틸리티 파티션과 함께 사용 하 여 관리 및 배포를 간소화할 수 있습니다. 또한 루트 OS 스케줄러는 컨테이너 내에서 워크 로드 CPU 사용률에 대 한 메트릭을 쉽게 수집 하 고이 데이터를 시스템의 다른 모든 워크 로드에 적용 되는 동일한 예약 정책에 대 한 입력으로 사용할 수 있습니다. 이러한 동일한 메트릭은 응용 프로그램 컨테이너에서 수행 되는 특성을 호스트 시스템에 명확 하 게 적용 하는 데도 도움이 됩니다. 이러한 메트릭을 추적 하는 것은 기존 가상 컴퓨터 작업을 사용 하는 것 보다 어렵습니다. 이러한 작업을 실행 하는 모든 VM의 작업은 루트 파티션에서 수행 됩니다.

#### <a name="root-scheduler-use-on-client-systems"></a>클라이언트 시스템에서 루트 스케줄러 사용

Windows 10 버전 1803부터 루트 스케줄러는 기본적으로 클라이언트 시스템 에서만 사용 됩니다 .이 경우 하이퍼바이저는 가상화 기반 보안 및 WDAG 워크 로드 격리를 지원 하 고,는 이후 시스템의 적절 한 운영에 사용 될 수 있습니다. 다른 유형의 핵심 아키텍처. 클라이언트 시스템에 대해 지원 되는 유일한 하이퍼바이저 스케줄러 구성입니다. 관리자는 Windows 10 클라이언트 시스템의 기본 하이퍼바이저 스케줄러 유형을 재정의 하려고 해서는 안 됩니다.

#### <a name="virtual-machine-cpu-resource-controls-and-the-root-scheduler"></a>가상 컴퓨터 CPU 리소스 컨트롤 및 루트 스케줄러

루트 운영 체제의 스케줄러 논리가 글로벌 기반으로 호스트 리소스를 관리 하 고 VM에 대 한 지식이 없으므로 Hyper-v에서 제공 하는 가상 컴퓨터 프로세서 리소스 컨트롤은 하이퍼바이저 루트 스케줄러를 사용 하도록 설정할 때 지원 되지 않습니다. 특정 구성 설정. Cap, 가중치 및 예약과 같은 Hyper-v VM 별 프로세서 리소스 컨트롤은 하이퍼바이저에서 클래식 및 핵심 스케줄러 유형과 같은 VP 일정을 직접 제어 하는 경우에만 적용할 수 있습니다.

#### <a name="root-scheduler-use-on-server-systems"></a>서버 시스템에서 루트 스케줄러 사용

루트 스케줄러는 현재 서버에서 Hyper-v와 함께 사용 하지 않는 것이 좋습니다. 대부분의 서버 가상화 배포에 일반적으로 사용 되는 광범위 한 워크 로드를 수용 하기 위해 성능 특성이 아직 완전히 특징 및 조정 되지 않았기 때문입니다.

## <a name="enabling-smt-in-guest-virtual-machines"></a>게스트 가상 컴퓨터에서 SMT 사용

핵심 스케줄러 유형을 사용 하도록 가상화 호스트의 하이퍼바이저가 구성 되 면 원하는 경우 SMT를 활용 하도록 게스트 가상 머신을 구성할 수 있습니다. VPs가 게스트 가상 컴퓨터에 하이퍼 스레드 하는 사실을 노출 하면 게스트 운영 체제의 스케줄러와 VM에서 실행 되는 작업을 통해 자체 작업 일정으로 SMT 토폴로지를 검색 하 고 활용할 수 있습니다. Windows Server 2016에서 게스트 SMT는 기본적으로 구성 되지 않으며 Hyper-v 호스트 관리자가 명시적으로 사용 하도록 설정 해야 합니다. Windows Server 2019부터 호스트에 생성 된 새 Vm은 기본적으로 호스트의 SMT 토폴로지를 상속 합니다.  즉, 코어 당 2 개의 SMT 스레드를 포함 하는 호스트에 생성 된 버전 9.0 VM은 코어 당 2 개의 SMT 스레드를 볼 수도 있습니다.

게스트 가상 머신에서 SMT를 사용 하도록 설정 하려면 PowerShell을 사용 해야 합니다. Hyper-v 관리자에서 제공 하는 사용자 인터페이스가 없습니다.
게스트 가상 머신에서 SMT를 사용 하도록 설정 하려면 충분 한 권한이 있는 PowerShell 창을 열고 다음을 입력 합니다.

``` powershell
Set-VMProcessor -VMName <VMName> -HwThreadCountPerCore <n>
```

여기서 <n> 는 게스트 VM에 표시 되는 코어 당 SMT 스레드 수입니다.  
<n> = 0은 HwThreadCountPerCore 값을 코어 값 당 호스트의 SMT 스레드 수와 일치 하도록 설정 합니다.

>[!NOTE] 
>HwThreadCountPerCore = 0 설정은 Windows Server 2019부터 지원 됩니다.

다음은 두 개의 가상 프로세서와 SMT를 사용 하는 가상 머신에서 실행 되는 게스트 운영 체제에서 가져온 시스템 정보의 예입니다. 게스트 운영 체제가 동일한 코어에 속하는 2 개의 논리적 프로세서를 검색 하 고 있습니다.

![SMT를 사용 하는 게스트 VM에서 msinfo32를 보여 주는 스크린샷](media/Hyper-V-CoreScheduler-VM-Msinfo32.png)

## <a name="configuring-the-hypervisor-scheduler-type-on-windows-server-2016-hyper-v"></a>Windows Server 2016 Hyper-v에서 하이퍼바이저 스케줄러 유형 구성

Windows Server 2016 Hyper-v에서는 기본적으로 클래식 하이퍼바이저 스케줄러 모델을 사용 합니다. 하이퍼바이저는 선택적으로 핵심 스케줄러를 사용 하도록 구성 하 여 게스트 VPs이 해당 물리적 SMT 쌍에서 실행 되도록 제한 하 고 게스트 VPs에 대 한 SMT 일정에 따라 가상 컴퓨터를 사용할 수 있도록 하 여 보안을 강화할 수 있습니다.

>[!NOTE]
>Microsoft는 Windows Server 2016 Hyper-v를 실행 하는 모든 고객이 잠재적으로 악성 게스트 Vm 으로부터 가상화 호스트가 최적으로 보호 되도록 핵심 스케줄러를 선택 하는 것을 권장 합니다.

## <a name="windows-server-2019-hyper-v-defaults-to-using-the-core-scheduler"></a>Windows Server 2019 Hyper-v는 기본적으로 핵심 스케줄러를 사용 합니다.

최적의 보안 구성으로 Hyper-v 호스트를 배포 하기 위해 Windows Server 2019 Hyper-v에서는 기본적으로 핵심 하이퍼바이저 스케줄러 모델을 사용 합니다. 호스트 관리자는 필요에 따라 레거시 클래식 스케줄러를 사용 하도록 호스트를 구성할 수 있습니다. 관리자는 스케줄러 형식 기본 설정을 재정의 하기 전에 각 스케줄러 형식이 가상화 호스트의 보안 및 성능에 미치는 영향을 신중 하 게 읽고 이해 하 고 고려해 야 합니다.  자세한 내용은 [hyper-v scheduler 형식 선택 이해](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/understanding-hyper-v-scheduler-type-selection) 를 참조 하세요.

### <a name="required-updates"></a>필수 업데이트

>[!NOTE]
>이 문서에 설명 된 하이퍼바이저 스케줄러 기능을 사용 하려면 다음 업데이트가 필요 합니다. 이러한 업데이트에는 호스트 구성에 필요한 새로운 ' hypervisorschedulertype ' BCD 옵션을 지원 하기 위한 변경 내용이 포함 되어 있습니다.

| 버전 | 릴리스  | 업데이트 필요 | 기술 자료 문서 |
|--------------------|------|---------|-------------:|
|Windows Server 2016 | 1607 | 2018.07 C | [KB4338822](https://support.microsoft.com/help/4338822/windows-10-update-kb4338822) |
|Windows Server 2016 | 1703 | 2018.07 C | [KB4338827](https://support.microsoft.com/help/4338827/windows-10-update-kb4338827) |
|Windows Server 2016 | 1709 | 2018.07 C | [KB4338817](https://support.microsoft.com/help/4338817/windows-10-update-kb4338817) |
|Windows Server 2019 | 1804 | 없음 | 없음 |

## <a name="selecting-the-hypervisor-scheduler-type-on-windows-server"></a>Windows Server에서 하이퍼바이저 스케줄러 유형 선택

하이퍼바이저 스케줄러 구성은 hypervisorschedulertype BCD 항목을 통해 제어 됩니다.

스케줄러 형식을 선택 하려면 관리자 권한으로 명령 프롬프트를 엽니다.

``` command
     bcdedit /set hypervisorschedulertype type
```

여기서 `type` 은 다음 중 하나입니다.

* 클래식
* Core
* 루트

하이퍼바이저 스케줄러 형식에 대 한 변경 내용을 적용 하려면 시스템을 다시 부팅 해야 합니다.

>[!NOTE]
>하이퍼바이저 루트 스케줄러는 현재 Windows Server Hyper-v에서 지원 되지 않습니다. Hyper-v 관리자는 서버 가상화 시나리오에서 사용할 루트 스케줄러를 구성 하려고 해서는 안 됩니다.

## <a name="determining-the-current-scheduler-type"></a>현재 스케줄러 형식 확인

가장 최근의 하이퍼바이저 시작 이벤트 ID 2에 대 한 이벤트 뷰어의 시스템 로그를 검사 하 여 현재 하이퍼바이저 스케줄러 유형을 확인할 수 있습니다 .이 ID는 하이퍼바이저 시작 시 구성 된 하이퍼바이저 스케줄러 유형을 보고 합니다. 하이퍼바이저 시작 이벤트는 Windows 이벤트 뷰어 또는 PowerShell을 통해 가져올 수 있습니다.

하이퍼바이저 시작 이벤트 ID 2는 하이퍼바이저 스케줄러 유형을 나타냅니다. 여기서는 다음과 같습니다.

    1 = Classic scheduler, SMT disabled

    2 = Classic scheduler

    3 = Core scheduler

    4 = Root scheduler

![하이퍼바이저 시작 이벤트 ID 2 세부 정보를 보여 주는 스크린샷](media/Hyper-V-CoreScheduler-EventID2-Details.png)

![하이퍼바이저 시작 이벤트 ID 2를 표시 이벤트 뷰어 표시 하는 스크린샷](media/Hyper-V-CoreScheduler-EventViewer.png)

### <a name="querying-the-hyper-v-hypervisor-scheduler-type-launch-event-using-powershell"></a>PowerShell을 사용 하 여 Hyper-v 하이퍼바이저 scheduler 유형 시작 이벤트 쿼리

PowerShell을 사용 하 여 하이퍼바이저 이벤트 ID 2에 대해 쿼리하려면 PowerShell 프롬프트에서 다음 명령을 입력 합니다.

``` powershell
Get-WinEvent -FilterHashTable @{ProviderName="Microsoft-Windows-Hyper-V-Hypervisor"; ID=2} -MaxEvents 1
```

![PowerShell 쿼리 및 하이퍼바이저 시작 이벤트 ID 2에 대 한 결과를 보여 주는 스크린샷](media/Hyper-V-CoreScheduler-PowerShell.png)
