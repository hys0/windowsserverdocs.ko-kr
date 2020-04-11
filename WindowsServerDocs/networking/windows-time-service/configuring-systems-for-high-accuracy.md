---
ms.assetid: ''
title: 높은 정확성을 위한 시스템 구성
description: Windows 10 및 Windows Server 2016의 시간 동기화가 크게 향상되었습니다.  합리적인 운영 조건에서 시스템은 UTC와 관련하여 1ms(밀리초) 이상의 정확도를 유지하도록 구성할 수 있습니다.
author: dcuomo
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 25472e4ba4837bd68c9b6914e22c2219c91d3ac0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861656"
---
# <a name="configuring-systems-for-high-accuracy"></a>높은 정확성을 위한 시스템 구성
>적용 대상: Windows Server 2016 및 Windows 10 버전 1607 이상:

Windows 10 및 Windows Server 2016의 시간 동기화가 크게 향상되었습니다.  합리적인 운영 조건에서 시스템은 UTC와 관련하여 1ms(밀리초) 이상의 정확도를 유지하도록 구성할 수 있습니다.

다음 지침은 높은 정확도를 얻도록 시스템을 구성하는 데 도움이 됩니다.  이 문서에서는 다음과 같은 요구 사항을 설명합니다.

- 지원되는 운영 체제
- 시스템 구성 

> [!WARNING]
> **이전 운영 체제 정확도 목표**<br>
>Windows Server 2012 R2 이하에서는 동일한 높은 정확도 목표를 충족할 수 없습니다. 이러한 운영 체제는 높은 정확도를 지원하지 않습니다.
>
>이러한 버전의 Windows 시간 서비스는 다음 요구 사항을 충족했습니다.
>
> - Kerberos 버전 5 인증 요구 사항을 충족하기 위해 필요한 시간 정확도를 제공했습니다.
> - 일반적인 Active Directory 포리스트에 조인된 Windows 클라이언트 및 서버에 대해 정확도가 낮은 시간을 제공했습니다.
>
>2012 R2 이하의 경우 더 큰 허용 오차가 Windows 시간 서비스의 디자인 사양을 벗어납니다.

## <a name="windows-10-and-windows-server-2016-default-configuration"></a>Windows 10 및 Windows Server 2016 기본 구성

Windows 10 또는 Windows Server 2016에서 1ms까지 정확도를 지원하지만 대부분의 고객은 매우 정확한 시간이 필요하지 않습니다.

따라서 **기본 구성**은 다음과 같이 이전 운영 체제와 동일한 요구 사항을 충족하기 위한 것입니다.

- Kerberos 버전 5 인증 요구 사항을 충족하기 위해 필요한 시간 정확도를 제공합니다.
- 일반적인 Active Directory 포리스트에 조인된 Windows 클라이언트 및 서버에 대해 정확도가 낮은 시간을 제공합니다.

## <a name="how-to-configure-systems-for-high-accuracy"></a>높은 정확성을 위한 시스템 구성 방법

>[!IMPORTANT]
>**정확도가 높은 시스템의 지원 가능성에 대 한 참고 사항**<br>
> 시간 정확도는 신뢰할 수 있는 시간 원본에서 최종 디바이스로의 정확한 시간에 대한 엔드투엔드 배포를 수반합니다.  이 경로를 따라 측정에 측정값을 추가하는 것은 정확도에 부정적인 영향을 미치며, 디바이스에서 달성할 수 있는 정확도에도 영향을 미칩니다.
>
>이러한 이유로, 높은 정확도 목표에 도달하기 위해 충족해야 하는 환경 요구 사항을 간략하게 설명하는 [경계 지원으로 정확도가 높은 환경을 위한 Windows 시간 서비스 구성](support-boundary.md)을 마련했습니다.

### <a name="operating-system-requirements"></a>운영 체제 요구 사항

높은 정확도 구성에는 Windows 10 또는 Windows Server 2016이 필요합니다.  시간 토폴로지의 모든 Windows 디바이스는 상위 계층의 Windows 시간 서버를 포함하여 이 요구 사항을 충족해야 하며, 가상화된 시나리오에서는 시간이 중요한 가상 머신을 실행하는 Hyper-V 호스트가 필요합니다. 이러한 모든 디바이스는 Windows 10 또는 Windows Server 2016 이상이어야 합니다.

아래 그림에서 높은 정확도가 필요한 가상 머신은 Windows 10 또는 Windows Server 2016을 실행하고 있습니다.  마찬가지로 가상 머신이 상주하는 Hyper-V 호스트와 업스트림 Windows 시간 서버도 Windows Server 2016을 실행해야 합니다.

![시간 토폴로지 - 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/Topology2016.png)


>[!TIP] 
>**Windows 버전 확인**<br>
> 명령 프롬프트에서 명령 `winver`를 실행하여 아래와 같이 OS 버전이 1607 이상이고 OS 빌드가 14393 이상인지 확인할 수 있습니다.
>
> ![Winver - 2016 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/winver2016.png)

### <a name="system-configuration"></a>시스템 구성

높은 정확도 대상에 도달하려면 시스템 구성이 필요합니다.  레지스트리에서 직접 또는 그룹 정책을 통해 이 구성을 수행하는 다양한 방법이 있습니다.  이러한 각 설정에 대한 자세한 내용은 Windows 시간 서비스 기술 참조 – [Windows 시간 서비스 도구](Windows-Time-Service-Tools-and-Settings.md#windows-time-service-tools)에서 확인할 수 있습니다.

#### <a name="windows-time-service-startup-type"></a>Windows 시간 서비스 시작 유형

W32Time(Windows 시간 서비스)은 계속 실행해야 합니다.  이렇게 하려면 Windows 시간 서비스의 시작 유형을 ‘자동’ 시작으로 구성합니다.

![자동 구성](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/AutomaticService.PNG)

#### <a name="cumulative-one-way-network-latency"></a>누적 단방향 네트워크 대기 시간

네트워크 대기 시간이 늘어나면 측정 불확실성 및 “노이즈”가 유입됩니다.  따라서 네트워크 대기 시간이 타당한 경계 내에 있어야 합니다.  특정 요구 사항은 대상 정확도에 따라 다르며, [경계 지원으로 정확도가 높은 환경을 위한 Windows 시간 서비스 구성](support-boundary.md) 문서에 간략히 설명되어 있습니다.

누적 단방향 네트워크 대기 시간을 계산하려면 대상에서 시작하여 높은 정확도 계층 1 시간 원본에서 끝나는 시간 토폴로지에서 NTP 클라이언트-서버 노드 쌍 사이에 개별 단방향 지연을 추가합니다.

예: 정확도가 매우 높은 원본, 두 개의 중간 NTP 서버 A와 B, 마지막으로 대상 머신을 순서대로 사용하는 시간 동기화 계층을 고려합니다. 대상과 원본 간의 누적 네트워크 대기 시간을 가져오려면 다음 사이에서 평균 개별 NTP RTT(왕복 시간)를 측정합니다.

- 대상 및 시간 서버 B
- 시간 서버 B 및 시간 서버 A
- 시간 서버 A 및 원본

이 측정값은 inbox w32tm.exe 도구를 사용하여 가져올 수 있습니다.  이렇게 하려면 다음을 수행합니다.

1. 대상 및 시간 서버 B에서 계산을 수행합니다.
    
    `w32tm /stripchart /computer:TimeServerB /rdtsc /samples:450 > c:\temp\Target_TsB.csv`

2. 시간 서버 A에 대한(를 가리키는) 시간 서버 B에서 계산을 수행합니다.
    
    `w32tm /stripchart /computer:TimeServerA /rdtsc /samples:450 > c:\temp\Target_TsA.csv`

3. 원본에 대한 시간 서버 A에서 계산을 수행합니다.
 
4. 다음으로, 이전 단계에서 측정한 평균 RoundTripDelay를 추가하고 2로 나누어서 대상과 원본 간의 누적 네트워크 지연 시간을 가져옵니다.

#### <a name="registry-settings"></a>레지스트리 설정

# <a name="minpollinterval"></a>[MinPollInterval](#tab/MinPollInterval)
시스템 폴링에 허용되는 최소 간격(log2초)을 구성합니다.

|  |  | 
|---------|---------|
|주요 위치     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|설정    | 6        |
|결과 | 최소 폴링 간격은 이제 64초입니다. |

다음 명령은 Windows 시간에게 업데이트된 설정을 선택하도록 신호를 보냅니다.

`w32tm /config /update`


# <a name="maxpollinterval"></a>[MaxPollInterval](#tab/MaxPollInterval)
시스템 폴링에 허용되는 최대 간격(log2초)을 구성합니다.

|  |  |  
|---------|---------|
|주요 위치     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|설정    | 6        |
|결과 | 최대 폴링 간격은 이제 64초입니다.  |

다음 명령은 Windows 시간에게 업데이트된 설정을 선택하도록 신호를 보냅니다.

`w32tm /config /update`

# <a name="updateinterval"></a>[UpdateInterval](#tab/UpdateInterval)
단계 수정 조정 사이의 클록 틱 수입니다.

|  |  |  
|---------|---------|
|주요 위치     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config       |
|설정    | 100        |
|결과 | 이제 단계 수정 조정 사이의 클록 틱 수가 100개입니다. |

다음 명령은 Windows 시간에게 업데이트된 설정을 선택하도록 신호를 보냅니다.

`w32tm /config /update`

# <a name="specialpollinterval"></a>[SpecialPollInterval](#tab/SpecialPollInterval)
SpecialInterval 0x1 플래그를 사용하는 경우 폴링 간격(초)을 구성합니다.

|  |  |  
|---------|---------|
|주요 위치     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient        |
|설정    | 64        |
|결과 | 이제 폴링 간격이 64초입니다. |

다음 명령은 업데이트된 설정을 선택하도록 Windows 시간을 다시 시작합니다.

`net stop w32time && net start w32time`

# <a name="frequencycorrectrate"></a>[FrequencyCorrectRate](#tab/FrequencyCorrectRate)

|  |  |  
|---------|---------|
|주요 위치     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config      |
|설정    | 2        |


---
