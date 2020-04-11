---
title: 성능 카운터를 사용하여 원격 데스크톱 세션 호스트에서 애플리케이션 응답성 문제 진단
description: RDS에서 앱이 느리게 실행되나요? RDSH에서 앱 성능 문제를 진단하는 데 사용할 수 있는 성능 카운터에 대해 알아보기
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 07/11/2019
ms.topic: article
author: lizap
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: c33e5c6309c41e39aeda3a2bdff1a0caf72b2675
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860336"
---
# <a name="use-performance-counters-to-diagnose-app-performance-problems-on-remote-desktop-session-hosts"></a>성능 카운터를 사용하여 원격 데스크톱 세션 호스트에서 앱 성능 문제 진단

> 적용 대상: Windows Server 2019, Windows 10

진단하기가 가장 어려운 문제 중 하나는 열악한 애플리케이션 성능 즉, 애플리케이션이 느리게 실행되거나 응답하지 않는 경우입니다. 일반적으로 CPU, 메모리, 디스크 입출력 및 기타 메트릭을 수집하여 진단을 시작한 다음, Windows Performance Analyzer와 같은 도구를 사용하여 문제의 원인을 파악하려고 합니다. 이러한 데이터는 불행히도 대부분의 상황에서 근본 원인을 식별하는 데 도움이 되지 않습니다. 리소스 소비 카운터에는 큰 차이가 빈번하게 있기 때문입니다. 그래서 데이터를 읽고, 보고된 문제와 상관 관계를 지정하기가 어렵습니다. 앱 성능 문제를 신속하게 해결할 수 있도록 사용자 입력 흐름을 측정하는 몇 가지 새로운 성능 카운터([Windows 참가자 프로그램](https://insider.windows.com)을 통해 [다운로드](#download-windows-server-insider-software) 가능)가 추가되었습니다.

>[!NOTE]
>사용자 입력 지연 카운터는 다음 제품과만 호환됩니다.
> - Windows Server 2019 이상
> - Windows 10, version 1809 이상

사용자 입력 지연 카운터는 양호하지 않은 최종 사용자 RDP 환경의 근본적인 원인을 신속하게 파악하는 데 도움이 됩니다. 이 카운터는 사용자 입력(예: 마우스 또는 키보드 사용)이 프로세스에서 선택되기 전에 큐에 머무르는 시간의 길이를 측정하며, 로컬 세션과 원격 세션 모두에서 작동합니다.

다음 이미지는 클라이언트에서 애플리케이션으로 이동하는 사용자 입력 흐름을 대략적으로 보여줍니다.

![원격 데스크톱 - 사용자 입력은 사용자의 원격 데스크톱 클라이언트에서 애플리케이션으로 흐릅니다.](./media/rds-user-input.png)

사용자 입력 지연 카운터는 다음 순서도에 표시된 대로 입력이 큐에 대기되는 시간과 [일반적인 메시지 루프](https://msdn.microsoft.com/library/windows/desktop/ms644927.aspx#loop)에서 앱에 의해 선택되는 시간 사이의 최대 델타(시간 간격 내)를 측정합니다.

![원격 데스크톱 - 사용자 입력 지연 성능 카운터 흐름](./media/rds-user-input-delay.png)

이 카운터의 한 가지 중요한 세부 정보는 구성 가능한 간격 내에서 최대 사용자 입력 지연을 보고한다는 점입니다. 이것은 입력이 애플리케이션에 도달하는 데 걸리는 가장 긴 시간이며, 입력과 같이 중요하고 가시적인 동작의 속도에 영향을 미칠 수 있습니다.

예를 들어, 다음 표에서 사용자 입력 지연은 이 간격 내에서 1,000밀리초로 보고됩니다. 카운터는 간격에서 가장 느린 사용자 입력 지연을 보고합니다. 그 이유는 사용자가 "느리다"고 인식하는 것이 모든 총 입력의 평균 속도에 의해 결정되는 것이 아니라 사용자가 경험하는 가장 느린 입력 시간(최댓값)에 따라 결정되기 때문입니다.

|번호| 0 | 1 | 2 |
|------|---|---|---|
|지연 |16밀리초| 20밀리초| 1,000밀리초|

## <a name="enable-and-use-the-new-performance-counters"></a>새 성능 카운터 사용 설정 및 사용

새로운 성능 카운터를 사용하려면 먼저 다음 명령을 실행하여 레지스트리 키를 사용하도록 설정해야 합니다.

```
reg add "HKLM\System\CurrentControlSet\Control\Terminal Server" /v "EnableLagCounter" /t REG_DWORD /d 0x1 /f
```

>[!NOTE]
> Windows 10, 버전 1809 이상 또는 Windows Server 2019 이상을 사용하는 경우에는 레지스트리 키를 사용하도록 설정할 필요가 없습니다.

다음으로, 서버를 다시 시작합니다. 그런 다음, 성능 모니터를 열고 다음 스크린샷과 같이 더하기 기호(+)를 선택합니다.

![원격 데스크톱 - 사용자 입력 지연 성능 카운터를 추가하는 방법을 보여주는 스크린샷](./media/rds-add-user-input-counter-screen.png)

그러면 카운터 추가 대화 상자가 보이고, **User Input Delay per Process**(프로세스별 사용자 입력 지연) 또는 **User Input Delay per Session**(세션별 사용자 입력 지연)를 선택할 수 있습니다.

![원격 데스크톱 - 세션별 사용자 입력 지연을 추가하는 방법을 보여주는 스크린샷](./media/rds-user-delay-per-session.png)

![원격 데스크톱 - 프로세스별 사용자 입력 지연을 추가하는 방법을 보여주는 스크린샷](./media/rds-user-delay-per-process.png)

**User Input Delay per Process**(프로세스별 사용자 입력 지연)을 선택하면 **선택한 개체의 인스턴스**(즉, 프로세스)가 ```SessionID:ProcessID <Process Image>``` 형식으로 보입니다.

예를 들어, 계산기 앱이 [세션 ID 1](https://msdn.microsoft.com/library/ms524326.aspx)에서 실행되면, ```1:4232 <Calculator.exe>```가 보입니다.

> [!NOTE]
> 모든 프로세스가 포함되는 것은 아닙니다. SYSTEM으로 실행되는 프로세스는 보이지 않습니다.

카운터를 추가하자마자 사용자 입력 지연이 보고되기 시작합니다. 최대 배율은 기본적으로 100(밀리초)으로 설정되어 있습니다. 

![원격 데스크톱 - 성능 모니터에서 User Input Delay per process(프로세스별 사용자 입력 지연)에 대한 작업의 예](./media/rds-sample-user-input-delay-perfmon.png)

다음으로 **세션별 사용자 입력 지연**을 살펴보겠습니다. 각 세션 ID에 대한 인스턴스가 있으며, 해당 카운터에는 지정된 세션 내 프로세스에 대한 사용자 입력 지연이 표시됩니다. 또한, "최대"(모든 세션에서 최대 사용자 입력 지연)와 "평균"(모든 세션의 평균)이라는 두 가지 인스턴스가 있습니다.

다음 표는 이러한 인스턴스의 시각적 예를 보여줍니다. (보고서 그래프 형식으로 전환하면 성능 모니터에서 동일한 정보를 얻을 수 있습니다.)

|카운터의 형식|인스턴스 이름|보고된 지연(밀리초)|
|---------------|-------------|-------------------|
|프로세스별 사용자 입력 지연|1:4232 <Calculator.exe>|    200|
|프로세스별 사용자 입력 지연|2:1000 <Calculator.exe>|    16|
|프로세스별 사용자 입력 지연|1:2000 <Calculator.exe>|    32|
|세션별 사용자 입력 지연|1|    200|
|세션별 사용자 입력 지연|2|    16|
|세션별 사용자 입력 지연|평균|     108|
|세션별 사용자 입력 지연|최대|     200|

## <a name="counters-used-in-an-overloaded-system"></a>오버로드된 시스템에서 사용되는 카운터

이제 앱 성능이 저하되는 경우 보고서에 표시되는 내용을 살펴보겠습니다. 다음 그래프는 Microsoft Word에서 원격으로 작업하는 사용자에 대한 정보를 보여줍니다. 이 경우 시간이 지남에 따라 더 많은 사용자가 로그인하면서 RDSH 서버 성능이 저하됩니다.

![원격 데스크톱 - Microsoft Word를 실행하는 RDSH 서버의 성능 그래프 예제](./media/rds-user-input-perf-graph.png)

그래프에서 선을 읽는 방법은 다음과 같습니다.

- 분홍색 선은 서버에 로그인된 세션 수를 보여줍니다.
- 빨간색 선은 CPU 사용량입니다.
- 녹색 선은 모든 세션에서 최대 사용자 입력 지연입니다.
- 파란색 선(이 그래프에는 검은색으로 표시됨)은 모든 세션의 평균 사용자 입력 지연을 나타냅니다.

CPU 스파이크와 사용자 입력 지연 사이에 상관 관계가 있는 것을 볼 수 있습니다. CPU 사용량이 많아지면 사용자 입력 지연이 증가합니다. 또한 시스템에 사용자가 더 많이 추가되고 CPU 사용량이 100%에 가까워지면서 사용자 입력 지연이 급격히 증가합니다. 이 카운터는 서버의 리소스가 부족한 경우 매우 유용하지만 특정 애플리케이션과 관련된 사용자 입력 지연을 추적하는 데 사용할 수도 있습니다.

## <a name="configuration-options"></a>구성 옵션

성능 카운터를 사용할 때 기억해야 할 중요한 사항은 기본적으로 1,000밀리초 간격으로 사용자 입력 지연을 보고한다는 것입니다. 성능 카운터 샘플 간격 속성을 다른 값으로 설정하면(다음 스크린샷과 같이) 보고된 값이 올바르지 않을 수 있습니다.

![원격 데스크톱 - 성능 모니터의 속성](./media/rds-user-input-perfmon-properties.png)

이 문제를 해결하려면, 원하는 간격(밀리초)과 일치하도록 다음 레지스트리 키를 설정하면 됩니다. 예를 들어, 샘플링 간격 x초를 5초로 변경하면 이 키를 5000ms로 설정해야 합니다.

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server]

"LagCounterInterval"=dword:00005000
```

>[!NOTE]
>Windows 10, 버전 1809 이상 또는 Windows Server 2019 이상을 사용하는 경우에는 성능 카운터를 수정하기 위해 LagCounterInterval을 설정할 필요가 없습니다.

또한 동일한 레지스트리 키에서 유용할 수 있는 몇 가지 키가 추가되었습니다.

**LagCounterImageNameFirst** — 이 키는 `DWORD 1`로 설정합니다(기본값 0이며, 그렇지 않으면 키가 존재하지 않음). 카운터의 이름이 "이미지 이름 <SessionID:ProcessId>"으로 변경됩니다. 예, "탐색기 <1:7964>." 이미지 이름을 기준으로 정렬하려는 경우에 유용합니다.

**LagCounterShowUnknown** — 이 키는 `DWORD 1`로 설정합니다(기본값 0이며, 그렇지 않으면 키가 존재하지 않음). 서비스 또는 SYSTEM으로 실행 중인 프로세스가 표시됩니다. 일부 프로세스는 세션이 "?"로 설정된 상태로 표시됩니다.

두 키를 모두 켜면 다음과 같이 표시됩니다.

![원격 데스크톱 - 두 키가 모두 켜진 성능 모니터](./media/rds-user-input-delay-with-two-counters.png)

## <a name="using-the-new-counters-with-non-microsoft-tools"></a>타사 도구로 새 카운터 사용

모니터링 도구는 [Perfmon API](https://msdn.microsoft.com/library/windows/desktop/aa371903.aspx)를 사용하여 이 카운터를 소비할 수 있습니다.

## <a name="download-windows-server-insider-software"></a>Windows Server Insider 소프트웨어 다운로드

등록된 참가자는 [Windows Server Insider Preview 다운로드 페이지](https://www.microsoft.com/software-download/windowsinsiderpreviewserver)로 직접 이동하여 최신 Insider 소프트웨어 다운로드를 받을 수 있습니다.  참가자를 등록하는 방법을 알아보려면 [Server 시작](https://insider.windows.com/en-us/for-business-getting-started-server/)을 참조하세요.

## <a name="share-your-feedback"></a>피드백 공유

피드백 허브를 통해 이 기능에 대한 피드백을 제출할 수 있습니다. **앱 > 기타 모든 앱**을 선택하고 게시물 제목에 "RDS 성능 카운터—성능 모니터"를 포함시킵니다.

일반적인 기능 아이디어는 [RDS UserVoice 페이지](https://aka.ms/uservoice-rds)를 방문하세요.
