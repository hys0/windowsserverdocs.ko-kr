---
ms.assetid: ''
title: 높은 정확도 대 한 시스템 구성
description: Windows 10 및 Windows Server 2016에서 시간 동기화 크게 향상 되었습니다.  적절 한 작동 조건 시스템이 1ms (밀리초)을 유지 하기 위해 구성 수 (UTC)에 대해 정확도 이상.
author: shortpatti
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: d872252180d49bd41a91e9a8eaf516b834ed242a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814674"
---
# <a name="configuring-systems-for-high-accuracy"></a>높은 정확도 대 한 시스템 구성
>적용 대상: Windows Server 2016 및 Windows 10 버전 1607 이상

Windows 10 및 Windows Server 2016에서 시간 동기화 크게 향상 되었습니다.  적절 한 작동 조건 시스템이 1ms (밀리초)을 유지 하기 위해 구성 수 (UTC)에 대해 정확도 이상.

다음 지침은 높은 정확도 달성 하기 위해 시스템을 구성 하는 데 도움이 됩니다.  이 문서에는 다음 요구 사항을 설명합니다.

- 지원되는 운영 체제
- 시스템 구성 

> [!WARNING]
> **이전 운영 체제 정확도 목표**<br>
>Windows Server 2012 R2 및 다음 동일한 고정밀 목표를 충족할 수 있습니다. 이러한 운영 체제 높은 정확도 대 한 지원 되지 않습니다.
>
>이러한 버전의 Windows 시간 서비스에는 다음 요구 사항을 충족 시키는:
>
> - Kerberos 버전 5 인증 요구 사항을 충족 하는 데 필요한 시간 정확도 제공 합니다.
> - Windows 클라이언트 및 일반적인 Active Directory 포리스트에 가입 된 서버에 대해 느슨하게 정확한 시간을 제공 합니다.
>
>큰 허용 오차 2012 R2에서 Windows 시간 서비스의 디자인 사양 외부에 있습니다.

## <a name="windows-10-and-windows-server-2016-default-configuration"></a>Windows 10 및 Windows Server 2016 기본 구성

Windows 10 또는 Windows Server 2016에서 1ms까지 정확도 지원 했습니다 대부분 고객의 매우 정확한 시간을 필요 하지 않습니다.

이와 같이 합니다 **기본 구성** 하는 이전 운영 체제와 같은 요구 사항이 충족 됩니다.

- Kerberos 버전 5 인증 요구 사항을 충족 하는 데 필요한 시간 정확도 제공 합니다.
- Windows 클라이언트 및 일반적인 Active Directory 포리스트에 가입 된 서버에 대해 느슨하게 정확한 시간을 제공 합니다.

## <a name="how-to-configure-systems-for-high-accuracy"></a>높은 정확도 대 한 시스템을 구성 하는 방법

>[!IMPORTANT]
>**매우 정확 하 게 시스템의 지원 가능성에 대 한 참고**<br>
> 시간 정확도 최종 장치에 신뢰할 수 있는 시간 원본에서 정확한 시간을 엔드-투-엔드 배포를 수반합니다.  이 경로 따라 측정값에서 assymetry 정확도 영향을 주는 부정적인를 추가 하는 모든 장치에서 달성할 수 있는 정확도 적용 됩니다.
>
>따라서이 문서화 했습니다 합니다 [지원 정확도 높은 환경에 대 한 Windows 시간 서비스를 구성 하는 경계](support-boundary.md) 고정밀 대상에 연결할 역시 만족 해야 하는 환경 요구 사항 개요.

### <a name="operating-system-requirements"></a>운영 체제 요구 사항

높은 정확도 구성에는 Windows 10 또는 Windows Server 2016 필요합니다.  모든 Windows 시간 토폴로지에서 더 높은 계층 Windows 시간 서버를 포함 하 여이 요구 사항을 충족 해야 합니다 장치와의 가상화 시나리오, 시간이 중요 한 가상 컴퓨터를 실행 하는 Hyper-v 호스트 이러한 모든 장치 이상 이어야 합니다 Windows 10 또는 Windows Server 2016 합니다.

아래 그림에서는 높은 정확도 필요로 하는 가상 컴퓨터는 Windows 10 또는 Windows Server 2016를 실행 중인 합니다.  마찬가지로, 업스트림 Windows 시간 서버와 가상 컴퓨터가 있는 Hyper-v 호스트는 Windows Server 2016를 실행도 해야 합니다.

![시간 토폴로지-1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/Topology2016.png)


>[!TIP] 
>**Windows 버전 확인**<br>
> 명령을 실행할 수 있습니다 `winver` OS를 확인 하려면 명령 프롬프트에서 버전이 1607 (또는 이상) 및 OS 빌드 14393 (또는 이상)는 아래와 같이:
>
> ![Winver - 2016 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/winver2016.png)

### <a name="system-configuration"></a>시스템 구성

높은 정확도 대상에 도달 시스템 구성에 필요 합니다.  다양 한 방법으로이 구성에서는 그룹 정책을 통해 또는 레지스트리에서 직접 포함 하 여 수행할 수 있습니다.  Windows 시간 서비스 기술 참조-에서 각이 설정에 대 한 자세한 정보를 찾을 수 있습니다 [Windows 시간 서비스 도구가](Windows-Time-Service-Tools-and-Settings.md#windows-time-service-tools)합니다.

#### <a name="windows-time-service-startup-type"></a>Windows 시간 서비스 시작 유형

Windows 시간 서비스 (w32time))는 지속적으로 실행 해야 합니다.  이 작업을 수행 하려면 Windows 시간 서비스의 시작 유형을 '자동'으로 시작 되도록 구성 합니다.

![자동 구성](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/AutomaticService.PNG)

#### <a name="cumulative-one-way-network-latency"></a>누적 단방향 네트워크 대기 시간

측정 불확실성 및 "노이즈" 따라 올라가는 네트워크 대기 시간이 증가 합니다.  따라서 반드시 네트워크 대기 시간을 적절 한 경계에 포함 되도록 합니다.  특정 요구 사항 대상 정확도에 종속 되며에 설명 된 합니다 [지원 정확도 높은 환경에 대 한 Windows 시간 서비스를 구성 하는 경계](support-boundary.md) 문서.

누적 단방향 네트워크 대기 시간을 계산 하려면 대상을 사용 하 여 시작 하 고 1 시간 원본 정확도 높은 계층에서 끝나는 시간 토폴로지에서 NTP 클라이언트-서버 노드 쌍 간의 개별 단방향 지연을 추가 합니다.

예를 들어 다음과 같은 가치를 제공해야 합니다. 시간 동기화 계층을 매우 정확 하 게 원본, 두 명의 중간 NTP 서버 A 및 B 및 지정 된 순서로 대상 컴퓨터를 사용 하 여는 것이 좋습니다. 원본과 대상 간의 누적 네트워크 대기 시간을 얻으려면 개별 NTP 왕복 사이 (RTTs) 시간이 평균을 측정 합니다.

- 대상 및 시간 서버 B
- 시간 서버 B와 시간 서버는
- 시간 서버 A와 원본

받은 편지함 w32tm.exe 도구를 사용 하 여이 측정을 얻을 수 있습니다.  가상 하드 디스크 파일에 대한 중요 정보를 제공하려면
<!-- Use PowerShell to import the CSV then average the RTT Column -->

1. 대상 및 시간 서버 B에서에서 계산을 수행 합니다.
    
    `w32tm /stripchart /computer:TimeServerB /rdtsc /samples:450 > c:\temp\Target_TsB.csv`

2. 에 대 한 시간 서버 b에서 계산을 수행 (가리키는) 시간 서버를 합니다.
    
    `w32tm /stripchart /computer:TimeServerA /rdtsc /samples:450 > c:\temp\Target_TsA.csv`

3. 시간 서버에서 계산을 수행 된 원본에 대 한 합니다.
 
4. 다음으로, 이전 단계에서 측정 된 평균 RoundTripDelay 추가 하 고 대상과 원본 간의 누적 네트워크 지연 시간을 가져오려면 2로 나눕니다.

#### <a name="registry-settings"></a>레지스트리 설정

# <a name="minpollintervaltabminpollinterval"></a>[MinPollInterval](#tab/MinPollInterval)
Log2 시스템 폴링에 대 한 허용 하는 시간 (초)에서 최소 간격을 구성 합니다.

|  |  | 
|---------|---------|
|키 위치     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|설정    | 6        |
|결과 | 최소 폴링 간격은 이제 64 초입니다. |

다음 명령을 업데이트 된 설정을 선택할 Windows 시간 신호를 보냅니다.

`w32tm /config /update`


# <a name="maxpollintervaltabmaxpollinterval"></a>[MaxPollInterval](#tab/MaxPollInterval)
Log2 시스템 폴링에 대 한 허용 하는 시간 (초)에서 가장 큰 간격을 구성 합니다.

|  |  |  
|---------|---------|
|키 위치     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|설정    | 6        |
|결과 | 최대 폴링 간격은 이제 64 초입니다.  |

다음 명령을 업데이트 된 설정을 선택할 Windows 시간 신호를 보냅니다.

`w32tm /config /update`

# <a name="updateintervaltabupdateinterval"></a>[UpdateInterval](#tab/UpdateInterval)
단계 수정 조정 간의 클록 틱 수입니다.

|  |  |  
|---------|---------|
|키 위치     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config       |
|설정    | 100        |
|결과 | 단계 수정 조정 간의 클록 틱 수가 100 틱 되었습니다. |

다음 명령을 업데이트 된 설정을 선택할 Windows 시간 신호를 보냅니다.

`w32tm /config /update`

# <a name="specialpollintervaltabspecialpollinterval"></a>[SpecialPollInterval](#tab/SpecialPollInterval)
0x1 SpecialInterval 플래그를 사용 하도록 설정 하는 시간 (초)에서 폴링 간격을 구성 합니다.

|  |  |  
|---------|---------|
|키 위치     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient        |
|설정    | 64        |
|결과 | 폴링 간격은 이제 64 시간 (초)입니다. |

다음 명령을 업데이트 된 설정을 선택할 Windows 시간을 다시 시작 합니다.

`net stop w32time && net start w32time`

# <a name="frequencycorrectratetabfrequencycorrectrate"></a>[FrequencyCorrectRate](#tab/FrequencyCorrectRate)

|  |  |  
|---------|---------|
|키 위치     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config      |
|설정    | 2        |


---
