---
title: Hyper-v 하이퍼바이저 스케줄러 유형 선택에 대 한
description: 모드 Hyper-v의 스케줄러를 사용 하 여 Hyper-v 호스트 관리자에 대 한 정보를 제공
author: allenma
ms.author: allenma
ms.date: 08/14/2018
ms.topic: article
ms.prod: windows-server-hyper-v
ms.technology: virtualization
ms.localizationpriority: low
ms.assetid: 5fe163d4-2595-43b0-ba2f-7fad6e4ae069
ms.openlocfilehash: c5360d8e2fdc23f8b05c6be0f665407eebedeba2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823884"
---
# <a name="about-hyper-v-hypervisor-scheduler-type-selection"></a>Hyper-v 하이퍼바이저 스케줄러 유형 선택에 대 한

적용 대상:

* Windows Server 2016
* Windows Server, 버전 1709
* Windows Server, 버전 1803
* Windows Server 2019

이 문서는 Hyper-v의 기본 중요 한 변경 내용을 설명 합니다 하 고 스케줄러 형식 하이퍼바이저의 사용을 권장 합니다. 이러한 변경 내용을 모두 시스템 보안 및 가상화 성능 영향을 합니다. 가상화 호스트 관리자는 검토 변경 및이 문서에서 설명 하는 의미를 이해 하 고 영향, 제안 된 배포 지침 및 배포 하 고 관리 하는 방법을 이해 하는 데 관련 된 위험 요소를 신중 하 게 평가 신속 하 게 변화 하는 보안 상황 발생 하는 경우 Hyper-v 호스트입니다.

>[!IMPORTANT]
>현재 알려진 동시 설치 된 호스트에서 실행 하는 경우 레거시 하이퍼바이저 클래식 스케줄러 형식의 예약 동작을 통해 악성 게스트 VM에서 여러 프로세서 아키텍처에서 보이는 취약점 악용 될 수 사이드 채널 보안 다중 스레딩 (SMT) 사용 하도록 설정 합니다.  취약점을 악용 하는 경우 악의적인 작업 수의 파티션 경계 외부에 있는 데이터를 관찰 합니다. 하이퍼바이저 core 스케줄러 유형 및 다시 구성 게스트 Vm 활용 하려면 Hyper-v 하이퍼바이저를 구성 하 여이 클래스의 공격을 완화할 수 있습니다. Core 스케줄러를 사용 하 여 하이퍼바이저 게스트 VM의 VPs 하므로 VM의 데이터에 액세스할 수 실행 되는 실제 코어의 경계를 강력 하 게 격리를 동일한 물리적 프로세서 코어에서 실행 되도록 제한 합니다.  이 VM 인지 다른 파티션에서 모든 아티팩트를 관찰 하지 못하게 하는 이러한 사이드 채널 공격 으로부터 매우 효과적인 완화 루트 또는 다른 게스트 파티션 합니다.  따라서 Microsoft 기본값을 변경 하 고 가상화 호스트 및 게스트 Vm에 대 한 구성 설정을 권장 합니다.

## <a name="background"></a>배경

Windows Server 2016부터 Hyper-v는 예약 및 하이퍼바이저 스케줄러 형식 이라고 하는 가상 프로세서를 관리 하는 여러 방법을 지원 합니다.  모든 하이퍼바이저 스케줄러 유형에 대 한 자세한 설명을 찾을 수 있습니다 [이해 하 고 Hyper-v 하이퍼바이저 스케줄러 형식을 사용 하 여](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types)입니다.

>[!NOTE]
>새 하이퍼바이저 스케줄러 형식에는 Windows Server 2016을 사용 하 여 처음으로 도입 및 이전 릴리스에서 사용할 수 없는 합니다. 모든 버전의 Windows Server 2016 이전 Hyper-v 클래식 스케줄러만 지원합니다. Core 스케줄러에 대 한 지원이 최근에 게시 되었습니다.

## <a name="about-hypervisor-scheduler-types"></a>하이퍼바이저 스케줄러 형식에 대 한

이 문서에서는 레거시 "클래식" 스케줄러와 새 하이퍼바이저 core 스케줄러 형식 사용 하 여 및 대칭 다중 스레딩 또는 SMT 사용 하 여 스케줄러 이와 교차 하는 방법에 특히 중점을 둡니다.  코어 및 클래식 스케줄러 및 기본 시스템 프로세서에서 게스트 Vm에서 작업 각 배치 하는 방법 간의 차이점을 이해 하는 것이 반드시 합니다.

### <a name="the-classic-scheduler"></a>클래식 스케줄러

클래식 스케줄러-루트 VPs 뿐만 아니라 게스트 Vm에 속한 VPs 비롯 한 시스템에서 가상 프로세서 (VPs)에서 작업을 예약 하는 공유 fair 라운드 로빈 메서드를 가리킵니다. 클래식 스케줄러가 기본 스케줄러 유형 (Windows Server 2019, 여기에 설명 된 대로)까지 모든 버전의 Hyper-v에서 사용 되었습니다.  클래식 스케줄러의 성능 특징을 잘 이해 하 고 ably 과도 한 워크 로드-적절 한 여백으로 호스트의 VP:LP 비율 과도 한 구독, 구독을 지원 하기 위해 클래식 스케줄러를 보여 줍니다 (따라는 유형의 워크 로드 가상화 되 고, 전체 리소스 사용률 등.).

사용 하도록 설정 하는 SMT를 사용 하 여 가상화 호스트에서 실행 하는 경우 클래식 스케줄러 속하는 하지 코어를 독립적으로 각 SMT 스레드에서 모든 VM에서 게스트 VPs 예약 됩니다. 따라서 동시 (다른 VM이 다른 스레드에서 실행 되는 동안 코어의 스레드에서 실행 중인 하나의 VM)에 여러 Vm을 동일한 코어에서 실행할 수 있습니다.

### <a name="the-core-scheduler"></a>Core 스케줄러

Core 스케줄러 보안과 시스템 성능에 영향을 줍니다 게스트 워크 로드의 격리를 제공 하는 SMT의 속성을 활용 합니다. Core 스케줄러 VM에서 VPs 된 형제 SMT 스레드에서 예약 되었는지 확인 합니다. 있도록 LPs가 있는 경우 두 VPs 그룹 두 개를 그룹에서 예약 된 시스템 CPU 코어 Vm 간에 공유 되지 않는 대칭적으로 수행 됩니다.

기본 SMT 쌍에 대해 게스트 VPs에 예약 하 여 핵심 스케줄러가 워크 로드 격리에 대 한 강력한 보안 경계를 제공 하 고 대기 시간이 중요 한 워크 로드에 대 한 성능 변화를 줄이기 위해 사용할 수도 있습니다.

Note는 VP SMT를 사용 하도록 설정 하지 않고 가상 컴퓨터에 대 한 예약 된 실행 및 코어의 형제 SMT 스레드 유휴 상태가 될 때 VP가 전체 코어를 사용 하면 됩니다.  이 올바른 워크 로드 격리를 제공 해야 하지만 특히 해지면 시스템 LPs 과도 하 게 구독-즉, 총 VP:LP 비율이 1:1을 초과할 경우 전체 시스템 성능에 영향을 줍니다. 따라서 게스트 Vm 코어당 여러 스레드 없이 구성 실행 구성은 최적입니다.

### <a name="benefits-of-the-using-the-core-scheduler"></a>Core 스케줄러를 사용 하는 이점

Core 스케줄러는 다음과 같은 이점을 제공합니다.

* 강력한 보안 경계를 게스트 워크 로드 격리-게스트 VPs 사이드 채널 스누핑 공격에 대 한 취약점을 줄이는 기본 물리적 코어 쌍에서 실행 되도록 제한 됩니다.

* 축소 된 워크 로드 변화-게스트 워크 로드에 대 한 처리량의 변동 크게 줄어들고 큰 워크 로드 일관성을 제공 합니다.

* 게스트 OS 및 게스트 가상 머신에서 실행 중인 응용 프로그램 Vm에에서 SMT 사용 하는 SMT 동작을 활용할 수 있습니다 및 프로그래밍 인터페이스 (Api)를 제어 하 고 실행할 때 것 처럼 SMT 스레드 간에 작업을 분산 가상화 되지 않은 합니다.

강력한 보안 경계 및 낮은 워크 로드 variabilty 활용 하도록 특별히 core 스케줄러는 현재 Azure 가상화 호스트에서 사용 됩니다. Microsoft은 핵심 스케줄러 형식 이어야 하는 대부분의 가상화 시나리오에 대 한 형식을 예약 기본 하이퍼바이저에 계속 믿습니다.  따라서 고객에 게는 기본적으로 보안을 위해 Microsoft는이 변경을 사항을 Windows Server 2019에 대해 이제 합니다.

### <a name="core-scheduler-performance-impacts-on-guest-workloads"></a>게스트 워크 로드 핵심 스케줄러 성능에 미치는 영향

을 효과적으로 특정 종류의 문제를 완화 하는 데 필요 하지만 핵심 스케줄러는 성능 수도 줄일 수 있습니다. 고객에 게 해당 가상화 호스트의 전체 워크 로드 용량에 영향을 확인 하 고 Vm을 사용 하 여 성능 특성에 차이가 나타날 수 있습니다. Core 스케줄러 비-SMT VP 실행할 해야 하는 경우에서 다른 두어야 유휴 하는 동안 실행 기본 논리 코어에서 명령 스트림 중 하나에 합니다. 이 게스트 워크 로드에 대 한 총 호스트 용량을 제한 합니다.

이 문서에서는 배포 지침에 따라 이러한 성능에 미치는 영향을 최소화할 수 있습니다. 신중 하 게 호스트 관리자가 특정 가상화 배포 시나리오를 고려 하 고 최대 워크 로드 밀도, 가상화 호스트 등의 과도 한 통합에 대 한 보안 위험에 대 한 허용 범위를 분산 해야 합니다.

## <a name="changes-to-the-default-and-recommended-configurations-for-windows-server-2016-and-windows-server-2019"></a>기본 및 Windows Server 2016 및 Windows Server 2019에 대 한 권장된 구성 변경

최대 보안 태세를 사용 하 여 Hyper-v 호스트를 배포 하려면 하이퍼바이저 core 스케줄러 형식 사용 합니다. 고객에 게는 기본적으로 보안을 위해 Microsoft는 다음과 같은 기본 변경과 권장 설정입니다.

>[!NOTE]
>Scheduler 형식에 대 한 하이퍼바이저의 내부 지원 Windows Server 2016, Windows Server 1709 및 Windows Server 1803의 초기 릴리스에서 포함 된, 업데이트는 선택 허용 하는 구성 컨트롤에 액세스 하기 위해 필요 합니다 하이퍼바이저 스케줄러 형식입니다.  참조 하십시오 [이해 하 고 Hyper-v 하이퍼바이저 스케줄러 형식을 사용 하 여](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types) 이러한 업데이트에 대 한 자세한 내용은 합니다.

### <a name="virtualization-host-changes"></a>가상화 호스트 변경

* 하이퍼바이저는 Windows Server 2019부터 기본적으로 core 스케줄러를 사용 합니다.

* Microsoft reccommends Windows Server 2016 core scheduler를 구성 합니다. 하지만 하이퍼바이저 핵심 스케줄러 형식은 기본값은 클래식 스케줄러 Windows Server 2016에서 지원 됩니다. Core 스케줄러는 선택 사항이 며 Hyper-v 호스트 관리자가 명시적으로 설정 해야 합니다.

### <a name="virtual-machine-configuration-changes"></a>가상 컴퓨터 구성 변경

* Windows Server 2019에 기본 VM 버전 9.0을 사용 하 여 만든 새 가상 컴퓨터는 자동으로 상속 SMT 속성 (사용 또는 사용 안 함)의 가상화 호스트 합니다. 즉, SMT를 사용 하는 경우 새로 만든 Vm, 물리적 호스트 사용 하도록 설정 하는 SMT를 갖게 됩니다 및 기본 시스템으로 코어당 하드웨어 스레드 수가 동일한 VM을 사용 하 여 기본적으로 호스트의 SMT 토폴로지를 상속 합니다. 이 HwThreadCountPerCore 사용 하 여 VM의 구성에 반영 됩니다 = 0, 여기서 0은 VM 호스트의 SMT 설정을 상속 합니다.

* 8.2 또는 이전 버전의 VM 버전을 사용 하 여 기존 가상 머신을 유지 HwThreadCountPerCore에 대 한 원래 VM 프로세서 설정 및 8.2 VM 버전 게스트에 대 한 기본값은 HwThreadCountPerCore = 1입니다. 이러한 게스트를 Windows Server 2019 호스트에서 실행 하는 경우 다음과 같이 처리 됩니다.

    1. VM에 VP count를 LP 코어의 개수 보다 작거나 같은 경우 VM 코어 scheduler에 의해으로 비-SMT VM 처리 됩니다. 게스트 VP 단일 SMT 스레드에서 실행 되 면 SMT 스레드 코어의 형제 유휴 됩니다. 최적이 아닌 이며 전반적인 성능이 저하 됩니다.

    2. VM LP 코어 보다 자세한 VPs 있으면 VM은 SMT VM으로 core scheduler에 의해 처리 됩니다. 그러나 VM는 SMT VM에는 다른 문제가 관찰 하지 않습니다. 예를 들어, OS 또는 응용 프로그램에서 CPU 토폴로지를 쿼리 하 CPUID 명령이 나 Windows Api의 사용은 SMT를 사용할 수 있도록을 표시 하지 않습니다.

* 기존 VM이 명시적으로 업데이트 VM 작업을 통해 버전 9.0 VM 버전 이전 버전에서에서 업데이트를 하는 경우 VM HwThreadCountPerCore에 대 한 현재 값을 유지 합니다.  VM에 SMT 강제 사용 없을 것입니다.

* Windows Server 2016에서 게스트 Vm에 SMT를 사용 하도록 하는 것이 좋습니다.  기본적으로 SMT 사용 하지 않도록 설정한, Windows Server 2016에서 만든 Vm의 경우 이것이 HwThreadCountPerCore 1로 설정 된 명시적으로 변경 되지 않은 경우입니다.

>[!NOTE]
>Windows Server 2016에는 0으로 HwThreadCountPerCore 설정을 지원 하지 않습니다.

#### <a name="managing-virtual-machine-smt-configuration"></a>가상 머신 SMT 구성 관리

게스트 가상 머신 SMT 구성은 VM 당 단위로 설정 됩니다. 호스트 관리자는 검사 하 고 VM의 SMT 구성에서 다음 옵션을 선택할 수 있습니다.

    1. 으로 SMT 지원, 필요에 따라 호스트 SMT 토폴로지를 자동으로 상속을 실행 하는 Vm 구성

    2. Vm이 비-SMT로 실행 되도록 구성 합니다.

VM에 SMT 구성 Hyper-v Manager 콘솔에서 요약 창에 표시 됩니다.  VM의 SMT 설정을 구성 하는 VM 설정 또는 PowerShell을 사용 하 여 수행할 수 있습니다.

#### <a name="configuring-vm-smt-settings-using-powershell"></a>PowerShell을 사용 하 여 VM SMT 설정 구성

게스트 가상 머신에 대 한 SMT 설정을 구성 하려면 충분 한 권한이 및 형식으로 PowerShell 창을 엽니다.

``` powershell
Set-VMProcessor -VMName <VMName> -HwThreadCountPerCore <0, 1, 2>
```

각 항목이 나타내는 의미는 다음과 같습니다.

    0 = Inherit SMT topology from the host (this setting of HwThreadCountPerCore=0 is not supported on Windows Server 2016)

    1 = Non-SMT

    Values > 1 = the desired number of SMT threads per core. May not exceed the number of physical SMT threads per core.

SMT 설정이 게스트 가상 머신에 대 한 내용은 충분 한 권한이 및 형식으로 PowerShell 창을 엽니다.

``` powershell
(Get-VMProcessor -VMName <VMName>).HwThreadCountPerCore
```

해당 게스트 HwThreadCountPerCore로 구성 된 Vm을 참고 = 0 나타냅니다 SMT 게스트에 대 한 사용 하도록 설정 하 고 일반적으로 2 기본 가상화 호스트의 경우와 동일한 게스트 SMT 스레드 수가 표시 됩니다.

### <a name="guest-vms-may-observe-changes-to-cpu-topology-across-vm-mobility-scenarios"></a>게스트 Vm VM 모바일 시나리오에 걸쳐 CPU 토폴로지 변경 내용을 관찰할 수 있습니다.

OS 및 VM에서 응용 프로그램 VM 수명 주기 이벤트와 같은 실시간 마이그레이션 또는 저장 및 복원 작업 후 변경 하기 전에 VM 설정을 호스트에 표시 될 수 있습니다. 어떤 VM 상태를 저장 하 고 복원 작업 중 VM의 HwThreadCountPerCore 설정과 실현된 값 (즉, VM의 설정을 원본 호스트의 구성과 계산된 조합)을 모두 마이그레이션됩니다. VM은 대상 호스트에서 이러한 설정 사용 하 여 실행을 계속 합니다. VM이 종료 시점 및 다시 시작 수 있습니다.이 표시 값을 관찰 하는 VM에서 변경 됩니다. 무해 한 해야, OS 및 응용 프로그램으로 계층의 소프트웨어는 일반 시작 및 초기화 코드 흐름의 일부로 CPU 토폴로지 정보를 확인 해야 합니다. 그러나 이러한 시퀀스는 실시간 마이그레이션 또는 저장/복원 작업, 이러한 상태 전환 되는 Vm 중 건너뜁니다 초기화의 부팅 시 관찰 수 때문에 원래 계산 종료 될 때까지 값을 실현 하 고 다시 시작 합니다.  

### <a name="alerts-regarding-non-optimal-vm-configurations"></a>최적화 되지 않은 VM 구성에 대 한 경고

가상 컴퓨터에 실제 코어를 호스트 하면 최적이 아닌 구성에서 보다 자세한 VPs를 사용 하 여 구성 합니다. 하이퍼바이저 스케줄러는 SMT 인식 된 것 처럼 이러한 Vm을 처리 합니다. 그러나 OS는 VM에서 응용 프로그램 소프트웨어 SMT 되지 보여 주는 CPU 토폴로지를 표시 됩니다. Hyper-v가 작업자 프로세스는 VM의 구성이 최적이 아닌 이며 SMT를 권장할 호스트 관리자 경고 가상화 호스트에 이벤트가 기록 됩니다이 상태가 감지 되 면 VM에 대해 사용 하도록 설정 합니다.

#### <a name="how-to-identify-non-optimally-configured-vms"></a>Vm을 구성 하는 비 최적으로 식별 하는 방법

비-SMT Vm Hyper-v 작업자 프로세스 ID 3498 이벤트에 대 한 이벤트 뷰어에서 시스템 로그를 검사 하 여 VM에서 VPs 수가 실제 코어 수보다 큰 때마다 VM에 대 한 트리거를 식별할 수 있습니다. 이벤트 뷰어를에서 또는 PowerShell을 통해 이벤트를 처리 하는 작업자를 가져올 수 있습니다.

#### <a name="querying-the-hyper-v-worker-process-vm-event-using-powershell"></a>PowerShell을 사용 하 여 Hyper-v 작업자 프로세스 VM 이벤트를 쿼리 합니다.

쿼리를 PowerShell 프롬프트에서 다음 명령을 입력 PowerShell을 사용 하 여 Hyper-v 작업자 프로세스 ID 3498 이벤트에 대 한 합니다.

``` powershell
Get-WinEvent -FilterHashTable @{ProviderName="Microsoft-Windows-Hyper-V-Worker"; ID=3498}
```

### <a name="impacts-of-guest-smt-configuaration-on-the-use-of-hypervisor-enlightenments-for-guest-operating-systems"></a>게스트 운영 체제에 대 한 하이퍼바이저 enlightenments 사용 게스트 SMT 구성의 영향을 줍니다.

Microsoft 하이퍼바이저 여러 enlightenments 또는 게스트 VM에서에서 실행 중인 OS를 쿼리하고 성능에 도움이 될 수 있습니다 하거나 실행 하는 경우 다양 한 조건 처리를 개선 하는 것과 같은 최적화를 트리거하는 데 사용할 수 있는 힌트 제공 가상화 합니다. 하나의 최근에 도입 된 계몽 SMT를 악용 하는 사이드 채널 공격에 대 한 OS 완화 방법 사용 하 여 가상 프로세서 스케줄링 처리와 관련 됩니다.

>[!NOTE]
>호스트 관리자 워크 로드 성능을 최적화 하기 위해 게스트 Vm에 SMT 수 있도록 하는 것이 좋습니다.

하지만이 게스트 계몽의 세부 정보에는 아래 가상화 호스트가 관리자에 대 한 요점은 가상 컴퓨터 호스트의 실제 SMT 구성과 일치 하도록 HwThreadCountPerCore 있어야 함을 제공 됩니다. 이 보고서 없습니다 아키텍처 core는 하이퍼바이저를 통해 공유 합니다. 따라서 계몽을 필요로 하는 모든 게스트 OS 지원 최적화를 사용할 수 있습니다. Windows Server 2019에 새 Vm 만들기 및 HwThreadCountPerCore (0)의 기본값을 그대로 둡니다. 이전 Vm 마이그레이션 Windows Server 2016에서 호스트를 Windows Server 2019 구성 버전을 업데이트할 수 있습니다. 그러면 권장 HwThreadCountPerCore 설정 = 0.  Windows Server 2016에서 호스트 구성 (일반적으로 2)에 맞게 HwThreadCountPerCore 설정을 권장 합니다.

### <a name="nononarchitecturalcoresharing-enlightenment-details"></a>NoNonArchitecturalCoreSharing 계몽 세부 정보

Windows Server 2016 부터는 하이퍼바이저 VP 예약 및 게스트 OS에 대 한 배치 처리를 설명 하는 새 계몽을 정의 합니다. 이 계몽에 정의 된 [하이퍼바이저 최상위 기능 사양 v5.0c](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/tlfs)합니다.

하이퍼바이저 가상 CPUID 리프 CPUID.0x40000004.EAX:18[NoNonArchitecturalCoreSharing = 1] 가상 프로세서 SMT 형제로 보고 되는 가상 프로세서를 제외 하 고 다른 가상 프로세서를 사용 하 여 실제 코어를 공유 하지 않습니다를 나타냅니다. 스레드입니다. 예를 들어 게스트 VP 실행 되지 않습니다 루트 VP 함께 SMT 스레드에서 형제 SMT 스레드에서 동일한 프로세서 코어에서 동시에 실행 합니다. 이 문제는 가상화 된를 실행 하는 경우에 가능 않으며 하므로 심각한 보안 문제가 발생할 수도 있는 아키텍처 SMT 동작을 나타냅니다. 게스트 OS NoNonArchitecturalCoreSharing를 사용할 수 = 1 STIBP를 설정 하는 성능 오버 헤드를 방지 하는 데 도움이 되는 최적화를 사용 하도록 설정 해도 안전 하다 나타냅니다.

특정 구성에서 하이퍼바이저 표시 하지 것입니다는 NoNonArchitecturalCoreSharing = 1입니다. 예를 들어 호스트를 사용 하도록 설정 하는 SMT가 있고 하이퍼바이저 클래식 scheduler를 사용 하 여 구성 된 경우 NoNonArchitecturalCoreSharing 0이 됩니다. 이 지원된 게스트 특정 최적화를 사용 하도록 설정할 수 못할 수 있습니다. 따라서 Microsoft 권장 SMT를 사용 하 여 호스트 관리자 하이퍼바이저 core 스케줄러를 사용 하 고 가상 컴퓨터가 최적의 작업 성능을 보장 하기 위해 호스트에서 해당 SMT 구성을 상속 하도록 구성 되어 있는지 확인 합니다.

## <a name="summary"></a>요약

보안 위협 상황에 계속 발전 하는 것입니다. 고객에 게는 기본적으로 보안을 위해 Microsoft는 하이퍼바이저 및에서 Windows Server 2019 Hyper-v를 시작 하는 virtual machines에 대 한 기본 구성 변경과 지침과 Windows를 실행 하는 고객에 대 한 권장 업데이트 제공 서버 2016 Hyper-v가 설치 합니다. 가상화 호스트 관리자는 다음 작업을 수행 해야합니다.

* 읽고이 문서에서 제공 하는 지침 이해

* 신중 하 게 평가 하 고 보안, 성능, 가상화 밀도 및 고유한 요구 사항에 대 한 워크 로드 응답성 목표를 충족 하는지 확인 하 여 가상화 배포를 조정 합니다.

* 하이퍼바이저 core 스케줄러에서 제공 하는 강력한 보안 이점을 활용 하 여 기존 Windows Server 2016 Hyper-v 호스트를 다시 구성 고려

* 기존 비 SMT Vm 하드웨어 보안 취약점을 해결 하는 VP 격리에서 설정한 제약 조건의 예약에서 성능에 미치는 영향을 줄이기 위해 업데이트
