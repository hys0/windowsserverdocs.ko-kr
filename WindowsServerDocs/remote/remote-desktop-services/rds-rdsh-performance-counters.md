---
title: 성능 카운터를 사용 하 여 원격 데스크톱 세션 호스트에서 응용 프로그램 응답성 문제를 진단 하려면
description: RDS에서 앱 느리게 실행 중인? RDSH의 앱 성능 문제를 진단 하는 데 사용할 수 있는 성능 카운터에 알아보기
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
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133719"
---
# 성능 카운터를 사용 하 여 원격 데스크톱 세션 호스트에서 앱 성능 문제를 진단 하려면

진단 하려면 가장 어려운 문제 중 하나는 응용 프로그램 성능이 저하-응용 프로그램 느리게 실행 중인 또는 응답 하지 않습니다. 일반적으로 사용자 진단 수집 CPU, 메모리, 디스크 입출력 및 기타 메트릭을 하 여 시작한 다음 Windows Performance Analyzer와 같은 도구를 사용 하 여 문제 원인을 파악 합니다. 안타깝게도 대부분의 경우이 데이터 하지 도움이 되는 리소스 소비 카운터 자주 발생 하 고 큰 변형 때문에 근본 원인을 파악 합니다. 이 인해 데이터를 읽고 보고 된 문제가 있는 상관 관계를 지정 합니다. 을 더 신속 하 게 앱 성능 문제를 해결할 수 있도록 몇 가지 새로운 성능 카운터 (사용 가능한 [다운로드 하려면](#download-windows-server-insider-software) [Windows 참가자 프로그램](https://insider.windows.com)을 통해) 사용자 입력된 흐름을 측정 하는 추가 했습니다.

사용자 입력 지연 카운터 빠르게 RDP 경험 잘못 된 최종 사용자에 대 한 근본 원인을 식별할 수 있습니다. 기간 (예: 마우스 또는 키보드 사용)을 입력 한 모든 사용자에에서 머물게 큐 프로세스에 의해 선택 하기 전에이 카운터를 측정 하 고 카운터 로컬 및 원격 세션에서 작동 합니다.

다음 이미지는 클라이언트에서 응용 프로그램 사용자 입력된 흐름의 대략적인 표현을 보여 줍니다.

![원격 데스크톱-응용 프로그램에 사용자가 원격 데스크톱 클라이언트에서 사용자 입력된 흐름](.\media\rds-user-input.png)

다음 흐름 차트에 표시 된 대로 간의 대기 중인 입력 및 [기존 메시지 루프](https://msdn.microsoft.com/library/windows/desktop/ms644927.aspx#loop)에서 앱에서 선택한 시간 간격) (내 최대 델타를 측정 하는 사용자 입력 지연 카운터:

![원격 데스크톱-사용자 입력 지연 성능 카운터 흐름](.\media\rds-user-input-delay.png)

이 카운터의 한 가지 중요 사항이 구성 가능한 간격 내에서 최대 사용자 입력된 지연 보고 함을입니다. 입력 입력 등의 중요 한 되 고 표시 작업의 속도 영향을 줄 수 있는 응용 프로그램에 도달 하는 데 걸리는 시간이 긴입니다.

예를 들어 다음 표의 사용자 입력된 지연 것으로 보고 될 1,000 ms이이 간격 내에서. 카운터 가장 느린 사용자의 "느린" 사용자가 인식 느린 입력된 시간 따라 결정 되므로 지연 간격에서 입력을 보고 (최대값)은 경험을 평균 총 모든 입력 속도 하지 합니다.

|숫자| 0 | 1 | 2 |
|------|---|---|---|
|지연 |16 ms| 20 ms| 1,000 ms|

## 설정 하 고 새 성능 카운터를 사용 합니다.

이러한 새 성능 카운터를 사용 하려면 먼저이 명령을 실행 하 여 레지스트리 키를 활성화 해야 합니다.

```
reg add "HKLM\System\CurrentControlSet\Control\Terminal Server" /v "EnableLagCounter" /t REG_DWORD /d 0x1 /f
```

>[!NOTE]
> Windows 10, 버전 1809 이상 또는 Windows Server 2019를 사용 하는 경우 나중에 레지스트리 키를 활성화할 필요가 없습니다.

다음으로 서버를 다시 시작 합니다. 그런 다음 성능 모니터를 열고 다음 화면에 표시 된 대로 더하기 기호 (+)를 선택 합니다.

![원격 데스크톱-사용자를 추가 하는 방법을 보여 주는 스크린샷 입력 지연 성능 카운터](.\media\rds-add-user-input-counter-screen.png)

하는 작업을 수행한 후 **프로세스 당 사용자 입력 지연** 또는 **사용자 입력 지연 세션별**를 선택할 수 있는 카운터 추가 대화 상자에서 볼 수 있습니다.

![원격 데스크톱-세션별 사용자 입력된 지연을 추가 하는 방법을 보여 주는 스크린샷](.\media\rds-user-delay-per-session.png)

![원격 데스크톱-프로세스 당 사용자 입력된 지연을 추가 하는 방법을 보여 주는 스크린샷](.\media\rds-user-delay-per-process.png)

**사용자 입력 지연 당 프로세스를**선택 하면 **선택한 개체의 인스턴스** (즉, 프로세스) 확인할 ```SessionID:ProcessID <Process Image>``` 형식입니다.

예를 들어 [세션 ID가 1](https://msdn.microsoft.com/library/ms524326.aspx)에서 계산기 앱이 실행 보면 ```1:4232 <Calculator.exe>```.

> [!NOTE]
> 모든 프로세스에 포함 되어 있습니다. 시스템으로 실행 되는 모든 프로세스 표시 되지 않습니다.

카운터 추가 되는 즉시 사용자 입력된 지연 보고를 시작 합니다. Note 기본적으로 최대 배율 100 (밀리초)으로 설정 됩니다. 

![원격 데스크톱-성능 모니터의 프로세스 당 사용자 입력 지연에 대 한 작업의 예](.\media\rds-sample-user-input-delay-perfmon.png)

다음으로 **사용자 입력 지연 세션별**살펴보겠습니다. 각 세션 ID에 대 한 인스턴스가 및 해당 카운터 지정 된 세션 내에서 모든 프로세스의 사용자 입력된 지연 표시 합니다. 또한 "최대" (최대 사용자 입력된 지연 모든 세션에서) 및 "평균" (의 평균 acorss 모든 세션) 라는 두 개의 인스턴스가 있습니다.

이 표에서 이러한 인스턴스의 시각적 예를 보여줍니다. (수 정보를 가져오면 동일한 성능 모니터에서 보고서 그래프 유형으로 전환 하 여.)

|카운터의 유형|인스턴스 이름|보고 된 지연 시간 (밀리초)|
|---------------|-------------|-------------------|
|프로세스 당 사용자 입력 지연|< Calculator.exe > 1:4232|  200|
|프로세스 당 사용자 입력 지연|< Calculator.exe > 2:1000|  16|
|프로세스 당 사용자 입력 지연|< Calculator.exe > 1:2000|  32|
|세션별 사용자 입력 지연|1|    200|
|세션별 사용자 입력 지연|2|    16|
|세션별 사용자 입력 지연|평균|  108|
|세션별 사용자 입력 지연|최대|  200|

## 오버 로드 된 시스템에서 사용 되는 카운터

이제 어떤 경우에 표시 됩니다 보고서에는 앱에 대 한 성능이 살펴보겠습니다. 다음 그래프는 Microsoft Word에서 원격으로 작업 하는 사용자에 대 한 정보를 보여 줍니다. 이 경우 더 많은 사용자가 로그인 하는 대로 시간이 지남에 따라 RDSH 서버 성능이 저하 됩니다.

![원격 데스크톱-Microsoft Word 실행 RDSH 서버에 대 한 예제 성능 그래프](.\media\rds-user-input-perf-graph.png)

그래프의 줄을 읽는 방법은 다음과 같습니다.

- 분홍색 줄의 서버에 로그인 세션 수를 보여 줍니다.
- 빨간색 선 CPU 사용량입니다.
- 녹색 줄 모든 세션에서 최대 사용자 입력된 지연 됩니다.
- 파란색 줄 (이 그래프에 검정으로 표시 됨)는 모든 세션에서 평균 사용자 입력된 지연을 나타냅니다.

CPU 스파이크 및 사용자 입력된 지연 간의 상관 관계 임을 알 수-사용자 입력 지연 증가 CPU 높아질수록 자세한 사용 합니다. 또한 더 많은 사용자가 시스템에 추가 하는 대로 CPU 사용량 더 자주 발생 사용자 입력된 지연 급증을 100%로 더 가까이 가져옵니다. 이 카운터 서버 리소스가 실행 되는 위치 하는 경우에 매우 유용 하지만 사용자 입력된 지연와 관련 된 특정 응용 프로그램을 추적 하기 위해도 사용할 수 있습니다.

## 구성 옵션

이 성능 카운터를 사용 하 여 기본적으로 사용자 입력된 지연 1,000 ms 간격에 보고 하는 것을 기억 하는 중요 한 점은 합니다. 성능 카운터 샘플 간격 속성을 설정 하면 (다음 스크린샷에 표시 된) 하는 대로 다른, 보고 된 값 올바른 됩니다.

![원격 데스크톱-성능 모니터에 대 한 속성](.\media\rds-user-input-perfmon-properties.png)

이 문제를 해결 하려면 간격 (밀리초)을 사용 하려면 일치 하도록 다음 레지스트리 키를 설정할 수 있습니다. 예를 들어 5 초 샘플 x 초 마다 변경, 경우 해야 5000 밀리초로이 키를 설정 합니다.

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server]

"LagCounterInterval"=dword:00005000
```

>[!NOTE]
>Windows 10, 버전 1809 이상 또는 Windows Server 2019를 사용 하는 경우 나중에 성능 카운터를 해결 하려면 LagCounterInterval 설정할 필요가 없습니다.

또한 동일한 레지스트리 키에서 유용 하지 못할 키의 몇 가지를 추가 했습니다.

**LagCounterImageNameFirst** -이 키를 설정 `DWORD 1` (기본값 0 또는 키 없습니다). 카운터 이름으로 "이미지 Name < SessionID:ProcessId >." 변경 예를 들어, "" < 1:7964 > explorer 합니다. 이미지 이름으로 정렬 하려는 경우에 유용 합니다.

**LagCounterShowUnknown** -이 키를 설정 `DWORD 1` (기본값 0 또는 키 없습니다). 서비스 또는 시스템으로 실행 되는 모든 프로세스를 표시 합니다. 설정의 세션을 사용 하 여 일부 프로세스 나타납니다 "?."

이 다음과 같은 키를 모두 설정한 경우:

![원격 데스크톱-에 두 키를 사용 하 여 성능 모니터](.\media\rds-user-input-delay-with-two-counters.png)

## Microsoft가 아닌 타사 도구를 사용 하 여 새 카운터를 사용 하 여

모니터링 도구 [성능 모니터 API](https://msdn.microsoft.com/library/windows/desktop/aa371903.aspx)를 사용 하 여이 카운터를 사용할 수 있습니다.

## Windows Server 참가자 소프트웨어를 다운로드 합니다.

등록 된 참가자는 [Windows Server Insider Preview 다운로드 페이지를](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver) 최신 Insider 소프트웨어 다운로드에 직접 이동할 수 있습니다.  참가자로 등록 하는 방법을 알아보려면 [서버와 시작](https://insider.windows.com/en-us/for-business-getting-started-server/)을 참조 하세요.

## 피드백을 공유 합니다.

피드백 허브를 통해이 기능에 대 한 피드백을 제출할 수 있습니다. 선택 **앱 > 다른 모든 앱** 포함 하 고 "RDS 성능 카운터-성능 모니터" 게시물의 제목입니다.

일반 기능 아이디어 [RDS UserVoice 페이지](https://aka.ms/uservoice-rds)를 방문 하세요.
