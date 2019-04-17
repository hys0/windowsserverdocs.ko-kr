---
title: Hyper-v 하이퍼바이저 스케줄러 유형 선택에 대 한
description: 모드 Hyper-v의 스케줄러 사용에 Hyper-v 호스트 관리자에 대 한 정보를 제공
author: allenma
ms.author: allenma
ms.date: 08/14/2018
ms.topic: article
ms.prod: windows-server-hyper-v
ms.technology: virtualization
ms.localizationpriority: low
ms.assetid: 5fe163d4-2595-43b0-ba2f-7fad6e4ae069
ms.openlocfilehash: c5360d8e2fdc23f8b05c6be0f665407eebedeba2
ms.sourcegitcommit: 546229d6b5fa7e16f725c6c35f4dcc272711b811
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2018
ms.locfileid: "4905130"
---
# Hyper-v 하이퍼바이저 스케줄러 유형 선택에 대 한

적용 대상:

* Windows Server 2016
* Windows Server 버전 1709
* Windows Server 버전 1803
* Windows Server 2019

이 문서는 Hyper-v의 기본 중요 한 변경 설명 하 고 스케줄러 형식 하이퍼바이저의 사용을 권장 합니다. 이러한 변경 내용을 모두 시스템 보안 및 가상화 성능에 영향을 합니다. 가상화 호스트 관리자 해야 검토 및 변경 내용 및이 문서에 설명 된 의미를 이해 하 고 신중 하 게 평가 영향, 제안 된 배포 지침과 가장 잘 배포 및 관리 하는 방법을 이해 하는 관련 된 위험 요소 보안 환경은 빠르게 변화에 관계 없이 Hyper-v 호스트 합니다.

>[!IMPORTANT]
>현재 알려진 악성 게스트 VM Simultaneous 통해 호스트에서 실행 되는 레거시 하이퍼바이저 클래식 스케줄러 형식의 일정 동작을 통해 하 여 여러 프로세서 아키텍처에서 보이는 취약성 악용 될 수 쪽 채널 보안 다중 스레딩 (SMT) 사용 하도록 설정 합니다.  악용, 악성 워크 로드 데이터 파티션 경계 외부 관찰 수 있습니다. 하이퍼바이저 core 스케줄러 유형 및 재구성 게스트 Vm 활용 하는 Hyper-v 하이퍼바이저를 구성 하 여이 클래스의 공격을 완화할 수 있습니다. 핵심 스케줄러를 사용 하 여 하이퍼바이저 게스트 VM의 Vp 따라서 강력 하 게 실행 되는 물리적 코어의 경계를 데이터에 액세스 하는 VM의 기능을 격리, 동일한 물리적 프로세서 코어에서 실행을 제한 합니다.  이 다른 파티션으로부터의 모든 아티팩트가 여부 관찰에서 VM을 방지 하는 이러한 쪽 채널 공격에 대 한 효과적인 완화 루트 또는 다른 게스트 파티션의 합니다.  따라서 Microsoft 기본값을 변경 하 고 가상화 호스트 및 게스트 Vm에 대 한 구성 설정을 것이 좋습니다.

## Background

Windows Server 2016부터 Hyper-v 예약 하 고 하이퍼바이저 스케줄러 형식 이라고, 가상 프로세서 관리의 몇 가지 메서드를 지원 합니다.  모든 하이퍼바이저 스케줄러 형식에 대 한 자세한 설명은 [이해 하 고 Hyper-v 하이퍼바이저 스케줄러 형식을 사용 하 여](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types)에서 찾을 수 있습니다.

>[!NOTE]
>새 하이퍼바이저 스케줄러 Windows Server 2016에서 처음 도입 형식과 이전 릴리스에서 사용할 수 없습니다. 모든 버전의 Windows Server 2016 이전 Hyper-v 클래식 스케줄러만 지원합니다. 핵심 스케줄러에 대 한 지원만 최근 게시 합니다.

## 하이퍼바이저 스케줄러 형식에 대 한

이 문서에서는 레거시 "클래식" 스케줄러와 새 하이퍼바이저 core 스케줄러 형식 사용 하 고 대칭 다중 스레딩 또는 SMT를 사용 하 여 이러한 스케줄러 형식 교차 하는 방법에 특별히 중점을 둡니다.  것이 핵심 및 기본 스케줄러 및 기본 시스템 프로세서에서 작업 게스트 Vm에서 각 배치 방법을 간의 차이점을 이해 해야 합니다.

### 클래식 스케줄러

클래식 스케줄러-게스트 Vm에 속하는 Vp 뿐만 아니라 루트 Vp 포함 하 여 시스템 전체 가상 프로세서 (Vp)에서 작업을 예약의 박람회-공유 라운드 로빈 메서드를 참조 합니다. 클래식 스케줄러 (Windows Server 2019, 여기에 설명 된 대로)까지 모든 버전의 Hyper-v에서 사용 하는 기본 스케줄러 형식 이었습니다.  클래식 스케줄러의 성능 특성은 잘 이해 하 고 클래식 스케줄러 ably 과도 한 워크 로드-과도 구독 즉, 적절 한 여백 하 여 호스트의 VP:LP 비율의 가입을 지원 하기 위해 방식이 (에 따라 합니다 유형 가상화 되 고 워크 로드, 전체 리소스 사용률, 등).

가상화 호스트에서 활성화 SMT에서 실행 하는 경우 클래식 스케줄러 독립적으로 코어 하지 속하는 각 SMT 스레드에서 모든 VM에서 게스트 Vp 예약 됩니다. 따라서 다른 Vm 동시 (다른 VM은 다른 스레드에서 실행 되는 동안 코어가 한 스레드에서 실행 되 고 하나의 VM)에 동일한 코어에서 실행할 수 있습니다.

### 핵심 스케줄러

핵심 스케줄러 보안과 시스템 성능에 영향을 줍니다 게스트 워크 로드의 격리를 제공 하는 SMT의 속성을 활용 합니다. 핵심 스케줄러 VM에서 Vp 형제 SMT 스레드가 예정 되어 있는지 확인 합니다. 이렇게 대칭 되도록 Lp에 있는 경우 두, Vp의 그룹 2의 그룹에 예약 되어 시스템 CPU 코어 Vm 간에 공유 되지 않습니다.

기본 SMT 쌍에서 게스트 Vp, 예약 하 여 핵심 스케줄러가 격리는 워크 로드에 대 한 강력한 보안 경계를 제공 하 고 대기 시간이 중요 한 워크 로드에 대 한 성능 가변성을 줄이고 사용할 수도 있습니다.

Note는 부사장 SMT 사용 하도록 설정 하지 않고 가상 컴퓨터에 대 한 예약 되 면, 실행 및 핵심의 형제 SMT 스레드가 유휴 상태가 될 때 VP가 전체 핵심을 사용 합니다.  이 올바른 워크 로드를 분리 하 여 제공 하는 데 필요한 하지만 시스템 Lp 될 과도 하 게 가입-즉, 총 VP:LP 비율 1: 1을 초과 하는 경우 처럼 특히 전체 시스템 성능에 영향을 줍니다. 따라서 게스트 Vm 코어 당 여러 스레드에서 없이 구성 실행 되는 성능이 저하 구성 합니다.

### 사용 하 여 핵심 스케줄러 혜택

핵심 스케줄러는 다음과 같은 이점을 제공합니다.

* 게스트 워크 로드 격리-게스트 Vp에 대 한 강력한 보안 경계 쪽 채널 다른 공격 취약성을 줄여 기본 물리적 코어 쌍에서 실행 하도록 제한 됩니다.

* 축소 된 워크 로드의 변동-게스트 워크 로드 처리량 가변성 크게 줄어들고 큰 워크 로드 일관성을 제공 합니다.

* 게스트 Vm-운영 체제 및 게스트 가상 컴퓨터에서 실행 되는 응용 프로그램에서에서 SMT 사용 SMT 동작을 활용할 수 및 프로그래밍 인터페이스 (Api)를 제어 하 고 작업을 분배 SMT 스레드가 실행 되는 것 처럼 가상화 되지 않은 합니다.

핵심 스케줄러 강력한 보안 경계 및 낮은 워크 로드 variabilty 활용 하기 위해 특별히 Azure 가상화 호스트에서 현재 사용 됩니다. Microsoft 한다고 생각 핵심 스케줄러 형식 이어야 대부분의 가상화 시나리오에 대 한 형식 일정 기본 하이퍼바이저를 계속 합니다.  따라서 고객은 기본적으로 보안을 보장 하려면 Microsoft는이 변경을 사항을 Windows Server 2019에 대해 이제 합니다.

### 게스트 워크 로드에 핵심 스케줄러 성능 영향

을 효과적으로 특정 종류의 문제를 완화 하는 데 필요 하지만 핵심 스케줄러 성능을 잠재적으로 줄일 수 있습니다. 고객은 가상화 호스트의 전반적인 워크 로드 용량 Vm 및 영향을 사용 하 여 성능 특성의 차이 알 수 있습니다. 여기서 핵심 스케줄러 비-SMT VP를 실행 해야 하는 경우, 다른 남아 있어야 유휴 동안 실행 내부 논리 코어에서 명령 스트림 중 하나만. 이 게스트 워크 로드에 대 한 총 호스트 용량을 제한 합니다.

이 문서의 배포 지침에 따라 이러한 성능 영향을 최소화할 수 있습니다. 신중 하 게 호스트 관리자가 특정 가상화 배포 시나리오를 고려 하 고 보안 위험 최대 워크 로드 밀도, 가상화 호스트 등의 과도 하 게 통합에 대 한 필요성에 대해 어느 정도 허용할 균형 해야 합니다.

## 기본 및 Windows Server 2016 및 Windows Server 2019에 대 한 권장된 구성

최대 보안 환경 사용 하 여 Hyper-v 호스트를 배포 하이퍼바이저 core 스케줄러 형식 사용을 해야 합니다. 고객은 기본적으로 보안을 보장 하려면 Microsoft에서 다음과 같은 기본 뀌 및 권장 설정 합니다.

>[!NOTE]
>스케줄러 형식에 대 한 하이퍼바이저의 내부 지원에 Windows Server 2016, Windows Server 1709 및 Windows Server 1803의 초기 릴리스에 포함 된 업데이트는 선택 엔드가 구성 컨트롤에 액세스 하기 위해 필요 합니다 하이퍼바이저 스케줄러 유형입니다.  이러한 업데이트에 대 한 자세한 내용은 [이해 하 고 Hyper-v 하이퍼바이저 스케줄러 형식을 사용 하 여](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types) 를 참조 하십시오.

### 가상화 호스트 변경

* 하이퍼바이저는 Windows Server 2019부터 기본적으로 핵심 스케줄러를 사용 합니다.

* Microsoft reccommends Windows Server 2016에서 핵심 스케줄러를 구성 합니다. 기본값은 클래식 스케줄러 하이퍼바이저 core 스케줄러 유형 Windows Server 2016에서 지원 됩니다. 핵심 스케줄러는 선택 사항이 고 Hyper-v 호스트 관리자가 명시적으로 사용할 수 있어야 합니다.

### 가상 컴퓨터 구성 변경

* Windows Server 2019에 9.0 기본 VM 버전을 사용 하 여 만든 새 가상 컴퓨터는 자동으로 상속 SMT 속성 (활성화 또는 비활성화) 가상화 호스트입니다. 즉, SMT에서 활성화 된 경우 새로 만든 Vm 물리적 호스트 SMT 활성화는 및 기본 시스템 동일한 개수의 핵심 당 하드웨어 스레드 VM과 기본적으로 호스트의 SMT 토폴로지를 상속 합니다. 이것은 HwThreadCountPerCore 사용 하 여 VM의 구성에 반영 됩니다 = 0, 0 VM 호스트의 SMT 설정을 상속 해야 위치를 나타냅니다.

* 기존 가상 컴퓨터는 8.2 또는 이전 버전의 VM 버전으로 HwThreadCountPerCore, 자신의 원래 VM 프로세서 설정 유지 및 8.2 VM 버전 게스트에 대 한 기본값은 HwThreadCountPerCore = 1. 이러한 게스트는 Windows Server 2019 호스트에서 실행, 같이 처리 될 됩니다.

    1. VM에 VP count를 LP 코어의 개수 보다 작거나 같은 경우 VM 핵심 스케줄러가으로 비-SMT VM 처리 됩니다. 게스트 VP 단일 SMT 스레드에서 실행 되 면 핵심의 형제 SMT 스레드가 idled 됩니다. 이 최적화 되지 않은 이며 전반적인 성능이 저하 됩니다.

    2. VM LP 코어 보다 더 많은 Vp에 있는 경우 VM 핵심 스케줄러가 SMT VM으로 처리 됩니다. 그러나 VM는 SMT VM는 다른 표시가 관찰 하지 않습니다. 예를 들어를 사용 하 여 CPUID 지시 사항이 나 Windows Api 쿼리 OS 또는 응용 프로그램에서 CPU 토폴로지는 SMT 활성화 되어 있는지 나타냅니다.

* 버전 9.0 업데이트 VM 작업을 통해 업데이트 eariler VM 버전에서 명시적으로 기존 VM은 VM HwThreadCountPerCore에 대 한 현재 값을 유지 합니다.  VM SMT 힘 사용 하지 않아도 됩니다.

* Windows Server 2016에서는 SMT 게스트 Vm에 대 한 사용 하도록 설정 하는 것이 좋습니다.  기본적으로 SMT을 비활성화 한 Windows Server 2016에서 만든 Vm는 않는 HwThreadCountPerCore 1로 설정 되어 명시적으로 변경.

>[!NOTE]
>Windows Server 2016에는 0으로 HwThreadCountPerCore 설정을 지원 하지 않습니다.

#### 가상 컴퓨터 SMT 구성 관리

게스트 가상 컴퓨터 SMT 구성은 VM 당 단위로 설정 됩니다. 호스트 관리자 검사 하 고 다음 옵션 중에서 선택 하는 VM의 SMT 구성할 수 있습니다.

    1. Vm이 같이 SMT 지원, 선택적으로 호스트 SMT 토폴로지를 자동으로 상속 실행 되도록 구성

    2. Vm이 아닌 SMT으로 실행 되도록 구성

VM에 대 한 SMT 구성 Hyper-v 관리자 콘솔에서 요약 창에 표시 됩니다.  VM의 SMT 설정을 구성 하는 VM 설정 또는 PowerShell을 사용 하 여 수행할 수 있습니다.

#### PowerShell을 사용 하 여 VM SMT 설정 구성

게스트 가상 컴퓨터에 대해 SMT 설정을 구성 하려면 충분 한 권한이와 형식이 PowerShell 창을 엽니다.

``` powershell
Set-VMProcessor -VMName <VMName> -HwThreadCountPerCore <0, 1, 2>
```

여기서

    0 = Inherit SMT topology from the host (this setting of HwThreadCountPerCore=0 is not supported on Windows Server 2016)

    1 = Non-SMT

    Values > 1 = the desired number of SMT threads per core. May not exceed the number of physical SMT threads per core.

게스트 가상 컴퓨터에 대 한 SMT 설정을 읽으려면 충분 한 권한이와 형식이 PowerShell 창을 엽니다.

``` powershell
(Get-VMProcessor -VMName <VMName>).HwThreadCountPerCore
```

해당 게스트 Vm HwThreadCountPerCore를 사용 하 여 구성 참고 = 0은 SMT 해당 게스트에 대해 사용 하도록 설정 하 고 기본 가상화 호스트에서 일반적으로 2는 동일한 수의 SMT 스레드가 게스트를 노출 합니다.

### 게스트 Vm CPU 토폴로지를 변경 VM 이동성 시나리오에서 발생할 수 있습니다.

OS 및 VM에서 응용 프로그램 VM 수명 주기 이벤트와 같은 실시간 마이그레이션 또는 저장 및 복원 작업 후 호스트와 하기 전에 VM 설정 하 고 변경 내용을 볼 수 있습니다. 어떤 VM 상태를 저장 하 고 복원 작업 중 VM의 HwThreadCountPerCore 설정 및 실현된 값 (즉, VM의 설정 및 원본 호스트의 구성의 계산 된 조합)를 모두 마이그레이션할 됩니다. VM 계속 대상 호스트에서 이러한 설정 사용 하 여 실행 됩니다. 시점에 VM을 종료 하 고 다시 시작의 가능한 실현된 값 관찰 되는 VM으로 변경 됩니다. 양성 이어야 합니다, 그리고 OS 및 응용 프로그램의 일반적인 시작 및 초기화 코드 흐름의 일부로 CPU 토폴로지 정보에 대 한 계층 소프트웨어 찾아야 합니다. 그러나 이러한 부팅 시간 초기화 시퀀스 실시간 마이그레이션 또는 저장/복원 작업 도중, 이러한 상태 전환이 겪지 Vm 건너뛸 관찰할 수 있으므로 계산 된 원래 종료 될 때까지 값을 실현 및 다시 시작 합니다.  

### 최적화 되지 않은 VM 구성에 대 한 경고

가상 컴퓨터를 호스트 결과에 물리적 코어에서 최적화 되지 않은 구성에서 된 것 보다 더 많은 Vp를 사용 하 여 구성 합니다. 하이퍼바이저 스케줄러는 SMT 인식 하는 경우 이러한 Vm 처리 됩니다. 그러나 OS 및 VM에서 응용 프로그램 소프트웨어 SMT 불가능 보여 주는 CPU 토폴로지 제공 됩니다. 이 조건은 감지 되 면 Hyper-v 작업자 프로세스는 VM의 구성이 이며 최적화 되지 않은 SMT 권장 되는 호스트 관리자 경고 가상화 호스트에서 이벤트를 기록 VM에 대 한 사용 하도록 설정 합니다.

#### 비 최적으로 식별 하는 방법 Vm 구성

비-SMT Vm Hyper-v 작업자 프로세스 이벤트 ID 3498에 대 한 이벤트 뷰어에서 시스템 로그를 검토 하 여 VM에서 Vp 수가 물리적 코어 개수 보다 크면 때마다 VM에 대 한 트리거할 수 있는 식별할 수 있습니다. 이벤트 뷰어 또는 PowerShell을 통해 작업자 프로세스 이벤트를 얻을 수 있습니다.

#### PowerShell을 사용 하 여 Hyper-v 작업자 프로세스 VM 이벤트 쿼리

쿼리를 PowerShell 프롬프트에서 다음 명령을 입력 PowerShell을 사용 하 여 Hyper-v 작업자 프로세스 이벤트 ID 3498 합니다.

``` powershell
Get-WinEvent -FilterHashTable @{ProviderName="Microsoft-Windows-Hyper-V-Worker"; ID=3498}
```

### 게스트 운영 체제에 대 한 하이퍼바이저 enlightenments 사용에서 게스트 SMT 구성의 영향

Microsoft 하이퍼바이저 여러 enlightenments 또는 게스트 VM에서에서 실행 중인 OS를 쿼리하고 최적화, 성능 이점을 활용할 수도 실행할 때 다양 한 조건 중 처리를 개선 하는 등의 트리거를 사용 하 여 수 있는 힌트를 제공 합니다. 가상화. 하나의 최근에 도입 된 인식 SMT 악용 하는 쪽 채널 공격에 대 한 OS 완화 사용 하 여 가상 프로세서 일정 처리와 관련 됩니다.

>[!NOTE]
>호스트 관리자 워크 로드 성능을 최적화 하기 위해 게스트 Vm에 대 한 SMT을 사용 하는 것이 좋습니다.

하지만이 게스트 인식의 세부 정보는 아래 가상화 호스트 관리자에 대 한 요점은 가상 컴퓨터는 호스트의 물리적 SMT 구성과 일치 하도록 구성 HwThreadCountPerCore 있어야 한다는 제공 합니다. 이 아키텍처 코어 없음 중임을 보고 하는 하이퍼바이저를 통해 공유 합니다. 따라서는 인식 해야 하는 모든 게스트 OS 지원 최적화를 사용할 수 있습니다. Windows Server 2019에 새로운 Vm을 만들고 HwThreadCountPerCore (0)의 기본값을 그대로 둡니다. Windows Server 2016에서 마이그레이션할 이전 Vm 호스트는 Windows Server 2019 구성 버전으로 업데이트할 수 있습니다. 그런 다음, Microsoft 권장 설정 HwThreadCountPerCore = 0입니다.  Windows Server 2016에서는 설정 HwThreadCountPerCore 호스트 구성 (일반적으로 2)와 일치 하도록 권장 합니다.

### NoNonArchitecturalCoreSharing 인식 세부 정보

Windows Server 2016 부터는 하이퍼바이저 VP 예약 및 게스트 OS에 배치의 처리를 설명 하는 새 인식을 정의 합니다. 이 인식 [v5.0c 하이퍼바이저 상위 수준 기능 사양에서](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/tlfs)에서 정의 됩니다.

하이퍼바이저 가상 CPUID 리프 CPUID.0x40000004.EAX:18[NoNonArchitecturalCoreSharing = 1] 가상 프로세서 형제 SMT으로 보고 되는 가상 프로세서를 제외 하 고 다른 가상 프로세서를 사용 하 여 물리적 코어를 공유 하지는 나타냅니다. 스레드입니다. 예를 들어, 게스트 VP 실행 되지 않습니다 루트 VP 함께 SMT 스레드에서 동일한 프로세서 코어에 SMT 스레드가 형제에서 동시에 실행 합니다. 이 조건은 가상화 된를 실행할 때만 가능 있으며, 따라서 심각한 보안에 미치는 영향에도 있는 아키텍처 SMT 동작을 나타냅니다. 게스트 OS NoNonArchitecturalCoreSharing를 사용할 수 = 1 안전한 STIBP 설정의 성능 오버 헤드를 방지 하는 데 도움이 되는 최적화를 사용 하도록 설정 되었는지 확인 합니다.

특정 구성에서는 하이퍼바이저는 나타내지 해당 NoNonArchitecturalCoreSharing = 1. 예를 들어 호스트 SMT 사용할 수 있으며 하이퍼바이저 클래식 스케줄러를 사용 하도록 구성 된 경우 NoNonArchitecturalCoreSharing 0이 됩니다. 따라서 인식된 게스트 특정 최적화를 사용 하도록 설정 하면서 못할 수 있습니다. 따라서 Microsoft 권장 SMT를 사용 하 여 호스트 관리자 하이퍼바이저 핵심 스케줄러에 의존 하 고 가상 컴퓨터에서 SMT 구성을 최적의 워크 로드 성능을 보장 하기 위해 호스트에서 상속 하도록 구성 되어 있는지 확인 합니다.

## 요약

보안 위협 환경은 진화 하 여 계속 합니다. 고객은 기본적으로 보안, Microsoft 하이퍼바이저와 가상 컴퓨터에서 Windows Server 2019 Hyper-v, 시작에 대 한 기본 구성을 변경 하 고 지침과 권장 사항은 Windows를 실행 하는 고객에 대 한 업데이트 제공 서버 2016 Hyper-v가 설치 합니다. 가상화 호스트 관리자가 수행 해야합니다.

* 읽고이 문서에서 제공 하는 지침을 이해

* 신중 하 게 평가 하 고 보안, 성능, 가상화 밀도 및 고유한 요구 사항에 대 한 워크 로드 응답성 목표 충족을 위해 가상화 배포 조정

* 하이퍼바이저 핵심 스케줄러에서 제공 하는 강력한 보안 이점을 활용할 수 기존 Windows Server 2016 Hyper-v 호스트를 다시 구성 것이 좋습니다.

* 기존 비-SMT Vm 예약 하드웨어 보안 취약점을 해결 하는 VP 격리 사용할 제약 조건에서 성능 영향을 줄이기 위해 업데이트
