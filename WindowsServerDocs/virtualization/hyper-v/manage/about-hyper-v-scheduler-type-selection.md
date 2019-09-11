---
title: Hyper-v 하이퍼바이저 scheduler 유형 선택 정보
description: Hyper-v의 스케줄러 모드 사용에 대 한 정보를 Hyper-v 호스트 관리자에 게 제공 합니다.
author: allenma
ms.author: allenma
ms.date: 08/14/2018
ms.topic: article
ms.prod: windows-server-hyper-v
ms.technology: virtualization
ms.localizationpriority: low
ms.assetid: 5fe163d4-2595-43b0-ba2f-7fad6e4ae069
ms.openlocfilehash: 1e77535548cccd1c821163dabbad381f35d2948a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70872061"
---
# <a name="about-hyper-v-hypervisor-scheduler-type-selection"></a>Hyper-v 하이퍼바이저 scheduler 유형 선택 정보

적용 대상:

* Windows Server 2016
* Windows Server, 버전 1709
* Windows Server, 버전 1803
* Windows Server 2019

이 문서에서는 Hyper-v의 기본 및 권장 되는 하이퍼바이저 스케줄러 형식 사용에 대 한 중요 한 변경 내용을 설명 합니다. 이러한 변경 내용은 시스템 보안과 가상화 성능 모두에 영향을 줍니다. 가상화 호스트 관리자는이 문서에 설명 된 변경 내용 및 의미를 검토 하 고 이해 하 고, 영향, 제안 된 배포 지침 및 위험 요소를 신중 하 게 평가 하 여 배포 및 관리 방법을 잘 이해 해야 합니다. Hyper-v는 빠르게 변화 하는 보안 환경에서 호스트 합니다.

>[!IMPORTANT]
>동시에 실행 되는 호스트에서 실행 하는 경우 레거시 하이퍼바이저 클래식 스케줄러 형식의 예약 동작을 통해 악의적인 게스트 VM이 여러 프로세서 아키텍처에서 sighted 하는 알려진 측면 채널 보안 취약성을 악용할 수 있습니다. 다중 스레딩 (SMT)을 사용할 수 있습니다.  성공적으로 악용 되 면 악의적인 작업에서 파티션 경계 외부의 데이터를 관찰할 수 있습니다. 하이퍼바이저 코어 스케줄러 유형을 활용 하 고 게스트 Vm을 다시 구성 하도록 Hyper-v 하이퍼바이저를 구성 하 여이 공격 클래스를 완화할 수 있습니다. 코어 스케줄러를 사용 하는 경우 하이퍼바이저는 게스트 VM의 VPs가 동일한 실제 프로세서 코어에서 실행 되도록 제한 하므로 데이터에 액세스 하는 VM이 실행 되는 실제 코어의 경계에 데이터에 액세스 하는 기능을 강력 하 게 격리 합니다.  이는 루트 또는 다른 게스트 파티션에 있는지와 상관 없이 VM이 다른 파티션의 아티팩트를 관찰 하지 못하도록 하는 이러한 측면 채널 공격에 대해 매우 효과적입니다.  따라서 Microsoft는 가상화 호스트 및 게스트 Vm에 대 한 기본 및 권장 구성 설정을 변경 합니다.

## <a name="background"></a>배경

Windows Server 2016부터 Hyper-v는 하이퍼바이저 스케줄러 형식 이라고 하는 가상 프로세서를 예약 하 고 관리 하는 여러 방법을 지원 합니다.  모든 하이퍼바이저 스케줄러 유형에 대 한 자세한 설명은 [hyper-v 하이퍼바이저 스케줄러 유형을 이해 하 고 사용 하](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types)는 방법을 참조 하세요.

>[!NOTE]
>새 하이퍼바이저 스케줄러 형식은 Windows Server 2016에 처음 도입 되었으며 이전 릴리스에서는 사용할 수 없습니다. Windows Server 2016 이전의 모든 Hyper-v 버전은 클래식 스케줄러만 지원 합니다. 핵심 scheduler에 대 한 지원은 최근에 게시 되었습니다.

## <a name="about-hypervisor-scheduler-types"></a>하이퍼바이저 스케줄러 형식 정보

이 문서에서는 특히 새 하이퍼바이저 코어 스케줄러 형식 및 레거시 "클래식" 스케줄러를 사용 하는 방법과 이러한 스케줄러 형식이 대칭 다중 스레딩 또는 SMT의 사용과 교차 하는 방법에 대해 중점적으로 설명 합니다.  핵심 및 클래식 스케줄러의 차이점과 각 위치가 기본 시스템 프로세서의 게스트 Vm에서 어떻게 작동 하는지 이해 하는 것이 중요 합니다.

### <a name="the-classic-scheduler"></a>클래식 스케줄러

클래식 스케줄러는 게스트 Vm에 속한 VPs 뿐만 아니라 루트 VPs를 포함 하 여 시스템 전체에서 VPs (가상 프로세서)에 대 한 작업을 예약 하는 공평 하 게 공유 하는 라운드 로빈 방법을 나타냅니다. 클래식 스케줄러는 모든 버전의 Hyper-v에서 사용 되는 기본 스케줄러 유형 (여기에 설명 된 대로 Windows Server 2019까지)입니다.  클래식 스케줄러의 성능 특성을 잘 이해 하 고 있으며, 클래식 스케줄러는 호스트의 VP (호스트의 VP: LP 비율에 따른 ably)의 구독을 가상화 되는 워크 로드의 유형, 전체 리소스 사용률 등

SMT를 사용 하는 가상화 호스트에서 실행 하는 경우 클래식 스케줄러는 독립적으로 코어에 속하는 각 SMT 스레드의 VM에서 게스트 VPs을 예약 합니다. 따라서 서로 다른 vm은 동일한 코어에서 동시에 실행 될 수 있습니다 (한 VM은 코어의 한 스레드에서 실행 되 고 다른 VM은 다른 스레드에서 실행 됨).

### <a name="the-core-scheduler"></a>핵심 스케줄러

핵심 스케줄러는 SMT의 속성을 활용 하 여 보안 및 시스템 성능에 영향을 주는 게스트 워크 로드의 격리를 제공 합니다. 핵심 스케줄러는 VM의 VPs가 형제 SMT 스레드에 예약 되도록 합니다. 이는 대칭적으로 수행 되므로 LPs가 2 그룹에 있는 경우 VPs가 2 그룹으로 예약 되 고 시스템 CPU 코어는 Vm 간에 공유 되지 않습니다.

기본 SMT 쌍에 대해 게스트 VPs를 예약 하 여 코어 스케줄러는 워크 로드 격리를 위한 강력한 보안 경계를 제공 하 고, 대기 시간에 민감한 워크 로드에 대 한 성능 변동을 줄이기 위해 사용 될 수도 있습니다.

SMT를 사용 하지 않는 가상 컴퓨터에 대해 VP가 예약 된 경우 해당 VP는 실행할 때 전체 코어를 사용 하 고 코어의 형제 SMT 스레드는 유휴 상태로 유지 됩니다.  이는 올바른 워크 로드 격리를 제공 하기 위해 필요 하지만 특히 시스템 LPs가 과도 하 게 구독 되는 경우, 즉 총 VP: LP 비율이 1:1를 초과 하는 경우 전체 시스템 성능에 영향을 줍니다. 따라서 코어 당 여러 스레드 없이 구성 된 게스트 Vm을 실행 하는 것은 최적의 구성입니다.

### <a name="benefits-of-the-using-the-core-scheduler"></a>핵심 스케줄러 사용의 이점

핵심 스케줄러는 다음과 같은 이점을 제공 합니다.

* 게스트 워크 로드 격리-게스트 VPs에 대 한 강력한 보안 경계는 보조 채널 스누핑 공격에 대 한 취약성을 줄이기 위해 기본 실제 코어 쌍에서 실행 되도록 제한 됩니다.

* 워크 로드의 변동 감소-게스트 워크 로드 처리량의 변동은 훨씬 감소 하므로 워크 로드 일관성을 향상 시킬 수 있습니다.

* 게스트 Vm에서 SMT 사용-게스트 가상 머신에서 실행 되는 OS 및 응용 프로그램은 SMT 동작 및 프로그래밍 인터페이스 (Api)를 활용 하 여 가상화 되지 않은 실행 시와 마찬가지로 smt 스레드 간에 작업을 제어 하 고 배포할 수 있습니다.

핵심 스케줄러는 현재 Azure 가상화 호스트에서 사용 되며, 특히 강력한 보안 경계 및 낮은 워크 로드 variabilty을 활용 합니다. Microsoft에서는 핵심 스케줄러 유형이이 고 대부분의 가상화 시나리오에 대 한 기본 하이퍼바이저 일정 유형인 것으로 간주 합니다.  따라서 고객에 게 기본적으로 보안을 유지 하기 위해 Microsoft는 Windows Server 2019에 대해 이러한 변경을 수행 합니다.

### <a name="core-scheduler-performance-impacts-on-guest-workloads"></a>게스트 워크 로드에 대 한 핵심 scheduler 성능 영향

특정 취약점 클래스를 효과적으로 완화 하는 데 필요한 반면 핵심 스케줄러는 잠재적으로 성능을 저하 시킬 수도 있습니다. 고객은 Vm과 성능 특성의 차이점을 확인 하 고 가상화 호스트의 전체 워크 로드 용량에 영향을 줄 수 있습니다. 핵심 스케줄러가 비 SMT VP를 실행 해야 하는 경우에는 기본 논리 코어의 명령 스트림 중 하나만 실행 되 고 나머지는 유휴 상태로 유지 되어야 합니다. 게스트 워크 로드에 대 한 총 호스트 용량을 제한 합니다.

이러한 성능 영향은이 문서의 배포 지침에 따라 최소화할 수 있습니다. 호스트 관리자는 특정 가상화 배포 시나리오를 신중 하 게 고려 하 고 최대 워크 로드 밀도, 과도 한 가상화 호스트의 통합에 대 한 필요성에 대 한 보안 위험에 대 한 허용 범위를 조정 해야 합니다.

## <a name="changes-to-the-default-and-recommended-configurations-for-windows-server-2016-and-windows-server-2019"></a>Windows Server 2016 및 Windows Server 2019의 기본 및 권장 구성에 대 한 변경 내용

최대 보안 상태를 사용 하 여 Hyper-v 호스트를 배포 하려면 하이퍼바이저 코어 스케줄러 유형을 사용 해야 합니다. 기본적으로 고객의 보안을 유지 하기 위해 Microsoft는 다음과 같은 기본 설정 및 권장 설정을 변경 합니다.

>[!NOTE]
>스케줄러 형식에 대 한 하이퍼바이저의 내부 지원은 Windows Server 2016, Windows Server 1709 및 Windows Server 1803의 초기 릴리스에 포함 되어 있지만, 다음을 선택할 수 있는 구성 컨트롤에 액세스 하려면 업데이트가 필요 합니다. 하이퍼바이저 스케줄러 유형입니다.  이러한 업데이트에 대 한 자세한 내용은 [hyper-v 하이퍼바이저 스케줄러 형식 이해 및 사용](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types) 을 참조 하세요.

### <a name="virtualization-host-changes"></a>가상화 호스트 변경

* 하이퍼바이저는 기본적으로 Windows Server 2019부터 코어 스케줄러를 사용 합니다.

* Microsoft reccommends Windows Server 2016에서 핵심 scheduler를 구성 합니다. 하이퍼바이저 코어 스케줄러 형식은 Windows Server 2016에서 지원 되지만 기본값은 클래식 스케줄러입니다. 핵심 스케줄러는 선택 사항이 며 Hyper-v 호스트 관리자가 명시적으로 사용 하도록 설정 해야 합니다.

### <a name="virtual-machine-configuration-changes"></a>가상 컴퓨터 구성 변경

* Windows Server 2019에서 기본 VM 버전 9.0을 사용 하 여 만든 새 가상 컴퓨터는 가상화 호스트의 SMT 속성 (사용 또는 사용 안 함)을 자동으로 상속 합니다. 즉, 실제 호스트에서 SMT를 사용 하는 경우 새로 만든 Vm은 SMT를 사용 하도록 설정 되며, 기본적으로 VM의 하드웨어 스레드 수가 기본 시스템과 동일한 하드웨어 스레드 수를 사용 하 여 호스트의 SMT 토폴로지를 상속 합니다. 이는 VM의 구성에 HwThreadCountPerCore = 0으로 반영 됩니다. 여기서 0은 VM이 호스트의 SMT 설정을 상속 해야 함을 나타냅니다.

* VM 버전이 8.2 이전 버전인 기존 가상 컴퓨터는 HwThreadCountPerCore에 대 한 원래 VM 프로세서 설정을 유지 하 고, 8.2 VM 버전 게스트의 기본값은 HwThreadCountPerCore = 1입니다. 이러한 게스트는 Windows Server 2019 호스트에서 실행 될 때 다음과 같이 처리 됩니다.

    1. VM의 VP 수가 LP 코어 수보다 작거나 같은 경우, VM은 코어 스케줄러에 의해 비 SMT VM으로 처리 됩니다. 단일 SMT 스레드에서 게스트 VP를 실행 하는 경우 코어의 형제 SMT 스레드는 idled가 됩니다. 이는 최적화 되지 않으므로 전반적인 성능 저하가 발생 합니다.

    2. VM이 LP 코어 보다 더 VPs 경우, VM은 코어 스케줄러에 의해 SMT VM으로 처리 됩니다. 그러나 VM은 SMT VM 임을 나타내는 다른 표시를 관찰 하지 않습니다. 예를 들어 운영 체제 또는 응용 프로그램에의 한 CPU 토폴로지을 쿼리 하는 데 CPUID 명령 또는 Windows Api를 사용 하면 SMT가 사용 하도록 설정 된 것으로 표시 되지 않습니다.

* 업데이트 VM 작업을 통해 기존 VM이 eariler VM 버전에서 9.0 버전으로 명시적으로 업데이트 되는 경우 VM은 HwThreadCountPerCore의 현재 값을 유지 합니다.  VM은 SMT force를 사용 하지 않습니다.

* Windows Server 2016에서는 게스트 Vm에 대해 SMT를 사용 하도록 설정 하는 것이 좋습니다.  기본적으로 Windows Server 2016에서 만든 Vm은 SMT를 사용 하지 않도록 설정 됩니다. 즉, 명시적으로 변경 하지 않는 한 HwThreadCountPerCore가 1로 설정 됩니다.

>[!NOTE]
>Windows Server 2016에서는 HwThreadCountPerCore을 0으로 설정할 수 없습니다.

#### <a name="managing-virtual-machine-smt-configuration"></a>가상 머신 SMT 구성 관리

게스트 가상 머신 SMT 구성은 VM 별로 설정 됩니다. 호스트 관리자는 VM의 SMT 구성을 검사 하 고 구성 하 여 다음 옵션 중에서 선택할 수 있습니다.

    1. SMT 지원으로 실행 되도록 Vm 구성, 선택적으로 호스트 SMT 토폴로지를 자동으로 상속

    2. 비 SMT로 실행 되도록 Vm 구성

VM에 대 한 SMT 구성는 Hyper-v 관리자 콘솔의 요약 창에 표시 됩니다.  Vm의 SMT 설정 구성은 VM 설정 또는 PowerShell을 사용 하 여 수행할 수 있습니다.

#### <a name="configuring-vm-smt-settings-using-powershell"></a>PowerShell을 사용 하 여 VM SMT 설정 구성

게스트 가상 컴퓨터에 대 한 SMT 설정을 구성 하려면 충분 한 권한이 있는 PowerShell 창을 열고 다음을 입력 합니다.

``` powershell
Set-VMProcessor -VMName <VMName> -HwThreadCountPerCore <0, 1, 2>
```

각 항목이 나타내는 의미는 다음과 같습니다.

    0 = Inherit SMT topology from the host (this setting of HwThreadCountPerCore=0 is not supported on Windows Server 2016)

    1 = Non-SMT

    Values > 1 = the desired number of SMT threads per core. May not exceed the number of physical SMT threads per core.

게스트 가상 컴퓨터에 대 한 SMT 설정을 읽으려면 충분 한 권한이 있는 PowerShell 창을 열고 다음을 입력 합니다.

``` powershell
(Get-VMProcessor -VMName <VMName>).HwThreadCountPerCore
```

HwThreadCountPerCore = 0으로 구성 된 게스트 Vm은 SMT가 게스트에 대해 사용 하도록 설정 되었음을 나타내고, 일반적으로 2 인 기본 가상화 호스트에 있는 것과 동일한 수의 SMT 스레드를 게스트에 노출 합니다.

### <a name="guest-vms-may-observe-changes-to-cpu-topology-across-vm-mobility-scenarios"></a>게스트 Vm은 VM 이동성 시나리오에서 CPU 토폴로지의 변경 내용을 관찰할 수 있습니다.

VM의 OS 및 응용 프로그램은 실시간 마이그레이션 또는 저장 및 복원 작업과 같은 VM 수명 주기 이벤트 전후에 호스트 및 VM 설정의 변경 내용을 볼 수 있습니다. VM 상태를 저장 하 고 복원 하는 작업 중에 VM의 HwThreadCountPerCore 설정 및 실현 된 값 (즉, VM 설정 및 원본 호스트의 구성에 대 한 계산 된 조합)이 마이그레이션됩니다. VM은 대상 호스트에서 이러한 설정으로 계속 실행 됩니다. VM이 종료 되 고 다시 시작 되는 시점에는 VM에서 관찰 된 인식 값이 변경 될 수 있습니다. OS 및 응용 프로그램 계층 소프트웨어는 일반적인 시작 및 초기화 코드 흐름의 일부로 CPU 토폴로지 정보를 찾아야 하므로이는 무해 합니다. 그러나 실시간 마이그레이션 또는 저장/복원 작업 동안 이러한 부팅 시간 초기화 시퀀스를 건너뜀 때문에 이러한 상태 전환을 수행 하는 Vm은 종료 되 고 다시 시작 될 때까지 원래 계산 된 값을 관찰할 수 있습니다.  

### <a name="alerts-regarding-non-optimal-vm-configurations"></a>최적이 아닌 VM 구성에 대 한 경고

호스트의 물리적 코어 보다 더 VPs로 구성 된 가상 머신은 최적이 아닌 구성으로 구성 됩니다. 하이퍼바이저 스케줄러는 이러한 Vm을 SMT에서 인식 하는 것 처럼 처리 합니다. 그러나 VM의 OS 및 응용 프로그램 소프트웨어에는 SMT를 사용 하지 않는 것을 보여 주는 CPU 토폴로지가 제공 됩니다. 이 상태가 검색 되 면 Hyper-v 작업자 프로세스가 가상화 호스트 경고에서 VM의 구성이 최적이 아닌 것을 권장 하 고 VM에 대해 SMT를 사용 하도록 설정 하는 이벤트를 기록 합니다.

#### <a name="how-to-identify-non-optimally-configured-vms"></a>최적으로 구성 되지 않은 Vm을 확인 하는 방법

Hyper-v 작업자 프로세스 이벤트 ID 3498에 대 한 이벤트 뷰어의 시스템 로그를 검사 하 여 비 SMT Vm을 식별할 수 있습니다. VM의 VPs 수가 실제 코어 수보다 클 때마다 VM에 대해 트리거됩니다. 작업자 프로세스 이벤트는 이벤트 뷰어 또는 PowerShell을 통해 가져올 수 있습니다.

#### <a name="querying-the-hyper-v-worker-process-vm-event-using-powershell"></a>PowerShell을 사용 하 여 Hyper-v 작업자 프로세스 VM 이벤트 쿼리

PowerShell을 사용 하 여 Hyper-v 작업자 프로세스 이벤트 ID 3498를 쿼리하려면 PowerShell 프롬프트에서 다음 명령을 입력 합니다.

``` powershell
Get-WinEvent -FilterHashTable @{ProviderName="Microsoft-Windows-Hyper-V-Worker"; ID=3498}
```

### <a name="impacts-of-guest-smt-configuaration-on-the-use-of-hypervisor-enlightenments-for-guest-operating-systems"></a>게스트 운영 체제에 대해 하이퍼바이저 enlightenments를 사용할 때 게스트 SMT 구성의 영향

Microsoft 하이퍼바이저는 여러 enlightenments 또는 힌트를 제공 합니다 .이는 게스트 VM에서 실행 되는 OS가 성능을 향상 시키거나 실행 시 다양 한 조건의 처리를 향상 시킬 수 있는 것과 같은 최적화를 트리거하는 데 사용할 수 있습니다. 방식의. 최근 도입 된 계몽은 가상 프로세서 예약 처리와 SMT를 활용 하는 측면 채널 공격에 대 한 OS 완화의 사용을 고려 합니다.

>[!NOTE]
>호스트 관리자가 게스트 Vm에 대해 SMT를 사용 하도록 설정 하 여 워크 로드 성능을 최적화 하는 것이 좋습니다.

이 게스트 계몽의 세부 정보는 아래에 제공 됩니다. 그러나 가상화 호스트 관리자를 위한 주요 요점은는 가상 머신이 호스트의 물리적 SMT 구성과 일치 하도록 구성 HwThreadCountPerCore 해야 한다는 것입니다. 이렇게 하면 하이퍼바이저에서 아키텍처 이외의 핵심 공유가 없음을 보고할 수 있습니다. 따라서 계몽이 필요한 최적화를 지 원하는 모든 게스트 OS를 사용할 수 있습니다. Windows Server 2019에서는 새 Vm을 만들고 기본값은 HwThreadCountPerCore (0)으로 그대로 둡니다. Windows Server 2016 호스트에서 마이그레이션된 이전 Vm을 Windows Server 2019 구성 버전으로 업데이트할 수 있습니다. 이렇게 한 후에는 HwThreadCountPerCore = 0을 설정 하는 것이 좋습니다.  Windows Server 2016에서는 호스트 구성과 일치 하도록 HwThreadCountPerCore를 설정 하는 것이 좋습니다 (일반적으로 2).

### <a name="nononarchitecturalcoresharing-enlightenment-details"></a>NoNonArchitecturalCoreSharing 계몽 정보

Windows Server 2016부터 하이퍼바이저는 게스트 OS에 대 한 VP 일정 및 배치의 처리를 설명 하는 새로운 계몽을 정의 합니다. 이 계몽은 [하이퍼바이저 최상위 기능 사양 v 5.0 c](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/tlfs)에 정의 되어 있습니다.

하이퍼바이저 가상 CPUID 리프 CPUID. 0x40000004. EAX: 18 [NoNonArchitecturalCoreSharing = 1]은 가상 프로세서에서 형제 SMT로 보고 되는 가상 프로세서를 제외 하 고 실제 코어를 다른 가상 프로세서와 공유 하지 않음을 나타냅니다. 임계값. 예를 들어, 게스트 VP는 동일한 프로세서 코어의 형제 SMT 스레드에서 동시에 실행 되는 루트 VP와 함께 SMT 스레드에서 실행 되지 않습니다. 이 상태는 가상화 된를 실행 하는 경우에만 가능 하며, 따라서 심각한 보안 문제도 발생 하는 아키텍처 이외의 SMT 동작을 나타냅니다. 게스트 OS는 최적화를 사용 하도록 설정 하는 것이 안전 하다는 것을 나타내는 NoNonArchitecturalCoreSharing = 1을 사용할 수 있습니다 .이는 STIBP 설정의 성능 오버 헤드를 방지 하는 데 도움이 될 수 있습니다.

특정 구성에서는 하이퍼바이저가 NoNonArchitecturalCoreSharing = 1을 나타내지 않습니다. 예를 들어, 호스트에서 SMT를 사용 하도록 설정 하 고 하이퍼바이저 클래식 스케줄러를 사용 하도록 구성 된 경우 NoNonArchitecturalCoreSharing는 0이 됩니다. 이로 인해 지원 게스트가 특정 최적화를 사용 하지 못할 수 있습니다. 따라서 SMT를 사용 하는 호스트 관리자가 하이퍼바이저 코어 스케줄러를 사용 하 고 최적의 워크 로드 성능을 보장 하기 위해 호스트에서 SMT 구성을 상속 하도록 가상 컴퓨터를 구성 하는 것이 좋습니다.

## <a name="summary"></a>요약

보안 위협 가로는 지속적으로 발전 하 고 있습니다. 사용자가 기본적으로 보안을 유지 하기 위해 Microsoft는 Windows Server 2019 Hyper-v에서 시작 하는 하이퍼바이저 및 가상 컴퓨터에 대 한 기본 구성을 변경 하 고 Windows를 실행 하는 고객에 게 업데이트 된 지침 및 권장 사항을 제공 합니다. 서버 2016 Hyper-v. 가상화 호스트 관리자는 다음을 수행 해야 합니다.

* 이 문서에 제공 된 지침을 읽고 이해 합니다.

* 해당 가상화 배포를 신중 하 게 평가 하 고 조정 하 여 고유한 요구 사항에 대 한 보안, 성능, 가상화 밀도 및 워크 로드 응답성 목표를 충족 하는지 확인 합니다.

* 하이퍼바이저 핵심 스케줄러에서 제공 하는 강력한 보안 혜택을 활용 하도록 기존 Windows Server 2016 Hyper-v 호스트를 다시 구성 하는 것이 좋습니다.

* 하드웨어 보안 취약점을 해결 하는 VP 격리에 의해 적용 되는 일정 제약 조건에서 성능 영향을 줄이기 위해 기존 비 SMT Vm을 업데이트 합니다.
