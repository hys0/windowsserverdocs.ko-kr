---
title: 성능 카운터를 사용 하 여 원격 데스크톱 세션 호스트에서 응용 프로그램 응답성 문제를 진단 합니다.
description: RDS에서 앱 느리게 실행 되? RDSH에서 앱 성능 문제를 진단 하는 데 사용할 수는 성능 카운터에 대해 알아봅니다
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 09/19/2018
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 241b2b776a68cf5aec68a4d331201a07f0e5ea53
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844654"
---
# <a name="use-performance-counters-to-diagnose-app-performance-problems-on-remote-desktop-session-hosts"></a>성능 카운터를 사용 하 여 원격 데스크톱 세션 호스트에서 앱 성능 문제 진단

진단 하기 가장 어려운 문제 중 하나는 응용 프로그램 성능 저하가-응용 프로그램이 느리게 실행 됩니다. 또는 응답 하지 않습니다. 일반적으로 수집 CPU, 메모리, 디스크 입/출력 및 기타 메트릭에 의해 진단 시작 하 고 Windows Performance Analyzer와 같은 도구를 사용 하 여 문제 원인을 파악 하려고 합니다. 그러나 대부분의 경우이 데이터 도움이 되지 리소스 사용량 카운터 자주 크고 변형이 있으므로 근본 원인을 식별 합니다. 이렇게 하면 데이터 읽기 및 보고 된 문제를 사용 하 여 상관 관계를 지정 하기가 어렵습니다. 도움이 더 신속 하 게 앱 성능 문제를 해결, 몇 가지 새로운 성능 카운터가 추가 되었습니다 (사용 가능한 [다운로드 하려면](#download-windows-server-insider-software) 를 통해를 [Windows 참가자 프로그램](https://insider.windows.com)) 측정값 사용자 흐름을 입력 합니다.

사용자 입력 지연 카운터 RDP 환경을 잘못 된 최종 사용자에 대 한 근본 원인을 빠르게 식별할 수 있습니다. 이 카운터는 측정 기간 사용자 (예: 마우스 또는 키보드 사용) 입력 큐에 유지 프로세스에 의해 선택 전에 및 로컬 및 원격 세션에서 작동 하는 카운터입니다.

다음 이미지는 응용 프로그램에 클라이언트에서 사용자 입력된 흐름의 대략적인 표현을 보여 줍니다.

![원격 데스크톱-응용 프로그램에 사용자가 원격 데스크톱 클라이언트에서 사용자 입력된 흐름](.\media\rds-user-input.png)

사용자 입력 지연 카운터 사이의 대기 중인 입력 앱에서 시작한 경우 (시간 간격) 내 최대 델타를 측정 한 [일반적인 메시지 루프](https://msdn.microsoft.com/library/windows/desktop/ms644927.aspx#loop)다음 흐름 차트에 표시 된 것 처럼:

![원격 데스크톱-사용자 입력 지연 성능 카운터 흐름](.\media\rds-user-input-delay.png)

이 카운터의 하나의 중요 한 세부 정보 구성 가능한 간격 내에서 최대 사용자 입력된 지연을 보고 하는 합니다. 이것이 가장 긴 입력 등의 중요 하 고 표시 작업의 속도 영향을 줄 수 있는 응용 프로그램을 연결할 입력에 걸리는 시간입니다.

예를 들어 다음 테이블에서 사용자 입력된 지연 것으로 보고 1,000 밀리초가이 간격 내에서. 카운터 가장 느린 사용자 가장 느리게 입력된에 따라 "저속"에 대 한 사용자의 인식 결정 되므로 지연 간격에서 입력을 보고 (최대) 겪고, 모든 총 입력 평균 속도 없습니다.

|Number| 0 | 1 | 2 |
|------|---|---|---|
|지연 |16ms| 20 밀리초| 1,000 밀리초|

## <a name="enable-and-use-the-new-performance-counters"></a>설정 하 고 새 성능 카운터를 사용 합니다.

이러한 새 성능 카운터를 사용 하려면 먼저이 명령을 실행 하 여 레지스트리 키를 설정 해야 합니다.

```
reg add "HKLM\System\CurrentControlSet\Control\Terminal Server" /v "EnableLagCounter" /t REG_DWORD /d 0x1 /f
```

>[!NOTE]
> Windows 10, 버전 1809 이상 또는 Windows Server 2019를 사용 하는 경우 나중에 레지스트리 키를 활성화할 필요가 없습니다.

다음으로, 서버를 다시 시작 합니다. 그런 다음 성능 모니터를 열고 다음 스크린 샷과 같이 더하기 기호 (+)를 선택 합니다.

![원격 데스크톱-사용자를 추가 하는 방법을 보여주는 스크린 샷 입력 지연 성능 카운터](.\media\rds-add-user-input-counter-screen.png)

그 후 표시 카운터 추가 대화 상자에서 선택할 수 있습니다 **프로세스당 사용자 입력 지연** 하거나 **세션당 사용자 입력 지연**합니다.

![원격 데스크톱-세션당 사용자 입력된 지연을 추가 하는 방법을 보여 주는 스크린샷](.\media\rds-user-delay-per-session.png)

![원격 데스크톱-프로세스당 사용자 입력된 지연을 추가 하는 방법을 보여 주는 스크린샷](.\media\rds-user-delay-per-process.png)

선택 하는 경우 **프로세스당 사용자 입력 지연**를 표시 합니다 **선택한 개체의 인스턴스** (즉, 프로세스)에서 ```SessionID:ProcessID <Process Image>``` 형식.

예를 들어, 계산기 응용 프로그램에서 실행 중인 경우는 [세션 ID 1](https://msdn.microsoft.com/library/ms524326.aspx)를 보면 ```1:4232 <Calculator.exe>```합니다.

> [!NOTE]
> 일부 프로세스가 포함 됩니다. 시스템으로 실행 되는 모든 프로세스를 볼 수 없습니다.

카운터 추가 사용자 입력된 지연을 보고를 시작 합니다. 기본적으로 최대 소수 자릿수 (밀리초)을 100으로 설정 되어 있는지 note 합니다. 

![원격 데스크톱-성능 모니터에서 프로세스 별로 사용자 입력 지연에 대 한 작업 예제](.\media\rds-sample-user-input-delay-perfmon.png)

다음으로, 살펴보겠습니다 합니다 **세션당 사용자 입력 지연**합니다. 각 세션 ID에 대 한 인스턴스가 및 해당 카운터 지정 된 세션 내에서 모든 프로세스의 사용자 입력된 지연 시간을 표시 합니다. 또한 "Max" (최대 사용자 입력된 지연 모든 세션에 걸쳐) 및 "평균" (의 평균 acorss 모든 세션)를 호출 하는 두 개의 인스턴스가 있습니다.

이 표에서 이러한 인스턴스의 예를 보여 줍니다. (가져올 수 있습니다 동일한 정보를 Perfmon의 보고서 그래프 형식으로 전환 하 여.)

|카운터의 유형|인스턴스 이름|보고 된 지연 시간 (밀리초)|
|---------------|-------------|-------------------|
|프로세스 마다 사용자 입력 지연|1:4232 <Calculator.exe>|  200|
|프로세스 마다 사용자 입력 지연|2:1000 <Calculator.exe>|  16|
|프로세스 마다 사용자 입력 지연|1:2000 <Calculator.exe>|  32|
|세션당 사용자 입력 지연|1|    200|
|세션당 사용자 입력 지연|2|    16|
|세션당 사용자 입력 지연|평균|  108|
|세션당 사용자 입력 지연|최대값|  200|

## <a name="counters-used-in-an-overloaded-system"></a>오버 로드 된 시스템에서 사용 하는 카운터

이제 볼 수 있는 내용 보고서에서를 앱의 성능 저하 될 경우를 살펴보겠습니다. 다음 그래프는 Microsoft Word에서 원격으로 작업 하는 사용자에 대 한 정보를 보여 줍니다. 이 경우 RDSH 서버 성능이 저하 되 면 시간이 지남에 따라 더 많은 사용자가 로그인 합니다.

![원격 데스크톱-Microsoft Word를 실행 하는 RDSH 서버에 대 한 예제 성능 그래프](.\media\rds-user-input-perf-graph.png)

그래프의 줄 읽기 방법은 다음과 같습니다.

- 분홍색 줄에는 서버에 로그인 하는 세션 수를 보여 줍니다.
- 빨간색 선은 CPU 사용량입니다.
- 녹색 선은 모든 세션에 걸쳐 최대 사용자 입력된 지연입니다.
- 파란색 선 (이 그래프에서 검은색으로 표시 됨) 모든 세션에 걸쳐 평균 사용자 입력된 지연 시간을 나타냅니다.

CPU 스파이크 및 사용자 입력된 지연 간에 상관 관계가 있다는 것을 보면-CPU 가져옵니다 자세한 사용량에 따라 사용자 지연이 증가 입력 합니다. 또한 더 많은 사용자가 시스템에 추가, CPU 사용량 자주 사용자 입력된 지연 급증을 100%에 가까운 가져옵니다. 이 카운터는 서버가 실행 되는 리소스가 부족할 경우에서 매우 유용 하지만 특정 응용 프로그램과 관련 된 사용자 입력된 지연 시간을 추적 하도 사용할 수 있습니다.

## <a name="configuration-options"></a>구성 옵션

기본적으로 사용자 입력된 지연 1,000 밀리초 간격으로 보고 하는이 성능 카운터를 사용 하 여 때 기억해 야 할 중요 한 점입니다. 으로 설정한 경우 성능 카운터 샘플 간격 속성 (다음 스크린샷에 표시 된)으로 서로 다른 값으로 보고 되는 값 올바르지 않을 수 있습니다.

![원격 데스크톱-성능 모니터에 대 한 속성](.\media\rds-user-input-perfmon-properties.png)

이 해결 하려면 사용 하려는 하는 간격 (밀리초)와 일치 하도록 다음 레지스트리 키를 설정할 수 있습니다. 예를 들어 변경 하면 샘플 x 초 마다 5 초를 5000 밀리초를이 키를 설정 해야 합니다.

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server]

"LagCounterInterval"=dword:00005000
```

>[!NOTE]
>Windows 10, 버전 1809 이상 또는 Windows Server 2019를 사용 하는 경우 나중에 성능 카운터를 해결 하려면 LagCounterInterval 설정할 필요가 없습니다.

또한 몇 가지 동일한 레지스트리 키에서 유용한 키를 추가 했습니다.

**LagCounterImageNameFirst** -이 키로 `DWORD 1` (기본값 0 또는 키 없습니다). "이미지 이름 < SessionID:ProcessId >." 카운터의 이름 변경 예를 들어, "" < 1:7964 > 탐색기입니다. 이미지 이름을 기준으로 정렬 하려는 경우에 유용 합니다.

**LagCounterShowUnknown** -이 키로 `DWORD 1` (기본값 0 또는 키 없습니다). 서비스 또는 시스템으로 실행 중인 모든 프로세스를 표시 합니다. 일부 프로세스로 세션을 사용 하 여 표시 됩니다 "?."

다음은 모양 두 키를 설정 하는 경우입니다.

![원격 데스크톱-두 키를 사용 하 여 성능 모니터](.\media\rds-user-input-delay-with-two-counters.png)

## <a name="using-the-new-counters-with-non-microsoft-tools"></a>타사 도구를 사용 하 여 새 카운터를 사용 하 여

모니터링 도구를 사용 하 여이 카운터를 사용할 수는 [Perfmon API](https://msdn.microsoft.com/library/windows/desktop/aa371903.aspx)합니다.

## <a name="download-windows-server-insider-software"></a>Windows Server Insider 소프트웨어 다운로드

등록 된 참가자 수로 직접 이동 합니다 [Windows Server Insider Preview 다운로드 페이지](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver) 최신 Insider 소프트웨어를 다운로드 합니다.  참가자를 등록 하는 방법에 알아보려면 참조 [서버를 사용 하 여 시작](https://insider.windows.com/en-us/for-business-getting-started-server/)합니다.

## <a name="share-your-feedback"></a>의견 공유

피드백 허브를 통해이 기능에 대 한 피드백을 제출할 수 있습니다. 선택 **앱 > 다른 모든 앱** 포함 "RDS 성능 카운터-성능 모니터" 게시물의 제목입니다.

일반 기능 아이디어를 방문 합니다 [RDS UserVoice 페이지](https://aka.ms/uservoice-rds)합니다.
