---
title: Windows Server 2016 개선 사항
description: Windows Server 2016 시간을 수정 하 고 UTC와 동기화 할 로컬 시계 상태를 사용 하 여 알고리즘을 향상 시켰습니다.
author: dcuomo
ms.author: dacuo
manager: dougkim
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 34d05a8058db366714c0ff4fed0b7d80b9150aa4
ms.sourcegitcommit: e2b565ce85a97c0c51f6dfe7041f875a265b35dd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69626365"
---
## <a name="windows-server-2016-improvements"></a>Windows Server 2016 향상 된 기능

### <a name="windows-time-service-and-ntp"></a>Windows 시간 서비스 및 NTP
Windows Server 2016 시간을 수정 하 고 UTC와 동기화 할 로컬 시계 상태를 사용 하 여 알고리즘을 향상 시켰습니다.  NTP 4 개의 값을 사용 하 여 시간 오프셋을 계산 하는 클라이언트 요청/응답 및 서버 요청/응답의 타임 스탬프를 기반 합니다.  그러나 네트워크 흐르며 되며 급격히 증가 하는 네트워크 정체 및 네트워크 대기 시간에 영향을 주는 기타 요인으로 인해 NTP 데이터로 있을 수 있습니다.  Windows 2016 알고리즘 안정적이 고 정확 하 게 시계는 여러 가지 다른 기법을 사용 하 여이 소음 평균입니다.  또한 소스 사용 정확한 시간을 알려주는 향상 된 해상도 향상 된 API 참조 합니다.  이러한 세부 정보와 함께 도메인 전체에서 UTC와 관련 하 여 1 ms 정확도 달성 하기 위해 수 있습니다.

### <a name="hyper-v"></a>Hyper-V
Windows 2016 Hyper-v TimeSync 서비스를 향상 시켰습니다. VM start 또는 VM 복원 및 w32time에 제공 된 샘플에 대 한 대기 시간 보정 인터럽트에 초기 시간을 더 정확 하 게 포함 하는 향상 된 기능.  이러한 향상 된 기능을 사용 하면 75% 부하가 있는 컴퓨터의 경우에도 RMS (분산을 나타내는 근본 평균 제곱 50)를 사용 하 여 호스트의 10μs를 유지할 수 있습니다. 자세한 내용은 [hyper-v 아키텍처](https://msdn.microsoft.com/library/cc768520.aspx)를 참조 하세요.

> [!NOTE]
> 부하 분산 된 프로필을 사용 하 여 prime95 벤치 마크를 사용 하 여 생성 되었습니다.

또한 게스트에 보고 하는 계층 수준을 더 투명 하 게 됩니다.  이전에 호스트의 정확성에 관계 없이 2, 고정된 계층을 발생 하 게 합니다.  Windows Server 2016를 변경 하는 경우 호스트는 호스트 계층 보다 큰 계층를 보고 하므로 가상 게스트가 더 나은 시간이 발생 합니다.  호스트 계층은 원본 시간에 따라 일반적인 방법으로 w32time에 의해 결정 됩니다.  도메인 가입 Windows 2016 게스트가 호스트에 기본값으로 지정 하는 것이 아니라 가장 정확한 시계를 찾을 수 있습니다.  이러한 이유 때문에 수동으로 Windows 2012R2에 도메인에 가입 된 컴퓨터에 대 한 Hyper-v 시간 공급자 설정을 사용 하지 않도록 해야 한다고 것 이었습니다.

### <a name="monitoring"></a>모니터링
성능 모니터 카운터 추가 되었습니다.  모니터링 및 해결 시간 정확도 초기 계획을 수 있습니다 이러한 합니다.  이러한 카운터는 다음과 같습니다.

카운터|설명|
----- | ----- |
시간 오프셋을 계산합니다.|   절대 시간 마이크로초에서 W32Time 서비스에 의해 계산 시스템 시계와 선택한 시간 원본 간의 오프셋입니다. 새 유효한 샘플을 사용할 수 있는 경우 계산된 시간 샘플으로 표시 된 시간 오프셋으로 업데이트 됩니다. 이 로컬 시계의 실제 시간 오프셋입니다. W32time 클록 수정이이 오프셋을 사용 하 여 시작 하 고 로컬 시계를 적용 해야 하는 남은 시간 오프셋으로 계산된 시간 샘플 간격을 업데이트 합니다. 이 성능 카운터를 사용 하 여 낮은 폴링 간격으로 시계 정확도 추적할 수 있습니다 (예:: 256 초 이하의)은 카운터 값을 원하는 클록 정확도 제한 보다 작아야 하 고 있습니다.|
클럭 주파수 조정| 절대 클록 주파수를 조정 하면 당 10 억 부분에는 W32Time가 로컬 시스템 시계를 변경 합니다. 이 카운터는 W32time에서 수행 중인 작업을 시각화 하는 데 도움이 됩니다.|
NTP 왕복 지연|    가장 최근의 왕복 지연 시간 (마이크로초)에서 서버에서 응답을 받을 NTP 클라이언트에 의해 발생입니다. 이 시간을 NTP 서버는 요청을 전송 하 고 서버에서 올바른 응답을 받는 간에 NTP 클라이언트에서 경과 합니다. 이 카운터는 NTP 클라이언트도 지연 특징을 결정 하는 데 도움이 됩니다. 더 큰 또는 다양 한 왕복 노이즈 NTP 시간 계산에 영향을 줄 수 시간 동기화를 통해 NTP의 정확성을 추가할 수 있습니다.|
NTP 클라이언트 원본 수|    NTP 클라이언트에서 사용 되는 NTP 시간 원본과의 현재 수입니다. 이것이이 클라이언트의이 요청에 응답 하는 시간 서버 활성, 고유 IP 주소의 수입니다. 이 번호는 피어 이름 및 현재 도달률 능력의 DNS 확인에 따라 구성 된 피어 보다 크거나 작을 수 있습니다.|
NTP 서버 들어오는 요청|   NTP 서버 (요청/초)에 의해 수신 된 요청 수입니다.|
NTP 서버 나가는 응답|  NTP 서버 (응답/초)에서 응답 하는 요청 수입니다.|

처음 3 카운터 정확성 문제 해결에 대 한 시나리오를 대상으로 합니다.  문제 해결 시간 정확도 NTP 섹션 아래에서 [모범 사례](#BestPractices), 자세한 내용이 있습니다.
지난 3 카운터 NTP 서버 시나리오에 설명 하 고 할 때 도움이 부하 및 기준 지정 하면 현재 성능을 결정 됩니다.

### <a name="configuration-updates-per-environment"></a>환경 구성 업데이트
다음은 각 역할에 대 한 Windows 2016 버전과 이전 버전 간의 기본 구성 변경 내용에 대 한 설명입니다.  이제 Windows Server 2016 및 Windows 10 기념일 업데이트 (빌드 14393)의 설정이 고유 하므로 별도의 열로 표시 됩니다. 

|역할|설정|Windows Server 2016|Windows 10|Windows Server 2012 R2</br>Windows Server 2008 R2</br>Windows 10|
|---|---|---|---|---|
|**독립형/Nano 서버**||||
| |*시간 서버*|time.windows.com|NA|time.windows.com|
| |*폴링 빈도*|64-1024 초|NA|일주일에 한 번|
| |*클록 업데이트 빈도*|1 초|NA|한 시간에 한 번|
|**독립 실행형 클라이언트**||||
| |*시간 서버*|NA|time.windows.com|time.windows.com|
| |*폴링 빈도*|NA|하루에 한 번|일주일에 한 번|
| |*클록 업데이트 빈도*|NA|하루에 한 번|일주일에 한 번|
|**도메인 컨트롤러**||||
| |*시간 서버*|PDC/GTIMESERV|NA|PDC/GTIMESERV|
| |*폴링 빈도*|64-1024 초|NA|1024-32768 초|
| |*클록 업데이트 빈도*|하루에 한 번|NA|일주일에 한 번|
|**도메인 구성원 서버**||||
| |*시간 서버*|DC|NA|DC|
| |*폴링 빈도*|64-1024 초|NA|1024-32768 초|
| |*클록 업데이트 빈도*|1 초|NA|5 분 마다 한 번|
|**도메인 구성원 클라이언트**||||
| |*시간 서버*|NA|DC|DC|
| |*폴링 빈도*|NA|1204-32768 초|1024-32768 초|
| |*클록 업데이트 빈도*|NA|5 분 마다 한 번|5 분 마다 한 번|
|**Hyper-v 게스트**||||
| |*시간 서버*|계층 호스트 및 시간 서버에 따라 가장 적합 한 옵션을 선택 합니다.|계층 호스트 및 시간 서버에 따라 가장 적합 한 옵션을 선택 합니다.|호스트로 기본값 설정|
| |*폴링 빈도*|위의 역할 기반|위의 역할 기반|위의 역할 기반|
| |*클록 업데이트 빈도*|위의 역할 기반|위의 역할 기반|위의 역할 기반|

>[!NOTE]
>Hyper-v의 Linux에 대 한 참조는 [Hyper-v 호스트 시간을 사용 하도록 허용 Linux](#AllowingLinux) 아래의 섹션입니다.

### <a name="impact-of-increased-polling-and-clock-update-frequency"></a>증가 된 폴링 및 시계 업데이트 빈도의 영향
더 정확한 시간을 제공 하기 위해 폴링 주기 및 클럭 업데이트에 대 한 기본값 미세 조정 더 자주 수행할 수는 증가 합니다.  UDP/NTP 트래픽이 증가 하면,이 패킷을 사항은 작은 있어야 거의 하므로 또는 광대역 연결을 통해 영향을 주지 않습니다. 그러나 않은 시간은 다양 한 하드웨어 및 환경에서 더 잘 이어야 합니다.

백업 배터리 장치에 대 한 폴링 빈도 늘리면 문제가 발생할 수 있습니다.  배터리 장치 해제 하는 동안 시간을 저장 하지 않습니다.  다시 시작 될 때 시계를 자주 수정 해야 합니다.  폴링 빈도 늘리면 불안정 해질 수 클록 고 더욱 강력한 기능을 사용할 수도 있습니다.  클라이언트 기본 설정을 변경 하지 않는 것이 좋습니다.

AD 도메인에서 NTP 클라이언트에서 향상 된 업데이트를 곱한 값된 효과도 함께 도메인 컨트롤러를 최소한으로 영향 을지 않습니다.  NTP 다른 프로토콜 및 한계 영향을 비교 하 여 훨씬 더 작은 리소스 소비를 있습니다.  Windows Server 2016에 대 한 향상 된 설정에 의해 영향을 받지 하기 전에 다른 도메인 기능에 대 한 제한에 도달 하 가능성이 더 높습니다.  Active Directory에서 보안 NTP 인 경우에 간단한 NTP 보다 덜 정확 하 게 시간 동기화를 사용 하지만 확인 PDC에서 두 클라이언트 계층을 강화 됩니다.

신중한 계획으로 코어당 초당 NTP 요청 수가 100 개를 예약 해야 합니다.  예를 들어, 4 개 코어 4 Dc의 구성 된 도메인을 수 있습니다 초당 1600 NTP 요청을 처리 합니다.  64 초 마다 한 번, 시간을 동기화 하도록 구성 된 10, 000 클라이언트 있고 시간이 지남에 따라는 요청을 균일 하 게에 수신 하는 경우 표시 되는 10, 000/64 또는 약 160 모든 Dc 분산 요청/초입니다.  이 쉽게 우리의 1600 NTP 요청 수/초가 예에서 포함 됩니다.  물론가 네트워크, 프로세서 속도 및 로드에 대 한 많은 종속성 있으므로 항상으로 초기 계획 및 테스트 환경에서를 계획 권장 사항 보수적인 포함 됩니다.

또한 Dc가 CPU 부하가 40%를 초과 하 여 실행 되는 경우에는 거의 모든 시간을 NTP 응답에 추가 하 고 도메인의 시간 정확도에 영향을 줍니다.  마찬가지로 실제 결과 이해 하는 사용자 환경에서 테스트 해야 합니다.

## <a name="time-accuracy-measurements"></a>시간 정확도 측정
### <a name="methodology"></a>방법
Windows Server 2016에 대 한 시간 정확도 측정 하는 다양 한 도구, 메서드 및 환경 사용 했습니다.  측정 하 고 환경 조정 정확도 결과 요구 사항을 충족 하는지 확인할 이러한 기법을 사용할 수 있습니다. 

도메인 소스 시계 우리의 GPS 하드웨어와 2 명의 높은 정밀도 NTP 서버 구성 되어 있습니다.  또한 별도 참조가 테스트 컴퓨터를 다른 제조업체의 설치 된 높은 정밀도 GPS 하드웨어를 가진도 측정 단위가 사용 했습니다.  테스트의 일부에 대 한 도메인 클록 소스 외에 대 한 참조로 사용 하는 정확 하 고 신뢰할 수 있는 시계 원본이 필요 합니다.

실제 및 가상 컴퓨터를 모두 사용 하 여 정확도 측정 하 4 가지의 다른 방법을 사용 했습니다. 여러 방법을 결과 유효성을 검사할 독립 수단을 제공 합니다.


1. 별도 GPS 하드웨어에 있는 참조 테스트 컴퓨터에 대 한 조건 w32tm으로, 하는 로컬 시계를 측정 합니다.  
2.  이 경우 W32tm "stripchart"를 사용 하 여 클라이언트에 NTP 서버에서 측정 NTP ping
3.  이 경우 W32tm "stripchart"를 사용 하 여 NTP 서버에 클라이언트에서 측정값 NTP ping
4.  측정값 Hyper-v 게스트는 타임 스탬프 카운터 TSC ()를 사용 하 여 호스트에서 발생 합니다.  이 카운터는 양쪽 파티션에 파티션과 시스템 시간 간에 공유 됩니다.  가상 컴퓨터에서 호스트 시간과 클라이언트의 차이 계산 했습니다.  다음을 측정 값은 동시에 발생 하지 이후 게스트에서 호스트 시간 보간합니다 TSC 시계를 사용 합니다.  또한 지연 되 고 대기 시간으로 TSV 클록 분류 API에서 사용합니다.

이 경우 W32tm이 기본 제공 하지만 우리 테스트 하는 동안 사용 되는 다른 도구 사용할 수 GitHub의 Microsoft 저장소에 대 한 테스트 및 사용 현황에 대 한 오픈 소스로.  저장소에서 WIKI에 측정 작업을 수행 하는 도구를 사용 하는 방법을 설명 하는 자세한 정보가 있습니다.

> [https://github.com/Microsoft/Windows-Time-Calibration-Tools](https://github.com/Microsoft/Windows-Time-Calibration-Tools)

아래에 표시 된 테스트 결과 테스트 환경 중 하나에서 적용 하는 측정값의 하위 집합입니다.  시간 계층 및 끝 시간 계층에 자식 도메인 클라이언트의 시작 부분에 유지 관리 하는 정확도를 보여 줍니다.  이 비교에 대 한 2012 기반 토폴로지에서 동일한 컴퓨터와 비교 됩니다.

### <a name="topology"></a>토폴로지
비교를 위해 Windows Server 2012R2와 Windows Server 2016 기반 토폴로지를 테스트 했습니다.  두 토폴로지 모두 설치 된 GPS 클록 하드웨어와 Windows Server 2016 컴퓨터를 참조 하는 두 개의 실제 Hyper-v 호스트 컴퓨터의 구성 됩니다.  각 호스트에는 다음과 같은 토폴로지가 따라 정렬 되는 3 도메인에 가입 된 windows 게스트를 실행 합니다.  줄 시간 계층 및 사용 되는 프로토콜/전송을 나타냅니다.

![Windows 시간](../media/Windows-Time-Service/Windows-2016-Accurate-Time/topology1.png)

![Windows 시간](../media/Windows-Time-Service/Windows-2016-Accurate-Time/topology2.png)

### <a name="graphical-results-overview"></a>그래픽 결과 개요
다음과 같은 두 가지 그래프 위의 토폴로지에 따라 도메인에 두 명의 특정 멤버에 대 한 시간 정확도를 나타냅니다.  각 그래프 모두 Windows Server 2012R2 및 결과가 표시 됩니다 2016 겹쳐 표시 되며, 향상 된 기능을 시각적으로 보여 주는 합니다.  정확도 호스트에 비해 게스트 컴퓨터에를 측정 합니다.  그래픽 데이터 수행한 테스트의 전체 집합의 하위 집합을 나타내고 모범 사례와 최악의 시나리오를 보여 줍니다.  

![Windows 시간](../media/Windows-Time-Service/Windows-2016-Accurate-Time/topology3.png)

### <a name="performance-of-the-root-domain-pdc"></a>PDC 루트 도메인의 성능
루트 PDC (VMIC 사용)를 정확 하 고 안정적으로 입증 된 GPS 하드웨어와 Windows Server 2016 Hyper-v 호스트에 동기화 됩니다.  녹색 음영된 영역으로 표시 된 1 ms 정확도 대 한 중요 한 요구 사항입니다.

![Windows 시간](../media/Windows-Time-Service/Windows-2016-Accurate-Time/chart1.png)

### <a name="performance-of-the-child-domain-client"></a>자식 도메인 클라이언트의 성능
자식 도메인 클라이언트와 통신 하는 루트 PDC는 자식 도메인 PDC에 연결 됩니다.  시간이 것도 1에서 ms 요구 사항입니다.

![Windows 시간](../media/Windows-Time-Service/Windows-2016-Accurate-Time/chart2.png)


### <a name="long-distance-test"></a>시외 테스트
다음 차트에는 Windows Server 2016 6 물리적 네트워크 홉 가상 네트워크 1 홉을 비교합니다.  서로 겹치는 데이터를 표시 하는 투명도 있는 두 개의 차트 위에 표시 됩니다.  더 높은 대기 시간 및 보다 큰 시간 편차 증가 함에 따라 네트워크 홉을 의미합니다.  확대 하 고 있으므로 차트는 1 녹색 영역을 나타내는 ms 범위, 더 큽니다.  시간은 1에서 볼 수 있듯이 여러 홉 ms.  부정적인 이동, 네트워크 비대칭 보여 줍니다.  물론, 모든 네트워크는 서로 다르며 측정 다양 한 환경 요인에 따라 달라 집니다.

![Windows 시간](../media/Windows-Time-Service/Windows-2016-Accurate-Time/chart3.png)

## <a name="BestPractices"></a>정확한 계측 모범 사례
### <a name="solid-source-clock"></a>단색 소스 시계
컴퓨터 시간은 우수한 소스 시계와 동기화 할 수만 있습니다.  1을 달성 하기 위해 ms 정확도 해야 GPS 하드웨어 또는 시간 기기 마스터 소스 형식으로 참조 하 여 네트워크에 있습니다.  Time.windows.com의 기본값을 사용 하 여, 있습니다 현지 시간 원본과 안정적 제공 하지 않습니다.  또한 더 멀리 소스 클록 익숙해지면 정확도 네트워크에 적용 됩니다.  마스터 소스 클록이 있는 각 데이터 센터는 가장 높은 정확도에 필요 합니다.

### <a name="hardware-gps-options"></a>하드웨어 GPS 옵션
정확한 시간을 제공할 수 있는 다양 한 하드웨어 솔루션 있습니다.  일반적으로 솔루션 오늘날 기반으로 GPS 안테나 합니다.  라디오 및 전화 접속 모뎀 솔루션 전용된 회선을 사용 하 여 있습니다.  이러한 기기를 하나로 네트워크에 연결 하거나 PCIe 또는 USB 장치를 통해 예를 들어 Windows는 PC에 연결 합니다.  다른 옵션은 서로 다른 수준의 정확도 제공 하 고 항상 그렇듯이 결과에 따라 달라 집니다 환경.  정확도 영향을 줄 수 있는 변수 GPS 가용성, 네트워크 안정성 및 부하 및 PC 하드웨어를 포함 합니다.  이들은 했 듯이 우리는 안정적이 고 정확한 시간에 대 한 요구 사항이 있는 원본 시계를 선택할 때 모든 중요 한 요소입니다.

### <a name="domain-and-synchronizing-time"></a>도메인 및 시간을 동기화
도메인 구성원 컴퓨터를 확인 하려면 도메인 계층 구조를 사용 하 여 시간을 동기화 원본으로 사용 합니다.  각 도메인 구성원 클록 원본으로 저장 및 동기화 하는 다른 컴퓨터를 찾을 수 있습니다.  각 유형의 도메인 구성원 시간 동기화에 대 한 클럭 소스를 찾을 수 있도록 다양 한 규칙을 따릅니다.  포리스트 루트의 PDC는 모든 도메인에 대 한 기본 클록 소스.  아래에 나열 된은 다양 한 역할 및 소스를 찾는 방법에 대 한 높은 수준의 설명입니다.


- **도메인 컨트롤러와 PDC 역할** -이 컴퓨터가 도메인에 대 한 정식 시간 원본. 도메인에 사용할 수 있는 가장 정확한 시간을 갖습니다 하 고의 경우를 제외 하 고 부모 도메인의 DC와 동기화 해야 여기서 [GTIMESERV](#GTIMESERV) 역할이 사용 됩니다. 
- **다른 도메인 컨트롤러** -이 컴퓨터는 클라이언트와 도메인의 구성원 서버에 대 한 시간 소스로 작동 됩니다. DC는 자체 도메인의 PDC 또는 해당 부모 도메인의 모든 DC 동기화 할 수 있습니다.
- **클라이언트/구성원 서버** -이 컴퓨터는 DC 또는 자체 도메인 또는 DC의 PDC 또는 부모 도메인에서 PDC와 동기화 할 수 있습니다.

사용 가능한 후보에 따라, 점수 매기기 가장 적합 한 시간 원본을 찾는 데 사용 됩니다.  이 시스템 시간 원본과 상대 위치의 안정성을 고려합니다.  이 경우 서비스를 시작 하는 되 면 발생 합니다.  시간 동기화 하는 방법을 세밀 하 게 제어 해야 하는 경우에 특정 위치에 좋은 시간 서버를 추가 하거나 중복을 추가할 수 있습니다.  참조는 [지정 된 로컬 신뢰할 수 있는 시간 서비스를 사용 하 여 GTIMESERV](#GTIMESERV) 에 대 한 자세한 내용은 섹션입니다.

#### <a name="mixed-os-environments-win2012r2-and-win2008r2"></a>혼합된 OS 환경 (Win2012R2 및 Win2008R2)
순수 Windows Server 2016 도메인 환경을 가장 높은 정확도 대 한 필수 이지만, 이점이 여전히 혼합된 환경 에서입니다.  Windows Server 2016 Hyper-v는 Windows 2012에에서 배포만 하는 경우 게스트는 또한 Windows Server 2016 하지만 위에서 설명한 개선 사항으로 인해 게스트를 활용 합니다.  Windows Server 2016 PDC 더 안정적인 소스는 것이 향상 된 알고리즘으로 인해 보다 정확한 시간을 제공할 수 됩니다.  교체 하 여 PDC 아닐 옵션, 대신와 Windows Server 2016 DC을 추가할 수는 [GTIMESERV](#GTIMESERV) 롤링 업그레이드 도메인에 대 한 정확도 집합입니다.  그러나 Windows Server 2016 DC 다운스트림 시간 클라이언트에 게 보다 나은 시간을 제공할 수,만 찾아낼 소스 NTP 시간입니다.

또한 위에서 설명한 것 처럼 Windows Server 2016 클록 폴링 및 새로 고침 빈도 수정 되었습니다.  이러한 하위 수준 Dc로 수동으로 변경 하거나 수 그룹 정책을 통해 적용 합니다.  이러한 구성은 테스트 되지 않았습니다, 동안 해야 Win2008R2 및 Win2012R2에서 잘 작동 하며 몇 가지 이점을 제공.

Windows Server 2016 조정 변경 된 후에 즉시 시스템 시간 유동 결과 유지 하는 정확한 시간을 유지 하는 여러 문제를가 하기 전에 버전입니다.  이 때문에 정확한 NTP 원본에서 시간 예제를 자주 가져오기 및 데이터와 함께 로컬 시계 조화에서 잠재 고객 시스템 시계에서 더 작은 드리프트를 더 나은 시간을 장비를 하위 수준 OS 버전에서 발생 하는 방법은 샘플링 기간입니다. 관찰 된 가장 정확도 높은 정확도 설정을 사용 하 여 구성 된 Windows Server 2012R2 NTP 클라이언트를 정확 하 게 Windows 2016 NTP 서버에서 해당 시간을 동기화 하는 경우 약 5 밀리초 했습니다.

게스트 도메인 컨트롤러와 관련 된 일부 시나리오에서는 Hyper-v TimeSync 샘플 도메인 시간 동기화를 방해할 수 있습니다.  서버 2016 Hyper-v 호스트에서 실행 되는 서버 2016 게스트에 대 한 문제가 더 이상 이어야 합니다.

W32time에 대 한 샘플을 제공 하 여 Hyper-v TimeSync 서비스를 사용 하지 않으려면 다음 게스트 레지스트리 키를 설정 합니다.

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\VMICTimeProvider 
    "Enabled"=dword:00000000

#### <a name="AllowingLinux"></a>Linux에서 Hyper-v 호스트 시간을 사용 하도록 허용
Hyper-v에서 실행 하는 Linux 게스트에 대 한 클라이언트 NTP 서버에 대해 시간 동기화에 대 한 NTP 데몬을 사용 하 여 일반적으로 구성 됩니다.  Linux 배포판 TimeSync 버전 4 프로토콜을 지 원하는 Linux 게스트에 TimeSync 통합 서비스가 사용 하도록 설정 하는 경우 호스트 시간에 대해 동기화 됩니다. 일치 하지 않는 시간을 장비를 두 가지 방법을 모두 사용 하는 경우 발생할 수 있습니다.

호스트 시간에 대 한 단독으로 동기화 할 것이 좋습니다 NTP 시간 동기화를 사용 하지 않으려면 중 하나:

- Ntp.conf 파일에 NTP 서버를 사용 하지 않도록 설정
- 또는 NTP 데몬 사용 안 함

이 구성에서는 시간 서버 매개 변수는이 호스트입니다.  폴링 빈도 5 초 및 시계 업데이트 빈도 5 초도 합니다.

NTP를 통해서만 동기화 하기 위해 게스트에 TimeSync 통합 서비스를 사용 하지 않도록 설정 하는 것이 좋습니다.

> [!NOTE]
> 참고:  Linux 게스트를 사용 하 여 정확한 시간을 지원 하려면 최신 업스트림 Linux 커널 에서만 지원 되는 기능이 필요 하며, 모든 Linux 배포판에서 널리 사용 되는 것은 아닙니다. 지원 배포에 대 한 자세한 내용은 [Windows의 hyper-v에 대해 지원 되는 Linux 및 FreeBSD 가상 컴퓨터](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows) 를 참조 하세요.

#### <a name="GTIMESERV"></a>GTIMESERV를 사용 하 여 신뢰할 수 있는 로컬 시간 서비스 지정
정확한 시계로 하나 이상의 도메인 컨트롤러를 지정할 수는 GTIMESERV 좋은 시간 서버를 사용 하 여 플래그를 지정 합니다.  예를 들어, GPS 하드웨어를 장착 하는 특정 도메인 컨트롤러는 GTIMESERV 플래그 지정할 수 있습니다.  이 도메인 GPS 하드웨어에 따라 시계를 참조 하는 않은지 확인 합니다.

> [!NOTE]
> 도메인 플래그에 대 한 자세한 정보를 찾을 수는 [MS ADTS 프로토콜 설명서](https://msdn.microsoft.com/library/mt226583.aspx)합니다.

TIMESERV는 다른 관련된 도메인 서비스를 나타내는 플래그에 관계 없이 컴퓨터를 현재 신뢰할 수 있는 변경 될 수 있는 DC 연결이 끊어졌습니다.  이 상태에서 DC "알 수 없는 계층" NTP를 통해 쿼리할 때 반환 됩니다.  여러 번을 시도한 후 DC 시스템 이벤트 시간 서비스 이벤트 36를 기록 합니다.

DC는 GTIMESERV 구성 하려는 경우이 구성할 수 있습니다 다음 명령을 사용 하 여 수동으로.  이 경우 DC는 마스터 시계와 다른 컴퓨터를 사용 합니다.  이 기기 또는 전용된 컴퓨터 수 있습니다.

    w32tm /config /manualpeerlist:”master_clock1,0x8 master_clock2,0x8” /syncfromflags:manual /reliable:yes /update

> [!NOTE]
> 자세한 내용은 참조 [Windows 시간 서비스를 구성 합니다.](https://technet.microsoft.com/library/cc731191.aspx)

DC에 설치 된 GPS 하드웨어, NTP 클라이언트를 사용 하지 않도록 설정 하 고 NTP 서버를 사용 하도록 설정 하려면 다음이 단계를 사용 해야 합니다.

NTP 클라이언트를 사용 하지 않도록 설정 하 여 시작 하 고 이러한 레지스트리 키 변경 내용을 사용 하 여 NTP 서버를 사용 하도록 설정 합니다.

    reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpClient /v Enabled /t REG_DWORD /d 0 /f

    reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpServer /v Enabled /t REG_DWORD /d 1 /f

다음으로, Windows 시간 서비스를 다시 시작

    net stop w32time && net start w32time

마지막으로,이 컴퓨터에 사용 하 여 신뢰할 수 있는 시간 소스 수 있는지 나타냅니다.
   
    w32tm /config /reliable:yes /update

변경 내용을 제대로 완료 된를 확인 하려면 아래에 표시 된 결과 영향을 다음 명령을 실행할 수 있습니다. 

    w32tm /query /configuration

값|예상된 설정|
----- | ----- |
AnnounceFlags|  5 (로컬)|
NtpServer   |(로컬)|
DllName |C:\WINDOWS\SYSTEM32\w32time 합니다. DLL (로컬)|
Enabled |1 (로컬)|
NtpClient|  (로컬)|

    w32tm /query /status /verbose

값|  예상된 설정|
----- | ----- |
계층|    1 (기본 참조-라디오 클록으로)|
참조|    0x4C4F434C (원본 이름:  "LOCAL")|
Source| 로컬 시계입니다.|
위상 오프셋|   0.0000000s|
서버 역할|    576 (신뢰할 수 있는 시간 서비스)|

#### <a name="windows-server-2016-on-3rd-party-virtual-platforms"></a>타사 가상 플랫폼의 Windows Server 2016
Windows가 가상화 될 때 기본적으로 하이퍼바이저는 시간 제공을 담당 합니다.  그러나 Active Directory 제대로 작동 하려면 도메인에 가입 된 구성원이 도메인 컨트롤러와 동기화 해야 합니다.  게스트와 타사 가상 플랫폼의 호스트 간에 시간 가상화를 사용 하지 않도록 설정 하는 것이 가장 좋습니다.

#### <a name="discovering-the-hierarchy"></a>계층 구조를 검색합니다.
도메인에 동적이 고 협상 된 마스터 클록 원본에 시간 계층의 체인 이므로 시간 원본 이며 마스터 소스 클럭에 대 한 체인을 이해 하 여 특정 컴퓨터의 상태를 쿼리할 해야 합니다.  이 시간 동기화 문제를 진단할 수 있습니다.

부여한 문제를 해결 하려면 특정 클라이언트; 첫 번째 단계는이 경우 w32tm 명령을 사용 하 여 해당 시간 원본을 이해 하는 것입니다.

    w32tm /query /status

무엇 보다도 소스에 결과가 표시.  소스는 시간 도메인의 동기화 하면 사용자를 나타냅니다.  이이 컴퓨터 시간 계층의 첫 번째 단계입니다.
다음 위쪽에서 소스 항목을 사용 하 고 소스를 찾으려면 다음 시간 체인에 /StripChart 매개 변수를 사용 합니다.

    w32tm /stripchart /computer:MySourceEntry /packetinfo /samples:1

도 유용 다음 명령은 지정된 된 도메인에서 찾을 수 있는 각 도메인 컨트롤러를 나열 하 고 각 파트너를 확인할 수 있는 결과 출력 합니다.  이 명령은 수동으로 구성 된 컴퓨터에 포함 됩니다.
    
    w32tm /monitor /domain:my_domain

목록을 사용 하면 도메인을 통해 결과 추적할 수 있으며 계층 구조의 각 단계에서의 시간 오프셋을 이해 수도 있습니다.  여기서의 시간 오프셋 악화 크게 지점 두어의 잘못 된 경우 루트를 확인할 수 있습니다.  여기에서 왜 당시 올바르지 설정 하 여 이해 하려고 수 [w32tm 로깅](#W32Logging)합니다. 

#### <a name="using-group-policy"></a>그룹 정책을 사용 하 여
수 그룹 정책을 사용 하면 보다 엄격한 정확도가, 수행 하 예를 들어, 특정 NTP 서버를 사용 하 여 또는 제어 방법을 하위 수준 OS 가상화 하는 경우 구성 된 클라이언트를 할당 합니다.  
다음은 가능한 시나리오 및 관련 그룹 정책 설정의 목록이입니다.

**가상화 된 도메인** -Windows 2012r2 2에서 가상화 된 도메인 컨트롤러를 제어 하 여 hyper-v 호스트가 아닌 도메인과 시간을 동기화 하도록 하려면이 레지스트리 항목을 사용 하지 않도록 설정할 수 있습니다.   Pdc를 하지 않으려는 Hyper-v 호스트 가장 안정적인 시간 원본을 제공 하는 것으로 항목을 해제 합니다.  레지스트리 항목 데이터가 변경 되는 w32time 서비스를 다시 시작 하면 필요 합니다.

    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\VMICTimeProvider]
    "Enabled"=dword:00000000

**정확도 중요 한 로드** 시간 정확도 중요 한 작업에 대 한 NTP 서버를 설정 하는 컴퓨터의 그룹을 구성할 수 있습니다-및 폴링 및 시계 업데이트 빈도 같은 시간 설정 관련 됩니다.  이 일반적으로 도메인에서 처리 되어 있지만 더 많은 컨트롤에 대 한 마스터 시계를 직접 가리키도록 특정 컴퓨터를 대상 수 있습니다.

그룹 정책 설정|   새 값|
----- | ----- |
NtpServer|  0x8 ClockMasterName,|
MinPollInterval|    6-64 초|
MaxPollInterval|    6|
UpdateInterval| 100 – 초당 한 번|
EventLogFlags|  3-모든 특수 한 시간 로깅|

> [!NOTE]
> NtpServer 및 EventLogFlags 설정은 Windows NTP 클라이언트 설정 구성을 사용 하 여 System\Windows Time Service\Time 공급자 아래에 있습니다.  다른 3 System\Windows 시간 서비스의 전역 구성 설정을 사용 하 여 아래에 있습니다.

**원격 정확도 중요 한 로드 원격** – 소매 인스턴스와 신용 업계 PCI (Payment)에 대 한 분기 도메인에 시스템의 경우 Windows는 현재 사이트 정보를 사용 하 고 시간 구성 하는 원본 DC 로케이터 수동 NTP이 없는 경우에 로컬 DC를 찾을 수 있습니다.  이 환경에 올바른 시간으로 빠르게 수렴을 사용 하 여 정확도의 1 초 필요 합니다.  W32time 서비스 시계를 뒤로 이동 하려면이 옵션을 사용 합니다.  허용 되는이 요구 사항을 충족 하는 경우 다음 정책을 만들 수 있습니다.   모든 환경에서와 마찬가지로 실행 하면 테스트 및 초기 계획을 네트워크. 

그룹 정책 설정|   새 값|
----- | ----- |
MaxAllowedPhaseOffset|  1 이상에 있는 경우 두 번째 클록 시간으로 설정 올바른.|

전역 구성 설정을 사용 하 여 System\Windows 시간 서비스 MaxAllowedPhaseOffset 설정이 있습니다.

> [!NOTE]
> 그룹 정책 및 관련된 항목에 대 한 자세한 내용은 참조 하십시오. [Windows 시간 서비스 도구가](windows-time-service-tools-and-settings.md) 및 technet 문서를 설정 합니다.

## <a name="azure-and-windows-iaas-considerations"></a>Azure 및 Windows IaaS 고려 사항

### <a name="azure-virtual-machine-active-directory-domain-services"></a>Azure 가상 머신: Active Directory 도메인 서비스
Active Directory Domain Services 실행 중인 Azure VM이 기존 온-프레미스 Active Directory 포리스트의 일부 이면 TimeSync (VMIC)를 사용 하지 않도록 설정 해야 합니다. 이 한 번 동기화 계층 구조를 사용 하 여 실제 및 가상, 포리스트에서 모든 Dc를 허용 하도록 합니다. 모범 사례 백서를 참조 하십시오 ["실행 도메인 컨트롤러에서 하이퍼-V"](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx)

### <a name="azure-virtual-machine-domain-joined-machine"></a>Azure 가상 머신: 도메인에 가입 된 컴퓨터
도메인에는 기존 Active Directory 포리스트에 가입 되어 있는 컴퓨터를 호스트 하는 경우 가상이 든 실제 든이 가장 좋습니다를 게스트에 대 한 TimeSync를 사용 하지 않고 W32Time 시간 형식에 대 한 구성를 통해 해당 도메인 컨트롤러와 동기화 하도록 구성 되었는지 확인 NTP5 =

### <a name="azure-virtual-machine-standalone-workgroup-machine"></a>Azure 가상 머신: 독립 실행형 작업 그룹 컴퓨터
Azure VM을 도메인에 가입 되지 않은 되어 있지 않고는 도메인 컨트롤러, 기본 시간 구성을 유지 하 고 vm이 호스트와 동기화 하는 것이 좋습니다.

## <a name="windows-application-requiring-accurate-time"></a>Windows 응용 프로그램 요구 정확한 시간
### <a name="time-stamp-api"></a>타임 스탬프 API
시간 이동이 아니라 UTC와 관련 하 여 가장 큰 정확도가 필요한 프로그램은 [GETSYSTEMTIMEPRECISEASFILETIME API](https://msdn.microsoft.com/library/windows/desktop/Hh706895.aspx)를 사용 해야 합니다.  이 통해 응용 프로그램을 조건으로 Windows 시간 서비스 시스템 시간을 가져옵니다.

### <a name="udp-performance"></a>UDP 성능
응용 프로그램이 사용 하 여 UDP 통신 하며 트랜잭션 대기 시간을 최소화 하는 것이 중요 대는 레지스트리 항목에서 제외 되어야 하는 포트 범위를 구성 하는 데 관련 된 엔진을 필터링 하는 기본 포트 해야 합니다.  이 대기 시간을 개선 하 고 프로그램 처리량을 증가 합니다.  그러나 레지스트리를 변경 숙련 된 관리자에 게 제한 해야 합니다.  또한이 해결 방화벽에서 포트를 제외 합니다.  자세한 내용은 아래 문서 참조를 참조 하세요.

Windows Server 2012 및 Windows Server 2008의 경우 핫픽스를 먼저 설치 해야 합니다.  이 기술 자료 문서를 참조할 수 있습니다. [Windows 8 및 Windows Server 2012에서 멀티 캐스트 수신기 응용 프로그램을 실행 하는 경우 데이터 그램 손실](https://support.microsoft.com/kb/2808584)

### <a name="update-network-drivers"></a>네트워크 드라이버 업데이트
일부 네트워크 공급 업체 들이 드라이버 대기 시간 및 UDP 패킷을 버퍼링 작업과 관련 하 여 성능을 향상 시킬 드라이버 업데이트 합니다.  UDP 처리량에 대 한 도움말에 대 한 업데이트 있는지 확인 하려면 네트워크 공급 업체에 게 문의 하십시오.

## <a name="logging-for-auditing-purposes"></a>감사 목적에 대 한 로깅
수동으로 시간 추적 규정을 준수 하려면 w32tm 로그, 이벤트 로그 및 성능 모니터 정보를 보관할 수 있습니다.  나중에 보관 된 정보를 이전에 특정 시간에 대 한 준수를 증명 사용할 수 있습니다.  다음과 같은 요소는 정확도 나타내는 데 사용 됩니다.


1. 계산 시간 오프셋의 성능 모니터 카운터를 사용 하 여 클록 정확도입니다.  원하는 정확도 효과 보여 줍니다.
2.  W32tm 로그의 "피어 응답"을 찾는 클록 원본입니다.   메시지 텍스트를 다음 IP 주소 또는 시간 원본과 유효성을 검사에 대 한 참조 시계는 체인에서 다음을 설명 하는 VMIC입니다.
3.  W32tm 로그를 사용 하 여 "ClockDispl 분야: \*기울이기\*시간이\*발생 합니다.  이 시간에 해당 w32tm 상태인 것을 나타냅니다.

### <a name="event-logging"></a>이벤트 로깅
전체 스토리를 가져오려면도 이벤트 로그 정보가 필요 합니다.  시스템 이벤트 로그를 수집 하 고 시간 서버, Microsoft-Windows-커널-부팅, Microsoft-Windows-커널-일반에서 필터링 하 여 제 3 자의 시간을 변경 하는 다른 영향이 있는지 검색할 수 있습니다.  외부 간섭을 제외 하기 위해 이러한 로그가 필요할 수 있습니다.  그룹 정책 이벤트 로그는 로그에 기록 됩니다 영향을 줄 수 있습니다.  사용 하 여 그룹 정책에 대 한 자세한 내용은 위의 섹션을 참조 합니다.

### <a name="W32Logging"></a>W32time 디버그 로깅
이 감사를 위해 w32tm를 사용 하도록 설정 하려면 다음 명령을 사용 하 여 시계의 주기적인 업데이트를 표시 하 고 원본 클록을 나타내는 로깅을 사용 하도록 설정 합니다.  새 로깅을 사용 하도록 서비스를 다시 시작 합니다.  

자세한 내용은 참조 [디버그 로깅을 Windows 시간 서비스를 설정 하는 방법을](https://support.microsoft.com/kb/816043)합니다.

    w32tm /debug /enable /file:C:\Windows\Temp\w32time-test.log /size:10000000 /entries:0-73,103,107,110

### <a name="performance-monitor"></a>성능 모니터
Windows Server 2016 Windows 시간 서비스는 감사에 대 한 로깅을 수집을 사용할 수 있는 성능 카운터를 제공 합니다.  로컬 또는 원격으로 기록할 수 있습니다.  컴퓨터 시간 오프셋 및 왕복 지연 카운터를 기록할 수 있습니다.  
와 같은 모든 성능 카운터를 원격으로 모니터링 하 고 System Center Operations Manager를 사용 하 여 경고를 만들 수 있습니다.  예를 들어 시간 오프셋에서 원하는 정확도 이동 하는 경우이 경고를 경고를 사용할 수 있습니다.  [System Center 관리 팩](https://social.technet.microsoft.com/wiki/contents/articles/15251.system-center-management-pack-authoring-guide.aspx) 에 자세한 내용이 들어 있습니다.

### <a name="windows-traceability-example"></a>Windows 추적 가능성 예제
W32tm 로그 파일에서을 두 가지 정보를 검사 합니다.  첫 번째는 로그 파일은 현재 조건 클록을 나타냅니다.  이 벌어지고 시간에 시계는 Windows 시간 서비스에서 조건부 되 고 된 것을 증명 합니다.

    151802 20:18:32.9821765s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:223 CR:156250 UI:100 phcT:65 KPhO:14307
    151802 20:18:33.9898460s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:1 CR:156250 UI:100 phcT:64 KPhO:41
    151802 20:18:44.1090410s - ClockDispln Discipline: *SKEW*TIME* - PhCRR:1 CR:156250 UI:100 phcT:65 KPhO:38

요점은 증명 w32time 인 ClockDispln 분야 접두사로 추가 하는 메시지는 시스템 시계와 상호 작용 볼 있다는 것입니다.
 
다음 참조 형식으로 현재 사용 되 고 있는 원본 컴퓨터를 보고 하는 분쟁에 관심된 시간 전에 마지막 보고서 로그에서 찾을 해야 합니다.  이 IP 주소, 컴퓨터 이름 또는 hyper-v 호스트와 동기화 할 나타내는 VMIC 공급자 수 있습니다.  다음 예에서는 10.197.216.105의 IPv4 주소를 제공 합니다.

    151802 20:18:54.6531515s - Response from peer 10.197.216.105,0x8 (ntp.m|0x8|0.0.0.0:123->10.197.216.105:123), ofs: +00.0012218s

참조 시간 체인에서 첫 번째 시스템 유효성을 검사 한 했으므로 참조 시간 소스에서 로그 파일을 조사 하 고 동일한 단계를 반복 해야 합니다.  이 NIST 같은 알려진된 시간 원본 또는 GPS와 같은 실제 시간에 도달할 때까지 계속 됩니다.  참조 시계는 GPS 하드웨어를 다음 로그는 제조에서 필요한 수도 있습니다.

## <a name="network-considerations"></a>네트워크 고려 사항
네트워크의 대칭에 대 한 종속성 NTP 프로토콜 알고리즘입니다.  증가 네트워크 홉 수가 비대칭 확률이 증가 합니다.  있습니다,에 대 한 자신의 환경에서 보면 어떤 종류의 정확도 예측 하는 것이 어렵습니다. 

성능 모니터 및 Windows Server 2016에서 새 Windows 시간 카운터 수 할 환경 정확도 평가 하 고 기준을 만듭니다. 네트워크의 모든 컴퓨터의 현재 오프셋을 결정 하는 문제 해결을 수행할 수 있습니다.

두 가지 일반 표준 정확한 시간에 대 한 네트워크를 통해  PTP ([정밀도 Time Protocol-IEEE 1588](https://www.nist.gov/el/intelligent-systems-division-73500/introduction-ieee-1588)) 네트워크 인프라에서 더 엄격한 요구 사항에 있지만 하위 마이크로초 정확성을 얻을 수 있습니다.  NTP ([Network Time Protocol – RFC 1305](https://tools.ietf.org/html/rfc1305)) 보다 큰 다양 한 네트워크 및 환경을 쉽게 관리 하에서 작동 합니다. 

Windows는 기본적으로 비-도메인 가입 된 컴퓨터에 대 한 간단한 NTP (RFC2030)를 지원합니다.  호출 하는 보안 NTP 사용 하 여 도메인에 가입 된 컴퓨터에 대 한 [MS SNTP](https://msdn.microsoft.com/library/cc246877.aspx), RFC1305 및 RFC5905에 설명 하는 인증 NTP는 관리 이점이 제공 하는 협상 도메인 암호를 활용 하 합니다.   

도메인 및 비도메인 조인 된 프로토콜에는 UDP 포트 123 필요 합니다.  NTP 모범 사례에 대 한 자세한 내용은 참조 [네트워크 시간 프로토콜 최상의 현재 사례 IETF 초안](https://tools.ietf.org/html/draft-ietf-ntp-bcp-00)합니다.

### <a name="reliable-hardware-clock-rtc"></a>신뢰할 수 있는 하드웨어 클럭 (RTC)
특정 범위를 초과 하는 경우를 제외 하 고는 시간을 지정 하는 것이 아니라  즉, w32tm 클록 업데이트 빈도 설정, Windows Server 2016 초에 한 번에 기본값을 사용 하 여 정기적으로 시계는 빈도 조정 합니다.  빈도 계속 시계 뒤에 있는 경우와 앞 이면 저하 빈도.  그러나 간의 클럭 주파수 조정 되는 동안 컨트롤의 하드웨어 시간이 않았습니다.  펌웨어 또는 하드웨어 시계에 문제가 있으면 컴퓨터의 시간을 덜 정확 하 게 될 수 있습니다.

테스트 해야 하는 또 다른 이유 및 사용자 환경에서 초기 계획입니다.  대상으로 하는 정확도 "계산 시간 오프셋" 성능 카운터에 안정화 되지 않으면, 펌웨어를 최신 확인 하려는 수도 있습니다.  다른 테스트로 중복 하드웨어에서 동일한 문제를 재현할 수 있는지 확인할 수 있습니다.

### <a name="troubleshooting-time-accuracy-and-ntp"></a>시간 정확도 및 NTP 문제 해결
Discovering를 사용할 수 있습니다 정확 하지 않은 시간의 소스를 이해 하려면 위의 계층 구조 부분입니다.  시간 NTP 소스에서 가장 달라 지므로 있는 계층 구조에서 지점을 찾을 시간 오프셋을 살펴보겠습니다.  계층 구조를 이해 하 고 나면 해당 특정 시간 원본 정확한 시간을 수신 하지 이유를 이해 하도록 합니다.  

분기 시간을 사용 하 여 시스템에 초점을 맞추어 문제를 확인할 수 있도록 하 고 해결 방법을 찾으려면 자세한 정보를 수집 아래 이러한 도구를 사용할 수 있습니다.  아래 UpstreamClockSource 참조에는 "w32tm /config /status"를 사용 하 여 발견 된 시계입니다.


- 시스템 이벤트 로그
- 다음을 사용 하 여 로깅 사용: w32tm logs-w32tm/debug/enable/file: C:\Windows\Temp\w32time-test.log/size: 10000000/entries: 0-300
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time w32Time 레지스트리 키
- 로컬 네트워크 추적
- (로컬 컴퓨터의 UpstreamClockSource)에서 성능 카운터
- 이 경우 W32tm /stripchart /computer:UpstreamClockSource
- PING UpstreamClockSource 대기 시간 및 소스에 따라 홉 수를 이해 하기
- Tracert UpstreamClockSource

문제점|    증상|   해결 방법|
----- | ----- | ----- |
로컬 TSC 시간이 안정화 되지 않았습니다.| 여러 100us의 1-2 분 마다 여전히 있지만 Perfmon-물리적 컴퓨터 동기화 클록 안정적인 시계를 사용 하 여 표시 합니다. |   펌웨어 업데이트의 유효성을 검사 하거나 다른 하드웨어 에서도 같은 문제가 표시 되지 않습니다.|
네트워크 대기 시간|    이 경우 w32tm stripchart 이상 10ms의 RoundTripDelay 표시 됩니다.  예를 들어 한 방향에만 있는 지연 왕복 시간의 ½ 정도로 지연 원인 노이즈의 변형입니다.</br></br>UpstreamClockSource은 여러 홉을 PING 하 여 표시 된 대로  TTL 128 가까워야 합니다.</br></br>Tracert를 사용 하 여 각 홉에서 대기 시간을 찾을 수 있습니다.    | 시간에 대 한 자세히 클럭 소스를 찾습니다.  하나의 솔루션은 동일한 세그먼트에 소스 시계를 설치 하거나 수동으로 지리적으로 가까운 소스 시계를 가리키도록 하는 것입니다.  도메인 시나리오에 대 한 GTimeServ 역할이 있는 컴퓨터를 추가 합니다. |  
NTP 소스를 안정적으로 연결할 수 없습니다.|    W32tm /stripchart "요청 시간 초과"이 일시적으로 반환    |NTP 원본이 되지 응답|
NTP 원본이 되지 응답|    NTP 클라이언트 소스 수 NTP 서버 들어오는 요청을 NTP 서버 보내는 응답에 대 한 성능 모니터 카운터를 확인 하 고 사용자 기준 비교 하 여 사용 현황을 결정 합니다.|    서버 성능 카운터를 사용 하 여 기준을 관련해 부하 변경 되었는지 여부를 결정 합니다.</br></br>사항이 네트워크 정체 문제의 있습니까?|
가장 정확한 시간을 사용 하지는 도메인 컨트롤러|    토폴로지 또는 최근에 추가 된 마스터 시간 클록에서 변경 됩니다.|   이 경우 w32tm /resync /rediscover|
클라이언트 시계는 유동| 시간 서비스 이벤트 36 다음을 설명 하는 로그 파일의 시스템 이벤트 로그 및/또는 텍스트 1에서 0으로 이동 하는 "NTP 클라이언트 시간 원본 수" 카운터|업스트림 원본 문제를 해결 하 고 성능 문제에 실행 되 고 있는지 이해 합니다.|

### <a name="baselining-time"></a>기준 지정 시간
먼저, 성능 및 네트워크의 정확도 이해 하 고 기준선 나중에 문제가 발생할 때 비교할 수 있도록 기준 지정이 중요 합니다.  싶어하는 초기 루트 PDC 또는 모든 컴퓨터는 GTIMESRV로 표시 합니다.  것도 좋습니다 모든 포리스트에 PDC 초기를 합니다.  마지막으로 중요 한 모든 Dc 또는 초기 거리 또는 부하가 높은 상황 등의 흥미로운 특징을 갖는 컴퓨터를 선택 해당 합니다.

이는 Windows server 2016 vs 2012 r 2를 기준으로 하는 경우에도 유용 하지만, Windows Server 2012R2 2에는 성능 카운터가 없으므로이를 비교 하는 데 사용할 수 있는 도구로는 w32tm/stripchart 있습니다.  동일한 특성을 가진 두 개의 컴퓨터를 선택 하거나 컴퓨터를 업그레이드 하 고 업데이트 후 결과 비교 해야 합니다.  Windows 시간 측정 추 록 2016과 2012 간의 측정을 수행 하는 방법에 대 한 자세한 내용은 있습니다.

모든 w32time 성능 카운터를 사용 하는 최소한 주에 대 한 데이터를 수집 합니다.  이 되도록 충분 한 시간에 따라 네트워크에서 다양 한 계정에 대 한 참조 및 실행 시간 정확도 안정적 임을 전반의 충분 합니다.

### <a name="ntp-server-redundancy"></a>NTP 서버 중복성
비-도메인 가입 된 컴퓨터 또는 PDC와 함께 사용할 수동 NTP 서버 구성에 대 한 개 이상의 서버는 가용성의 경우 중복성이 양호 측정값입니다.  또한 가정할 때 모든 원본이 정확 하 고 안정적인 정확성을 제공 합니다.  그러나 토폴로지를 잘 설계 되지 않거나 시간 원본은 안정적이 지는, 결과 정확도 될 수 더 심각한 되므로 주의 해야 합니다.  지원 되는 시간 서버 w32time 수동으로 참조할 수 제한은 10입니다. 

## <a name="leap-seconds"></a>윤 초
지구 회전 기간 climatic 및 geological 이벤트에 의해 발생 한 시간에 따라 달라 집니다. 일반적으로, 변형을 2 년 마다 약 1 초입니다. 원자성 시간의 변형이 너무 커질 때마다 1 초 (위 또는 아래로)의 수정 내용이 삽입 됩니다 (윤 초 라고 함). 차이 0.9 초를 초과 하지 않습니다 하는 방식으로 수행 됩니다. 이 수정은 실제 수정의 6 개월 전에 발표 됩니다. Windows Server 2016 하기 전에 Microsoft 시간 서비스 윤 초를 인식 하지 못했던 수 있지만이 확인 하는 외부 시간 서비스에서. Windows Server 2016의 증가 시간 정확도, Microsoft 윤 초 문제에 대 한 더 적합 한 솔루션에서 작동 합니다.

## <a name="secure-time-seeding"></a>보안 시간 시드
서버 2016의 W32time에는 보안 시간 시드 기능이 포함 되어 있습니다. 이 기능은 나가는 SSL 연결의 대략적인 현재 시간을 결정 합니다.  이 시간 값은 로컬 시스템 클록을 모니터링 하 고 총 오류를 수정 하는 데 사용 됩니다. [이 블로그 게시물](https://blogs.msdn.microsoft.com/w32time/2016/09/28/secure-time-seeding-improving-time-keeping-in-windows/)에서 기능에 대해 자세히 알아볼 수 있습니다.  시간 오프셋에 대 한 모니터링을 포함 하는 신뢰할 수 있는 시간 원본 및 잘 모니터링 되는 컴퓨터를 사용 하는 배포에서는 보안 시간 시드 기능을 사용 하지 않고 대신 기존 인프라를 사용 하도록 선택할 수 있습니다. 

다음 단계를 통해이 기능을 사용 하지 않도록 설정할 수 있습니다.

1.  특정 컴퓨터에서 UtilizeSSLTimeData 레지스트리 구성 값을 0으로 설정 합니다.

    reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\w32time\Config/v UtilizeSslTimeData/t REG_DWORD/d 0/f


2.  어떤 이유로 인해 컴퓨터를 즉시 다시 부팅할 수 없는 경우 W32time 서비스에 구성 업데이트에 대 한 알림을 보낼 수 있습니다. 이렇게 하면 SSL 연결에서 수집 된 시간 데이터를 기준으로 모니터링 및 적용 시간이 중지 됩니다. 

    W32tm/config/update

3.  컴퓨터를 다시 부팅 하면 설정이 즉시 적용 되며,이로 인해 SSL 연결에서 시간 데이터 수집이 중지 됩니다.  후자 부분은 매우 작은 오버 헤드를 가지 며 성능 문제가 되지 않습니다.

4.  전체 도메인에서이 설정을 적용 하려면 W32time 그룹 정책 설정의 UtilizeSSLTimeData 값을 0으로 설정 하 고 설정을 게시 하십시오.  그룹 정책 클라이언트에서이 설정을 선택 하면 W32time 서비스에 알림이 표시 되 고 SSL 시간 데이터를 사용 하 여 모니터링 및 적용 시간이 중지 됩니다. 각 컴퓨터가 다시 부팅 되 면 SSL 시간 데이터 수집이 중지 됩니다. 도메인에 휴대용 슬림형 노트북/태블릿 및 기타 장치가 있는 경우이 정책 변경에서 이러한 컴퓨터를 제외 하는 것이 좋습니다. 이러한 장치는 결국 배터리를 소모 하 고 시간을 부트스트랩 하기 위해 보안 시간 시드 기능이 필요 합니다.


