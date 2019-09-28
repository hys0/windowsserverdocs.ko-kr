---
ms.assetid: ''
title: 정확도를 높이기 위해 시스템 구성
description: Windows 10 및 Windows Server 2016의 시간 동기화는 상당히 향상 되었습니다.  적절 한 운영 조건에서 시스템은 UTC와 관련 하 여 1ms (밀리초) 정확도를 유지 하도록 구성할 수 있습니다.
author: shortpatti
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: b7cd256fdbbdbe7432e5b5d5b16254314132560f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405195"
---
# <a name="configuring-systems-for-high-accuracy"></a>정확도를 높이기 위해 시스템 구성
>적용 대상: Windows Server 2016 및 Windows 10 버전 1607 이상

Windows 10 및 Windows Server 2016의 시간 동기화는 상당히 향상 되었습니다.  적절 한 운영 조건에서 시스템은 UTC와 관련 하 여 1ms (밀리초) 정확도를 유지 하도록 구성할 수 있습니다.

다음 지침은 높은 정확도를 얻기 위해 시스템을 구성 하는 데 도움이 됩니다.  이 문서에서는 다음과 같은 요구 사항을 설명 합니다.

- 지원되는 운영 체제
- 시스템 구성 

> [!WARNING]
> **이전 운영 체제 정확도 목표**<br>
>Windows Server 2012 R2이 하에서는 동일한 높은 정확도 목표를 충족할 수 없습니다. 이러한 운영 체제는 높은 정확도를 지원 하지 않습니다.
>
>이러한 버전의 Windows 시간 서비스는 다음 요구 사항을 충족 했습니다.
>
> - Kerberos 버전 5 인증 요구 사항을 충족 하기 위해 필요한 시간 정확도를 제공 했습니다.
> - 일반적인 Active Directory 포리스트에 조인 된 Windows 클라이언트 및 서버에 대해 느슨하게 정확한 시간을 제공 했습니다.
>
>2012 r 2의 경우 더 큰 공차가 Windows 시간 서비스의 디자인 사양을 벗어납니다.

## <a name="windows-10-and-windows-server-2016-default-configuration"></a>Windows 10 및 Windows Server 2016 기본 구성

Windows 10 또는 Windows Server 2016에서 1ms까지 정확도를 지원 하지만 대부분의 고객은 매우 정확한 시간이 필요 하지 않습니다.

따라서 **기본 구성은** 다음과 같은 이전 운영 체제와 동일한 요구 사항을 충족 하기 위한 것입니다.

- Kerberos 버전 5 인증 요구 사항을 충족 하기 위해 필요한 시간 정확도를 제공 합니다.
- 공용 Active Directory 포리스트에 연결 된 Windows 클라이언트 및 서버에 대해 느슨하게 정확한 시간을 제공 합니다.

## <a name="how-to-configure-systems-for-high-accuracy"></a>정확도를 높이기 위해 시스템을 구성 하는 방법

>[!IMPORTANT]
>**매우 정확한 시스템의 지원 가능성에 대 한 참고 사항**<br>
> 시간 정확도는 신뢰할 수 있는 시간 원본에서 최종 장치로의 정확한 시간에 대 한 종단 간 배포를 수반 합니다.  이 경로를 따라 측정값에 assymetry을 추가 하는 모든 항목은 장치에서 달성 가능한 정확도에 영향을 미칠 수 있습니다.
>
>이러한 이유로, 높은 정확도 목표에 도달 하기 위해 충족 해야 하는 환경 요구 사항을 설명 하는 [고성능 환경에 대해 Windows 시간 서비스를 구성 하는 지원 경계](support-boundary.md) 를 문서화 했습니다.

### <a name="operating-system-requirements"></a>운영 체제 요구 사항

높은 정확도 구성에는 Windows 10 또는 Windows Server 2016이 필요 합니다.  시간 토폴로지의 모든 Windows 장치는 더 높은 계층 Windows 시간 서버를 비롯 하 여이 요구 사항을 충족 해야 하며, 가상화 된 시나리오에서는 시간이 중요 한 가상 컴퓨터를 실행 하는 Hyper-v 호스트가 필요 합니다. 이러한 모든 장치는 Windows 10 또는 Windows Server 2016 이상 이어야 합니다.

아래 그림에 나와 있는 그림에서 높은 정확도를 필요로 하는 가상 머신은 Windows 10 또는 Windows Server 2016를 실행 하 고 있습니다.  마찬가지로 가상 컴퓨터가 상주 하는 Hyper-v 호스트와 업스트림 Windows 시간 서버도 Windows Server 2016를 실행 해야 합니다.

![시간 토폴로지-1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/Topology2016.png)


>[!TIP] 
>**Windows 버전 확인**<br>
> 명령 프롬프트에서 `winver`을 실행 하 여 OS 버전이 1607 이상 인지 확인 하 고 OS 빌드는 아래와 같이 14393 이상 인지 확인할 수 있습니다.
>
> ![Winver-2016 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/winver2016.png)

### <a name="system-configuration"></a>시스템 구성

높은 정확도 대상에 도달 하려면 시스템 구성이 필요 합니다.  레지스트리 또는 그룹 정책을 통해를 비롯 하 여이 구성을 수행 하는 다양 한 방법이 있습니다.  이러한 각 설정에 대 한 자세한 내용은 Windows 시간 서비스 기술 참조- [Windows 시간 서비스 도구](Windows-Time-Service-Tools-and-Settings.md#windows-time-service-tools)에서 찾을 수 있습니다.

#### <a name="windows-time-service-startup-type"></a>Windows 시간 서비스 시작 유형

W32Time (Windows 시간 서비스)은 계속 실행 해야 합니다.  이렇게 하려면 Windows 시간 서비스의 시작 유형을 ' 자동 ' 시작으로 구성 합니다.

![자동 구성](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/AutomaticService.PNG)

#### <a name="cumulative-one-way-network-latency"></a>누적 단방향 네트워크 대기 시간

네트워크 대기 시간이 늘어나면에서 측정 불확실성 및 "노이즈" creeps.  따라서 네트워크 대기 시간이 적절 한 경계 내에 있어야 합니다.  특정 요구 사항은 대상 정확도에 따라 다르며, [높은 정확도 환경에 대해 Windows 시간 서비스를 구성 하는 지원 경계](support-boundary.md) 문서에 요약 되어 있습니다.

누적 단방향 네트워크 대기 시간을 계산 하려면 대상에서 시작 하 여 높은 정확도 계층 1 시간 원본에서 끝나는 시간 토폴로지에서 NTP 클라이언트 서버 노드 쌍 사이에 개별 단방향 지연을 추가 합니다.

예를 들어 다음과 같은 가치를 제공해야 합니다. 매우 정확한 원본, 두 개의 중간 NTP 서버 A와 B 및 대상 컴퓨터를 순서 대로 사용 하는 시간 동기화 계층을 고려 합니다. 대상과 원본 간의 누적 네트워크 대기 시간을 가져오려면 다음 사이에서 평균 개별 NTP 왕복 시간 (RTTs)을 측정 합니다.

- 대상 및 시간 서버 B
- 시간 서버 B 및 시간 서버 A
- 시간 서버 A와 원본

이 측정값은 inbox sqlservr.exe 도구를 사용 하 여 가져올 수 있습니다.  가상 하드 디스크 파일에 대한 중요 정보를 제공하려면

1. 대상 및 시간 서버 B에서 계산을 수행 합니다.
    
    `w32tm /stripchart /computer:TimeServerB /rdtsc /samples:450 > c:\temp\Target_TsB.csv`

2. 시간 서버 b에서 (지점) 시간 서버 a에 대 한 계산을 수행 합니다.
    
    `w32tm /stripchart /computer:TimeServerA /rdtsc /samples:450 > c:\temp\Target_TsA.csv`

3. 원본에 대해 시간 서버 a에서 계산을 수행 합니다.
 
4. 다음으로, 이전 단계에서 측정 한 평균 RoundTripDelay를 추가 하 고 2로 나누면 대상과 원본 간의 누적 네트워크 지연 시간을 가져옵니다.

#### <a name="registry-settings"></a>레지스트리 설정

# <a name="minpollintervaltabminpollinterval"></a>[MinPollInterval](#tab/MinPollInterval)
시스템 폴링에 허용 되는 최소 간격 (log2 초)을 구성 합니다.

|  |  | 
|---------|---------|
|키 위치     | HKLM: \ SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|설정    | 6        |
|결과 | 최소 폴링 간격은 이제 64 초입니다. |

다음 명령은 Windows 시간을 신호로 업데이트 된 설정을 선택 합니다.

`w32tm /config /update`


# <a name="maxpollintervaltabmaxpollinterval"></a>[MaxPollInterval](#tab/MaxPollInterval)
시스템 폴링에 허용 되는 최대 간격 (log2 초)을 구성 합니다.

|  |  |  
|---------|---------|
|키 위치     | HKLM: \ SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|설정    | 6        |
|결과 | 최대 폴링 간격은 이제 64 초입니다.  |

다음 명령은 Windows 시간을 신호로 업데이트 된 설정을 선택 합니다.

`w32tm /config /update`

# <a name="updateintervaltabupdateinterval"></a>[UpdateInterval](#tab/UpdateInterval)
단계 수정 조정 사이의 클록 틱 수입니다.

|  |  |  
|---------|---------|
|키 위치     | HKLM: \ SYSTEM\CurrentControlSet\Services\W32Time\Config       |
|설정    | 100        |
|결과 | 단계 수정 조정 간의 클록 틱 수는 이제 100 틱입니다. |

다음 명령은 Windows 시간을 신호로 업데이트 된 설정을 선택 합니다.

`w32tm /config /update`

# <a name="specialpollintervaltabspecialpollinterval"></a>[SpecialPollInterval](#tab/SpecialPollInterval)
SpecialInterval 0x1 플래그를 사용 하는 경우 폴링 간격 (초)을 구성 합니다.

|  |  |  
|---------|---------|
|키 위치     | HKLM: \ SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient        |
|설정    | 64        |
|결과 | 이제 폴링 간격이 64 초입니다. |

다음 명령은 Windows 시간을 다시 시작 하 여 업데이트 된 설정을 선택 합니다.

`net stop w32time && net start w32time`

# <a name="frequencycorrectratetabfrequencycorrectrate"></a>[FrequencyCorrectRate](#tab/FrequencyCorrectRate)

|  |  |  
|---------|---------|
|키 위치     | HKLM: \ SYSTEM\CurrentControlSet\Services\W32Time\Config      |
|설정    | 2        |


---
