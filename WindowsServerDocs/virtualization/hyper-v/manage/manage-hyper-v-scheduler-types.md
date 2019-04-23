---
title: 이해 및 Hyper-v 하이퍼바이저 스케줄러 형식 사용
description: 모드 Hyper-v의 스케줄러를 사용 하 여 Hyper-v 호스트 관리자에 대 한 정보를 제공
author: allenma
ms.author: allenma
ms.date: 08/14/2018
ms.topic: article
ms.prod: windows-server-hyper-v
ms.technology: virtualization
ms.localizationpriority: low
ms.assetid: 6cb13f84-cb50-4e60-a685-54f67c9146be
ms.openlocfilehash: 7af6d68b02367d349580eacb27405c6f37e97ff8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871994"
---
# <a name="managing-hyper-v-hypervisor-scheduler-types"></a>관리 Hyper-v 하이퍼바이저 스케줄러 형식

>적용 대상: Windows 10, Windows Server 2016, Windows Server 1709 버전, Windows Server, 버전 1803에서 Windows Server 2019

이 문서에서는 Windows Server 2016에서 처음 도입 된 논리를 예약 하는 가상 프로세서의 새 모드에 설명 합니다. 이러한 모드 또는 스케줄러 형식 Hyper-v 하이퍼바이저 할당 하 고 게스트 가상 프로세서 간에 작업을 관리 하는 방법을 결정 합니다. Hyper-v 호스트 관리자 게스트 가상 컴퓨터 (Vm)에 가장 적합 한 예약 논리를 활용 하도록 Vm을 구성 하는 하이퍼바이저 스케줄러 형식 선택할 수 있습니다.

>[!NOTE]
>이 문서에 설명 된 하이퍼바이저 스케줄러 기능을 사용 하려면 업데이트가 필요 합니다. 자세한 내용은 참조 하세요 [필수 업데이트가](#required-updates)합니다.

## <a name="background"></a>배경

논리 및 예약 하는 Hyper-v 가상 프로세서 뒤의 컨트롤에 설명 하기 전에이 문서에서 다루는 기본 개념을 검토 하는 것이 유용 합니다.

### <a name="understanding-smt"></a>SMT 이해

다중 스레딩, 동시 또는 SMT 프로세서 리소스를 별도 독립 실행 스레드에 의해 공유할 수 있는 기술을 최신 프로세서 디자인에서 사용 되었습니다. 일반적으로 SMT 명령 처리량 증가 가능 하면 계산을 병렬화 하 여 대부분의 워크 로드는 어느 정도의 성능 향상을 제공, 성능 얻거나 성능이 약간 저하도 있지만 용 스레드 간의 경합 하는 경우 발생할 수 있습니다. 공유 프로세서 리소스가 발생 합니다.
SMT를 지 원하는 프로세서 Intel 및 AMD에서 제공 됩니다. Intel은 Intel 하이퍼 스레딩 기술 또는 Intel HT으로 SMT 제품을 가리킵니다.

이 문서에서는 SMT 및 Hyper-v에서 활용 하는 방식을 설명 Intel 및 AMD 시스템 모두에 동일 하 게 적용 됩니다.

* Intel HT 기술에 대 한 자세한 내용은 참조 [Intel 하이퍼 스레딩 기술](https://www.intel.com/content/www/us/en/architecture-and-technology/hyper-threading/hyper-threading-technology.html)

* AMD SMT에 대 한 자세한 내용은 참조 ["Zen" 핵심 아키텍처](https://www.amd.com/en/technologies/zen-core)

## <a name="understanding-how-hyper-v-virtualizes-processors"></a>Hyper-v는 프로세서를 가상화 하는 방법 이해

하이퍼바이저 스케줄러 형식을 고려 하기 전에 Hyper-v 아키텍처를 이해 하면 도움이 이기도 합니다. 일반 요약에서 찾을 수 있습니다 [Hyper-v 기술 개요](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-technology-overview)합니다. 다음은이 문서에 대 한 중요 한 개념입니다.

* Hyper-v가 만들고 파티션을 가상 컴퓨터 간에 계산 리소스 할당 되 고 공유, 하이퍼바이저의 제어를 관리 합니다. 파티션 및 게스트 Vm 및 루트 파티션에 모든 게스트 가상 컴퓨터 간의 강력한 격리 경계를 제공합니다.

* 루트 파티션에 파티션입니다 자체 가상 컴퓨터를 고유 속성 및 게스트 가상 머신 보다 훨씬 많은 권한이 있지만. 루트 파티션에 모든 게스트 가상 컴퓨터를 제어 하는 관리 서비스를 제공 하 고, 게스트 가상 장치 지, 게스트 가상 컴퓨터에 대 한 모든 장치 I/O를 관리 합니다. 루트 파티션에에서 모든 응용 프로그램 워크 로드를 실행 되지 않는 것이 좋습니다.

* 루트 파티션에의 각 가상 프로세서 (VP)은 기본 논리 프로세서 (LP)에 매핑된 1:1입니다. VP 호스트는 동일한 기본 LP 항상 실행 됩니다.-루트 파티션의 VPs의 마이그레이션이 합니다.

* 기본적으로 호스트 VPs 실행 LPs 게스트 VPs 실행할 수도 있습니다.

* 사용 가능한 모든 논리적 프로세서에서 실행 되도록 하이퍼바이저에서 게스트 VP은 예약할 수 있습니다. 게스트 VP를 예약할 때 임시 캐시 집약성, NUMA 토폴로지 및 기타 많은 요소를 고려해 야 할 하이퍼바이저 스케줄러 처리를 하는 동안는 VP LP 모든 호스트에 예약할 수 궁극적으로 합니다.

## <a name="hypervisor-scheduler-types"></a>하이퍼바이저 스케줄러 형식

Windows Server 2016 부터는 Hyper-v 하이퍼바이저 하이퍼바이저 기본 논리 프로세서의 가상 프로세서를 예약 하는 방법을 결정 하는 스케줄러 논리의 몇 가지 모드를 지원 합니다. 이러한 스케줄러 형식은 다음과 같습니다.

- [클래식, fair 공유 스케줄러](#the-classic-scheduler)
- [Core 스케줄러](#the-core-scheduler)
- [루트 스케줄러](#the-root-scheduler)

### <a name="the-classic-scheduler"></a>클래식 스케줄러

클래식 스케줄러에는 Windows Server 2016 Hyper-v를 비롯 한 초창기 Windows Hyper-v 하이퍼바이저의 모든 버전에 대 한 기본 되었습니다. 클래식 스케줄러 공평, 게스트 가상 프로세서에 대 한 선점형 라운드 로빈 예약 모델을 제공합니다.

클래식 스케줄러 형식은 가장 적절 한 대부분의 기존 Hyper-v 사용에 대 한 – 사설 클라우드, 호스팅 공급자 및 등입니다. 잘 이해 하 고 다양 한 범위의 LPs, Vm과 워크 로드에 대 한 많은 다른 유형의 동시에 실행, 더 큰 규모 높은 실행을 VPs의 과도 한 가입 등의 가상화 시나리오를 지원 하기 위해 가장 최적화 된 성능 특징 전체 기능을 지 원하는 Vm 성능 제한 없이 Hyper-v 등의 집합입니다.

### <a name="the-core-scheduler"></a>Core 스케줄러

하이퍼바이저 core 스케줄러는 Windows Server 2016 및 Windows 10 버전 1607에에서 도입 된 클래식 스케줄러 논리에 새로운 대체 합니다. Core 스케줄러 게스트 워크 로드 격리에 대 한 강력한 보안 경계 및 SMT 지원 가상화 호스트에서 실행 되는 Vm 내에서 워크 로드 성능 저하 가변성을 제공 합니다. Core 스케줄러 SMT와 SMT 아닌 가상 컴퓨터를 동일한 SMT 지원 가상화 호스트에서 동시에 실행할 수 있습니다.

Core 스케줄러는 가상화 호스트의 SMT 토폴로지를 활용 하 고 필요에 따라 SMT 논리 프로세서 그룹에 동일한 가상 머신에서 게스트 virtual machines 및 게스트 가상 프로세서의 일정 그룹에 SMT 쌍을 노출 합니다. LPs가 있는 경우 두 VPs 그룹 두 개를 그룹에서 예약 되 고 코어 Vm 간에 공유 되지 않는 있도록 대칭적으로 수행 됩니다.
VP SMT 없이 가상 컴퓨터에 대 한 예약 된 경우 사용 하도록 설정 실행 될 때 VP가 전체 코어를 사용 하면 됩니다.

Core 스케줄러의 전체 결과:

* 게스트 VPs 물리적 코어 쌍 내부, 프로세서 코어 경계에 VM을 격리, 악의적인 Vm에서 스누핑 사이드 채널 공격 취약점 감소에서 실행 되도록 제한 됩니다.

* 가변성 처리량이 크게 줄어듭니다.

* 다른 컴퓨터가 유휴 상태일 때 실행는 핵심 명령 스트림의 하나만 VPs 그룹 중 하나를 실행 하는 경우에 되기 때문에 성능이 저하 될 됩니다.

* OS 및 게스트 가상 머신에서 실행 중인 응용 프로그램 SMT 동작 및 프로그래밍 인터페이스 (Api)를 제어 하 고 가상화 되지 않은 경우 실행 됩니다 처럼 SMT 스레드 간에 작업 배포를 활용할 수 있습니다.

* 강력한 보안 경계를 게스트 워크 로드 격리-게스트 VPs 사이드 채널 스누핑 공격에 대 한 취약점을 줄이는 기본 물리적 코어 쌍에서 실행 되도록 제한 됩니다.

Core 스케줄러는 Windows Server 2019부터 기본적으로 사용 됩니다. Windows Server 2016에서 핵심 스케줄러는 선택 사항이 며, Hyper-v 호스트 관리자가 명시적으로 설정 해야 합니다 및 클래식 스케줄러는 기본값입니다.

#### <a name="core-scheduler-behavior-with-host-smt-disabled"></a>호스트 사용 하지 않도록 설정 하는 SMT 사용 하 여 핵심 스케줄러 동작

하이퍼바이저 핵심 스케줄러 형식을 사용 하도록 구성 되어 있지만 SMT 기능을 사용할 수 없거나 가상화 호스트에 없는 경우 하이퍼바이저는 하이퍼바이저 스케줄러 형식 설정에 관계 없이 클래식 스케줄러 동작을 사용 합니다.

### <a name="the-root-scheduler"></a>루트 스케줄러

Windows 10 버전 1803 루트 스케줄러 도입 되었습니다. 루트 스케줄러 형식을 사용 하는 경우 하이퍼바이저 cedes 작업 일정 루트 파티션에을 제어 합니다. 루트 파티션 OS 인스턴스에서 NT 스케줄러 LPs 시스템에 작업을 예약 하는 모든 측면을 관리 합니다.

루트 스케줄러 고유 요구 사항을 해결 유틸리티 파티션을 지원 내재 된 Windows Defender Application Guard (WDAG) 사용 하 여 사용 되는 강력한 워크 로드 격리를 제공 합니다. 이 시나리오에서는 루트 OS에 책임을 예약 종료는 여러 가지 이점을 제공 합니다. 예를 들어, 관리 및 배포를 간소화 유틸리티 파티션과 컨테이너 시나리오에 적용할 CPU 리소스 제어를 사용할 수 있습니다. 또한 루트 OS 스케줄러 수 쉽게 작업 컨테이너 내에서 CPU 사용률에 대 한 메트릭을 수집 및 시스템의 다른 모든 워크 로드에 적용 한 동일한 일정 정책에 대 한 입력으로이 데이터를 사용 합니다. 이러한 동일한 메트릭을 도움이 명확 하 게 응용 프로그램 컨테이너 호스트 시스템에서 수행 된 작업을 하는 특성입니다. 이러한 메트릭을 추적 어려워집니다 기존 가상 머신 워크 로드를 사용 하 여 모든 실행 중인 VM 대신에 이루어지는 곳입니다 루트 파티션에 합니다.

#### <a name="root-scheduler-use-on-client-systems"></a>클라이언트 시스템에서 루트 스케줄러 사용

Windows 10 버전 1803부터 루트 스케줄러는 기본적으로 사용 됩니다만, 클라이언트 시스템에서 향후 시스템의 적절 한 작업 및 가상화 기반 보안 및 WDAG 워크 로드 격리를 지 원하는 하이퍼바이저 사용 될 수 있는 유형이 다른 핵심 아키텍처입니다. 이 클라이언트 시스템만 지원 되는 하이퍼바이저 스케줄러 구성입니다. 관리자는 Windows 10 클라이언트 시스템에는 기본 하이퍼바이저 스케줄러 형식을 재정의 하지 않아야 합니다.

#### <a name="virtual-machine-cpu-resource-controls-and-the-root-scheduler"></a>가상 컴퓨터 CPU 리소스 제어 및 루트 스케줄러

Hyper-v에서 제공 하는 가상 컴퓨터 프로세서 리소스 컨트롤을 전역으로 호스트 리소스를 관리 하는 되 고 루트 운영 체제의 스케줄러 논리와 VM에 대 한 지식이 없는 하이퍼바이저 루트 스케줄러를 사용 하는 경우 지원 되지 않습니다. 특정 구성 설정입니다. 하이퍼바이저 예약, 예: 클래식 및 core 스케줄러 형식과 마찬가지로 VP에 간접적으로 제어 하는 경우에 Hyper-v VM 당 프로세서 리소스 제어 caps와 가중치를 예약, 적용 됩니다.

#### <a name="root-scheduler-use-on-server-systems"></a>서버 시스템에서 루트 스케줄러 사용

성능 특징 아직 완전히 구분 되어 광범위 한 많은 서버 가상화 배포의 일반적인 워크 로드에 맞게 조정 하는 대로 루트 스케줄러를 현재 서버에서 Hyper-v를 사용 하 여 사용에 대 한 권장 되지 않습니다.

## <a name="enabling-smt-in-guest-virtual-machines"></a>게스트 가상 컴퓨터에서 SMT를 사용 하도록 설정

가상화 호스트의 하이퍼바이저 core 스케줄러 형식을 사용 하도록 구성 되 면 원하는 경우 SMT를 활용 하도록 게스트 가상 컴퓨터를 구성할 수 있습니다. 게스트 운영 체제를 검색 하 고 자신의 작업 예약 SMT 토폴로지를 사용 하도록 VM에서 실행 되는 작업 스케줄러를 허용 VPs 게스트 가상 머신에 이들 버전이 하이퍼 스레드는 노출 합니다. Windows Server 2016에서 게스트 SMT 기본적으로 구성 되지 않으며 Hyper-v 호스트 관리자가 명시적으로 설정 해야 합니다. Windows Server 2019부터 기본적으로 호스트에서 만든 새 Vm 호스트의 SMT 토폴로지를 상속 합니다.  즉, 버전 9.0 VM 코어당 2 SMT 스레드를 사용 하 여 호스트에서 만든 코어당 2 SMT 스레드를도 표시 됩니다.

게스트 가상 머신에서; SMT를 사용 하도록 설정 하려면 PowerShell은 사용 해야 합니다. Hyper-v 관리자에서 제공 하는 사용자 인터페이스가 없는 경우
게스트 가상 머신에서 SMT를 사용 하려면 충분 한 권한이 및 형식으로 PowerShell 창을 엽니다.

``` powershell
Set-VMProcessor -VMName <VMName> -HwThreadCountPerCore <n>
```

여기서 <n> 게스트 VM 나타납니다 코어당 SMT 스레드 수입니다.  
<n> = 0 핵심 가치 당 호스트의 SMT 스레드 수에 맞게 HwThreadCountPerCore 값을 설정 합니다.

>[!NOTE] 
>HwThreadCountPerCore 설정 = 0은 Windows Server 2019부터 지원 됩니다.

다음은 두 개의 가상 프로세서를 사용 하 여 가상 머신에서 실행 되는 게스트 운영 체제에서 가져온 시스템 정보의 예 및 SMT 사용 하도록 설정 합니다. 게스트 운영 체제를 동일한 코어에 속한 두 개의 논리 프로세서를 감지 합니다.

![Msinfo32 사용 하도록 설정 하는 SMT 사용 하 여 VM 게스트에서 보여 주는 스크린샷](media/Hyper-V-CoreScheduler-VM-Msinfo32.png)

## <a name="configuring-the-hypervisor-scheduler-type-on-windows-server-2016-hyper-v"></a>Windows Server 2016 Hyper-v 하이퍼바이저 스케줄러 유형 구성

Windows Server 2016 Hyper-v는 기본적으로 클래식 하이퍼바이저 스케줄러 모델을 사용합니다. 하이퍼바이저는 게스트 VPs SMT 해당 게스트 VPs에 대 한 예약 된 가상 컴퓨터의 사용을 지원 하 고 해당 실제 SMT 쌍에 대해 실행 되도록 제한 하 여 보안을 강화할 core scheduler를 사용 하려면 필요에 따라 구성할 수 있습니다.

>[!NOTE]
>Windows Server 2016 Hyper-v를 실행 하는 모든 고객 core 스케줄러가 해당 가상화 호스트는 잠재적으로 악의적인 게스트 Vm에 대해 최적으로 보호 되도록 선택 하는 것이 좋습니다.

## <a name="windows-server-2019-hyper-v-defaults-to-using-the-core-scheduler"></a>Core 스케줄러를 사용 하 여 Windows Server 2019 Hyper-v 기본값

을 최적의 보안 구성에서 Hyper-v 호스트를 배포 하는 보장 하기 위해 이제 Windows Server 2019 Hyper-v 기본적으로 core 하이퍼바이저 스케줄러 모델을 사용 합니다. 호스트 관리자 호스트 클래식 레거시 스케줄러를 사용 하 여 선택적으로 구성할 수 있습니다. 관리자는 신중 하 게 읽기, 이해 및 스케줄러 유형별로 보안과 스케줄러 형식 기본 설정을 재정의 하기 전에 가상화 호스트의 성능에 영향을 고려 합니다.  참조 [이해 Hyper-v 스케줄러 유형 선택](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/understanding-hyper-v-scheduler-type-selection) 자세한 내용은 합니다.

### <a name="required-updates"></a>필수 업데이트

>[!NOTE]
>이 문서에 설명 된 하이퍼바이저 스케줄러 기능을 사용 하는 다음 업데이트가 필요 합니다. 이러한 업데이트에는 호스트 구성에 필요한 새 'hypervisorschedulertype' BCD 옵션을 지원 하기 위해 변경 내용이 포함 됩니다.

| 버전 | 릴리스  | 업데이트 해야 합니다. | 기술 자료 문서 |
|--------------------|------|---------|-------------:|
|Windows Server 2016 | 1607 | 2018.07 C | [KB4338822](https://support.microsoft.com/help/4338822/windows-10-update-kb4338822) |
|Windows Server 2016 | 1703 | 2018.07 C | [KB4338827](https://support.microsoft.com/help/4338827/windows-10-update-kb4338827) |
|Windows Server 2016 | 1709 | 2018.07 C | [KB4338817](https://support.microsoft.com/help/4338817/windows-10-update-kb4338817) |
|Windows Server 2019 | 1804 | 없음 | 없음 |

## <a name="selecting-the-hypervisor-scheduler-type-on-windows-server"></a>Windows server 하이퍼바이저 스케줄러 유형 선택

하이퍼바이저 스케줄러 구성은 hypervisorschedulertype BCD 항목을 통해 제어 됩니다.

스케줄러 유형을 선택 하려면 관리자 권한으로 명령 프롬프트를 엽니다.

``` command
     bcdedit /set hypervisorschedulertype type
```

여기서 `type` 중 하나입니다.

* 클래식
* Core

시스템 변경 내용을 적용 하려면 하이퍼바이저 스케줄러 형식으로 다시 부팅 해야 합니다.

>[!NOTE]
>하이퍼바이저 루트 스케줄러는이 이번에 Windows Server Hyper-v에서 지원 되지 않습니다. Hyper-v 관리자 사용에 대 한 루트 스케줄러 서버 가상화 시나리오를 사용 하 여 구성 하지 않아야 합니다.

## <a name="determining-the-current-scheduler-type"></a>현재 스케줄러 유형 결정

하이퍼바이저 시작 시 구성 된 하이퍼바이저 스케줄러 유형을 보고 하는 최신 하이퍼바이저 시작 이벤트 ID 2에 대 한 이벤트 뷰어에서 시스템 로그를 검사 하 여 사용 중인 현재 하이퍼바이저 스케줄러 형식을 확인할 수 있습니다. 하이퍼바이저 시작 이벤트는 Windows 이벤트 뷰어를에서 또는 PowerShell을 통해 얻을 수 있습니다.

하이퍼바이저 시작 이벤트 ID가 2 하이퍼바이저 스케줄러 형식을 나타내는 위치:

    1 = Classic scheduler, SMT disabled

    2 = Classic scheduler

    3 = Core scheduler

    4 = Root scheduler

![이벤트 ID가 2 세부 정보를 시작 표시 하이퍼바이저를 사용 하는 스크린샷](media/Hyper-V-CoreScheduler-EventID2-Details.png)

![ID가 2 하이퍼바이저 시작 이벤트를 표시 하는 이벤트 뷰어를 보여 주는 스크린 샷](media/Hyper-V-CoreScheduler-EventViewer.png)

### <a name="querying-the-hyper-v-hypervisor-scheduler-type-launch-event-using-powershell"></a>PowerShell을 사용 하 여 Hyper-v 하이퍼바이저 스케줄러 형식 시작 이벤트를 쿼리 합니다.

쿼리를 PowerShell 프롬프트에서 다음 명령을 입력 PowerShell을 사용 하 여 하이퍼바이저 이벤트 ID가 2에 대 한 합니다.

``` powershell
Get-WinEvent -FilterHashTable @{ProviderName="Microsoft-Windows-Hyper-V-Hypervisor"; ID=2} -MaxEvents 1
```

![PowerShell 쿼리 및 하이퍼바이저 시작 이벤트 ID가 2에 대 한 결과 보여 주는 스크린 샷](media/Hyper-V-CoreScheduler-PowerShell.png)
