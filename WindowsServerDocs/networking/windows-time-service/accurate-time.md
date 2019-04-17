---
ms.assetid: 72a90d00-56ee-48a9-9fae-64cbad29556c
title: Windows 2016 정확한 시간
description: ''
author: shortpatti
ms.author: pashort
manager: brianlic
ms.date: 3/12/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: f4b61dbf07fbc21820dd7b9326bbc990e4db3602
ms.sourcegitcommit: fb4e2ace2e0a29e0f6b028f1cb945cab6aa6ee2c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2018
---
# <a name="windows-server-2016-accurate-time"></a>Windows Server 2016 정확 하 게 시간

>Windows Server 2016 적용 됩니다.

전체 이전 버전과 호환성이 NTP 오래 된 Windows 버전과 호환성을 유지 하면서 시간 동기화 정확도 Windows Server 2016에 크게 향상 되었습니다. 합리적인 작동 조건 1를 유지할 수 UTC 또는 Windows Server 2016 및 Windows 10 1 주년 업데이트 도메인 구성원에 대해 더와 관련 하 여 ms 정확도 합니다.

Windows 시간 서비스에 대 한 클라이언트 및 서버 시간 동기화 공급자 플러그 인 모델을 사용 하는 구성 요소입니다.  Windows에는 두 가지 기본 제공 되는 클라이언트 공급자는 사용할 수 있는 제 3 자 플러그 인 및 합니다. 한 공급자 사용 하 여 [NTP (RFC 1305)](https://tools.ietf.org/html/rfc1305) 또는 [MS NTP](https://msdn.microsoft.com/en-us/library/cc246877.aspx) 로컬 시스템 시간 NTP 및/또는 MS NTP 호환 참조 서버에 동기화 됩니다. 다른 공급자 Hyper-v 되며 VM (가상 컴퓨터)는 Hyper-v 호스트를 동기화 합니다.  공급자를 여러 개 있는 경우 Windows는 먼저 계층 수준을 사용 하는 가장 좋은 공급자 지연 루트 루트 분산 이어서 선택한 마지막으로 오프셋 시간 합니다.

>[!NOTE]
>Windows 시간 서비스의 빠른 개요를 살펴보세요이 [비디오 고급 개요](https://aka.ms/WS2016TimeVideo)합니다.

<!-- Not sure what to do with the following -->
이 항목에서는 설명... 이러한 항목 관련 정확한 시간을 활성화 하 다음과 같습니다. 

- 향상 된 기능
- 측정
- 모범 사례

>[!IMPORTANT]
> Windows 2016 정확성 시간 문서에서 참조 되는 addendum 다운로드할 수 [여기](http://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf)합니다.  이 문서는 우리의 테스트 하 고 측정 방법에 대 한 자세한 내용을 제공합니다.



> [!NOTE] 
> Windows 시간 공급자 플러그 인 모델은 [technet 설명](https://msdn.microsoft.com/en-us/library/windows/desktop/ms725475%28v=vs.85%29.aspx)합니다.
<!-- -->





## <a name="domain-hierarchy"></a>도메인 계층
도메인 및 독립 실행형 구성 다르게 작동합니다.

- 도메인 회원 보안 및 시간 참조의 정품 인증을 사용 하는 보안 NTP 프로토콜을 사용 합니다.  도메인 회원 도메인 계층 및 득점 시스템에 의해 결정 마스터 시계와 동기화 합니다.  도메인에서은 계층 계층 시간 stratums, 각 DC 가리키는 더 정확 하 게 시간 계층와 부모 DC 때문입니다.  PDC 또는 루트 숲 속의 DC 또는 도메인의 좋은 시간 서버에서 GTIMESERV 도메인 플래그 지정, DC 계층을 해결 합니다.  참조는 [는 로컬 신뢰할 수 있는 시간 서비스를 사용 하 여 GTIMESERV 지정](#GTIMESERV) 아래 섹션.

- 기본적으로 time.windows.com 사용 하 여 독립 실행형 시스템 구성 됩니다.  이 이름은 리소스를 소유 Microsoft 가리키는 ISP 하면 해결 됩니다.  모든 원격으로 위치한 시간 참조, 네트워크 중단 같은 동기화를 하지 못할 수도 있습니다.  네트워크 교통 로드 하 고 비대칭 네트워크 경로 시간 동기화 정확성을 줄일 수 있습니다.  1 ms 정확도 대 한 원격 시간 정보에 따라 달라 수 없습니다.

Hyper-v 게스트 두 개 이상의 Windows 시간 공급자에서 선택할 수는 없으므로 호스트 시간 및 NTP를 볼 수 있습니다 도메인 또는 독립 실행형 다르게 동작 게스트로 실행 될 때.

> [!NOTE] 
> 도메인 계층 및 득점 시스템에 대 한 자세한 내용은 참조는 ["시간 서비스 Windows 란?"](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/) 블로그 게시물 합니다.

> [!NOTE]
> 계층 NTP와 Hyper-v 공급자에 사용 되는 개념 이며 값 계층에서 시계 위치를 표시 합니다.  계층 1 최상위 시계, 예약 된 및 계층 0 정확 하 게 것으로 간주 하드웨어에 대 한 예약 되 고 거의 또는와 관련 된 지연 되지 않습니다.  2 계층 등 서버 계층 1, 2 계층을 3 계층에 게 말합니다.  낮은 계층을 더 정확 하 게 시계 나타내기도, 동안 차이 찾을 수는 있습니다.  또한 W32time 계층 15 또는 아래 시간을 허용합니다.  사용 하는 클라이언트 계층을 보려면 *w32tm /query /status*합니다.

## <a name="critical-factors-for-accurate-time"></a>정확한 시간에 대 한 중요 한 요소
정확한 시간에 대 한 모든 경우에는 세 가지 중요 한 요소 다음과 같습니다.

1. **Solid 소스 시계** -안정적 이며 정확 하 게 도메인 요구에 소스 시계 합니다. 이 일반적으로 GPS 디바이스를 설치 하거나 #3 고려 계층 1 소스, 가리키는 의미 합니다. 두 보트 물을 켜고 사용 하는 경우,이 되는 다른에 비해 많음 하나의 측정 하려는 비유 정확도 소스 보트는 매우 안정적이 고 있지 움직이는 하는 경우 가장 좋습니다. 시간에도 마찬가지 및 소스 시계를 안정적인 없는 경우 다음 동기화 된 시계의 전체 체인은 영향을 받는 각 단계에서 확대 합니다. 것도 액세스할 수 있어야 않으므로 시간 동기화 연결에 중단 됩니다. 고 마지막으로, 보안 이어야 합니다. 를 참조가 올바르게 구성 되지에 유지 하거나 악의적인 파티에서 운영 도메인 시간 기반 공격에 노출 될 수 있습니다.
2. **안정적인 클라이언트 시계** -안정적인 클라이언트 시계 발진기의 자연, 바람은 containable 보장 합니다.  NTP 조건 로컬 컴퓨터 시계 분야를 수 있는 여러 NTP 서버에서 여러 샘플을 사용 합니다.  시간 변경 내용 실행 하지 않는 하지만 아니라 느려집니다 또는 NTP 요청 하는 정확 접근 하는 시간을 빠르게 로컬 시계 및 정확 하 게 유지 속도가 합니다.  그러나 클라이언트 컴퓨터 시계 발진기 안정적인 없는 경우 다음 조정 사이 더 많은 변동 발생할 수 있으며 시계 조건를 사용 하 여 Windows 알고리즘 정확 하 게 작동 하지 않습니다.  경우에 따라 정확 하 게 시간에 대 한 펌웨어 업데이트 필요할 수 있습니다.
3. **대칭 NTP 통신** -이 NTP 통신에 대 한 연결이 대칭적인 중요 합니다.  NTP 계산을 사용 하 여 네트워크 패치 대칭적인 가정 하 고 시간을 조정 합니다.  경로 NTP 패킷 하는 경우 이동 하 여 서버에는 반환 하는 다른 시간 하 정확도 영향을 받습니다.  예를 들어, 경로 네트워크 토폴로지 또는 다른 인터페이스 속도 있는 장치를 통해 전달 되 고 패킷 변경으로 인해 변경할 수 있습니다.


배터리 전원이 장치, 모바일 및 노트북을 모두 다른 전략 고려해 야 합니다.  권장 하는 것을 시간이 정확 하 게 유지 필요 합니다 시계를를 한 번에 두 번째, 시계 업데이트 빈도 통제 수 있습니다. 이러한 설정을 예상 보다 절전 모드를 사용할 수 있는 Windows에서 해당 디바이스에 대 한 방해할 수 있는 더 많은 배터리 전원을 사용 합니다. 배터리 전원이 장치는 실행 W32time의 분야 시계 및 시간이 정확 하 게 유지 하는 기능을 방해 하는 모든 응용 프로그램을 중지 하는 특정 전원 모드 수도 있습니다. 또한 모바일 디바이스의 시계 되지 않을 수 있습니다 매우 정확 함으로 시작 합니다.  주변 환경 조건 시계 정확도 영향을 및 모바일 장치 한 주변 조건에서 시간이 정확 하 게 유지 하는 능력을 방해할 수는 다음으로 이동할 수 있습니다.  Microsoft는 뛰어난 설정을 사용 하 여 배터리 전원을 휴대용 장치를 설정 하는 좋지 않습니다. 

## <a name="why-is-time-important"></a>시간 중요 한 이유는?  


## <a name="windows-server-2016-improvements"></a>Windows Server 2016 개선 사항
### <a name="windows-time-service-and-ntp"></a>Windows 시간 서비스 및 NTP
Windows Server 2016 시간을 수정 하 고 로컬 시계 UTC와 동기화 하도록 조건를 사용 하 여 알고리즘을 향상 시켰습니다.  NTP 4 값을 사용 하 여 시간 오프셋 계산 요청/응답 클라이언트 및 서버 요청/응답 타임 스탬프에 따라 합니다.  그러나 네트워크 번거롭고 이며 스파이크 네트워크 혼잡 및 기타 요인 네트워크 지연에 영향을 주는 인해 NTP의 데이터에 있을 수 있습니다.  Windows 2016 알고리즘 평균 안정적이 고 정확 하 게 시간에는 몇 가지 다른 기술 사용 하 여이 노이즈 하는 것입니다.  또한 원본을 사용 정확한 시간 참조 얻기 더 나은 해상도 향상 된 API 합니다.  이러한 향상 된 UTC와 관련 하 여 1 ms 정확도 도메인에서 결과 얻을 수 있습니다.

### <a name="hyper-v"></a>Hyper-v
Windows 2016 Hyper-v TimeSync 서비스를 개선 했습니다. 향상 된 기능 VM 시작 또는 VM 복원 및 샘플 w32time 제공에 대 한 지연 보정 인터럽트 초기 시간을 더 정확 하 게 포함 됩니다.  이 개선 사항을 통해 (루트 의미 제곱 차이 나타내는)는 rms 호스트의에 10µs 유지 50µs 75% 로드 된 컴퓨터 에서도 있습니다.

> [!NOTE]
> 이 문서에 표시 [Hyper-v 아키텍처](https://msdn.microsoft.com/library/cc768520.aspx) 에 대 한 자세한 내용은 합니다.

> [!NOTE]
> 균형된 프로필을 사용 하 여 prime95 벤치 마크를 사용 하 여 로드가 만들었습니다.

또한 계층 수준 호스트 보고 게스트 하는 더욱 투명 하 게 됩니다.  이전에 호스트 정확한에 관계 없이 2 고정된 계층을 표시 됩니다.  Windows Server 2016에 변경 내용으로 호스트 가상 게스트 시간이 더 나은 결과 즉 호스트 계층 보다 큰 하나 계층을 보고 합니다.  원본 시간에 따라 일반적인 방법으로 w32time 호스트 계층 결정 됩니다.  도메인 가입 Windows 2016를 호스트 하는 것이 아니라 가장 정확한 시계 게스트 볼 수 있습니다.  너무나 수동으로 사용 하지 않도록 Windows 2012R2 및 아래 도메인에 가입 컴퓨터에 대 한 설정 Hyper-v 시간 공급자에 게 권고 우리 이런 이유 때문입니다.

### <a name="monitoring"></a>모니터링
모니터 성능 카운터 추가 되었습니다.  모니터링 및 시간 정확도 문제를 해결 초기를 사용 하면 이러한 합니다.  이러한 카운터 다음과 같습니다.

카운터|설명|
----- | ----- |
시간 오프셋 계산|   시스템 클록 선택한 시간 소스 간의 오프셋 밀리초에서 W32Time 서비스에 의해 계산 절대 시간입니다. 새로운 유효한 샘플을 사용할 수 있는 계산된 시간 샘플으로 표시 시간 오프셋으로 업데이트 됩니다. 로컬 시간의 실제 시간 오프셋입니다. W32time 시계 수정이이 오프셋을 사용 하 여 시작 하 고 남은 시간 오프셋 로컬 시계에 적용 되는으로 샘플 사이 계산된 시간을 업데이트 합니다. 이 성능 카운터 낮은 폴링 간격으로 사용 하 여 시간 정확도 추적할 수 있습니다 (예: 256 초 이하로) 카운터 값 원하는 시간 정확도 제한 보다 작은 되도록 구경이 있습니다.|
시계 주파수 조정| 로컬 시스템 클록 W32Time 십억 당 부분에 의해 하려고 절대 시계 주파수 조정 합니다. 이 카운터 시각화 W32time에서 수행 중인 작업 하는 데 도움이 됩니다.|
NTP 왕복 지연|    가장 최근 왕복 지연 NTP 클라이언트가 밀리초에서 서버에서 응답을 받지에 발생 합니다. 이 시간 경과 NTP 클라이언트 NTP 서버에 요청을 송수신 유효한 응답 서버에서 사이 합니다. 이 카운터 NTP 클라이언트가 경험이 지연 규정 하는 데 도움이 됩니다. 결과적 영향을 미칠 수 NTP 통해 시간 동기화 정확도 NTP 시간이 계산을 더 크게 또는 다양 한 왕복 노이즈를 추가할 수 있습니다.|
클라이언트 소스 개수 NTP|    현재 수 NTP 클라이언트에서 사용 되 고 NTP 시간이 소스입니다. 이것은의이 클라이언트의이 요청에 응답 하는 시간 서버 활성 고유한 IP 주소 수 있습니다. 이 번호는 크거나 작게 피어 이름과 현재 reach 기능의 DNS 해상도 따라 구성 된 동료 보다 될 수 있습니다.|
NTP 서버 들어오는 요청|   요청 NTP 서버 (요청 초당)에서 수신 수 있습니다.|
NTP 서버 보내는 응답|  요청 NTP 서버 (응답 초당)에 대 한 대답이 수 있습니다.|

먼저 3 카운터 대상 시나리오 정확도 문제를 해결 합니다.  시간 정확도 문제 해결 및 NTP 섹션 아래에서 [모범 사례](#BestPractices), 자세히 했습니다.
지난 3 카운터 NTP 서버 시나리오 커버와 할 때 도움이 결정 로드 기준 현재 성능 됩니다.

### <a name="configuration-updates-per-environment"></a>환경 당 구성 업데이트
각 역할 Windows 2016 및 이전 버전 간에 기본 설정 변경을 다음 설명 합니다.  Windows 10 1 주년 Update(build 14393) 및 Windows Server 2016에 대 한 설정을 고유한 됩니다 이기 때문에 발생 별도 열으로 표시 됩니다. 

|역할|설정|Windows Server 2016|Windows 10 버전 1607|Windows Server 2012 r 2</br>Windows Server 2008 R2</br>Windows 10|
|---|---|---|---|---|
|**독립 실행형/Nano 서버**||||
| |*시간 서버*|time.windows.com|나|time.windows.com|
| |*폴링 주파수*|64-1024 초|나|한 주에 한 번|
| |*시계 새로 고침 빈도*|한 번 번째|나|한 번 시간|
|**독립 실행형 클라이언트**||||
| |*시간 서버*|나|time.windows.com|time.windows.com|
| |*폴링 주파수*|나|매일 한 번씩|한 주에 한 번|
| |*시계 새로 고침 빈도*|나|매일 한 번씩|한 주에 한 번|
|**도메인 컨트롤러**||||
| |*시간 서버*|PDC/GTIMESERV|나|PDC/GTIMESERV|
| |*폴링 주파수*|64-1024 초|나|1024-32768 초|
| |*시계 새로 고침 빈도*|매일 한 번씩|나|한 주에 한 번|
|**도메인 구성원 서버**||||
| |*시간 서버*|DC|나|DC|
| |*폴링 주파수*|64-1024 초|나|1024-32768 초|
| |*시계 새로 고침 빈도*|한 번 번째|나|5 분 마다|
|**도메인 회원 클라이언트**||||
| |*시간 서버*|나|DC|DC|
| |*폴링 주파수*|나|1204-32768 초|1024-32768 초|
| |*시계 새로 고침 빈도*|나|5 분 마다|5 분 마다|
|**Hyper-v 게스트**||||
| |*시간 서버*|계층 호스트 및 시간 서버에 따라 최상의 옵션을 선택 합니다.|계층 호스트 및 시간 서버에 따라 최상의 옵션을 선택 합니다.|호스트 기본값으로 설정|
| |*폴링 주파수*|위의 역할에 따라|위의 역할에 따라|위의 역할에 따라|
| |*시계 새로 고침 빈도*|위의 역할에 따라|위의 역할에 따라|위의 역할에 따라|

>[!NOTE]
>Hyper-v의 Linux 참조는 [Hyper-v 호스트 시간을 사용할 수 있도록 Linux](#AllowingLinux) 아래 섹션.

### <a name="impact-of-increased-polling-and-clock-update-frequency"></a>영향을 폴링이 및 새로 고침 빈도 시계
시간을 더 정확 하 게 제공 하기 위해 미세 조정 더 자주 수 있도록 하는 주파수와 시계 업데이트 투표에 대 한 기본값 증가 합니다.  이렇게 하면 더 많은 UDP/NTP 교통, 이러한 패킷이 사항은 작은 있어야 거의 하므로 또는 광대역 연결을 통해 영향을 주지 않습니다. 그러나 인가요 혜택을 시간 다양 한 하드웨어 및 환경에 더 나은 있어야 합니다.

배터리 장착 디바이스용 조사 빈도 증가 문제가 발생할 수 있습니다.  배터리 디바이스는 꺼져 있는 동안에 저장 하지 않습니다.  다시 시작 될 때 시계 자주 수정 해야 합니다.  불안정 시계 하면 조사 빈도 향상 시키고 더 많은 전원 사용할 수도 있습니다.  클라이언트 기본 설정을 변경 하지 않는 것이 좋습니다.

도메인 컨트롤러 최소한 곱한 효과 광고 도메인에 있는 NTP 클라이언트의 증가 된 업데이트와 함께 영향 을지 않습니다.  NTP 다른 프로토콜 하 고 한계 영향을 비교 하 여 훨씬 더 작은 리소스 사용량을 있습니다.  사용자은 Windows Server 2016에 대 한 향상 된 설정의 영향 되 고 하기 전에 다른 도메인 기능에 대 한도 도달 가능성이 큽니다.  Active Directory에는 간단한 NTP 보다 정확 시간 동기화, 보안 NTP는 사용 하지만 PDC 떨어진 클라이언트 2 계층을 크기가 조정 확인 했습니다.

신중 요금제로 코어 당 초당 100 NTP 요청 예약 해야 합니다.  예를 들어 4 Dc 4 코어도 구성 된 도메인 있어야 초당 1600 NTP 요청을 처리 하기 위해 합니다.  10 k 클라이언트 동기화 시간 마다 64 초 한 번으로 구성 되어 있고 요청은 시간이 지남에 따라 일관 되 게 받은 64 10, 000/확인할 수 있는 것 또는 정도 160 요청 월 초에 걸쳐 모든 Dc 합니다.  이 쉽게 우리의 1600 NTP 초이 이때에 따라에 포함 됩니다.  이들 추천 계획 신중 되며 물론 있고 네트워크, 프로세서 속도 로드에 큰 종속성 하므로 언제나 처럼 초기 테스트 사용자 환경에서 합니다.

것에 유의 Dc 사용 하 여 상당한 CPU 로드 40% 이상 실행 하는 경우이 거의 확실 노이즈 NTP 응답을 추가 도메인에 시간 정확도 영향을 이기도 합니다.  다시 실제 결과 이해 하 여 환경에서 테스트 해야 할 수도 있습니다.

## <a name="time-accuracy-measurements"></a>시간 정확도 측정
### <a name="methodology"></a>방법
Windows Server 2016 용 시간 정확도 측정 하는 다양 한 도구, 방법 및 환경을 사용 했습니다.  이러한 기술을 하 여 측정 및 귀하의 환경 조정 정확도 결과 요구 사항을 충족 하는 경우 사용할 수 있습니다. 

우리의 도메인 소스 시계 두 정밀 NTP 서버 GPS 하드웨어 구성 되어 있습니다.  저희 측정 준 이기도 하다는 다른 제조업체에서 설치한 정밀 GPS 하드웨어에 대 한 별도 참조 테스트 컴퓨터를 사용 합니다.  테스트의 몇 가지 도메인 시계 소스 외에 참조로 사용 하 여 정확 하 고 신뢰할 수 있는 시계 소스를 해야 합니다.

실제 및 가상 컴퓨터와 정확도 측정 네 가지 방법을 사용 했습니다. 여러 개의 방법을 독립 의미 유효성 검사 결과를 제공 합니다.


1. 참조 테스트 시스템이 별도 GPS 하드웨어에 대해 하는 조건으로 w32tm 부여, 로컬 시계를 측정 합니다.  
2.  측정 NTP에 대 한 핑 NTP 서버에서 W32tm "stripchart"를 사용 하는 클라이언트
3.  클라이언트의 측정 NTP ping W32tm "stripchart"를 사용 하 여 NTP 서버에
4.  측정 Hyper-v 호스트 타임 스탬프 카운터 (TSC)를 사용 하 여 게스트도 때문입니다.  이 카운터 양쪽 파티션에 파티션 및 시스템 시간 간에 공유 됩니다.  가상 컴퓨터에서 호스트 시간과 클라이언트의 차를 계산 했습니다.  다음을 동시에 측정 발생 하지 이후 게스트에서 호스트 시간이 보간합니다 TSC 시계를 사용 합니다.  또한 지연 및 대기 TSV 시계 인수 사용 하 여 api에서 합니다.

W32tm, 기본 제공 이지만 테스트 및 사용 현황에 대 한 오픈 소스를 테스트 하는 동안 사용 하는 도구 GitHub에서 Microsoft 저장소에 사용할 수 있는 것입니다.  WIKI 저장소에 더 많은 정보를 측정 도구를 사용 하는 방법을 설명에 있습니다.

> [https://github.com/Microsoft/Windows-Time-Calibration-Tools](https://github.com/Microsoft/Windows-Time-Calibration-Tools)

아래에 표시 된 테스트 결과 하위 집합 측정 테스트 환경 중 하나가 되었습니다.  시작 시간 계층 및 자녀가 도메인 클라이언트 시간 계층의 끝 부분에 유지 정확도를 보여 줍니다.  비교 2012 기반 토폴로지에서 동일한 디바이스에서 비교 됩니다.

### <a name="topology"></a>토폴로지
비교, Windows Server 2012R2와 Windows Server 2016 기반 토폴로지 테스트 했습니다.  두 토폴로지 설치 된 GPS 시계 하드웨어와 Windows Server 2016 기계 참조는 두 가지 물리적 Hyper-v 호스트 컴퓨터 구성 됩니다.  각 호스트 다음과 같은 토폴로지에 따라 정렬 하는 3 도메인에 가입 windows 게스트 실행 합니다.  줄 시간 계층 및 사용 되는 프로토콜/전송 나타냅니다.

![Windows 시간](media/Windows-2016-Accurate-Time/topology1.png)

![Windows 시간](media/Windows-2016-Accurate-Time/topology2.png)

### <a name="graphical-results-overview"></a>그래픽 결과 개요
다음 두 가지 그래프 두 특정 구성원 위의 토폴로지에 따라 도메인에 대 한 시간 정확도를 나타냅니다.  각 그래프 표시 Windows Server 2012R2 및 2016 결과 중첩를 시각적으로 향상 된 기능을 보여 주는 합니다.  정확도는 호스트에 비해 많음 게스트 컴퓨터에에서 측정 했습니다.  그래픽 데이터 테스트 제공한 전체의 하위 집합 나타내고 최상의 경우 및 최악의 상황 보여 줍니다.  

![Windows 시간](media/Windows-2016-Accurate-Time/topology3.png)

### <a name="performance-of-the-root-domain-pdc"></a>PDC 루트 도메인의 성능
루트 PDC (VMIC 사용 하 여)는 Hyper-v 호스트 정확 하 고 안정적인 것으로 판명이 된 GPS 하드웨어와 Windows Server 2016는 동기화 됩니다.  회색으로 표시 된 영역 녹색으로 표시 되는 1 ms 정확도 대 한 중요 한 요구 사항입니다.

![Windows 시간](media/Windows-2016-Accurate-Time/chart1.png)

### <a name="performance-of-the-child-domain-client"></a>자녀가 도메인 클라이언트의 성능
자녀가 도메인 클라이언트와 통신 루트 PDC 하는 자녀 PDC 도메인에 연결 됩니다.  시간이 이기도 1 내 ms 요구 합니다.

![Windows 시간](media/Windows-2016-Accurate-Time/chart2.png)


### <a name="long-distance-test"></a>시외 테스트
다음 차트는 6 실제 네트워크 홉와 Windows Server 2016에 1 가상 네트워크 홉을 비교합니다.  두 개의 차트 겹치는 데이터를 표시 하도록 투명도로 서로 위에 표시 됩니다.  네트워크 홉 점점 더 이상 지연 시간 및 큰 시간 편차 의미합니다.  확대 하 고 니 차트는 1 녹색 영역으로 표현 ms 범위 큽니다.  시간 1 내에 있는 것을 볼 수 있는 여러 홉 ms 합니다.  것은 부정적인 이동, 네트워크 비대칭을 보여 주는입니다.  물론, 모든 네트워크 다른, 이며 측정 다양 한 환경 요인에 따라 달라 집니다.

![Windows 시간](media/Windows-2016-Accurate-Time/chart3.png)

## <a name="BestPractices"></a>정확한 알아에 대 한 유용한
### <a name="solid-source-clock"></a>Solid 소스 시계
컴퓨터가 시간은와 동기화 소스 시계 우수한만 합니다.  1 달성 하기 위해 ms 정확도 필요 합니다 GPS 하드웨어 또는 시간 기기 마스터 소스 시계도 참조 네트워크에 있습니다.  Time.windows.com 기본을 사용 하 여 수 안정적인 및 로컬 시간 소스를 제공 하지 않습니다.  또한 멀리 떨어진 소스 시계를 받을 때 정확도 네트워크에 적용 됩니다.  마스터 소스 시계 하는 데 각 데이터 센터는 좋은 정확도 필요 합니다.

### <a name="hardware-gps-options"></a>하드웨어 GPS 옵션
정확한 시간을 제공할 수 있는 다양 한 하드웨어 솔루션 가지가 있습니다.  일반적으로 솔루션 오늘 기반으로 GPS 안테나 합니다.  라디오 및 전용된 줄을 사용 하 여 전화 접속 모뎀 솔루션 있습니다.  자녀가 기기, 하거나 사용자 네트워크에 연결 하거나 PCIe 또는 USB 장치를 통해 예를 들어 Windows PC에 연결 합니다.  언제나 귀하의 환경에 따라 달라 결과 다른 옵션 정확도의 여러 수준 제공할 됩니다.  정확도 영향을 주는 변수 GPS 사용 가능 여부, 네트워크의 안정성을 개선 하 고 부하 및 PC 하드웨어가 포함 됩니다.  모든 중요 한 요소는 안정적이 고 정확 하 게 시간에 대 한 요구 사항, 설명한 것 처럼 소스 시계를 선택할 때입니다.

### <a name="domain-and-synchronizing-time"></a>도메인 및 시간이 동기화
도메인 회원 도메인 계층 결정 있는 컴퓨터를 사용 하 여 자녀가 시간을 동기화 원본으로 사용할 합니다.  각 도메인 구성원 시계 원본으로 저장 하 고와 동기화 하는 다른 컴퓨터를 볼 수 있습니다.  각 유형의 도메인 구성원 시간 동기화 시계 소스를 찾기 위해 규칙의 다른 세트를 따릅니다.  PDC 숲 루트에서 모든 도메인에 대 한 기본 시계 소스입니다.  아래에 나열 된 다른 역할 및 높은 수준의 설명 소스를 찾을 방법에 대 한는 다음과 같습니다.


- **PDC 역할로 도메인 컨트롤러** – 컴퓨터가 도메인에 대 한 신뢰할 수 있는 시간 소스 합니다. 도메인에서 사용할 수 있는 가장 정확한 시간을 갖습니다 및 DC 부모 도메인에 있는 경우에서를 제외 하 고 동기화 해야 있는 [GTIMESERV](#GTIMESERV) 역할 사용 하도록 설정 합니다. 
- **다른 도메인 컨트롤러** -이 기계 클라이언트 및 도메인의 회원 서버에 대 한 시간 원본 처럼 작동 합니다. DC 자체 도메인 PDC 또는 모든 DC 부모 도메인에 동기화 할 수 있습니다.
- **클라이언트/구성원 서버** -이 기계 어떤 DC 또는 자체 도메인 또는 DC PDC 또는 PDC 부모 도메인에 동기화 할 수 있습니다.

사용 가능한 후보에 따라, 득점 시스템 최상의 시간 소스를 사용 됩니다.  이 시스템 시간 원본과 상대 위치의 안정성을 고려합니다.  이 시간 서비스를 시작 되 면 후 발생 합니다.  시간 동기화 하는 방법을 미세한 제어 하려는 경우 특정 위치에 좋은 시간 서버를 추가 하거나 중복 추가 수 있습니다.  참조는 [는 로컬 신뢰할 수 있는 시간 서비스를 사용 하 여 GTIMESERV 지정](#GTIMESERV) 섹션에 대 한 자세한 내용은 합니다.

#### <a name="mixed-os-environments-win2012r2-and-win2008r2"></a>혼합된 OS 환경을 (Win2012R2 및 Win2008R2)
순수한 Windows Server 2016 도메인 환경에 대 한 최상의 정확도 필요 이지만, 이점이 여전히 혼합된 환경에서 합니다.  Windows Server 2016 Hyper-v Windows 2012 도메인에 배포만 경우 게스트는 또한 Windows Server 2016 하지만 위에 언급 개선 사항으로 인해 게스트 도움이 됩니다.  Windows Server 2016 PDC 수 더 안정적인 소스는 것이 향상 된 알고리즘 때문 시간을 더 정확 하 게 제공 됩니다.  PDC 교체으로 되지 옵션, Windows Server 2016 DC 대신 추가할 수 있습니다의 [GTIMESERV](#GTIMESERV) 앨범 설정 도메인에 대 한 정확도에서 업그레이드 하는 것입니다.  그러나 Windows Server 2016 DC 다운스트림 시간 클라이언트 더 나은 시간을 제공할 수, 소스 NTP 시간 우수한만입니다.

위에서 언급 한 것 처럼도 시계 폴링 및 새로 고침 빈도와 Windows Server 2016 수정 되었습니다.  이러한 변경 수동으로 하위 수준 dc 또는 수 그룹 정책을 통해 적용 됩니다.  이 구성 테스트 되지 않았습니다를 동안 Win2008R2 및 Win2012R2 제대로 작동 하 고 몇 가지 이점을 제공 해야 있습니다.

Windows Server 2016 시간을 정확 하 게 유지 조정 만든 후에 바로 시스템 시간 흩날리는 중단 하는 여러 문제가 전이라 버전입니다.  이 인해 시간 샘플 정확 하 게 NTP 소스에서 자주 얻고 데이터와 로컬 시계 동의할로 연결 시계 시스템에서에서 더 작은, 바람 하위 수준 OS 버전을 유지 하는 더 나은 시간에 발생 하는 방법은 샘플링 기간에 됩니다. Windows Server 2012R2 NTP 클라이언트의 경우 높은 정확도 설정으로 구성 동기화 정확한 Windows 2016 NTP 서버에서 시간 가장 관찰된 정확도 5ms 약 했습니다.

Guest 도메인 컨트롤러 관련 된 일부 시나리오에서 Hyper-v TimeSync 샘플 도메인 시간 동기화 중단 될 수 있습니다.  이 Server 2016 게스트 서버 2016 Hyper-v 호스트에서 실행 되는 문제가 더 이상 이어야 합니다.

샘플 w32time 제공 하는 Hyper-v TimeSync 서비스를 사용 하지 않으려면 다음 게스트 레지스트리 키를 설정 합니다.

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\VMICTimeProvider 
    "Enabled"=dword:00000000

#### <a name="AllowingLinux"></a>Hyper-v 호스트 시간을 사용 하 여 Linux 허용
Hyper-v 실행 Linux 게스트에 대 한 클라이언트 NTP 데몬 NTP 서버에 대 한 동기화를 사용 하 여 일반적으로 구성 됩니다.  Linux 배포 TimeSync 버전 4 프로토콜을 지원 Linux 게스트 TimeSync 통합 서비스가 활성화 된 경우 호스트 시간에 대 한 동기화 됩니다. 일치 하지 않는 시간 두 가지 방법 활성화 되 면 유지 될 수 있습니다.

호스트 시간 비교 단독으로 동기화 할 것이 좋습니다 NTP 시간 동기화를 사용 하지 않도록 설정 하거나:

- 모든 NTP 서버 ntp.conf 파일에 사용 하지 않도록 설정
- 또는 NTP 데몬 사용 안 함

이 구성 시간 서버가이 호스트입니다.  해당 투표 주파수 5 초 고 시계 업데이트 빈도 5 초도 있습니다.

NTP을 통해만 동기화 하도록 게스트에서 TimeSync 통합 서비스를 비활성화 하는 것이 좋습니다.

> [!NOTE]
> 참고: Linux 게스트 정확 하 게 시간에 대 한 지원이 업스트림 최신 Linux 커널에서 지원 되는 기능 차지 하며 무언가 광범위 하 게에서 사용할 수 있는 모든 Linux distros 아직 없는 합니다. 참조 하세요 [windows Hyper-v에 대 한 지원 Linux 및 FreeBSD 가상 컴퓨터](https://technet.microsoft.com/en-us/windows-server-docs/virtualization/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows) 지원 배포에 대 한 자세한 내용은 합니다.

#### <a name="GTIMESERV"></a>로컬 신뢰할 수 있는 시간 GTIMESERV를 사용 하 여 서비스를 지정
하나 이상의 도메인 컨트롤러 정확 하 게 소스 시계로 지정할 수 좋은 시간 서버 GTIMESERV를 사용 하 여 플래그.  예를 들어 GPS 하드웨어가 장착 특정 도메인 컨트롤러를 GTIMESERV로 플래그 지정 수 있습니다.  이 도메인 참조 GPS 하드웨어에 따라 시계 하도록 합니다.

> [!NOTE]
> 도메인 플래그에 대 한 자세한 내용은에서 찾을 수 있습니다의 [MS ADTS 프로토콜 설명서](https://msdn.microsoft.com/library/mt226583.aspx)합니다.

TIMESERV는 또 다른 관련 도메인 서비스 나타내는 시스템을 현재 신뢰할 수 있는지 여부는 플래그 DC 연결이 끊어진 경우 변경할 수 있습니다.  이 상태에서 DC "알 수 없는 계층" NTP 통해 시 반환 됩니다.  여러 번 후, DC 시스템 이벤트 시간 서비스 이벤트 36 기록 합니다.

DC 한 GTIMESERV 구성 하려면이 구성할 수 있습니다 다음 명령을 사용 하 여 수동으로 합니다.  이 경우 DC 마스터 형식으로 다른 컴퓨터를 사용 하는 합니다.  기기 또는 전용된 기계 수 있습니다.

    w32tm /config /manualpeerlist:”master_clock1,0x8 master_clock2,0x8” /syncfromflags:manual /reliable:yes /update

> [!NOTE]
> 자세한 내용은 참조 [Windows 시간 서비스](https://technet.microsoft.com/library/cc731191.aspx)

DC GPS 하드웨어가 설치 되어 있으면 NTP 클라이언트를 사용 하지 않도록 설정 하 고 NTP 서버를 사용 하도록 설정 하려면 다음이 단계를 사용 해야 합니다.

NTP 클라이언트를 사용 하지 않도록 설정 하 여 시작 하 고이 레지스트리 주요 변경 내용은 사용 하 여 NTP 서버를 사용 하도록 설정 합니다.

    reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpClient /v Enabled /t REG_DWORD /d 0 /f

    reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpServer /v Enabled /t REG_DWORD /d 1 /f

그런 다음 Windows 시간 서비스 다시 시작

    net stop w32time && net start w32time

마지막으로,이 컴퓨터에 사용 하 여 신뢰할 수 있는 시간 소스를 나타냅니다.
   
    w32tm /config /reliable:yes /update

변경 내용을 올바르게 완료 되지를 확인 하려면 아래에 표시 된 결과 다음 명령의 실행할 수 있습니다. 

    w32tm /query /configuration

값|설정 필요 합니다.|
----- | ----- |
AnnounceFlags|  5 (로컬)|
NtpServer   |(로컬)|
DllName |C:\WINDOWS\SYSTEM32\w32time 합니다. DLL (로컬)|
사용 하도록 설정 |1 (로컬)|
NtpClient|  (로컬)|

    w32tm /query /status /verbose

값|  설정 필요 합니다.|
----- | ----- |
계층|    1 (기본 참조-라디오 클록으로)|
ReferenceId|    0x4C4F434C (원본 이름: "로컬")|
원본| 로컬 시계|
단계 오프셋|   0.0000000s|
서버 역할|    576 (신뢰할 수 있는 시간 서비스)|

#### <a name="windows-server-2016-on-3rd-party-virtual-platforms"></a>Windows Server 2016 3 파티 가상 플랫폼에서
Windows 가상화가 기본적으로 하이퍼바이저가 시간을 제공 해야 합니다.  하지만 도메인 가입 회원 하기만 하면 도메인 컨트롤러 Active Directory 제대로 작동 하도록 하기 위해에서와 동기화 합니다.  모든 시간 virtualization 게스트 사이의 호스트 된 타사 가상 플랫폼을 사용 하지 않도록 설정 하는 것이 좋습니다.

#### <a name="discovering-the-hierarchy"></a>계층 검색
도메인에 동적 및 하기로 마스터 시계 소스 시간 계층 체인 이므로 시간 원본 및 체인 마스터 출처 시간을 파악 하는 특정 디바이스의 상태 쿼리 해야 합니다.  시간 동기화 문제를 진단 하는 데 도움이 됩니다.

하면 제공 되는 문제를 해결 하려면 특정 클라이언트; 이 w32tm 명령을 사용 하 여 시간 원본을 이해 하는 첫 번째 단계가입니다.

    w32tm /query /status

무엇 보다도 소스에 결과가 표시 됩니다.  소스 시간 도메인에 동기화 할을 나타냅니다.  이 컴퓨터 시간 계층의 첫 번째 단계입니다.
다음 위쪽에서 소스 항목을 사용 하 고 /StripChart 매개 체인에서 다음 시간 소스를 사용 합니다.

    w32tm /stripchart /computer:MySourceEntry /packetinfo /samples:1

도 유용 다음 명령이 지정된 된 도메인의 찾을 수 있는 도메인 컨트롤러 각 목록과 각 파트너 확인할 수 있는 결과 인쇄 합니다.  이 명령을 수동으로 구성 된 컴퓨터 포함 됩니다.
    
    w32tm /monitor /domain:my_domain

목록을 사용 하는 도메인 통해 결과 추적 수 있으며 계층 각 단계에서 시간 오프셋을 이해 수도 있습니다.  시간 오프셋 가져옵니다 크게 상태가 더 나 빠지면 포인트를 찾아 잘못 된 시간 루트를 파악할 수 있습니다.  여기에서 이유 당시 올바르지 켜서 파악 하려고 수 [w32tm 로깅](#W32Logging)합니다. 

#### <a name="using-group-policy"></a>그룹 정책을 사용 하 여
사용할 수 있습니다 그룹 정책가 엄격한 정확성을 수행 하 예를 들어 할당 클라이언트를 사용 하 여 특정 NTP 서버 가상화 때 제어 하위 수준 운영 체제의 구성 됩니다.  
다음은 가능한 시나리오 및 관련 그룹 정책 설정의 목록이입니다.

**도메인 가상화** -Hyper-v 호스트가 레지스트리 항목이 해제할 수 있습니다 하는 것이 아니라 시간 해당 도메인와 동기화 하 않도록 가상화 도메인 컨트롤러에서 Windows 2012R2 제어 하기 위해 합니다.   Pdc, Hyper-v 호스트 가장 안정적인 시간 소스를 제공할 예정으로 항목을 해제 하려는 하지 않습니다.  레지스트리 항목이 활성화 된 변경 될 때 w32time 서비스를 다시 시작 하면 필요 합니다.

    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\VMICTimeProvider]
    "Enabled"=dword:00000000

**정확도 중요 한 로드** -시간 정확도 중요 한 작업에 대 한 그룹 NTP 서버 설정 하는 컴퓨터의 구성할 수 있습니다 및 시간 설정이 폴링과 시계 업데이트 빈도 같은 관련 된 합니다.  이 일반적으로 처리 도메인에 있지만 더 많은 제어 마스터 시계 직접 가리키도록 하려면 특정 시스템 대상 될 수 있습니다.

그룹 정책 설정|   새 값|
----- | ----- |
NtpServer|  ClockMasterName 0x8|
MinPollInterval|    6 – 64 초|
MaxPollInterval|    6|
UpdateInterval| 한 번 초당 100 –|
EventLogFlags|  3-모든 특별 한 시간 로그인|

> [!NOTE]
> Windows 구성 NTP 클라이언트 설정을 사용 하 여 System\Widows 시간 Service\Time 공급자에서 NtpServer 및 EventLogFlags 설정이 있습니다.  글로벌 구성 설정을 사용 하 여 System\Windows 시간 서비스에서 다른 3이 있습니다.

**원격 정확도 중요 한 로드 원격** 소매 인스턴스 및 결제 신용 산업 (PCI)에 대 한 분기 도메인에 있는 시스템용 Windows 현재 사이트 정보를 사용 및 수동 NTP 아닌 경우 로컬 DC 찾으려면 DC Locator 시간 구성 소스입니다.  이 환경을 빠른 수렴 올바른 시간에 사용 하 여 정확성 1 초 필요 합니다.  이 옵션을 사용 하면 w32time 서비스를 시계 뒤로 이동 합니다.  허용 되는이 요구 사항을 충족 하는 경우는 다음과 같은 정책을 만들 수 있습니다.   모든 환경와 마찬가지로 하면를 테스트 하 고 초기 네트워크. 

그룹 정책 설정|   새 값|
----- | ----- |
MaxAllowedPhaseOffset|  1, 경우 이상 초 설정 시계 올바른 시간에 합니다.|

글로벌 구성 설정을 사용 하 여 System\Windows 시간 서비스 MaxAllowedPhaseOffset 설정이 있습니다.

> [!NOTE]
> 그룹 정책 및 관련된 항목에 대 한 자세한 내용은 참조 [Windows 시간이 서비스 도구](windows-time-service-tools-and-settings.md) technet 설정 문서 및 합니다.

#### <a name="azure-and-windows-iaas-considerations"></a>Azure 및 Windows IaaS 고려 사항

##### <a name="azure-virtual-machine-active-directory-domain-services"></a>Azure 가상 컴퓨터: Active Directory 도메인 서비스
Azure VM 실행 Active Directory 도메인 서비스 기존 온-프레미스의 일부인 경우 다음 TimeSync(VMIC), Active Directory 숲 않도록 합니다. 단 한 번 동기화 계층을 사용 하 여 실제 및 가상, 숲 속의 모든 Dc 수 있도록입니다. 가장 좋은 방법은 백서 참조 ["실행 도메인 컨트롤러에서 Hyper-v"](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx)

##### <a name="azure-virtual-machine-domain-joined-machine"></a>도메인 가입 기계 azure 가상 컴퓨터:
도메인 가입 기존 Active Directory 숲 된 컴퓨터를 호스팅할 경우 가상 하거나, 물리적 것이 좋습니다 TimeSync에을 사용 하도록 게스트 W32Time 형식에 대 한 시간 구성 통해 도메인 컨트롤러의와 동기화 하도록 구성 되어 있는지 확인 NTP5 =

##### <a name="azure-virtual-machine-standalone-workgroup-machine"></a>Azure 가상 컴퓨터: 독립 실행형 작업 그룹 기계
Azure VM가 도메인에 가입 하지 않으며는 도메인 컨트롤러를 하는 경우 기본 시간 구성 vm이 호스트와 동기화 하는 것이 좋습니다.

### <a name="windows-application-requiring-accurate-time"></a>Windows 응용 프로그램을 요구 정확 하 게 시간
#### <a name="time-stamp-api"></a>타임 스탬프 API
가장 큰 정확도 UTC 및 시간 경과 하지 되는 프로그램을 사용할지는 [GetSystemTimePreciseAsFileTime API](https://msdn.microsoft.com/library/windows/desktop/Hh706895.aspx)합니다.  응용 프로그램 되는 조건 Windows 시간 서비스에 의해 부여 시스템 시간을 볼 수 있습니다.

#### <a name="udp-performance"></a>UDP 성능
포트 엔진 필터링 기본 응용 프로그램 사용 하 여 UDP 통신 거래 있으며의 대기 최소화 하는 것이 중요에 대 한 가지 일부 관련 레지스트리 항목이 포트에서 제외 될 범위가 구성 하는 데 사용할 수 있는 경우 합니다.  이 개선 모두 대기 시간이 되며 사용자의 처리 속도 향상 합니다.  그러나 레지스트리를 변경 경험이 관리자에 게 제한 해야 합니다.  또한,이 문제 해결 포트가 방화벽으로 보호 되 고에서 제외 됩니다.  자세한 내용은 아래 문서 참조를 참조 하십시오.

Windows Server 2008 및 Windows Server 2012에 대 한 먼저 핫픽스 설치 해야 합니다.  이 기술 자료 문서를 참조할 수 있습니다: [데이터 그램 손실 Windows 8 및 Windows Server 2012에서 멀티 캐스트 수신기 응용 프로그램을 실행 하는 경우](https://support.microsoft.com/en-us/kb/2808584)

#### <a name="update-network-drivers"></a>네트워크 드라이버 업데이트
일부 네트워크 공급 드라이버 대기 시간이 및 UDP 패킷을 버퍼링 성능을 향상 하는 드라이버 업데이트를 설치 합니다.  업데이트 UDP 처리량에 도움이 되는 경우 해당 네트워크 공급 업체에 문의 하세요.

### <a name="logging-for-auditing-purposes"></a>감사 용도로 로그인
수동으로 시간이 추적 규정을 준수 하기 w32tm 로그, 이벤트 로그 및 성능 모니터 정보 보관할 수 있습니다.  나중에 보관 된 정보를 이전에 특정 시간에 준수 증명 사용할 수 있습니다.  다음과 같은 요인 정확도 나타내는 데 사용 됩니다.


1. 시계 정확도 성능 모니터 시간 오프셋 계산 카운터 사용 합니다.  원하는 정확도 효과 표시합니다.
2.  시계 소스 "피어 응답" w32tm 로그에서에 보고 합니다.   IP 주소 또는 VMIC 시간 원본와 참조 시계의 체인에 다음의 유효성을 검사을 설명 하는 메시지 텍스트를 수행 합니다.
3.  W32tm 로그를 사용 하 여 유효성을 검사 하는 조건 상태 시계 "ClockDispl 분야: \*SKEW\*TIME\*"가 발생 합니다.  이 시간에 해당 w32tm 활성화 되어 나타냅니다.

#### <a name="event-logging"></a>이벤트 로깅에서
전체 이야기를 가져오려면도 이벤트 로그 정보가 필요 합니다.  시스템 이벤트 로그를 수집 하 고 시간-서버에 필터링, Windows 커널 부팅 Microsoft, Microsoft-Windows-커널-일반을 수 있습니다 변경 된 경우 예를 들어, 제 3 자 기타 영향 있는지 여부를 검색할 수 있습니다.  이러한 로그 외부 방해 하지 않도록 해야 할 수 있습니다.  그룹 정책 어떤 이벤트 로그 로그에 기록는 영향을 줄 수 있습니다.  그룹 정책을 사용 하 여에 대 한 자세한 내용은 위의 섹션을 참조 합니다.

#### <a name="W32Logging"></a>W32time 로깅 디버그
감사 용도로 w32tm을 사용 하려면 다음 명령을 시계 정기적으로 업데이트를 표시 하 고 원본 시계 나타냅니다는 로깅을 사용 합니다.  새 로깅을 서비스를 다시 시작 합니다.  

자세한 내용은 참조 [설정 디버그 Windows 시간 서비스에 로그인 하는 방법을](https://support.microsoft.com/en-us/kb/816043)합니다.

    w32tm /debug /enable /file:C:\Windows\Temp\w32time-test.log /size:10000000 /entries:0-73,103,107,110

#### <a name="performance-monitor"></a>성능 모니터
Windows Server 2016 Windows 시간 서비스 감사 로그를 수집 하는 데 사용할 수 있는 성능 카운터에서 제공 됩니다.  로컬에서 또는 원격 기록 될 수 있습니다.  컴퓨터 시간 오프셋 및 왕복 지연 카운터 기록할 수 있습니다.  
와 같은 성능 카운터 모든 원격으로 모니터링 하 고 알림을 System Center Operations Manager 사용 하 여 만들 수 있습니다.  예를 들어 알림을에서 원하는 정확도 이동 시간 오프셋 때 알람 사용자를 사용할 수 있습니다.  [System Center 팩 관리](https://social.technet.microsoft.com/wiki/contents/articles/15251.system-center-management-pack-authoring-guide.aspx) 자세한 정보가 포함 됩니다.

#### <a name="windows-traceability-example"></a>Windows 추적 기능 예제
W32tm 로그 파일에서 하려는 두 가지 정보를 확인 합니다.  첫 번째는 로그 파일은 현재 상태 시계를 나타냅니다.  이것 분쟁이 있는 시간에 시계, Windows 시간 서비스 조건부 되 고 된 것입니다.

    151802 20:18:32.9821765s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:223 CR:156250 UI:100 phcT:65 KPhO:14307
    151802 20:18:33.9898460s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:1 CR:156250 UI:100 phcT:64 KPhO:41
    151802 20:18:44.1090410s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:1 CR:156250 UI:100 phcT:65 KPhO:38

요점은은 메시지는 증명 w32time ClockDispln 분야 접두사가 시스템 클록 상호 작용 보게 됩니다.
 
다음 참조 시계도 현재 사용 중인 소스는 컴퓨터를 보고 하는 분쟁이 있는 시간 전에 로그에서 마지막 보고서를 확인 해야 합니다.  IP 주소, 컴퓨터 이름 또는 Hyper-v 호스트 된와 동기화 하는 VMIC 공급자 수 있습니다.  이때는 10.197.216.105 IPv4 주소를 제공합니다.

    151802 20:18:54.6531515s - Response from peer 10.197.216.105,0x8 (ntp.m|0x8|0.0.0.0:123->10.197.216.105:123), ofs: +00.0012218s

이제 참조 시간 체인의 첫 번째 시스템 유효성을 검사 한 해야 한다는 참조 시간 소스 로그 파일 조사 하 고 동일한 단계를 반복 합니다.  GPS 또는 NIST 같은 알려진된 시간 소스 같은 물리적 시계에 도달할 때까지 계속 합니다.  참조 시계 GPS 하드웨어 경우, 다음의 제조에서 로그도 필요할 수 있습니다.

### <a name="network-considerations"></a>네트워크 고려 사항
NTP 프로토콜 알고리즘 네트워크 대칭에 종속이 되어 있습니다.  증가 네트워크 홉 다양 가능성 비대칭 증가합니다.  여기, 어렵습니다 것을 예측 어떤 유형의 정확도 특정 사용자 환경에 표시 됩니다. 

모니터 성능 및 Windows Server 2016의 새로운 Windows 표준 카운터 환경 정확도 평가 하 고 초기 만들기를 사용할 수 있습니다. 네트워크에서 컴퓨터의 현재 오프셋 문제 해결을 수행할 수 있습니다.

네트워크를 통해 정확한 시간에 대 한 일반 표준 두 가지입니다.  PTP ([정밀 시간 프로토콜 IEEE 1588](https://www.nist.gov/el/intelligent-systems-division-73500/introduction-ieee-1588)) 네트워크 인프라에는 보다 엄격한 요구 사항이 있지만 하위 마이크로초 정확성을 제공할 수 있습니다.  NTP ([네트워크 시간 프로토콜 RFC 1305](https://tools.ietf.org/html/rfc1305)) 큰 다양 한 네트워크 및 환경을 쉽게 관리 하는에서 작동 합니다. 

Windows 간단한 NTP (RFC2030) 비 도메인 결합된 컴퓨터에 대 한 기본적으로 지원합니다.  라는 보안 NTP 사용 하 여 컴퓨터에 참여 하는 도메인에 대 한 [MS SNTP](https://msdn.microsoft.com/en-us/library/cc246877.aspx), 관리 장점은 RFC1305 및 RFC5905에 설명 된 인증 NTP를 통해 제공 되는 도메인 협상 암호를 활용 하는 합니다.   

도메인 및 비 도메인 결합된 프로토콜 UDP 포트 123 필요 합니다.  NTP 모범 사례에 대 한 자세한 내용은 참조 [네트워크 시간이 프로토콜 최상의 현재 관행 IETF 초안](https://tools.ietf.org/html/draft-ietf-ntp-bcp-00)합니다.

### <a name="reliable-hardware-clock-rtc"></a>신뢰할 수 있는 하드웨어 시계 (RTC)
Windows 시계 보다 다양 한 특정 범위를 초과 되 면 제외 단계 시간을 하지 않습니다.  즉, w32tm 시계 주파수를 한 번으로 Windows Server 2016 두 번째는 기본값 설정 시계 업데이트 주파수를 사용 하 여 정기적으로 조정 합니다.  주파수를 가속 시계 뒤 경우 하 고 앞이 떨어집니다 빈도 합니다.  그러나, 시계 주파수 조정 사이의 시간 동안 하드웨어 시계에서 제어 됩니다.  펌웨어 또는 하드웨어 시계 문제가 발생 하는 경우는 컴퓨터의 시간을 더 정확 하 게 될 수 있습니다.

테스트 해야 하는 이유 및 초기 사용자 환경에서입니다.  "시간 오프셋 계산" 성능 카운터 대상으로 하는 정확도에 안정화 하지 않는 경우 펌웨어 최신 상태 인지 확인 하려는 수 있습니다.  다른 테스트로 중복 하드웨어 같은 문제를 재현 하는 경우를 볼 수 있습니다.

### <a name="troubleshooting-time-accuracy-and-ntp"></a>NTP 및 시간 정확도 문제 해결
Discovering에서 사용할 수 부정확 한 번의 소스 이해 위의 계층 섹션.  지점을 계층 시간 NTP 소스에서 가장 모델과 어디에서 찾을 시간 오프셋에서 찾습니다.  계층을 이해 하 고 나면 해당 특정 시간 소스 정확한 시간을 수신 하지 않은 이유를 이해 하도록 합니다.  

서로 시간을 사용 하 여 시스템에 초점을 문제를 결정할 수 있도록 하 고 해결 방법을 찾으려면 자세한 정보를 수집 아래 이러한 도구를 사용할 수 있습니다.  아래의 UpstreamClockSource 참조 "w32tm 입력 /status"를 사용 하 여 검색 하 고 시계입니다.


- 시스템 이벤트 로그
- 사용 로깅 사용 하 여: w32tm 로그-w32tm /debug 같습니다 /file:C:\Windows\Temp\w32time-test.log /size:10000000 /entries:0-300
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time w32Time 레지스트리 키
- 로컬 네트워크 추적
- (출처: 로컬 컴퓨터 또는 UpstreamClockSource) 성능 카운터
- W32tm /stripchart /computer:UpstreamClockSource
- 대기 시간 및 소스 홉의 수를 이해 하 PING UpstreamClockSource
- Tracert UpstreamClockSource

문제|    증상이|   해결 방법|
----- | ----- | ----- |
로컬 TSC 시계 안정적인 하지 않습니다.| 하는 몇 가지 100us의 1 ~ 2 분 마다 표시 되지만 사용자도-물리적 컴퓨터 성능 동기화 시계 안정적인 시계, 사용 하 여 합니다. |   펌웨어를 업데이트 하거나 유효성을 다시 다른 하드웨어가 같은 문제가 표시 되지 않습니다.|
네트워크 대기|    w32tm stripchart 10 ms 이상 RoundTripDelay 표시 됩니다.  한 방향에만 있는 지연 예를 들어 왕복 시간을 지연 원인 노이즈 ½ 만큼 큰의 변동 합니다.</br></br>PING에 표시 된 UpstreamClockSource 여러 홉입니다.  TTL은 128에 있어야 합니다.</br></br>Tracert를 사용 하 여 각 홉 대기 시간이 찾을 수 있습니다.    | 시간에 대 한 자세히 시계 소스 찾기.  한 가지 방법은 같은 세그먼트에 소스 시계를 설치 하거나 지리적 가까이 있는 소스 시계 수동으로 가리킵니다.  도메인 시나리오에 대 한 GTimeServ 역할 컴퓨터를 추가 합니다. |  
NTP 소스 안정적으로 연결할 수 없습니다.|    W32tm /stripchart "요청 초과" 가끔 반환    |응답 하지 NTP 소스|
응답 하지 NTP 소스|    성능 카운터 NTP 클라이언트 소스 수 NTP 서버 들어오는 요청 NTP 서버 보내는 응답를 사용량에 베이스와 비교 하 여 확인 합니다.|    성능 카운터 서버를 사용 하 여 로드 대 여 초기 말합니다 변경 된 경우 결정 합니다.</br></br>사항이 네트워크 정체도 문제가 있나요?|
가장 정확한 시계를 사용 하지 도메인 컨트롤러|    토폴로지 또는 최근에 추가한 마스터 시간 시계의 변경 됩니다.|   w32tm /resync /rediscover|
클라이언트 시계 흩날리는| 시간 서비스 이벤트 36 시스템 이벤트 로그 및/또는 텍스트를 설명 하는 로그 파일에: "NTP 클라이언트 시간 소스 개수" 카운터 1에서 0로 이동|업스트림 소스 문제를 해결 한 성능 문제를 실행 되 고 있는지를 파악 합니다.|

### <a name="baselining-time"></a>기준 시간
먼저 성능과 정확도 네트워크를 이해 하 고 문제가 발생 하는 경우 나중에 기본와 비교할 수 있도록 기준이 중요 합니다.  해야 초기 루트 PDC 또는 GTIMESRV로 모든 디바이스 표시 됩니다.  이 것도 좋습니다 하면 PDC 모든 숲 속의 초기를 합니다.  모든 중요 한 Dc 또는 거리 또는 높은 로드 및 초기 같은 특징이 흥미로운 컴퓨터 선택 마지막으로 해당 합니다.

Windows Server 2012R2 성능 카운터 없는 이후 비교 하는 데 사용할 수 있는 도구도 w32tm /stripchart만 되어 있지만 기본 Windows Server 2016 vs 2012 r 2에도 유용 합니다.  두 개의 컴퓨터와 같은 특성을 선택 하거나 컴퓨터를 업그레이드 하 고 결과 업데이트 후 비교 해야 합니다.  Windows 시간 측정 addendum 2016 2012 사이의 측정 하는 방법에 대 한 자세한 내용은 있습니다.

모든 w32time 성능 카운터를 사용 하 여 최소한 한 주에 대 한 데이터를 수집 합니다.  이것은 시간이 지남에 따라 네트워크에서 다양 한에 계정에 대 한 참조 질리지 및 시간 정확도 안정적이 전반의 실행 질리지가 하도록 합니다.

### <a name="ntp-server-redundancy"></a>서버 중복 NTP
PDC 또는 도메인 비 결합된 컴퓨터와 함께 사용할 수동 NTP 서버 구성에 대 한 개 이상의 서버 하는 데 사용 가능한 경우 좋은 중복 측정입니다.  가정 모든 소스는 정확 하 고 안정화 하 고 정확성을 지정할 수도 될 수 있습니다.  그러나 토폴로지가 잘 설계 되지 않거나 시간 소스는 안정적, 결과 정확도 될 수 상태가 더 나 빠지면 되므로 주의 해야 합니다.  서버 w32time 수동으로 참조할 수 지원 되는 시간을 제한 10 됩니다. 

## <a name="leap-seconds"></a>Leap 초
지구의 회전 기간 climatic 및 지리 이벤트로 인해 발생할 시간이 지남에 따라 달라 집니다. 일반적으로 변형 2 년 마다 초에 대 한입니다. 자동 시간에서 편차 너무 크게 증가 하는 경우 때마다 1 초 (위나 아래로)의 수정 삽입는, 윤 번째 이라고 합니다. 이러한 차이점을 벗어날 0.9 초 하는 방식으로 수행 됩니다. 이 수정 실제 보정 미리 6 개월 동안 발표입니다. Windows Server 2016 하기 전에 Microsoft 시간 서비스 leap 초 인식 하지 못했던 하지만이 처리 하도록 외부 시간 서비스에 의존 합니다. Microsoft은 Windows Server 2016 증가 시간 정확도 leap 초 문제에 대 한 더 적합 한 솔루션에서 작동 합니다.

## <a name="secure-time-seeding"></a>보안 시간 홀씨
Server 2016에 W32time 시간 홀씨 보호 기능이 포함 되어 있습니다. 이 기능은 발신 SSL 연결에서 대략적인 현재 시간을 결정합니다.  로컬 시스템 클록 모니터링 총 오류를 수정 하는 시간 값이 사용 됩니다. 자세한 내용은 기능에 대 한 [이 블로그 게시물](https://blogs.msdn.microsoft.com/w32time/2016/09/28/secure-time-seeding-improving-time-keeping-in-windows/)합니다.  신뢰할 수 있는 시간 원본와 잘 모니터링된 컴퓨터를 모니터링 하 고 시간 오프셋 포함 배포에서 시간 홀씨 보안 기능을 사용 하 고 기존 인프라 의존 하지 하도록 선택할 수 있습니다. 

다음이 단계를 사용 하는 기능을 해제할 수 있습니다.

1.  특정 컴퓨터에 0을 UtilizeSSLTimeData 레지스트리 구성 값을 설정 합니다.

    레지스트리는 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\Config /v UtilizeSslTimeData /t REG_DWORD /d 0 /f 추가


2.  몇 가지 이유로 인해 즉시 컴퓨터를 다시 부팅 수 없는 경우 W32time 서비스에 대 한 구성 업데이트가 알릴 수 있습니다. 이 시간 모니터링 멈추고 SSL 연결에서 수집 된 데이터 시간에 따라 적용 됩니다. 

    입력 하 여 유형을 W32tm.exe

3.  컴퓨터를 다시 부팅 설정을 적용 즉시 고 SSL 연결에서 든 지 데이터 수집을 중지 하면도 합니다.  뒷부분 소규모 헤드가 및 성능 문제가 해서는 안 됩니다.

4.  전체 도메인에서이 설정을 적용 하려면 0 W32time 그룹 정책 설정에 UtilizeSSLTimeData 값 설정 하 고 설정을 게시 하세요.  그룹 정책 클라이언트가 설정을 선택는, 서비스 W32time 알리고 시간 모니터링 및 집행 SSL 시간 데이터를 사용 하 여 중지 됩니다. 각 컴퓨터를 다시 부팅 될 때 SSL 시간 데이터 수집이 중지 됩니다. 도메인에 휴대용 슬림 노트북/태블릿 및 다른 디바이스를이 정책 변경에서 이러한 디바이스를 제외 하 않도록 할 수 있습니다. 이러한 디바이스는 배터리 소모 얼굴 결국 및 시간 부트스트랩할 기능 시간 보안 홀씨 필요 합니다.














 













 




