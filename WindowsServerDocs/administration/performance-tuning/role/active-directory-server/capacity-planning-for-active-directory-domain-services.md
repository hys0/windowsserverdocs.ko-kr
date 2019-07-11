---
title: Active Directory Domain Services를 위한 용량 계획
description: AD DS를 위한 용량 계획 중 고려해 야 할 요인의 자세히 설명 합니다.
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; kenbrunf
author: Teresa-Motiv
ms.date: 7/3/2019
ms.openlocfilehash: 5a9e2d39d4eedd1e8fdb4bfeaf267ad4cb4c596a
ms.sourcegitcommit: be243a92f09048ca80f85d71555ea6ee3751d712
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67799835"
---
# <a name="capacity-planning-for-active-directory-domain-services"></a>Active Directory Domain Services를 위한 용량 계획

이 항목에서는 박 단은 Brumfield, 수석 필드 엔지니어로 Microsoft에서 작성 한 원래 및 Active Directory Domain Services (AD DS)를 위한 용량 계획에 대 한 권장 사항을 제공 합니다.

## <a name="goals-of-capacity-planning"></a>용량 계획의 목표

용량 계획 동일 하지는 성능 문제를 해결 합니다. 이들은 밀접 한 관련이 있지만 상당히 다릅니다. 용량 계획의 목표는 다음과 같습니다.  

- 올바르게 구현 하 고 환경 작동 
- 성능 문제를 해결 하는 데 걸린 시간을 최소화 합니다.  
  
용량 계획, 조직 클라이언트 성능 요구 사항을 충족 하 고 데이터 센터의 하드웨어를 업그레이드 하는 데 필요한 시간을 수용 하기 위해 사용량이 많은 기간 중 40% 프로세서 사용률의 기준 대상이 있을 수 있습니다. 반면, 비정상적인 성능 문제에 대 한 알림을 수를 5 분 간격 모니터링 경고 임계값을 90%로 설정할 수 있습니다.

차이점은 용량 관리 임계값을 지속적으로 초과 되 면 (일회성 이벤트를 발생 하지 않습니다), (즉, 더 많은 또는 더 빠른 프로세서에서 추가) 용량 솔루션 것 또는 수는 여러 서버에서 서비스 확장 추가 솔루션입니다. 성능 경고 임계값 나타내고 클라이언트 환경을 포괄적 현재는 즉시 문제를 해결 하는데 사용 됩니다.

예를 들어도: (방어 driving, 브레이크 등, 제대로 작동 하는지 만들기) 하는 교통 사고를 방지 하는 방법에 대 한 용량 관리는 경찰, 화재 부서 및 응급 의료 전문가 수행할 작업은 성능 문제 해결 이후에 실수로 합니다. 이 "방어적 driving" 하는 방법에 대 한 Active Directory 스타일입니다.

지난 몇 년간 시스템 확장에 대 한 용량 계획 지침 크게 변경 되었습니다. 시스템 아키텍처의 다음 변경 내용을 설계 하 고 서비스를 확장 하는 방법에 대 한 기본 가정 요구 됩니다.

- 64 비트 서버 플랫폼  
- 가상화  
- 향상 된 주의 전력 소비를  
- SSD 저장소  
- 클라우드 시나리오  

또한 접근 방식은 서비스 기반 용량 계획 실행에 대 한 연습을 계획 하는 서버 기반 용량에서 변화 합니다. Active Directory Domain Services (AD DS)에서 여러 Microsoft 및 타사 제품을 백 엔드로 사용 하는 완성도 높은 분산된 서비스가 한 가장 중요 한 제품을 실행 하려면 다른 응용 프로그램에 필요한 용량이 되도록 올바르게 계획 합니다.

### <a name="baseline-requirements-for-capacity-planning-guidance"></a>용량 계획 지침에 대 한 초기 요구 사항

이 기사에서는 다음 기본 요구 될 수 있습니다.

- 판독기가 읽고 익숙한 [성능 튜닝 지침에 대 한 Windows Server 2012 R2](https://docs.microsoft.com/previous-versions//dn529133(v=vs.85))합니다.
- Windows Server 플랫폼은 x64 아키텍처를 기반으로 합니다. Active Directory 환경의 Windows Server 2003 x86 (이제 끝 다음의 지원 수명 주기)에 설치 되어 있고 디렉터리 정보 트리 (DIT) 하는 경우에 즉 적은 1.5GB 크기에서 및는 쉽게에 보관할 수 있습니다이 지침 메모리 하지만 문서에 적용할 수 있습니다.
- 용량 계획은 지속적인 프로세스 및 환경은 기대를 충족 하는 정도 정기적으로 검토 해야 합니다.
- 최적화는 하드웨어 비용의 변화에 따라 여러 하드웨어 수명 주기를 통해 발생 합니다. 예를 들어 메모리가 매우 저렴 한 코어당 비용이 감소 또는 다른 저장소의 가격 옵션을 변경 합니다.
- 오늘의 최대 사용량이 많은 기간에 대 한 계획입니다. 30 분 또는 시간 간격으로이 확인 하는 것이 좋습니다. 실제 최대치 및 작은 "일시적인 스파이크." 하 여 왜곡 될 수 있습니다를 가릴 수 큰 항목
- 엔터프라이즈를 위한 하드웨어 수명 주기 동안 증가 계획 합니다. 이 전략을 업그레이드 하거나 하드웨어를 완전히 새로 3 ~ 5 년 마다 시차를에 추가 포함할 수 있습니다. 각 Active Directory의 부하를 훨씬 증가 하는 방법에 따라 "추측" 해야 합니다. 기록 데이터를 수집 하는 경우에 도움이 됩니다이 평가 합니다. 
- 내결함성에 대 한 계획입니다. 예상 값을 한 번 *N* 파생 된 포함 하는 시나리오에 대 한 계획 *N* &ndash; 1 *N* &ndash; 2 *N* &ndash; *x*합니다.
  - 단일 또는 여러 서버의 손실 최대 최대 용량 예측을 초과 하지 않도록 하려면 조직의 필요에 따라 추가 서버에 추가 합니다.
  - 또한 증가 계획과 내결함성 계획 오류 통합 해야 하는 것이 좋습니다. 예를 들어, 부하를 지원 하려면 DC가 하나 필요 하지만 예상 되는 경우 부하 내년에는 두 배로 늘어나고 내결함성을 지원 하도록 충분 한 용량이 수 없습니다. 전체 Dc를 두 개 필요 합니다. 솔루션 세 Dc를 시작 하는 것입니다. 예산을 긴밀 하 게 되 면 3 또는 6 개월 후 세 번째 DC를 추가 하려면 수 하나입니다.

    >[!NOTE]
    >활성 디렉터리 인식 응용 프로그램을 추가 부하는 응용 프로그램 서버 또는 클라이언트에서 제공 되는지 여부를 DC 부하에 눈에 띄는 영향을 미칠 수 있습니다.

### <a name="three-step-process-for-the-capacity-planning-cycle"></a>용량 주기를 계획에 대 한 3 단계로 이루어진 프로세스

용량 계획에 먼저 어떤 품질의 서비스는 필요한 결정 합니다. 예를 들어, 핵심 데이터 센터는 더 높은 수준의 동시성이 지원 하며 보다 일관 된 환경을 사용자 및 중복성을 큰 주의 기울여야 하는 응용 프로그램 사용 및 시스템 및 인프라 병목 상태를 최소화 합니다. 이와 대조적으로 소수의 사용자를 사용 하 여 위성 위치 같은 수준의 동시성 또는 내결함성 필요는 없습니다. 따라서 위성 office 기본 하드웨어 및 비용 절감 시킬 수 있는 인프라를 최적화 하는 데 많은 주의가 필요 하지 있습니다. 모든 권장 사항 및 지침은 여기에 포함 된 최적의 성능을 위해서는 되며 덜 까다로운 요구 사항 사용 하 여 시나리오에 대 한 선택적으로 완화할 수 있습니다.

다음 질문은: 가상 또는 실제? 용량 계획 관점에서은 오른쪽 또는 잘못 된 응답이 없습니다. 방법이 다른 변수를 사용 하 여 작업의 집합입니다. 가상화 시나리오 귀결 됩니다 두 옵션 중 하나:

- 호스트 (가상화 존재 하는 서버에서 물리적 하드웨어를 추상화 하기 위한 용도로) 당 하나의 게스트를 사용 하 여 "직접 매핑"
- "공유 호스트"

테스트 및 프로덕션 시나리오 "직접 매핑" 시나리오를 실제 호스트에 동일 하 게 처리할 수 있음을 나타냅니다. 하지만 다양 한 고려 사항 자세히 나중에 명시 소개, "호스트를 공유" 합니다. "공유 호스트" 시나리오를 AD DS는 리소스에 대 한 경쟁도 저하 및 작업 튜닝 시 고려 사항 있음을 의미 합니다.

이러한 점 고려를 사용 하 여 용량 계획 주기는 반복적인 3 단계 프로세스:

1. 기존 환경을 측정 시스템 병목 현상을 현재 인 하 고 받을 있는 환경 기본 사항 필요한 용량을 계획 하는 데 필요한를 확인 합니다.
1. 1 단계에 설명 된 조건에 따라 필요한 하드웨어를 확인 합니다.
1. 모니터링 하 고 구현 된 대로 인프라 사양 내에서 작동 하는지 확인 합니다. 이 단계에서 수집 된 일부 데이터 용량 계획의 다음 주기에 대 한 기준이 됩니다.

### <a name="applying-the-process"></a>프로세스를 적용합니다.

성능을 최적화 하기 위해 이러한 주요 구성 요소는 올바르게 선택한 응용 프로그램 부하에 맞게 조정 해야 합니다.

1. 메모리
1. 네트워크
1. 스토리지
1. 프로세서
1. Net Logon

잘 작성 된 클라이언트 소프트웨어의 일반적인 동작 및 AD DS의 기본 저장소 요구 사항을 허용 용량 거의 모든 최신 서버와 실제 하드웨어와 관련 하 여 계획에 막대 한 투자를 하지 않게 하려면 만큼 10,000 20,000 사용자 환경 클래스 시스템 부하를 처리 합니다. 즉, 다음 표에서 올바른 하드웨어를 선택 하려면 기존 환경을 평가 하는 방법입니다. 각 구성 요소를 AD DS 관리자가 기준 권장 사항 및 환경의 특정 보안 주체를 사용 하 여 해당 인프라를 평가할 수 있도록 후속 섹션에서 자세히 분석 합니다.

일반적으로:

- 현재 데이터를 기반으로 하는 모든 크기 조정에서 현재 환경에 정확 하 게 됩니다.
- 모든 예측에 대 한 수요를 예상 하드웨어의 수명 주기 동안 증가 합니다.
- 지금 초과에 있는지 여부를 확인 하 및 대규모 환경으로 확장 하거나 수명 주기를 통해 용량을 추가 합니다.
- 가상화에 대 한 모두 동일한 보안 주체 및 방법론을 계획 하는 용량 적용, 점을 제외 하 고 가상화 오버 헤드와 관련 된 도메인 값으로 추가 해야 합니다.
- 용량 계획, 예측 하려고 하는 요소와 마찬가지로 정확 하 게 과학 아닙니다. 완벽 하 게 및 100% 정확도로 계산 하는 작업을 기다리지는 않습니다. 여기이 가이드는 leanest 것이 좋습니다. 보안 강화에 대 한 용량에 추가 하 고 지속적으로 환경을 대상에 남아 있는지를 확인 합니다.

### <a name="data-collection-summary-tables"></a>데이터 컬렉션의 요약 테이블

#### <a name="new-environment"></a>새 환경

| 구성 요소 | 예상 값 |
|-|-|
|저장소/데이터베이스 크기|각 사용자에 대 한 60KB으로 40KB-|
|RAM|데이터베이스 크기<br />기본 운영 체제의 권장 사항<br />타사 응용 프로그램|
|네트워크|1GB|
|CPU|각 코어에 대해 1000 명의 동시 사용자|

#### <a name="high-level-evaluation-criteria"></a>상위 수준 평가 조건

| 구성 요소 | 평가 조건 | 계획 시 고려 사항 |
|-|-|-|
|저장소/데이터베이스 크기|조각 모음이 해제 된 디스크 공간 로깅 활성화 "를"에 관해서는 [저장소 제한](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10))| |
|저장소 성능 데이터베이스|<ul><li>"논리 디스크 ( *\<NTDS 데이터베이스 드라이브\>* ) \Avg Disk sec/Read," "논리 디스크 ( *\<NTDS 데이터베이스 드라이브\>* ) \Avg Disk sec/Write," " 논리 디스크 ( *\<NTDS 데이터베이스 드라이브\>* ) \Avg Disk sec/Transfer "</li><li>"LogicalDisk( *\<NTDS Database Drive\>* )\Reads/sec," "LogicalDisk( *\<NTDS Database Drive\>* )\Writes/sec," "LogicalDisk( *\<NTDS Database Drive\>* )\Transfers/sec"</li></ul>|<ul><li>저장소의 주소로 두 문제<ul><li>사용 가능한 공간, 오늘날의 기반으로 하는 스핀 들 및 SSD의 크기를 사용 하 여 저장소를 기반으로 하는 대부분의 AD 환경에 대 한 관련이 없습니다.</li> <li>입/출력 (IO) 작업 다양 한 환경에서 사용할 수 있습니다이 방식은 간과 됩니다. 환경에만 평가 해야 하지만 충분 한 RAM 메모리에 NTDS 데이터베이스 전체를 로드할 수 없는 경우.</li></ul><li>저장소는 복잡 한 항목 수 및 적절 한 크기 조정에 대 한 하드웨어 공급 업체 전문성을 참여 시켜야 합니다. 특히 시나리오로 더 복잡 한 iSCSI 시나리오, SAN 및 NAS, 등입니다. 그러나 일반적으로 기가바이트 단위의 저장소 비용 경우가 직접 반대인 IO 당 비용:<ul><li>RAID 5는 Raid 1 보다 기가바이트당 비용이 낮은 되었지만 Raid 1 IO 당 더 낮은 비용</li><li>하드 드라이브 스핀 들 기반 기가바이트당, 저렴 한 비용 있지만 Ssd IO 당 더 낮은 비용</li></ul><li>컴퓨터 또는 Active Directory Domain Services를 다시 시작 후 엔진 ESE (Extensible Storage) 캐시가 비어 있는 및 성능에는 디스크 캐시 지남에 하는 동안 바인딩된 됩니다.</li><li>대부분의 환경에서 AD 읽기 캐싱의 이점이 많은 부정 디스크에 임의 패턴에서 집약적인 I/O 이며 최적화 전략을 읽습니다.  또한 AD 대부분의 저장소 시스템 캐시 보다 메모리의 방식으로 더 큰 캐시를 있습니다.</li></ul>
|RAM|<ul><li>데이터베이스 크기</li><li>기본 운영 체제의 권장 사항</li><li>타사 응용 프로그램</li></ul>|<ul><li>저장소는 컴퓨터에서 가장 느린 구성 요소입니다. 보다 RAM에 상주 될 수 있습니다, 그리고 디스크로 이동 하는 데 필요한 것은 줄어듭니다.</li><li>운영 체제에 에이전트 (바이러스 백신, 백업, 모니터링)을 저장할 충분 한 RAM은 할당 하기 위해 NTDS 데이터베이스 및 시간이 지남에 따라 증가 합니다.</li><li>Ram 크기를 최대화 하지 않은 환경에 대 한 비용 (예: 위성 위치) 유효한 또는 적합 하지 않은 경우 (DIT은 너무 큼), 해당 저장소를 확인 하려면 [저장소] 섹션 크기가 제대로 참조 합니다.</li></ul>|
|네트워크|<ul><li>“Network Interface(\*)\Bytes Received/sec”</li><li>“Network Interface(\*)\Bytes Sent/sec”|<ul><li>일반적으로 훨씬 DC에서 전송 되는 트래픽이 DC로 전송 되는 트래픽을 초과 합니다.</li><li>전환 된 이더넷 연결 전이중 그대로 인바운드 및 아웃 바운드 네트워크 트래픽을 독립적으로 조정 해야 합니다.</li><li>수를 통합 Dc의 각 DC에 대 한 클라이언트 요청에 다시 응답을 전송 하는 데 사용 되는 대역폭의 양을 증가 하지만 전체 사이트에 대 한 선형 수 있을 만큼 가까이 됩니다.</li><li>위성 위치 Dc를 제거 하는 경우 위성 DC Dc 허브에 대 한 대역폭을 추가할 수 있을 뿐만 아니라 WAN 트래픽 양이 됩니다 평가 사용할 것을 잊지 마세요.</li></ul>|
|CPU“Logical Disk( *\<NTDS Database Drive\>* )\Avg Disk sec/Read”descripti"Process(lsass)\\' Processor Time"tors to consider during capacity planning for AD DS.
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; kenbrunf
author: Teresa-Motiv
ms.date: 7/3/2019
---

# Capacity planning for Active Directory Domain Services

This topic is originally written by Ken Brumfield, Senior Premier Field Engineer at Microsoft, and provides recommendations for capacity planning for Active Directory Domain Services (AD DS).

## Goals of capacity planning

Capacity planning is not the same as troubleshooting performance incidents. They are closely related, but quite different. The goals of capacity planning are:  

- Properly implement and operate an environment 
- Minimize the time spent troubleshooting performance issues.  
  
In capacity planning, an organization might have a baseline target of 40% processor utilization during peak periods in order to meet client performance requirements and accommodate the time necessary to upgrade the hardware in the datacenter. Whereas, to be notified of abnormal performance incidents, a monitoring alert threshold might be set at 90% over a 5 minute interval.

The difference is that when a capacity management threshold is continually exceeded (a one-time event is not a concern), adding capacity (that is, adding in more or faster processors) would be a solution or scaling the service across multiple servers would be a solution. Performance alert thresholds indicate that client experience is currently suffering and immediate steps are needed to address the issue.

As an analogy: capacity management is about preventing a car accident (defensive driving, making sure the brakes are working properly, and so on) whereas performance troubleshooting is what the police, fire department, and emergency medical professionals do after an accident. This is about “defensive driving,” Active Directory-style.

Over the last several years, capacity planning guidance for scale-up systems has changed dramatically. The following changes in system architectures have challenged fundamental assumptions about designing and scaling a service:

- 64-bit server platforms  
- Virtualization  
- Increased attention to power consumption  
- SSD storage  
- Cloud scenarios  

Additionally, the approach is shifting from a server-based capacity planning exercise to a service-based capacity planning exercise. Active Directory Domain Services (AD DS), a mature distributed service that many Microsoft and third-party products use as a backend, becomes one the most critical products to plan correctly to ensure the necessary capacity for other applications to run.

### Baseline requirements for capacity planning guidance

Throughout this article, the following baseline requirements are expected:

- Readers have read and are familiar with [Performance Tuning Guidelines for Windows Server 2012 R2](https://docs.microsoft.com/previous-versions//dn529133(v=vs.85)).
- The Windows Server platform is an x64 based architecture. But even if your Active Directory environment is installed on Windows Server 2003 x86 (now beyond the end of the support lifecycle) and has a directory information tree (DIT) that is less 1.5 GB in size and that can easily be held in memory, the guidelines from this article are still applicable.
- Capacity planning is a continuous process and you should regularly review how well the environment is meeting expectations.
- Optimization will occur over multiple hardware lifecycles as hardware costs change. For example, memory becomes cheaper, the cost per core decreases, or the price of different storage options change.
- Plan for the peak busy period of the day. It is recommended to look at this in either 30 minute or hour intervals. Anything greater may hide the actual peaks and anything less may be distorted by “transient spikes.”
- Plan for growth over the course of the hardware lifecycle for the enterprise. This may include a strategy of upgrading or adding hardware in a staggered fashion, or a complete refresh every three to five years. Each will require a “guess” as how much the load on Active Directory will grow. Historical data, if collected, will help with this assessment. 
- Plan for fault tolerance. Once an estimate *N* is derived, plan for scenarios that include *N* &ndash; 1, *N* &ndash; 2, *N* &ndash; *x*.
  - Add in additional servers according to organizational need to ensure that the loss of a single or multiple servers does not exceed maximum peak capacity estimates.
  - Also consider that the growth plan and fault tolerance plan need to be integrated. For example, if one DC is required to support the load, but the estimate is that the load will be doubled in the next year and require two DCs total, there will not be enough capacity to support fault tolerance. The solution would be to start with three DCs. One could also plan to add the third DC after 3 or 6 months if budgets are tight.

    >[!NOTE]
    >Adding Active Directory-aware applications might have a noticeable impact on the DC load, whether the load is coming from the application servers or clients.

### Three-step process for the capacity planning cycle

In capacity planning, first decide what quality of service is needed. For example, a core datacenter supports a higher level of concurrency and requires more consistent experience for users and consuming applications, which requires greater attention to redundancy and minimizing system and infrastructure bottlenecks. In contrast, a satellite location with a handful of users does not need the same level of concurrency or fault tolerance. Thus, the satellite office might not need as much attention to optimizing the underlying hardware and infrastructure, which may lead to cost savings. All recommendations and guidance herein are for optimal performance, and can be selectively relaxed for scenarios with less demanding requirements.

The next question is: virtualized or physical? From a capacity planning perspective, there is no right or wrong answer; there is only a different set of variables to work with. Virtualization scenarios come down to one of two options:

- “Direct mapping” with one guest per host (where virtualization exists solely to abstract the physical hardware from the server)
- “Shared host”

Testing and production scenarios indicate that the “direct mapping” scenario can be treated identically to a physical host. “Shared host,” however, introduces a number of considerations spelled out in more detail later. The “shared host” scenario means that AD DS is also competing for resources, and there are penalties and tuning considerations for doing so.

With these considerations in mind, the capacity planning cycle is an iterative three-step process:

1. Measure the existing environment, determine where the system bottlenecks currently are, and get environmental basics necessary to plan the amount of capacity needed.
1. Determine the hardware needed according to the criteria outlined in step 1.
1. Monitor and validate that the infrastructure as implemented is operating within specifications. Some data collected in this step becomes the baseline for the next cycle of capacity planning.

### Applying the process

To optimize performance, ensure these major components are correctly selected and tuned to the application loads:

1. Memory
1. Network
1. Storage
1. Processor
1. Net Logon

The basic storage requirements of AD DS and the general behavior of well written client software allow environments with as many as 10,000 to 20,000 users to forego heavy investment in capacity planning with regards to physical hardware, as almost any modern server class system will handle the load. That said, the following table summarizes how to evaluate an existing environment in order to select the right hardware. Each component is analyzed in detail in subsequent sections to help AD DS administrators evaluate their infrastructure using baseline recommendations and environment-specific principals.

In general:

- Any sizing based on current data will only be accurate for the current environment.
- For any estimates, expect demand to grow over the lifecycle of the hardware.
- Determine whether to oversize today and grow into the larger environment, or add capacity over the lifecycle.
- For virtualization, all the same capacity planning principals and methodologies apply, except that the overhead of the virtualization needs to be added to anything domain related.
- Capacity planning, like anything that attempts to predict, is NOT an accurate science. Do not expect things to calculate perfectly and with 100% accuracy. The guidance here is the leanest recommendation; add in capacity for additional safety and continuously validate that the environment remains on target.

### Data collection summary tables

#### New environment

| Component | Estimates |
|-|-|
|Storage/Database Size|40 KB to 60 KB for each user|
|RAM|Database Size<br />Base operating system recommendations<br />Third-party applications|
|Network|1 GB|
|CPU|1000 concurrent users for each core|

#### High-level evaluation criteria

| Component | Evaluation criteria | Planning considerations |
|-|-|-|
|Storage/Database size|The section entitled “To activate logging of disk space that is freed by defragmentation” in [Storage Limits](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10))| |
|Storage/ Database performance|<ul><li>"LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read," "LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Write," "LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Transfer"</li><li>"LogicalDisk(*\<NTDS Database Drive\>*)\Reads/sec," "LogicalDisk(*\<NTDS Database Drive\>*)\Writes/sec," "LogicalDisk(*\<NTDS Database Drive\>*)\Transfers/sec"</li></ul>|<ul><li>Storage has two concerns to address<ul><li>Space available, which with the size of today’s spindle based and SSD based storage is irrelevant for most AD environments.</li> <li>Input/Output (IO) Operations available – In many environments, this is often overlooked. But it is important to evaluate only environments where there is not enough RAM to load the entire NTDS Database into memory.</li></ul><li>Storage can be a complex topic and should involve hardware vendor expertise for proper sizing. Particularly with more complex scenarios such as SAN, NAS, and iSCSI scenarios. However, in general, cost per Gigabyte of storage is often in direct opposition to cost per IO:<ul><li>RAID 5 has lower cost per Gigabyte than Raid 1, but Raid 1 has lower cost per IO</li><li>Spindle-based hard drives have lower cost per Gigabyte, but SSDs have a lower cost per IO</li></ul><li>After a restart of the computer or the Active Directory Domain Services service, the Extensible Storage Engine (ESE) cache is empty and performance will be disk bound while the cache warms.</li><li>In most environments AD is read intensive I/O in a random pattern to disks, negating much of the benefit of caching and read optimization strategies.  Plus, AD has a way larger cache in memory than most storage system caches.</li></ul>
|RAM|<ul><li>Database size</li><li>Base operating system recommendations</li><li>Third-party applications</li></ul>|<ul><li>Storage is the slowest component in a computer. The more that can be resident in RAM, the less it is necessary to go to disk.</li><li>Ensure enough RAM is allocated to store the operating system, Agents (antivirus, backup, monitoring), NTDS Database and growth over time.</li><li>For environments where maximizing the amount of RAM is not cost effective (such as a satellite locations) or not feasible (DIT is too large), reference the Storage section to ensure that storage is properly sized.</li></ul>|
|Network|<ul><li>“Network Interface(\*)\Bytes Received/sec”</li><li>“Network Interface(\*)\Bytes Sent/sec”|<ul><li>In general, traffic sent from a DC far exceeds traffic sent to a DC.</li><li>As a switched Ethernet connection is full-duplex, inbound and outbound network traffic need to be sized independently.</li><li>Consolidating the number of DCs will increase the amount of bandwidth used to send responses back to client requests for each DC, but will be close enough to linear for the site as a whole.</li><li>If removing satellite location DCs, don’t forget to add the bandwidth for the satellite DC into the hub DCs as well as use that to evaluate how much WAN traffic there will be.</li></ul>|
|CPU|<ul><li>“Logical Disk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read”</li><li>“Process(lsass)\\% Processor Time”</li></ul>|<ul><li>병목 상태 저장소를 제거한 후 필요한 계산 능력의 양에 해결 합니다.</li><li>완벽 하 게 선형이 아닌, 하는 동안 (예: 사이트) 특정 범위에 있는 모든 서버에서 사용 하는 프로세서 코어 수가 얼마나 많은 프로세서는 총 클라이언트 부하를 지 원하는 데 필요한 측정을 사용할 수 있습니다. 현재 서비스 수준의 범위 내에서 모든 시스템에서 유지 관리 하는 데 필요한 최소를 추가 합니다.</li><li>프로세서 속도, 전원 관리를 포함 하 여 변경 관련 변경 내용, 현재 환경에서 파생 된 영향을 줄 번호입니다. 일반적으로 2.5ghz 프로세서에서 진행 중인 3ghz 프로세서에 필요한 Cpu의 수를 줄일 수 방법을 정확 하 게 평가할 수 아닙니다.</li></ul>|
|NetLogon|<ul><li>“Netlogon(\*)\Semaphore Acquires”</li><li>“Netlogon(\*)\Semaphore Timeouts”</li><li>“Netlogon(\*)\Average Semaphore Hold Time”</li></ul>|<ul><li>Net Logon 보안 채널/MaxConcurrentAPI PAC 유효성 검사 및/또는 NTLM 인증을 사용 하 여 환경을만 영향을 줍니다. PAC 유효성 검사는 Windows Server 2008 이전 운영 체제 버전에서 기본적으로 켜져 있습니다. 이므로 클라이언트 설정, dc가이 끌 때까지 모든 클라이언트 시스템에 영향을 받습니다.</li><li>내부 포리스트 트러스트를 포함 하는 중요 한 상호 트러스트 인증을 사용 하 여 환경 큰 위험이 그렇지 않은 경우 적절 한 크기로 조정 합니다.</li><li>서버 통합 간 트러스트 인증의 동시성이 증가 합니다.</li><li>사용자를 새 클러스터 노드에 집단 다시 인증 하는 대로 급증 동반 되는 클러스터 장애 조치 등 필요 합니다.</li><li>개별 클라이언트 시스템 (예: 클러스터)는 너무 튜닝 해야 할 수 있습니다.</li></ul>|

## <a name="planning"></a>계획

오랜 시간 동안, AD DS를 크기 조정에 대 한 커뮤니티의 권장 사항 되었으므로 "데이터베이스 크기와 많은 RAM에 저장 합니다." 대부분의 경우 권장 사항 인지는 대부분의 환경에 대 한 고려 필요 합니다. 하지만 AD DS를 사용 하는 에코 시스템을 해달라는 훨씬 더 큰 1999 년에 소개 된 이후로 AD DS 환경 자체가 동일 합니다. 하지만 계산 능력 및 x86에서 스위치를 늘리는 아키텍처에는 실제 하드웨어 가상화의 증가에 AD DS를 실행 하는 고객의 큰 집합에 관련이 없는 성능에 대 한 크기 조정의 미묘한 측면을 수행한 x64로 아키텍처 이전 보다 광범위 한 대상에 튜닝 문제를 다시 추가 합니다.

다음 지침을 확인 하 고 실제, 가상/실제 조합 또는 순수 하 게 가상화 된 경우 배포 되었는지 여부에 관계 없이 서비스로 Active Directory의 요구를 계획 하는 방법에 대 한 따라서 됩니다. 따라서 네 가지 기본 구성의 각 평가 분류 됩니다: 저장소, 메모리, 네트워크 및 프로세서입니다. 즉, AD DS에서 성능을 최대화 하기 위해 최대한 바인딩된 프로세서에 가깝게를 가져오려는 목표가입니다.

## <a name="ram"></a>RAM

더는 캐시할 수 있는 RAM, 단순히 디스크로 이동 해야 하는 덜 합니다. RAM의 최소 크기는 서버의 확장성을 최대화 하기 위해는 현재 데이터베이스 크기, 전체 SYSVOL 크기, 운영 체제의 합 권장 양과 (바이러스 백신, 모니터링, 백업 및 등 에이전트에 대 한 공급 업체 권장 ). 추가 된 서버 수명 동안 증가 맞게 추가 되어야 합니다. 이 경전철 주관적 일의 환경 변화에 따라 데이터베이스 증가 예측을 기준으로 합니다.

Ram 크기를 최대화 하지 않은 환경에 대 한 비용 (예: 위성 위치) 유효한 또는 적합 하지 않은 경우 (DIT은 너무 큼), 해당 저장소를 확인 하려면 [저장소] 섹션은 제대로 참조 합니다.

메모리 크기를 조정 하는 일반 컨텍스트에서 제공 하는 필연적인 결과로, 페이지 파일의 크기 조정 됩니다. 메모리 관련, 다른 모든 요소와 동일한 컨텍스트에서 목표 하려는 훨씬 더 느리게 디스크를 최소화 하는 것입니다. 따라서 질문 해야에서 이동, "어떻게 페이지 파일 크기를 조정 하 시겠습니까?" "RAM의 양을 페이징을 최소화 하는 데 필요한가?"를 두 번째 질문에 대 한 답이이 섹션의 나머지 부분에 나와 있습니다. 이렇게 하면 대부분의 일반 운영 체제의 권장 사항 및 AD DS 성능에 관련 되지 않는 메모리 덤프에 대 한 시스템을 구성 해야 영역 페이지 파일 크기 조정에 대 한 토론 합니다.

### <a name="evaluating"></a>Evaluating

도메인 컨트롤러 (DC)가 필요한 RAM의 이러한 이유로 실제로 복잡 한 작업은 다음과 같습니다.

- LSASS 메모리 부족 상황에서 잘라야 합니다 인위적 필요 deflating와 RAM의 양이 필요한 계기를 기존 시스템을 사용 하려고 하면 오류가 발생할 가능성이 높습니다.
- 새로운 기능 "흥미로운" 클라이언트에 캐시 하는 개별 DC 필요 함을 주관적인 사실입니다. 이 Exchange server 사용 하 여 사이트의 DC에 캐시 되어야 하는 데이터가 사용자를 인증 하는 DC에 캐시 되어야 하는 데이터는 매우 다르게 된다는 것을 의미 합니다.
- 노동 상황별으로에 각 DC에 대 한 RAM을 평가 하는 편이 하 고 환경 변경 사항으로 변경 합니다.
- 권장 사항 뒤 조건이 합리적인된 결정을 내리는 데 도움이 됩니다. 
- 더는 캐시할 수 있는 RAM을 디스크로 이동 하는 데 필요한 것 덜 합니다. 
- 저장소는 지금까지 컴퓨터의 가장 느린 구성 요소입니다. 액세스 스핀 들을 기반으로 데이터를 SSD 저장소 미디어 시간은 1,000,000 x RAM의 데이터에 대 한 액세스 보다 느립니다.

따라서 서버에 RAM의 최소 크기의 확장성을 최대화 하기 위해 현재 데이터베이스 크기, 전체 SYSVOL 크기, 운영 체제의 합 권장 양과 (바이러스 백신, 모니터링, 백업, 에이전트에 대 한 공급 업체 권장 사항 등에)입니다. 서버 수명 동안 증가 맞게 추가 금액을 추가 합니다. 이 경전철 주관적 일 데이터베이스 증가 예측을 기준으로 합니다. 그러나 최종 사용자의 작은 집합으로 위성 위치에 대 한 이러한 요구 사항은 완화 될 수 있습니다 이러한 사이트는 필요가 캐시에 최대한 대부분의 요청을 서비스 합니다.

Ram 크기를 최대화 하지 않은 환경에 대 한 비용 (예: 위성 위치) 유효한 또는 적합 하지 않은 경우 (DIT은 너무 큼), 해당 저장소를 확인 하려면 [저장소] 섹션 크기가 제대로 참조 합니다.

> [!NOTE]
> 메모리 크기를 조정 하는 동안 그 결과 페이지 파일의 크기 조정 합니다. 질문 "어떻게 페이지 파일 크기를 조정 하 시겠습니까?"에서 이동 하려는 훨씬 더 느리게 디스크를 최소화 하기 위해 목표 이기 때문에 "RAM의 양을 페이징을 최소화 하는 데 필요한가?"를 두 번째 질문에 대 한 답이이 섹션의 나머지 부분에 나와 있습니다. 이렇게 하면 대부분의 일반 운영 체제의 권장 사항 및 AD DS 성능에 관련 되지 않는 메모리 덤프에 대 한 시스템을 구성 해야 영역 페이지 파일 크기 조정에 대 한 토론 합니다.

### <a name="virtualization-considerations-for-ram"></a>RAM에 대 한 가상화 고려 사항

호스트에서 과도 한 커밋 메모리를 방지 합니다. 기본 목적은 RAM의 양을 최적화 디스크로 이동 하는 데 걸린 시간을 최소화 하는 것입니다. 가상화 시나리오에서 과도 한 메모리 커밋 개념이 더 많은 RAM 게스트는 할당할 존재 다음 물리적 컴퓨터에 존재 합니다. 이 자체는 문제가 되지 않습니다. 호스트의 RAM 용량을 초과 하는 모든 게스트에서 현재 사용 중인 전체 메모리 및 페이징을 시작 하는 기본 호스트 하는 경우 문제가 됩니다. 성능이 디스크 바인딩된 경우에 데이터를 가져오는 NTDS.dit 하려는 도메인 컨트롤러 또는 도메인 컨트롤러 파일로 데이터를 가져오는 것 또는 호스트 디스크 RAM의 게스트 판단 하는 데이터를 가져오는 것입니다.

### <a name="calculation-summary-example"></a>계산 요약 예제

|구성 요소|예상된 메모리 (예:)|
|-|-|
|기본 운영 체제 (Windows Server 2008) RAM 권장|2GB|
|LSASS 내부 작업|200MB|
|모니터링 에이전트|100MB|
|바이러스 백신|100MB|
|데이터베이스 (글로벌 카탈로그)|8.5GB 시겠습니까???|
|영향을 주지 않고 로그온 할 관리자를 실행 하려면 백업 장치|1GB|
|Total|12GB|

**권장: 16GB**

시간이 지남에 따라 데이터베이스에 추가할 더 많은 데이터를 서버 3 ~ 5 년 동안 프로덕션 환경에서 가능성이 가정을 만들 수 있습니다. 33% 증가 예상에 따라 16GB 것에 적절 한 양의 RAM 물리적 서버에 배치 합니다. 가상 컴퓨터에서 지정 된 설정을 수정할 수와 RAM을 VM에 추가할 수 용이성 계획을 모니터링 하 고 나중에 업그레이드를 사용 하 여 12GB부터 적합 합니다.

## <a name="network"></a>네트워크

### <a name="evaluating"></a>Evaluating
이 섹션을 사용 하면 WAN을 트래버스하는 트래픽에 대 포커스가 하며 철저 하 게에 대해서는 복제 트래픽에 대 한 요구를 평가 하는 방법에 대 한 작습니다 [Active Directory 복제 트래픽을](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10))합계를 계산 하는 방법에 대 한 것 보다, 클라이언트 쿼리, 그룹 정책 응용 프로그램 및 등을 포함 하 여 필요한 대역폭 및 네트워크 용량입니다. 성능 카운터를 사용 하 여 수집 될이 기존 환경에 대 한 "네트워크 인터페이스 (\*) \Bytes Received/sec" 및 "네트워크 인터페이스 (\*) \Bytes Sent/sec." 15, 30 일 또는 60 분 후에 네트워크 인터페이스 카운터에 대 한 샘플 간격입니다. 아무 것도 작은 일반적으로 더 좋은 측정 단위가 미터법 이면 너무 volatile 에 대해서는 매끄럽게 일일 피킹 과도 하 게 합니다.

> [!NOTE]
> 일반적으로 DC 클라이언트 쿼리에 응답 하는 대로 대부분의 DC에서 네트워크 트래픽 아웃 바운드 됩니다. 또한 각 환경에 대 한 인바운드 트래픽 평가 하는 것이 좋습니다. 하지만 아웃 바운드 트래픽을 포커스에 대 한 이유입니다. 인바운드 네트워크 트래픽 요구 사항을 검토 및 해결 방법과 동일한 방법은 사용할 수 있습니다. 자세한 내용은 기술 자료 문서를 참조 하세요. [929851: TCP/IP에 대 한 기본 동적 포트 범위에 Windows Server 2008 및 Windows Vista에서 변경](http://support.microsoft.com/kb/929851)합니다.

### <a name="bandwidth-needs"></a>대역폭 요구 사항

두 개의 고유 범주를 포함 하는 네트워크 확장성에 대 한 계획: 네트워크 트래픽에서 트래픽 양 및 CPU에 로드 합니다. 이러한 각 시나리오는이 문서의 다른 항목 중 일부에 비해 간단 합니다.

지원 해야 하는 트래픽 양을 평가는 네트워크 트래픽 측면에서 AD DS를 위한 용량 계획의 두 고유 범주가 있습니다. 첫 번째는 도메인 컨트롤러 간의 순회 하 고 참조에서 철저 하 게 설명 하는 복제 트래픽과 [Active Directory 복제 트래픽을](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10)) 및 현재 버전의 AD DS와 여전히 관련이 있습니다. 두 번째는 사이트 간 클라이언트와 서버 간 트래픽입니다. 사이트 간 트래픽에 대 한 계획을 주로 간단한 시나리오 중 하나는 많은 양의 데이터를 클라이언트로 다시 전송 기준으로 클라이언트에서 작은 요청을 받습니다. 일반적으로 100MB 5,000 명의 사용자가 사이트에는 서버당 최대 환경에서 적절 한 수 있습니다. 1GB 네트워크 어댑터 및 수신 RSS (수신측 배율)를 사용 하 여 지원 5,000 명의 사용자가 위의 어떤 항목도에 권장 됩니다. 서버 통합 시나리오의 경우 특히이 시나리오의 유효성을 검사 하려면 네트워크 인터페이스 확인 (\*) 사이트에 있는 모든 Dc에서 \Bytes/sec 함께 추가 하 고 확인 하는 도메인 컨트롤러의 대상 수로 나눕니다 적절 한 용량이입니다. 이 작업을 수행 하는 가장 쉬운 방법은 동일한 확장할 수 있도록 모든 카운터 Windows 안정성 및 성능 모니터 (Perfmon 이전의 함)를 "누적 영역형" 뷰를 사용 하는 합니다.

다음 예제에서는 (라고도 실제로 일반적인 규칙은 특정 환경에 적용할 수 있는지 유효성을 검사 하는 매우 복잡 한 방법). 다음과 같이 가정이 됩니다.

- 목표 최대한 적은 서버에 필요한 공간을 줄이는 것입니다. 이상적으로 서버만 부하를 수행 하 고 추가 서버 중복성을 위해 배포 됩니다 (*N* + 1 시나리오). 
- 이 시나리오에서는 현재 네트워크 어댑터만 100MB를 지원 하며 전환 된 환경에서입니다.  
  최대 대상 네트워크 대역폭 사용량은 N 시나리오 (DC 손실)에서 60%입니다.
- 각 서버에 연결 된 약 10,000 개 클라이언트에 있습니다.

차트의 데이터에서 얻은 (네트워크 인터페이스 (\*) \Bytes Sent/sec).

1. 영업일 간다면 홍수와 바람 약 5시 30분 아래로 오후 7 시에 시작 합니다.
1. 오전 8 시에서 오전 8시 15분, 25 보낸 바이트/초 가장 많이 사용 되는 DC에 보다 클 경우 사용량이 최대치가 됩니다.  
   > [!NOTE]
   > 모든 성능 데이터를 기록 합니다. 따라서 최대 데이터 지점 8시 15분 8:15 8시 부하를 나타냅니다.
1. 오전 4:00, 20 바이트/sec 가장 많이 사용 되는 DC에 보다 사용 하 여 백업 등의 인프라 작업을 백그라운드 되거나 다른 표준 시간대에서 로드 중 하나를 나타낼 수 있는 전에 스파이크가 있습니다. 이 작업을 초과 하는 오전 8 시에 최고 되므로 관련이 없습니다.
1. 사이트에 도메인 컨트롤러를 5 개 있습니다.
1. 최대 부하가 당 100MB 연결의 44%를 나타내는 DC에 대 한 5.5 MB/s를 보여 줍니다. 이 데이터를 사용 하 고 예상할 수 있습니다. 오전 8 시와 오전 8 시 15 간에 필요한 총 대역폭 28 MB/s는 합니다.
   >[!NOTE]
   >카운터를 송수신 하는 네트워크 인터페이스에에서 있는 바이트 네트워크 대역폭은 비트 단위로 측정 된 팩트를 사용 하 여 주의 해야 합니다. 100MB &divide; 8 = 12.5, 1GB &divide; 8 = 128MB입니다.
  
결론:

1. 현재이 환경에는 내결함성 대상 사용률이 60%의 N + 1 수준을 충족 합니다. 단일 시스템을 오프 라인 5.5에 대 한 MB/s (44%)에서 서버 당 대역폭을 이동 합니다. 약 7 MB/s (56%).
1. 최대 목표 사용률 및 이론적으로 100MB 연결의 가능한 사용률 초과 하나의 서버로 통합의 이전에 언급 된 목표에 따라이 둘 다 합니다.
1. 1GB 연결이 총 용량의 22% 나타냅니다 됩니다.
1. 일반 작동 조건에는 *N* + 1 시나리오에서는 클라이언트 부하가 서버 또는 총 용량의 11% 당 약 14 MB/s에서 상대적으로 균일 하 게 분산 될 합니다.
1. 용량은 적절 한 DC 사용할 수 없게 하는 동안 일반 운영 대상 서버당 약 30 가지의 것 되도록 하려면 % 사용률 또는 서버당 38 MB/s 네트워크입니다. 장애 조치 대상 서버당 72 초당 또는 네트워크 사용률이 60% 것입니다.  
  
즉, 시스템의 최종 배포 1GB 네트워크 어댑터가 있어야 및 언급된 부하에서 지원 되는 네트워크 인프라를 연결 합니다. 추가 참고는 생성 된 네트워크 트래픽 양, 지정 된 네트워크 통신에서 CPU 부하를 수 상당한 영향을 미칠 AD DS의 최대 확장성 제한입니다. DC에 인바운드 통신의 크기를 추정 하려면이 동일한 프로세스를 사용할 수 있습니다. 하지만 인바운드 트래픽 기준으로 아웃 바운드 트래픽의 일 경우에 대부분의 환경에 대 한 교육 연습 합니다. RSS에 대 한 하드웨어 지원을 보장 하는 것이 서버당 5,000 명의 사용자가 보다 큰 환경에서 중요 합니다. 네트워크 트래픽이 많은 시나리오에 대 한 인터럽트 부하 분산을 병목 지점이 될 수 있습니다. 프로세서를 검색할 수 있습니다 (\*)\% 인터럽트 시간 비율 Cpu 간에 고르게 분산 되 고 있습니다. RSS 사용 Nic 이러한 제한을 완화 하 고 확장성을 높일 수 있습니다.

> [!NOTE]
> 데이터 센터를 통합 하는 경우 필요한 추가 용량을 추정 하 유사한 방법을 사용할 수 있습니다 하거나 도메인 컨트롤러를 위성 위치 사용을 중지 합니다. 단순히 클라이언트에 아웃 바운드 및 인바운드 트래픽을 수집 하 고 WAN 링크 있을 이제는 트래픽의 양을 사용 됩니다.  
>  
> 경우에 따라 트래픽 속도가 느리므로 인증서 확인에 실패 한 경우 WAN에 엄격한 시간에 맞게 같은 예상 보다 더 많은 트래픽을 발생할 수 있습니다. 이러한 이유로 WAN 크기 조정 및 사용률 반복적이 고 지속적인 프로세스를 해야 합니다.

### <a name="virtualization-considerations-for-network-bandwidth"></a>네트워크 대역폭에 대 한 가상화 고려 사항

물리적 서버에 대 한 권장 사항을 제공 하는 것이 쉽습니다. 5000 사용자 수보다 클 지 원하는 서버에는 1GB입니다. 여러 게스트 내부 가상 스위치 인프라를 공유 시작 되 면 좀 더 주의 호스트 시스템에서 모든 게스트를 지원 하기 위해 적절 한 네트워크 대역폭이 하며 따라서 추가 규칙을 확인 해야 하는 합니다. 호스트 컴퓨터에 네트워크 인프라를 보장의 확장인 일 뿐입니다. 이 관계 없이 가상 스위치를 통한 트래픽은 네트워크를 사용 하 여 호스트에서 가상 컴퓨터 게스트 실행 도메인 컨트롤러를 포함 하 여 네트워크 인지 아니면 물리적 스위치에 직접 연결. 가상 스위치는 업링크 전송 중인 데이터 양을 지원 해야 하는 자세한 구성 요소가 하나 뿐입니다. 따라서 스위치에 연결 된 실제 호스트 실제 네트워크 어댑터 DC 부하와 실제 네트워크 어댑터에 연결 된 가상 스위치를 공유 하는 다른 모든 게스트 수 있어야 합니다.

### <a name="calculation-summary-example"></a>계산 요약 예제

|시스템|최대 대역폭|
|-|-|
DC 1|6.5 MB/s|
DC 2|6.25 MB/s|
|DC 3|6.25 MB/s|
|DC 4|5.75 MB/s|
|DC 5|4.75 MB/s|
|Total|28.5 MB/s|

**권장: 72 MB/s** (40%로 나눈 28.5 MB/s)

|대상 시스템 개수|(위에서) 총 대역폭|
|-|-|
|2|28.5 MB/s|
|일반적인 동작 결과|28.5 &divide; 2 = 14.25 MB/s|

늘 그렇듯이 시간이 지남에 따라 가정 가능 클라이언트 로드가 증가 하 고 가능한 가장이 증가 대 한 계획 해야 합니다. 권장된 크기를 계획 하는 네트워크 트래픽 50%의 예상된 증가 허용 합니다.

## <a name="storage"></a>스토리지

두 구성 요소를 구성 저장소를 계획 합니다.

- 용량 또는 저장소 크기
- 성능

시간 및 설명서의 많은 계획을 남겨 완전히 종종 간과 하는 성능 소비 됩니다. 현재 하드웨어 비용을 사용 하 여 대부분의 환경 없는 충분히 해당 중 하나에 해당 이러한 문제가 실제로 및 "데이터베이스 크기와 많은 RAM의 put"에 대 한 권장 큰 일반적으로 설명 나머지 부분에서는 위성 위치에 대 한 과도 수는 없지만 큰 환경입니다.

### <a name="sizing"></a>크기 조정

#### <a name="evaluating-for-storage"></a>저장소에 대 한 평가

13 년 전에 Active Directory에 도입 하면 4GB 및 9GB 드라이브의 가장 일반적인 드라이브 크기가 된 경우 한 번에 비해, Active Directory에 대 한 크기 조정이 않습니다도 모든 고려 하지만 가장 큰 환경. 최소 하드 드라이브를 사용 하 여 크기 180GB 범위, 전체 운영 체제, SYSVOL 및 NTDS.dit에 하나의 드라이브에 쉽게 맞출 수 있습니다. 이와 같이이 영역에 대 한 투자를 많이 사용할 수 없게 하는 것이 좋습니다.

NTDS.dit 크기의 110% 조각 모음을 사용 하도록 설정 하기 위해 사용할 수 있는지 확인 하도록 고려 사항에 대 한 유일한 권장이 합니다. 또한 하드웨어의 수명 동안 증가 대 한 숙박 이루어져야 합니다.

첫 번째 및 가장 중요 한 고려 사항 평가 크기 NTDS.dit 및 SYSVOL 됩니다. 이러한 측정값은 RAM 할당 크기 조정 모두 고정 디스크에 연결 됩니다. (비교적) 저렴 한 비용의 이러한 구성 요소, 인해 수학 엄격한 고 정확 하 게 될 필요가 없습니다. 기존 및 새 환경에서 확인할 수 있습니다이 평가 하는 방법에 대 한 콘텐츠를 [데이터 저장소](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961771(v=technet.10)) 일련의 문서. 특히, 다음 문서를 참조 하십시오.

- **기존 환경에 대 한 &ndash;**  문서의 조각 모음이 해제 된 디스크 공간 로깅 활성화 "를" 라는 제목의 섹션 [저장소 제한](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10))합니다.
- **새 환경에 대 한 &ndash;**  라는 문서 [Active Directory 사용자 및 조직 구성 단위에 대 한 증가 예측](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961779(v=technet.10))합니다.

  > [!NOTE]
  > 문서를 Windows 2000에서 Active Directory의 릴리스 시점에 대 한 데이터 크기 추정을 기반으로 합니다. 사용자 환경에서 개체의 실제 크기를 반영 하는 개체 크기를 사용 합니다.

여러 도메인을 사용 하 여 기존 환경을 검토할 때는 데이터베이스 크기에 변형이 있을 수 있습니다. True 이면 최소 GC (글로벌 카탈로그) 및 비 GC 크기를 사용 하세요.  

데이터베이스 크기는 운영 체제 버전 간에 달라질 수 있습니다. Dc를 Windows Server 2003에 Windows Server 2008 R2와 같은 운영 체제를 실행 하는 DC 보다 작은 데이터베이스 크기와 같은 이전 버전의 운영 체제를 실행, 특히 기능 이러한 Active Directory 휴지통 Bin 또는 자격 증명 로밍는 사용 하도록 설정 합니다.

> [!NOTE]  
  >
>- 새 환경에는 Active Directory 사용자 및 조직 구성 단위에 대 한 예상 증가 예상 나타냅니다 약 450MB의 공간을 사용 하는 동일한 도메인) (에: 100,000 명의 사용자를 확인 합니다. 하세요 특성이 채워지는 참고 총 금액에 상당한 영향 있습니다. 타사와 Microsoft Exchange Server 및 Lync 등 Microsoft 제품에서 여러 개체에 특성을 채워집니다. 환경에서 제품 포트폴리오에 따라 평가 하는 것이 좋습니다, 있지만 수학 아웃 자세히 설명 하 고 모두에 대 한 정확한 예측 하지만 가장 큰 환경에 대 한 테스트 실습 상당한 시간과 노력이 가치가 실제로 없을 수 있습니다.
>- 크기가 사용 가능한 공간으로 사용할 수 있는 오프 라인으로 사용 하도록 설정 하려면 NTDS.dit의 110% 조각 모음 하는 3 ~ 5 년 하드웨어 수명을 통해 증가 대 한 계획을 확인 합니다. 아무리 저렴 하더라도 저장소 지정한를 300 %DIT 크기 저장소 할당은 오프 라인으로 증가 및에 대 한 잠재적 필요성을 수용 하기 위해 안전 하 게 조각 모음에 저장소를 예측 합니다.

#### <a name="virtualization-considerations-for-storage"></a>저장소에 대 한 가상화 고려 사항

여러 가상 하드 디스크 (VHD) 파일의 단일 볼륨에 할당 되는 시나리오에서 사용 하 여 고정된 크기의 디스크 210% (DIT + 110% 사용 가능한 공간 100%) 이상의 예약 된 공간이 충분 한지 확인 하려면 DIT 크기입니다.  

#### <a name="calculation-summary-example"></a>계산 요약 예제

|평가 단계에서 수집 된 데이터| |
|-|-|
|NTDS.dit 크기|35GB|
|한정자에 대 한 오프 라인 조각 모음|2.1|
|필요한 총 저장소|73.5 GB|

> [!NOTE]
> SYSVOL, 운영 체제, 페이지 파일, 임시 파일, 캐시 된 데이터 (예: 설치 관리자 파일), 로컬 및 응용 프로그램에 필요한 저장소 외에도 필요한이 저장소는 됩니다.

### <a name="storage-performance"></a>저장소 성능

#### <a name="evaluating-performance-of-storage"></a>저장소의 성능 평가

컴퓨터 내에서 가장 느린 구성 요소와 저장소 클라이언트 환경에 가장 큰 부정적인 영향을 수 있습니다. 대규모 환경에서는 충분히는 RAM 크기 조정 권장 사항을 이용할 수 없는 내다보이는 성능을 위해 저장소를 계획의 결과 심각한 손상을 입힐 수 있습니다.  또한 복잡성과 다양 한 저장소 기술 좀 더 증가 오류의 위험 유용한 시나리오와 모범 사례를 "별도 실제 디스크에" 운영 체제, 로그 및 데이터베이스 배치 긴 고정의 관련 제한 됩니다.  긴 고정 모범 사례는 가정을 기반으로 한 "디스크"는 전용된 스핀 들이 I/O 격리를 허용 되는 때문입니다.  이 true 설정 하는이 가정이 되면서 더 이상 관련이:

- 새 저장소 유형 및 가상화 및 공유 저장소 시나리오
- 공유 저장소 영역 네트워크 (SAN)에 포함 된 스핀
- SAN 또는 network attached storage의 VHD 파일
- 반도체 드라이브
- 계층화 된 저장소 아키텍처 (즉, SSD 저장소 계층 캐싱 더 큰 스핀 들 기반 저장소)

간단히, 최종 목표를 기본 저장소 아키텍처 및 디자인에 관계 없이 모든 저장소 성능 요구가 필요한 IOPS (초당) 입/출력 작업 양을 사용할 수 있고 해당 IOPS는 허용 가능한 시간 프레임 내에서 발생 함을 확인 하는 것 . 이 섹션에서는 저장소 솔루션을 보장 하기 위해 기본 저장소의 어떤 AD DS 요구는 제대로 설계 된 평가 하는 방법에 설명 합니다.  오늘날의 저장소 기술의 가변성 들어 충분 한 IOPS를 확인 하 고 저장소 공급 업체를 사용 하려면 좋습니다.  로컬로 연결 된 저장소를 사용 하 여 이러한 시나리오에 대 한 기존 로컬 저장소 시나리오를 디자인 하는 방법의 기본 사항에 대 한 부록 C를 참조 합니다.  이 보안 주체 일반적으로 더 복잡 한 저장소 계층에 적용 되며 백 엔드 저장소 솔루션을 지 원하는 공급 업체를 사용 하 여 대화 상자에도 도움이 됩니다.

- 다양 한 범위의 사용 가능한 저장소 옵션에 지정 된 것이 좋습니다 하드웨어 지원 팀 이나 특정 솔루션에서 AD DS의 요구 사항을 충족 하기 위해 공급 업체의 전문 지식을 참여 합니다. 다음 숫자는 저장소 전문가에 제공 되는 정보입니다.

데이터베이스가 너무 커서 RAM에 저장할 수 있는 환경에 대 한 I/O를 지원 해야 하는 정도 확인 하려면 성능 카운터를 사용 합니다.

- 논리 디스크 (\*) \Avg Disk sec/Read (NTDS.dit d:에 저장 된 경우에 예를 들어, / 드라이브의 전체 경로 논리 디스크 (d:) \Avg Disk sec/Read 것)
- LogicalDisk(\*)\Avg Disk sec/Write
- LogicalDisk(\*)\Avg Disk sec/Transfer
- LogicalDisk(\*)\Reads/sec
- LogicalDisk(\*)\Writes/sec
- LogicalDisk(\*)\Transfers/sec

현재 환경의 요구 벤치 마크를 60/30/15 분 간격으로 샘플링 해야 합니다.

#### <a name="evaluating-the-results"></a>결과 평가

> [!NOTE]
> 초점은 읽기 데이터베이스에서 가장 까다로운 구성 하는 것은 일반적으로, 논리 디스크를 대체 하 여 로그 파일에 쓰기를 동일한 논리를 적용할 수 있는 ( *\<NTDS 로그\>* ) \Avg Disk sec/Write 및 논리 디스크 ( *\<NTDS 로그\>* ) \Writes/sec):
>  
> - 논리 디스크 ( *\<NTDS\>* ) \Avg Disk sec/Read 현재 저장소의 크기가 적절 하 게 지정 여부를 나타냅니다.  결과 거의 같은 논리 디스크 디스크 형식에 대 한 디스크 액세스 시간을 하는 경우 ( *\<NTDS\>* ) \Reads/sec 유효한 측정값입니다.  확인 제조업체 사양 백 엔드에서 저장용 하지만 논리 디스크에 대 한 적절 한 범위 ( *\<NTDS\>* ) \Avg Disk sec/Read는 약 수:
>   - 7200 – 12.5 9를 밀리초 (ms)
>   - ms 10,000 – 6 ~ 10
>   - ms 15,000 – 4 ~ 6  
>   - SSD – 1 ~ 3 밀리초  
>   - >[!NOTE]
>     >권장 사항 (원본)에 따라 20ms를 15ms에서 저장소 성능을 성능이 저하 되었음을 알리는 존재 합니다.  위의 값과 다른 관련 지침 간의 차이점은 정상 작동 범위는 위의 값.  다른 권장 클라이언트 환경을 크게 저하 됩니다 및 현저한 때 식별 하는 지침 문제를 해결 합니다.  자세한 내용은 부록 C를 참조 합니다.
> - 논리 디스크 ( *\<NTDS\>* ) \Reads/sec 수행 되는 I/O의 양입니다.
>   - 경우 논리 디스크 ( *\<NTDS\>* )가 백 엔드 저장소 논리 디스크에 대 한 최적의 범위 내에 \Avg Disk sec/Read ( *\<NTDS\>* ) \Reads/ 초는 저장소 크기를 직접 사용할 수 있습니다.
>   - 경우 논리 디스크 ( *\<NTDS\>* ) \Avg Disk sec/Read가 아닙니다. 백 엔드 저장소에 대 한 최적의 범위 내에서 다음 수식에 따라 추가 I/O가 필요 합니다.
>     > (LogicalDisk( *\<NTDS\>* )\Avg Disk sec/Read) &divide; (Physical Media Disk Access Time) &times; (LogicalDisk( *\<NTDS\>* )\Avg Disk sec/Read)

고려 사항:

- 서버가 최적 양의 RAM 사용 하 여를 구성 하는 경우 이러한 값이 정확 하지 않게 계획 하기 위해 note 합니다.  이러한 높은 쪽에서 잘못 되 고 최악의 시나리오를 계속 사용할 수 있습니다.
- 추가 최적화 RAM 구체적으로 드라이브 읽기 I/O 양이 감소 (논리 디스크 ( *\<NTDS\>* ) \Reads/Sec 합니다.  이 저장소 솔루션으로 처음에 계산 된 대로 강력한 없을 것을 의미 합니다.  그러나 모든 것이 일반적인 문의 경전철 종속 클라이언트 로드 및 일반적인 지침 보다 좀 더 구체적인 제공할 수 없습니다.  가장 적합 한 옵션 RAM을 최적화 한 후 저장소 크기를 조정 하는 것입니다.

#### <a name="virtualization-considerations-for-performance"></a>성능에 대 한 가상화 고려 사항

마찬가지로 모든 이전 가상화 토론 여기 키는는 기본 공유 인프라 DC 부하를 지원할 수와 미디어 및 모든 경로에 기본을 사용 하 여 다른 리소스를 공유 하도록 합니다. 이것이 사실이 실제 도메인 컨트롤러를 다른 서버 또는 응용 프로그램, SAN, NAS, 또는 iSCSI 인프라에 동일한 기본 미디어를 공유 하는 여부를 공유 하는 iSCSI SAN, NAS를 인프라에 대 한 액세스 통과 사용 하 여 게스트 인지는 미디어에서 기본 게스트 공유 미디어를 로컬로 또는 iSCSI SAN, NAS를 인프라에 상주 하는 VHD 파일을 사용 하는 경우 또는 합니다. 계획 연습은 기본 미디어를 모든 소비자의 총 부하를 지원할 수 있는지 확인 합니다.

또한 게스트 관점에서 이동 해야 하는 추가 코드 경로 가지는 모든 저장소에 액세스할 수 있는 호스트를 통해 이동 하지 않아도에 성능 영향을 줍니다. 저장소 성능 테스트가 가상화 호스트 시스템의 프로세서 사용률에 대 한 주관적인는 처리량에 영향을 줄에 있는지를 나타냅니다 당연히 (부록 a:를 참조 하세요. CPU 크기 조정 조건)에 영향을 확실히 받습니다 게스트에서 요구 하는 호스트의 리소스입니다. 이 가상화 시나리오에서 처리 요구 사항에 대 한 가상화 고려 사항에 기여 (참조 [처리를 위해 가상화 고려 사항](#virtualization-considerations-for-processing)).

더 복잡 하 게 여러 가지 다양 한 성능 영향 모두 사용할 수 있는 다른 저장소 옵션을 된다는 점입니다. 실제에서 가상으로 마이그레이션할 때 안전 하 게 예상치를 사용 하 여 1.10의 승수로 옵션에 대 한 다른 저장소 가상화 된 게스트에 대 한 hyper-v, IDE 또는 SCSI 어댑터를 통과 저장소와 같은 조정. 다른 저장소 시나리오 간에 전송할 때 되어야 하는 조정 작업 저장소 인지 로컬, SAN, NAS 또는 iSCSI에 대 한 관련이 있습니다.

#### <a name="calculation-summary-example"></a>계산 요약 예제

정상적인 작업 조건 양호한 시스템에 필요한 I/O의 양을 결정 합니다.

- 논리 디스크 ( *\<NTDS 데이터베이스 드라이브\>* ) 최대 사용 기간 15 분의 기간 동안 \Transfers/sec 
- 기본 저장소의 용량을 초과 하는 저장소에 필요한 I/O의 양을 결정 합니다.
  >*Needed IOPS* = (LogicalDisk( *\<NTDS Database Drive\>* )\Avg Disk sec/Read &divide; *\<Target Avg Disk sec/Read\>* ) &times; LogicalDisk( *\<NTDS Database Drive\>* )\Read/sec

|카운터|값|
|-|-|
|Actual LogicalDisk( *\<NTDS Database Drive\>* )\Avg Disk sec/Transfer|.02 초 (20 밀리초)|
|Target LogicalDisk( *\<NTDS Database Drive\>* )\Avg Disk sec/Transfer|.01 시간 (초)|
|사용할 수 있는 IO 변경에 대 한 승수|0.02 &divide; 0.01 = 2|  
  
|값 이름|값|
|-|-|
|LogicalDisk( *\<NTDS Database Drive\>* )\Transfers/sec|400|
|사용할 수 있는 IO 변경에 대 한 승수|2|
|최대 사용 기간 중에 필요한 총 IOPS|800|

캐시 되는 속도 확인 하 준비 하려는:

- 캐시를 준비 하는 최대 허용 시간을 결정 합니다. 디스크에서 전체 데이터베이스를 로드 하는 데 소요 됩니다을 시간의 양을 나 RAM의 전체 데이터베이스를 로드할 수 없습니다 경우 RAM을 입력 하는 최대 시간 것이 있습니다.
- 공백 문자를 제외한 데이터베이스의 크기를 결정 합니다.  자세한 내용은 [저장소에 대 한 평가](#evaluating-for-storage)합니다.  
- 데이터베이스 크기를 8KB; 나눕니다 데이터베이스를 로드 하는 데 필요한 총 Io 사용 됩니다.
- Total Io는 정의 된 시간 내에 시간 (초) 수로 나눕니다.

Note ESE 고정된 캐시 크기 구성 되지 않으며 기본적으로 AD DS 변수 캐시 크기를 사용 하는 경우 이전에 로드 된 페이지 제거는 때문에 정확 하지만 계산 속도 정확 하 게 되지 않습니다.

|데이터를 수집 하는 요소|값
|-|-|
|웜에 허용 되는 최대 시간|10 분 (600 초)
|데이터베이스 크기|2GB|  
  
|계산 단계|수식|결과|
|-|-|-|
|데이터베이스 페이지의 크기를 계산 합니다.|(2 GB &times; 1024 &times; 1024) = *KB 데이터베이스의 크기*|2,097,152 KB|
|데이터베이스의 페이지 수를 계산 합니다.|2,097,152 KB &divide; 8KB = *페이지 수*|262,144 페이지|
|완벽 하 게 캐시를 준비 하는 데 필요한 IOPS를 계산 합니다.|페이지 262,144 &divide; 600 초 = *필요한 IOPS*|437 IOPS|

## <a name="processing"></a>처리 중

### <a name="evaluating-active-directory-processor-usage"></a>Active Directory 프로세서 사용량을 평가

대부분의 환경에 대 한 처리 용량을 관리 계획 섹션에 설명 된 대로 저장소, RAM 및 네트워킹 제대로 조정 되며 나면은 가장 주목 하는 구성 요소 수 있습니다. 필요한 CPU 용량을 계산할 때 두 가지 과제는

- 환경에서 응용 프로그램의 공유 서비스 인프라에 정상적으로 작동 되는 여부 및 문서에서 "추적 비용이 많이 드는 및 비효율적인 검색" 섹션에 설명 되어 만드는 더 효율적으로 Microsoft Active 디렉터리 사용 응용 프로그램 또는 하위 수준 SAM에서 LDAP 호출을 호출 합니다.  
  
  규모가 큰 환경에서는 이것이 중요 한 이유는 잘못 코딩 된 응용 프로그램 수 것 CPU 부하의 변동성 드라이브, "도용" 투자할 필요가 없지 되는 다른 응용 프로그램에서 CPU 시간, 용량 요구를 인위적으로 높입니다에 대 한 부하를 균등 하 게 배포 dc가 있습니다.  
- AD DS 다양 한 잠재적 클라이언트를 사용 하 여 분산된 환경 이기 때문에 "단일 클라이언트"의 비용 예측은 형식 또는 AD DS를 활용 하 여 응용 프로그램의 수량 및 사용 패턴으로 인해 경전철 주관적입니다. 즉, 광범위 한 적용 가능성에 대 한 네트워킹 섹션을 비슷하게이 더 접근 환경에 필요한 총 용량을 평가 하는 관점입니다.

기존 환경에 대 한 저장소 크기 조정에서 이전에 설명한 대로 양호한 상태로 저장소 이제 크기가 적절 하 고 따라서 프로세서 부하에 대 한 데이터가 잘못 되었습니다. 다시 말하지만, 시스템의 병목 상태 저장소의 성능이 되지 않도록 하려면 반드시 합니다. 병목 상태가 존재 하 고 프로세서 대기를 하는 경우에 사라집니다 병목 상태가 제거 되 면 하는 유휴 상태입니다.  프로세서 대기 상태는 제거 되 면 당연히 데이터에서 대기 하도록 더 이상 CPU 사용률이 증가 합니다. Thus, collect performance counters “Logical Disk( *\<NTDS Database Drive\>* )\Avg Disk sec/Read” and “Process(lsass)\\% Processor Time”. 데이터를 "Process(lsass)\\% Processor Time" 인위적으로 줄어들게 됩니다 하는 경우 "논리 디스크 ( *\<NTDS 데이터베이스 드라이브\>* ) \Avg Disk sec/Read" 일반 임계값은 10 ~ 15 밀리초를 초과 하는 Microsoft 지원 저장소와 관련 된 성능 문제 해결에 사용 합니다. 이전과 마찬가지로 샘플 간격으로 15, 30 일 또는 60 분 되도록 하는 것이 좋습니다. 아무 것도 작은 일반적으로 더 좋은 측정 단위가 미터법 이면 너무 volatile 에 대해서는 매끄럽게 일일 피킹 과도 하 게 합니다.

### <a name="introduction"></a>소개

가장 주 및 이해 도메인 컨트롤러에 대 한 용량 계획을 계획 하려면 필요한 처리 능력입니다. 최대 성능을 보장 하기 위해 시스템의 크기를 조정 하는 경우 항상 병목 상태는 구성 요소 및 올바른 크기의 도메인 컨트롤러에서 프로세서 됩니다.

사이트 간 기준 환경의 요청을 검토 하는 위치 네트워킹 섹션 마찬가지로 동일한 수행 되어야 합니다는 계산 용량에 대 한. 여기서 사용 가능한 네트워킹 기술을 일반 요청을 훨씬 뛰어넘습니다, 네트워킹 섹션을 달리 더 많은 주의를 CPU 용량 크기 조정 합니다.  도 보통 크기의 모든 환경 CPU에 상당한 부하를 넣을 수 몇 천 동시 사용자 아무 것도 합니다.

그러나 AD를 활용 하는 클라이언트 응용 프로그램의 방대한 가변성을 인해 CPU 당 사용자 일반 예측 적용 되지 않습니다 필요한 모든 환경에. 특히 계산 요구 사항이 사용자 동작 및 응용 프로그램 프로필입니다. 따라서 각 환경 개별적으로 크기를 조정 해야 합니다.

#### <a name="target-site-behavior-profile"></a>대상 사이트 동작 프로필

목표 대상으로 하 여 설계 하는 것에서 설명한 대로, 전체 사이트에 대 한 용량을 계획 하는 경우는 *N* +에 적절 한 서비스의 연속에 대 한 최대 기간 동안 시스템 오류가 발생 하면 되도록 1 용량 디자인 품질 수준입니다. 즉,에 "*N*" 시나리오에서는 모든 상자 부하가 100% 보다 작으면 (아직 80% 개선) 해야 합니다 최대 기간입니다.

또한 응용 프로그램 및 사이트의 클라이언트에에서 도메인 컨트롤러를 찾기 위한 모범 사례를 사용 중인 경우 (즉, 사용 하 여는 [DsGetDcName 함수](http://msdn.microsoft.com/en-us/library/windows/desktop/ms675983(v=vs.85).aspx)), 클라이언트는 부를 사용 하 여 상대적으로 균일 하 게 배포 되어야 합니다 모든 다양 한 요인으로 인해 일시적인 스파이크 합니다.

다음 예제에서는 다음과 같이 가정이 됩니다.

- 각 사이트의 다섯 가지 Dc에 cpu 4 개 있습니다.
- 총 대상 업무 시간 동안 CPU 사용량은 정상 작동 조건 40% ("*N* + 1") 및 60%가 고 그렇지 ("*N*"). 업무 시간 이외에 대상 CPU 사용량 이므로 80% 백업 소프트웨어 및 기타 유지 관리 해야 하는 모든 사용 가능한 리소스를 소모 합니다.

![CPU 사용 현황 차트](media/capacity-planning-considerations-cpu-chart.png)

차트의 데이터 분석 (프로세서 Information(_Total)\% 프로세서 유틸리티) Dc의 각각에 대해:

- 대부분의 경우 부하 클라이언트 DC 로케이터를 사용 하 고 검색을 잘 작성 한 경우 예상 되는 분산 상대적으로 균일 하 게 됩니다. 
- 있습니다 수의 가능한 큰 일부를 사용 하 여 10 %5 분 동안 급증으로 20%입니다. 일반적으로 초과 용량 계획 대상, 발생 하지 않는 한 이러한 조사 아닙니다 것이 좋습니다.  
- 모든 시스템에 대 한 최대 기간은 약 8 오전 오전 9시 15분 사이입니다. 약 5: 00에서 약 오후 5:00 통해 원활 하 게 전환를 사용 하 여 일반적으로 비즈니스 주기 암시적입니다. 용량 계획 외부에서 오후 5 시 사이의 오전 4 시-상자 시나리오에서 CPU 사용량의 임의 보다 급격 한 것입니다.

  >[!NOTE]
  >잘 관리 되는 시스템을 언급 스파이크가 될 수 있습니다 백업 소프트웨어 실행, 바이러스 백신 검사 전체 시스템, 하드웨어 또는 소프트웨어 인벤토리, 소프트웨어 또는 패치 배포 및 등입니다. 최대 사용자 비즈니스 주기를 벗어나기 때문에 대상 벗어나지 않습니다.

- 나머지 시스템 예상 53%는 실행, 실패 하거나 오프 라인 상태로 하나 각 시스템에는 약 40%가 있고 모든 시스템 Cpu의 동일한 번호, 해야 (System D의 40% 부하는 균등 하 게 분할 및 시스템 A와 시스템 C의 기존 40% 부하에 추가). 다양 한 이유로이 선형 가정 하지 않습니다 완벽 하 게 정확 하지만 충분 한 정확도 측정을 제공 합니다.  

  **대체 시나리오 –** 40%를 실행 하는 두 명의 도메인 컨트롤러: 예상된 CPU에 나머지 하나의 도메인 컨트롤러 실패는 예상된 80%는 것입니다. 이 훨씬 용량 계획에는 앞서 설명한 임계값을 초과 하 고도 시작 심각 하 게 헤드 공간에는 10 ~ 20%는 급격 한 100% 중 90%로 DC를 드라이브는 즉 위의 부하 프로필의 표시를 제한 하는 "*N*"시나리오 및 응답성을 확실 하 게 저하 됩니다.

### <a name="calculating-cpu-demands"></a>계산의 CPU 요구 사항

"프로세스\\% Processor Time" 성능 개체 카운터 합계 총 시간의 CPU에서 사용 가능한 모든 응용 프로그램의 스레드가 하는 시스템의 총합으로 나눕니다 시간 경과 합니다. 이 설정의 효과 다중 CPU 시스템에서 다중 스레드 응용 프로그램을 100 %CPU 시간을 초과할 수 및 보다 매우 다르게 해석 되는 "프로세서 정보\\% 프로세서 유틸리티"입니다. 실제로 "Process(lsass)\\% Processor Time" 실행 프로세스의 요구를 지 원하는 데 필요한 100 %Cpu 수로 볼 수 있습니다. 200%를 전체 AD DS 로드를 지원 하기 위해 100%, 각 2 개 Cpu 필요 함을 의미 합니다. 100% 용량으로 실행 되는 CPU가 있지만 가장 비용 효율적인 Cpu에 소요 되는 비용 관점에서 및 시스템의 경우는 다양 한 이유로 부록 A 인 다중 스레드 시스템에서 더 나은 응답성 자세한 전력 및 에너지 소비량 100%에서 실행 되지 않습니다.

클라이언트 부하의 일시적인 스파이크를 수용 하기 위해 40% 사이의 시스템 용량의 60%의 최대 기간 CPU를 대상으로 것이 좋습니다. 위의 예제를 사용 하는 3.33 (60% 대상)과 5 (40% 대상) 사이의 Cpu 필요 AD DS 로드 (lsass 프로세스)를 의미 합니다. 기본 운영 체제 및 (예: 바이러스 백신, 백업, 모니터링 및 등)에 필요한 기타 에이전트의 요구에 따라 추가 용량에 추가 되어야 합니다. 에이전트의 영향을 환경 당 기준 평가 해야 하지만 단일 CPU의 10% 5% 사이의 예상 될 수 있습니다. 현재 예제에서는이 것이 좋습니다 (60% 대상) 3.43 및 5.1 (40% 대상) 간에 Cpu는 필요한 사용량이 많은 기간 중.

이 작업을 수행 하는 가장 쉬운 방법은 동일한 확장할 수 있도록 모든 카운터 Windows 안정성 및 성능 모니터 (perfmon)에서 "누적 영역형" 뷰를 사용 하는 합니다.

가정:

- 목표를 최대한 적은 서버로 좁히는 것입니다. 부하 및 중복성을 위해 추가 하는 추가 서버 서버만 수행 하는 것이 좋습니다 (*N* + 1 시나리오).

![(모든 프로세서)를 통해 lsass 프로세스에 대 한 프로세서 시간 차트](media/capacity-planning-considerations-proc-time-chart.png)

차트의 데이터에서 얻은 (Process(lsass)\\% 프로세서 시간):

- 영업일 7:00 약 늘려 시작 하 고 오후 5 시에 감소 합니다.
- 가장 많이 사용 되 로드가에서 오전 9:30-오전 11 시입니다. 
  > [!NOTE]
  > 모든 성능 데이터를 기록 합니다. 최대 데이터 지점 9시 15분 9:15 9:00에서 부하를 나타냅니다.
- 오전 7:00 다른 표준 시간대에서 로드 또는 백업 같은 백그라운드 인프라 작업을 나타낼 수 있는 전에 스파이크가 있습니다. 이 작업을 초과 하는 오전 9:30에 최고 되므로 관련 없습니다.
- 사이트에 도메인 컨트롤러 3 가지 있습니다.

최대 부하에서 lsass 약 485% 하나의 CPU의 100%에서 실행 중인 4.85 Cpu를 사용 합니다. 계산에 따라 이전, 즉 사이트 약 12.25 Cpu AD DS에 대 한 합니다. 5 ~ 10% 백그라운드 프로세스에 대 한 위의 제안에 추가 하 고 즉, 약 12.30를 12.35 Cpu 부하를 동일를 지원 하기 위해 지금 서버를 교체 해야 합니다. 이제 증가 대 한 환경 예상 가능성을 해야 합니다.

### <a name="when-to-tune-ldap-weights"></a>LDAP 가중치를 조정 하는 경우

일부의 시나리오에서는 [LdapSrvWeight](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc957291(v=technet.10)) 고려해 야 합니다. 용량 계획의 컨텍스트 내에서이 작업은 응용 프로그램 또는 사용자 부하는 균등 하 게 분산 하지, 또는 기본 시스템 기능 측면에서 균등 하 게 분산 된 경우. 이 문서의 범위 외부의 초과 용량 계획 작업을 수행 하는 이유는.

LDAP 가중치를 조정 하는 두 가지 일반적인 이유는

- PDC 에뮬레이터는 어떤 사용자 또는 응용 프로그램에 대 한 로드 동작 균등 하 게 분산 되지 모든 환경에 영향을 주는 예시입니다. PDC 에뮬레이터에서 CPU 리소스를 다른 곳에서 보다 더 많이 요청 된 경우도 특정 도구 및 작업 그룹 정책 관리 도구, 인증 실패, 트러스트 설정 및 등의 경우 두 번째 시도 같은 PDC 에뮬레이터를 대상 사이트입니다.
  - 만 경우 PDC 에뮬레이터에서 부하를 줄이고 다른 도메인 컨트롤러에 대 한 로드를 증가 하기 위해 CPU 사용률의 두드러진 차이 더 균등 부하 하면이 조정 하는 것이 유용 합니다.
  - 이 경우 PDC 에뮬레이터에 대 한 50-75 LDAPSrvWeight를 설정 합니다.
- Cpu (및 속도) 사이트에 서로 다른 수를 사용 하 여 서버입니다.  예를 들어 두 명의 8 코어 서버 및 4 코어 서버만 가정해 보겠습니다.  마지막으로 서버에 다른 두 서버 중 절반 프로세서가 있습니다.  즉, 잘 분산된 클라이언트 로드가 8 코어 상자는 두 번 약 4 코어 상자에서 평균 CPU 로드가 증가 하는 것을 의미 합니다.
  - 예를 들어, 40%에서 실행 되 고 두 개의 8 코어 상자 및 4 코어 상자는 80%에서을 실행 합니다.
  - 또한이 시나리오는 4 코어 상자는 이제 오버 로드 될 팩트 특히 8 코어 상자 손실의 영향을 고려 합니다.

#### <a name="example-1---pdc"></a>예제 1-PDC

| |기본값을 사용 하 여 사용률|New LdapSrvWeight|새 예상된 사용률|
|-|-|-|-|
|DC 1 (PDC 에뮬레이터)|53%|57|40%|
|DC 2|33%|100|40%|
|DC 3|33%|100|40%|

여기서 주목 해야 할 경우 PDC 에뮬레이터 역할을 점유 되는 사이트의 다른 도메인 컨트롤러에 특히 또는 전송 하는 경우 것 새 PDC 에뮬레이터에서 급격 한 증가

섹션에서 예제를 사용 하 여 [대상 사이트 동작 프로필](#target-site-behavior-profile), 사이트의 모든 세 가지 도메인 컨트롤러는 4 개의 Cpu를 가정 했습니다. 수행할 동작, 정상 조건에서는 8 개의 Cpu에 있으면 도메인 컨트롤러 중 하나? 40% 사용률에서 도메인 컨트롤러 2 개 및 20% 사용률에 하나씩 것입니다. 이 잘못 된 약간 더 나은 부하를 분산 시킬 수가 있습니다. 이렇게 하려면 LDAP 가중치를 활용 합니다.  예제 시나리오는 다음과 같습니다.

#### <a name="example-2---differing-cpu-counts"></a>예제 2-다른 CPU 계산

| |프로세서 정보\\ %&nbsp;프로세서 Utility(_Total)<br />기본값을 사용 하 여 사용률|New LdapSrvWeight|새 예상된 사용률|
|-|-|-|-|
|4-CPU DC 1|40|100|30%|
|4-CPU DC 2|40|100|30%|
|8-CPU DC 3|20|200|30%|

이러한 시나리오를 사용 하 여 매우 주의 통해 해야 합니다. 위에서 볼 수 있듯이 매우 깔끔하고 종이에 멋진 수학이 찾습니다. 하지만이 기사에서는 대 한 계획을 "*N* + 1" 시나리오는 매우 중요 합니다. 모든 시나리오에 대 한 오프 라인으로 전환 하는 한 DC의 영향을 계산 되어야 합니다. 60%를 보장 하기 위해 부하 분산을도는 바로 앞의 시나리오 중 로드는 "*N*" 시나리오에서는 모든 서버에 걸쳐 균등 하 게 분산 된 부하 분포를 그대로 두어도 됩니다 비율이 유지 일치 합니다. 찾고 튜닝 시나리오는 PDC 에뮬레이터에서 일반적으로 모든 시나리오 사용자 또는 응용 프로그램 부하를 분산 되지 않는, 효과 매우 다릅니다.

| |튜닝 된 사용률|New LdapSrvWeight|새 예상된 사용률|
|-|-|-|-|
|DC 1 (PDC 에뮬레이터)|40%|85|47%|
|DC 2|40%|100|53%|
|DC 3|40%|100|53%|

### <a name="virtualization-considerations-for-processing"></a>처리를 위해 가상화 고려 사항

가상화 된 환경에서 수행 해야 하는 용량 계획의 두 계층이 있습니다. 이전에 처리 하는 도메인 컨트롤러에 대해 설명 하 고 비즈니스 주기도 식별 비슷합니다 호스트 수준에서 최대 사용 기간 동안 임계값 식별할 수 있도록 해야 합니다. 기본 보안 주체는 게스트 물리적 컴퓨터의 CPU에서 AD DS 스레드를 시작 하는 경우와 CPU 스레드를 예약 하는 호스트 컴퓨터에 대해 동일한 이기 때문에 동일한 목표의 40% ~ 60% 기본 호스트에 권장 됩니다. 다음 계층에서 게스트 계층인 스레드 예약의 보안 주체 이후 변경 되지 않은 40 ~ 60% 범위에 게스트 남아 내 목표입니다.

직접 매핑된 시나리오에서는 호스트당 하나의 게스트의 기본 호스트 운영 체제 요구 사항 (RAM, 디스크, 네트워크)에 추가 해야 수행이 지점에는 모든 용량 계획 합니다. 공유 호스트 시나리오에서는 테스트 것 10% 영향 기본 프로세서의 효율성에 있습니다. 즉, 사이트 전체 할당할 가상 Cpu 권장된 크기가 40%의 대상에서 10 개의 Cpu를 해야 하는 경우는 "*N*" 게스트 11 것입니다. 물리적 서버 및 가상 서버의 혼합 된 배포를 사용 하 여 사이트의 경우 한정자를 Vm에만 적용 됩니다. 예를 들어 사이트에는 "*N* + 1" 시나리오를 10 개의 Cpu 사용 하 여 하나의 물리적 또는 직접 매핑된 서버 도메인 컨트롤러에 대 한 예약 된 11 Cpu 사용 하 여 호스트에서 cpu가 11 개 이상의 게스트에 해당 하는 방법에 대 한 것입니다.

분석 및 필요한 CPU 수량의 계산 전체 AD DS 로드를 지원 하기 위해 용어 실제 하드웨어에서 구입할 수 있습니다에 매핑되는 Cpu 수가 반드시 매핑되지 않는 완전히 합니다. 가상화 뒤섞인 반응이 필요가 없습니다. 가상화는 VM에 CPU를 추가할 수 있습니다는 간편 하 게 지정 된 사이트에 계산 용량을 추가 하는 데 필요한 노력을 줄입니다. 추가 Cpu가 게스트를 추가 해야 하는 경우 기본 하드웨어를 사용할 수 있도록 필요한 계산 능력을 정확 하 게 평가 해야를 제거 하지는 않습니다.  늘 그렇듯이 계획 및 수요에서 증가 대 한 모니터링 해야 합니다.

### <a name="calculation-summary-example"></a>계산 요약 예제

|시스템|최대 CPU|
|-|-|-|
|DC 1|120%|
|DC 2|147%|
|Dc 3|218%|
|사용 중인 총 CPU|485%|  
  
|대상 시스템 개수|(위에서) 총 대역폭|
|-|-|
|40% 대상에 필요한 Cpu|4.85 &divide; .4 = 12.25|

이 이때의 중요도 때문 반복 *확장을 계획 해야*합니다. 50% 증가 다음 3 년간 가정 하 고이 환경에 18.375 Cpu 해야 합니다. (12.25 &times; 1.5) 3 년 표시 합니다. 대체 계획 첫 해 이후에 검토 하 고 필요에 따라 추가 용량에 추가할 수 있습니다.

### <a name="cross-trust-client-authentication-load-for-ntlm"></a>Ntlm 인증 부하 간 신뢰할 수 있는 클라이언트

#### <a name="evaluating-cross-trust-client-authentication-load"></a>교차 신뢰 클라이언트 인증 부하를 평가합니다.

다양 한 환경에는 하나 이상의 도메인 트러스트에 의해 연결 되어 있을 수 있습니다. Kerberos 인증을 사용 하지 않는 다른 도메인의 id에 대 한 인증 요청을 대상 도메인 또는 경로에서 다음 도메인에서 다른 도메인 컨트롤러에 도메인 컨트롤러의 보안 채널을 사용 하 여 트러스트를 트래버스하 해야 합니다. 대상 도메인입니다. 트러스트 된 도메인에 도메인 컨트롤러에 도메인 컨트롤러를 만들 수 있는 보안 채널을 사용 하 여 동시 호출 수가 라고 하는 설정으로 제어 됩니다 **MaxConcurrentAPI**합니다. 도메인 컨트롤러에 대 한 두 가지 방법 중 하나에 의해 수행은 보안 채널 부하의 양을 처리할 수 있는지 확인 합니다: 튜닝 **MaxConcurrentAPI** 또는 바로 가기 트러스트를 만들어 포리스트 내의 이름 접미사입니다. 개별 트러스트를 통해 트래픽 볼륨이 계기 참조 [MaxConcurrentApi 설정을 사용 하 여 NTLM 인증에 대 한 성능 튜닝을 수행 하는 방법을](https://support.microsoft.com/kb/2688798)합니다.

데이터를 수집 하는 동안이 다른 모든 시나리오와 마찬가지로 수집 해야 합니다 유용 하 게 데이터에 대 한 일의 최대 사용량이 많은 기간 중입니다.

> [!NOTE]
> 포리스트 내 및 포리스트 간 시나리오를 여러 트러스트를 트래버스하는 인증 발생할 수 있습니다 하 고 각 단계는 조정 해야 합니다.

#### <a name="planning"></a>계획

기본적으로 NTLM 인증을 사용 하거나 특정 구성 시나리오에서 사용 하는 응용 프로그램의 여러 가지가 있습니다. 응용 프로그램 서버는 용량 증가 및 서비스의 활성 클라이언트 수는 증가 합니다. 클라이언트는 제한 된 시간에 대 한 세션을 열린 상태로 유지 하 고 (예: 전자 메일 끌어오기 동기화)를 정기적으로 다시 연결 대신 추세 이기도 합니다. 높은 NTLM 부하에 대 한 다른 일반적인 예에는 인터넷 액세스를 위해 인증이 필요한 웹 프록시 서버입니다.

이러한 응용 프로그램에는 사용자와 리소스가 서로 다른 도메인에 있고 경우에 특히 중요 한 스트레스를 Dc에 배치할 수 있는 NTLM 인증에 상당한 부하를 발생할 수 있습니다.

여러 가지 방법이 있습니다 관리 간 트러스트 부하에 실제로 사용 되는 배타적 아닌 함께에서 하거나 / 또는 시나리오입니다. 가능한 옵션은:

- 사용자에는 동일한 도메인에 사용자를 사용 하는 서비스를 배치 하 여 교차 신뢰 클라이언트 인증을 줄입니다.
- 보안-사용 가능한 채널의 수를 늘립니다. 이 포리스트 내 트래픽과 크로스 포리스트 관련이 및 바로 가기 트러스트 라고 합니다.
- 에 대 한 기본 설정을 조정 **MaxConcurrentAPI**합니다.

튜닝에 대 한 **MaxConcurrentAPI** 그 이유는 기존 서버에서:

> *New_MaxConcurrentApi_setting* &ge; (*semaphore_acquires* + *semaphore_time 아웃*) &times; *average_semaphore_ hold_time* &divide; *time_collection_length*

자세한 내용은 참조 하세요. [2688798 KB 문서: MaxConcurrentApi 설정을 사용 하 여 NTLM 인증에 대 한 성능 튜닝을 수행 하는 방법을](http://support.microsoft.com/kb/2688798)합니다.

## <a name="virtualization-considerations"></a>가상화 고려 사항

None,이 운영 체제 설정을 조정 합니다.

### <a name="calculation-summary-example"></a>계산 요약 예제

|데이터 형식|값|
|-|-|
|세마포 획득 (최소)|6,161|
|세마포 획득 (최대)|6,762|
|세마포 시간 제한|0|
|평균 세마포 확보 시간|0.012|
|컬렉션 기간 (초)|1시 11분 분 (71 초)|
|수식 (에서 2688798 KB)|((6762 &ndash; 6161) + 0) &times; 0.012 /|
|에 대 한 최소값 **MaxConcurrentAPI**|((6762 &ndash; 6161) + 0) &times; 0.012 &divide; 71 = .101|

이 기간에 대 한이 시스템에 대 한 기본값은 허용 합니다.

## <a name="monitoring-for-compliance-with-capacity-planning-goals"></a>용량 계획을 목표를 사용 하 여 규정 준수에 대 한 모니터링

이 기사에서는 설명 했습니다 계획 및 크기 조정 사용률 대상 쪽으로 이동 합니다. 시스템은 적절 한 용량 임계값 내에서 작동 하도록 모니터링 해야 하는 권장 되는 임계값 요약 차트는 다음과 같습니다. 이 성능 임계값을 용량 임계값 계획 염두에 두어야 합니다. 이러한 임계값 초과 운영 하는 서버를 작동 하지만 시작 유효성을 검사 하는 모든 응용 프로그램은 제대로 되지 않게 동작 하는 시간입니다. 응용 프로그램은 정상적으로 작동 됩니다. 그러나 인지 하드웨어 업그레이드 또는 다른 구성 변경 내용을 평가 시작 합니다.

|범주|성능 카운터|샘플링 간격 /|대상|Warning|
|-|-|-|-|-|
|프로세서|Processor Information(_Total)\\% Processor Utility|60 min|40%|60%|
|RAM (Windows Server 2008 R2 or earlier)|Memory\Available MB|< 100 MB|N/A|< 100 MB|
|RAM (Windows Server 2012)|Memory\Long-Term Average Standby Cache Lifetime(s)|30 min|Must be tested|Must be tested|
|Network|Network Interface(\*)\Bytes Sent/sec<br /><br />Network Interface(\*)\Bytes Received/sec|30 min|40%|60%|
|Storage|LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read<br /><br />LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Write|60 min|10 ms|15 ms|
|AD Services|Netlogon(\*)\Average Semaphore Hold Time|60 min|0|1 second|

## Appendix A: CPU sizing criteria

### Definitions

**Processor (microprocessor) –** a component that reads and executes program instructions  

**CPU –** Central Processing Unit  

**Multi-Core processor –** multiple CPUs on the same integrated circuit  

**Multi-CPU –** multiple CPUs, not on the same integrated circuit  

**Logical Processor –** one logical computing engine from the perspective of the operating system  

This includes hyper-threaded, one core on multi-core processor, or a single core processor.  

As today’s server systems have multiple processors, multiple multi-core processors, and hyper-threading, this information is generalized to cover both scenarios. As such, the term logical processor will be used as it represents the operating system and application perspective of the available computing engines.

### Thread-level parallelism

Each thread is an independent task, as each thread has its own stack and instructions. Because AD DS is multi-threaded and the number of available threads can be tuned by using [How to view and set LDAP policy in Active Directory by using Ntdsutil.exe](http://support.microsoft.com/kb/315071), it scales well across multiple logical processors.

### Data-level parallelism

This involves sharing data across multiple threads within one process (in the case of the AD DS process alone) and across multiple threads in multiple processes (in general). With concern to over-simplifying the case, this means that any changes to data are reflected to all running threads in all the various levels of cache (L1, L2, L3) across all cores running said threads as well as updating shared memory. Performance can degrade during write operations while all the various memory locations are brought consistent before instruction processing can continue.

### CPU speed vs. multiple-core considerations

The general rule of thumb is faster logical processors reduce the duration it takes to process a series of instructions, while more logical processors means that more tasks can be run at the same time. These rules of thumb break down as the scenarios become inherently more complex with considerations of fetching data from shared-memory, waiting on data-level parallelism, and the overhead of managing multiple threads. This is also why scalability in multi-core systems is not linear.

Consider the following analogies in these considerations: think of a highway, with each thread being an individual car, each lane being a core, and the speed limit being the clock speed.

1. If there is only one car on the highway, it doesn’t matter if there are two lanes or 12 lanes. That car is only going to go as fast as the speed limit will allow.
1. Assume that the data the thread needs is not immediately available. The analogy would be that a segment of road is shutdown. If there is only one car on the highway, it doesn’t matter what the speed limit is until the lane is reopened (data is fetched from memory).
1. As the number of cars increase, the overhead to manage the number of cars increases. Compare the experience of driving and the amount of attention necessary when the road is practically empty (such as late evening) versus when the traffic is heavy (such as mid-afternoon, but not rush hour). Also, consider the amount of attention necessary when driving on a two-lane highway, where there is only one other lane to worry about what the drivers are doing, versus a six-lane highway where one has to worry about what a lot of other drivers are doing.
   > [!NOTE]
   > The analogy about the rush hour scenario is extended in the next section: Response Time/How the System Busyness Impacts Performance.

As a result, specifics about more or faster processors become highly subjective to application behavior, which in the case of AD DS is very environmentally specific and even varies from server to server within an environment. This is why the references earlier in the article do not invest heavily in being overly precise, and a margin of safety is included in the calculations. When making budget-driven purchasing decisions, it is recommended that optimizing usage of the processors at 40% (or the desired number for the environment) occurs first, before considering buying faster processors. The increased synchronization across more processors reduces the true benefit of more processors from the linear progression (2&times; the number of processors provides less than 2&times; available additional compute power).

> [!NOTE]
> Amdahl’s Law and Gustafson’s Law are the relevant concepts here.

### Response time/How the system busyness impacts performance

Queuing theory is the mathematical study of waiting lines (queues). In queuing theory, the Utilization Law is represented by the equation:

*U* k = *B* &divide; *T*

Where *U* k is the utilization percentage, *B* is the amount of time busy, and *T* is the total time the system was observed. Translated into the context of Windows, this means the number of 100-nanosecond (ns) interval threads that are in a Running state divided by how many 100-ns intervals were available in given time interval. This is exactly the formula for calculating % Processor Utility (reference [Processor Object](https://docs.microsoft.com/previous-versions/ms804036(v=msdn.10)) and [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/previous-versions/windows/embedded/ms901169(v=msdn.10))).

Queuing theory also provides the formula: *N* = *U* k &divide; (1 &ndash; *U* k) to estimate the number of waiting items based on utilization ( *N* is the length of the queue). Charting this over all utilization intervals provides the following estimates to how long the queue to get on the processor is at any given CPU load.

![Queue length](media/capacity-planning-considerations-queue-length.png)

It is observed that after 50% CPU load, on average there is always a wait of one other item in the queue, with a noticeably rapid increase after about 70% CPU utilization.

Returning to the driving analogy used earlier in this section:

- The busy times of “mid-afternoon” would, hypothetically, fall somewhere into the 40% to 70% range. There is enough traffic such that one’s ability to pick any lane is not majorly restricted, and the chance of another driver being in the way, while high, does not require the level of effort to “find” a safe gap between other cars on the road.
- One will notice that as traffic approaches rush hour, the road system approaches 100% capacity. Changing lanes can become very challenging because cars are so close together that increased caution must be exercised to do so.

This is why the long term averages for capacity conservatively estimated at 40% allows for head room for abnormal spikes in load, whether said spikes transitory (such as poorly coded queries that run for a few minutes) or abnormal bursts in general load (the morning of the first day after a long weekend).

The above statement regards % Processor Time calculation being the same as the Utilization Law is a bit of a simplification for the ease of the general reader. For those more mathematically rigorous:  
- Translating the [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10))
  - *B* = The number of 100-ns intervals “Idle” thread spends on the logical processor. The change in the “*X*” variable in the [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10)) calculation
  - *T* = the total number of 100-ns intervals in a given time range. The change in the “*Y*” variable in the [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10)) calculation.
  - *U* k = The utilization percentage of the logical processor by the “Idle Thread” or % Idle Time.  
- Working out the math:
  - *U* k = 1 – %Processor Time
  - %Processor Time = 1 – *U* k
  - %Processor Time = 1 – *B* / *T*
  - %Processor Time = 1 – *X1* – *X0* / *Y1* – *Y0*

### Applying the concepts to capacity planning

The preceding math may make determinations about the number of logical processors needed in a system seem overwhelmingly complex. This is why the approach to sizing the systems is focused on determining maximum target utilization based on current load and calculating the number of logical processors required to get there. Additionally, while logical processor speeds will have a significant impact on performance, cache efficiencies, memory coherence requirements, thread scheduling and synchronization, and imperfectly balanced client load will all have significant impacts on performance that will vary on a server-by-server basis. With the relatively cheap cost of compute power, attempting to analyze and determine the perfect number of CPUs needed becomes more an academic exercise than it does provide business value.

Forty percent is not a hard and fast requirement, it is a reasonable start. Various consumers of Active Directory require various levels of responsiveness. There may be scenarios where environments can run at 80% or 90% utilization as a sustained average, as the increased wait times for access to the processor will not noticeably impact client performance. It is important to re-iterate that there are many areas in the system that are much slower than the logical processor in the system, including access to RAM, access to disk, and transmitting the response over the network. All of these items need to be tuned in conjunction. Examples:

- Adding more processors to a system running 90% that is disk-bound is probably not going to significantly improve performance. Deeper analysis of the system will probably identify that there are a lot of threads that are not even getting on the processor because they are waiting on I/O to complete.
- Resolving the disk-bound issues potentially means that threads that were previously spending a lot of time in a waiting state will no longer be in a waiting state for I/O and there will be more competition for CPU time, meaning that the 90% utilization in the previous example will go to 100% (because it can not go higher). Both components need to be tuned in conjunction.
  > [!NOTE]
  > Processor Information(*)\\% Processor Utility can exceed 100% with systems that have a "Turbo" mode.  This is where the CPU exceeds the rated processor speed for short periods.  Reference CPU manufacturers documentation and description of the counter for greater insight.  

Discussing whole system utilization considerations also brings into the conversation domain controllers as virtualized guests. [Response time/How the system busyness impacts performance](#response-timehow-the-system-busyness-impacts-performance) applies to both the host and the guest in a virtualized scenario. This is why in a host with only one guest, a domain controller (and generally any system) has near the same performance it does on physical hardware. Adding additional guests to the hosts increases the utilization of the underlying host, thereby increasing the wait times to get access to the processors as explained previously. In short, logical processor utilization needs to be managed at both the host and at the guest levels.

Extending the previous analogies, leaving the highway as the physical hardware, the guest VM will be analogized with a bus (an express bus that goes straight to the destination the rider wants). Imagine the following four scenarios:

- It is off hours, a rider gets on a bus that is nearly empty, and the bus gets on a road that is also nearly empty. As there is no traffic to contend with, the rider has a nice easy ride and gets there just as fast as if the rider had driven instead. The rider’s travel times are still constrained by the speed limit.
- It is off hours so the bus is nearly empty but most of the lanes on the road are closed, so the highway is still congested. The rider is on an almost-empty bus on a congested road. While the rider does not have a lot of competition in the bus for where to sit, the total trip time is still dictated by the rest of the traffic outside.
- It is rush hour so the highway and the bus are congested. Not only does the trip take longer, but getting on and off the bus is a nightmare because people are shoulder to shoulder and the highway is not much better. Adding more busses (logical processors to the guest) does not mean they can fit on the road any more easily, or that the trip will be shortened.
- The final scenario, though it may be stretching the analogy a little, is where the bus is full, but the road is not congested. While the rider will still have trouble getting on and off the bus, the trip will be efficient after the bus is on the road. This is the only scenario where adding more busses (logical processors to the guest) will improve guest performance.

From there it is relatively easy to extrapolate that there are a number of scenarios in between the 0%-utilized and the 100%-utilized state of the road and the 0%- and 100%-utilized state of the bus that have varying degrees of impact.

Applying the principals above of 40% CPU as reasonable target for the host as well as the guest is a reasonable start for the same reasoning as above, the amount of queuing.

## Appendix B: Considerations regarding different processor speeds, and the effect of processor power management on processor speeds

Throughout the sections on processor selection the assumption is made that the processor is running at 100% of clock speed the entire time the data is being collected and that the replacement systems will have the same speed processors. Despite both assumptions in practice being false, particularly with Windows Server 2008 R2 and later, where the default power plan is **Balanced**, the methodology still stands as it is the conservative approach. While the potential error rate may increase, it only increases the margin of safety as processor speeds increase.

- For example, in a scenario where 11.25 CPUs are demanded, if the processors were running at half speed when the data was collected, the more accurate estimate might be 5.125 &divide; 2.
- It is impossible to guarantee that doubling the clock speeds would double the amount of processing that happens for a given time period. This is due to the fact the amount of time that the processors spend waiting on RAM or other system components could stay the same. The net effect is that the faster processors might spend a greater percentage of the time idle while waiting on data to be fetched. Again, it is recommended to stick with the lowest common denominator, being conservative, and avoid trying to calculate a potentially false level of accuracy by assuming a linear comparison between processor speeds.

Alternatively, if processor speeds in replacement hardware are lower than current hardware, it would be safe to increase the estimate of processors needed by a proportionate amount. For example, it is calculated that 10 processors are needed to sustain the load in a site, and the current processors are running at 3.3 Ghz and replacement processors will run at 2.6 Ghz, this is a 21% decrease in speed. In this case, 12 processors would be the recommended amount.

That said, this variability would not change the Capacity Management processor utilization targets. As processor clock speeds will be adjusted dynamically based on the load demanded, running the system under higher loads will generate a scenario where the CPU spends more time in a higher clock speed state, making the ultimate goal to be at 40% utilization in a 100% clock speed state at peak. Anything less than that will generate power savings as CPU speeds will be throttled back during off peak scenarios.

> [!NOTE]
> An option would be to turn off power management on the processors (setting the power plan to **High Performance**) while data is collected. That would give a more accurate representation of the CPU consumption on the target server.

To adjust estimates for different processors, it used to be safe, excluding other system bottlenecks outlined above, to assume that doubling processor speeds doubled the amount of processing that could be performed.  Today, the internal architecture of processors is different enough between processors, that a safer way to gauge the effects of using different processors than data was taken from is to leverage the SPECint_rate2006 benchmark from Standard Performance Evaluation Corporation.

1. Find the SPECint_rate2006 scores for the processor that are in use and that plan to be used.
    1. On the website of the Standard Performance Evaluation Corporation, select **Results**, highlight **CPU2006**, and select **Search all SPECint_rate2006 results**.
    1. Under **Simple Request**, enter the search criteria for the target processor, for example **Processor Matches E5-2630 (baselinetarget)** and **Processor Matches E5-2650 (baseline)**.
    1. Find the server and processor configuration to be used (or something close, if an exact match is not available) and note the value in the **Result** and **# Cores** columns.
1. To determine the modifier use the following equation:
   >((*Target platform per-core score value*) &times; (*MHz per-core of baseline platform*)) &divide; ((*Baseline per-core score value*) &times; (*MHz per-core of target platform*))  

    Using the above example:
   >(35.83 &times; 2000) &divide; (33.75 &times; 2300) = 0.92
1. Multiply the estimated number of processors by the modifier.  In the above case to go from the E5-2650 processor to the E5-2630 processor multiply the calculated 11.25 CPUs &times; 0.92 = 10.35 processors needed.

## Appendix C: Fundamentals regarding the operating system interacting with storage

The queuing theory concepts outlined in [Response time/How the system busyness impacts performance](#response-timehow-the-system-busyness-impacts-performance) are also applicable to storage. Having a familiarity of how the operating system handles I/O is necessary to apply these concepts. In the Microsoft Windows operating system, a queue to hold the I/O requests is created for each physical disk. However, a clarification on physical disk needs to be made. Array controllers and SANs present aggregations of spindles to the operating system as single physical disks. Additionally, array controllers and SANs can aggregate multiple disks into one array set and then split this array set into multiple “partitions”, which is in turn presented to the operating system as multiple physical disks (ref. figure).

![Block spindles](media/capacity-planning-considerations-block-spindles.png)  

In this figure the two spindles are mirrored and split into logical areas for data storage (Data 1 and Data 2). These logical areas are viewed by the operating system as separate physical disks.

Although this can be highly confusing, the following terminology is used throughout this appendix to identify the different entities:

- **Spindle –** the device that is physically installed in the server.
- **Array –** a collection of spindles aggregated by controller.
- **Array partition –** a partitioning of the aggregated array
- **LUN –** an array, used when referring to SANs
- **Disk –** What the operating system observes to be a single physical disk.
- **Partition –** a logical partitioning of what the operating system perceives as a physical disk.

### Operating system architecture considerations

The operating system creates a First In/First Out (FIFO) I/O queue for each disk that is observed; this disk may be representing a spindle, an array, or an array partition. From the operating system perspective, with regard to handling I/O, the more active queues the better. As a FIFO queue is serialized, meaning that all I/Os issued to the storage subsystem must be processed in the order the request arrived. By correlating each disk observed by the operating system with a spindle/array, the operating system now maintains an I/O queue for each unique set of disks, thereby eliminating contention for scarce I/O resources across disks and isolating I/O demand to a single disk. As an exception, Windows Server 2008 introduces the concept of I/O prioritization, and applications designed to use the “Low” priority fall out of this normal order and take a back seat. Applications not specifically coded to leverage the “Low” priority default to “Normal.”

### Introducing simple storage subsystems

Starting with a simple example (a single hard drive inside a computer) a component-by-component analysis will be given. Breaking this down into the major storage subsystem components, the system consists of:

- **1 –** 10,000 RPM Ultra Fast SCSI HD (Ultra Fast SCSI has a 20 MB/s transfer rate)
- **1 –** SCSI Bus (the cable)
- **1 –** Ultra Fast SCSI Adapter
- **1 –** 32-bit 33 MHz PCI bus

Once the components are identified, an idea of how much data can transit the system, or how much I/O can be handled, can be calculated. Note that the amount of I/O and quantity of data that can transit the system is correlated, but not the same. This correlation depends on whether the disk I/O is random or sequential and the block size. (All data is written to the disk as a block, but different applications using different block sizes.) On a component-by-component basis:

- **The hard drive –** The average 10,000-RPM hard drive has a 7-millisecond (ms) seek time and a 3 ms access time. Seek time is the average amount of time it takes the read/write head to move to a location on the platter. Access time is the average amount of time it takes to read or write the data to disk, once the head is in the correct location. Thus, the average time for reading a unique block of data in a 10,000-RPM HD constitutes a seek and an access, for a total of approximately 10 ms (or .010 seconds) per block of data.

  When every disk access requires movement of the head to a new location on the disk, the read/write behavior is referred to as “random.” Thus, when all I/O is random, a 10,000-RPM HD can handle approximately 100 I/O per second (IOPS) (the formula is 1000 ms per second divided by 10 ms per I/O or 1000/10=100 IOPS).

  Alternatively, when all I/O occurs from adjacent sectors on the HD, this is referred to as sequential I/O. Sequential I/O has no seek time because when the first I/O is complete, the read/write head is at the start of where the next block of data is stored on the HD. Thus a 10,000-RPM HD is capable of handling approximately 333 I/O per second (1000 ms per second divided by 3 ms per I/O).

  >[!NOTE]
  >This example does not reflect the disk cache, where the data of one cylinder is typically kept. In this case, the 10 ms are needed on the first I/O and the disk reads the whole cylinder. All other sequential I/O is satisfied from the cache. As a result, in-disk caches might improve sequential I/O performance.
  
  So far, the transfer rate of the hard drive has been irrelevant. Whether the hard drive is 20 MB/s Ultra Wide or an Ultra3 160 MB/s, the actual amount of IOPS the can be handled by the 10,000-RPM HD is ~100 random or ~300 sequential I/O. As block sizes change based on the application writing to the drive, the amount of data that is pulled per I/O is different. For example, if the block size is 8 KB, 100 I/O operations will read from or write to the hard drive a total of 800 KB. However, if the block size is 32 KB, 100 I/O will read/write 3,200 KB (3.2 MB) to the hard drive. As long as the SCSI transfer rate is in excess of the total amount of data transferred, getting a “faster” transfer rate drive will gain nothing. See the following tables for comparison.

  | |7200 RPM 9ms seek, 4ms access|10,000 RPM 7ms seek, 3ms access|15,000 RPM 4ms seek, 2ms access
  |-|-|-|-|
  |Random I/O|80|100|150|
  |Sequential I/O|250|300|500|  
  
  |10,000 RPM drive|8 KB block size (Active Directory Jet)|
  |-|-|
  |Random I/O|800 KB/s|
  |Sequential I/O|2400 KB/s|

- **SCSI backplane (bus) –** Understanding how the “SCSI backplane (bus)”, or in this scenario the ribbon cable, impacts throughput of the storage subsystem depends on knowledge of the block size. Essentially the question would be, how much I/O can the bus handle if the I/O is in 8 KB blocks? In this scenario, the SCSI bus is 20 MB/s, or 20480 KB/s. 20480 KB/s divided by 8 KB blocks yields a maximum of approximately 2500 IOPS supported by the SCSI bus.

  >[!NOTE]
  >The figures in the following table represent an example. Most attached storage devices currently use PCI Express, which provides much higher throughput.  
  
  |I/O supported by SCSI bus per block size|2 KB block size|8 KB block size (AD Jet) (SQL Server 7.0/SQL Server 2000)
  |-|-|-|
  |20 MB/s|10,000|2,500|
  |40 MB/s|20,000|5,000|
  |128 MB/s|65,536|16,384|
  |320 MB/s|160,000|40,000|

  As can be determined from this chart, in the scenario presented, no matter what the use, the bus will never be a bottleneck, as the spindle maximum is 100 I/O, well below any of the above thresholds.

  >[!NOTE]
  >This assumes that the SCSI bus is 100% efficient.
  
- **SCSI adapter –** For determining the amount of I/O that this can handle, the manufacturer’s specifications need to be checked. Directing I/O requests to the appropriate device requires processing of some sort, thus the amount of I/O that can be handled is dependent on the SCSI adapter (or array controller) processor.

  In this example, the assumption that 1,000 I/O can be handled will be made.

- **PCI bus –** This is an often overlooked component. In this example, this will not be the bottleneck; however as systems scale up, it can become a bottleneck. For reference, a 32 bit PCI bus operating at 33Mhz can in theory transfer 133 MB/s of data. Following is the equation:  
  > 32 bits &divide; 8 bits per byte &times; 33 MHz = 133 MB/s.  

  Note that is the theoretical limit; in reality only about 50% of the maximum is actually reached, although in certain burst scenarios, 75% efficiency can be obtained for short periods.

  A 66Mhz 64-bit PCI bus can support a theoretical maximum of (64 bits &divide; 8 bits per byte &times; 66 Mhz) = 528 MB/sec. Additionally, any other device (such as the network adapter, second SCSI controller, and so on) will reduce the bandwidth available as the bandwidth is shared and the devices will contend for the limited resources.

After analysis of the components of this storage subsystem, the spindle is the limiting factor in the amount of I/O that can be requested, and consequently the amount of data that can transit the system. Specifically, in an AD DS scenario, this is 100 random I/O per second in 8 KB increments, for a total of 800 KB per second when accessing the Jet database. Alternatively, the maximum throughput for a spindle that is exclusively allocated to log files would suffer the following limitations: 300 sequential I/O per second in 8 KB increments, for a total of 2400 KB (2.4 MB) per second.

Now, having analyzed a simple configuration, the following table demonstrates where the bottleneck will occur as components in the storage subsystem are changed or added.

|Notes|Bottleneck analysis|Disk|Bus|Adapter|PCI bus|
|-|-|-|-|-|-|
|This is the domain controller configuration after adding a second disk. The disk configuration represents the bottleneck at 800 KB/s.|Add 1 disk (Total=2)<br /><br />I/O is random<br /><br />4 KB block size<br /><br />10,000 RPM HD|200 I/Os total<br />800 KB/s total.| | | |
|After adding 7 disks, the disk configuration still represents the bottleneck at 3200 KB/s.|**Add 7 disks (Total=8)**  <br /><br />I/O is random<br /><br />4 KB block size<br /><br />10,000 RPM HD|800 I/Os total.<br />3200 KB/s total| | | |
|After changing I/O to sequential, the network adapter becomes the bottleneck because it is limited to 1000 IOPS.|Add 7 disks (Total=8)<br /><br />**I/O is sequential**<br /><br />4 KB block size<br /><br />10,000 RPM HD| | |2400 I/O sec can be read/written to disk, controller limited to 1000 IOPS| |
|After replacing the network adapter with a SCSI adapter that supports 10,000 IOPS, the bottleneck returns to the disk configuration.|Add 7 disks (Total=8)<br /><br />I/O is random<br /><br />4 KB block size<br /><br />10,000 RPM HD<br /><br />**Upgrade SCSI adapter (now supports 10,000 I/O)**|800 I/Os total.<br />3,200 KB/s total| | | |
|After increasing the block size to 32 KB, the bus becomes the bottleneck because it only supports 20 MB/s.|Add 7 disks (Total=8)<br /><br />I/O is random<br /><br />**32 KB block size**<br /><br />10,000 RPM HD| |800 I/Os total. 25,600 KB/s (25 MB/s) can be read/written to disk.<br /><br />The bus only supports 20 MB/s| | |
|After upgrading the bus and adding more disks, the disk remains the bottleneck.|**Add 13 disks (Total=14)**<br /><br />Add second SCSI adapter with 14 disks<br /><br />I/O is random<br /><br />4 KB block size<br /><br />10,000 RPM HD<br /><br />**Upgrade to 320 MB/s SCSI bus**|2800 I/Os<br /><br />11,200 KB/s (10.9 MB/s)| | | |
|After changing I/O to sequential, the disk remains the bottleneck.|Add 13 disks (Total=14)<br /><br />Add second SCSI Adapter with 14 disks<br /><br />**I/O is sequential**<br /><br />4 KB block size<br /><br />10,000 RPM HD<br /><br />Upgrade to 320 MB/s SCSI bus|8,400 I/Os<br /><br />33,600 KB\s<br /><br />(32.8 MB\s)| | | |
|After adding faster hard drives, the disk remains the bottleneck.|Add 13 disks (Total=14)<br /><br />Add second SCSI adapter with 14 disks<br /><br />I/O is sequential<br /><br />4 KB block size<br /><br />**15,000 RPM HD**<br /><br />Upgrade to 320 MB/s SCSI bus|14,000 I/Os<br /><br />56,000 KB/s<br /><br />(54.7 MB/s)| | | |
|After increasing the block size to 32 KB, the PCI bus becomes the bottleneck.|Add 13 disks (Total=14)<br /><br />Add second SCSI adapter with 14 disks<br /><br />I/O is sequential<br /><br />**32 KB block size**<br /><br />15,000 RPM HD<br /><br />Upgrade to 320 MB/s SCSI bus| | | |14,000 I/Os<br /><br />448,000 KB/s<br /><br />(437 MB/s) is the read/write limit to the spindle.<br /><br />The PCI bus supports a theoretical maximum of 133 MB/s (75% efficient at best).|

### Introducing RAID

The nature of a storage subsystem does not change dramatically when an array controller is introduced; it just replaces the SCSI adapter in the calculations. What does change is the cost of reading and writing data to the disk when using the various array levels (such as RAID 0, RAID 1, or RAID 5).

In RAID 0, the data is striped across all the disks in the RAID set. This means that during a read or a write operation, a portion of the data is pulled from or pushed to each disk, increasing the amount of data that can transit the system during the same time period. Thus, in one second, on each spindle (again assuming 10,000-RPM drives), 100 I/O operations can be performed. The total amount of I/O that can be supported is N spindles times 100 I/O per second per spindle (yields 100*N I/O per second).

![Logical d: drive](media/capacity-planning-considerations-logical-d-drive.png)

In RAID 1, the data is mirrored (duplicated) across a pair of spindles for redundancy. Thus, when a read I/O operation is performed, data can be read from both of the spindles in the set. This effectively makes the I/O capacity from both disks available during a read operation. The caveat is that write operations gain no performance advantage in a RAID 1. This is because the same data needs to be written to both drives for the sake of redundancy. Though it does not take any longer, as the write of data occurs concurrently on both spindles, because both spindles are occupied duplicating the data, a write I/O operation in essence prevents two read operations from occurring. Thus, every write I/O costs two read I/O. A formula can be created from that information to determine the total number of I/O operations that are occurring:  

> *Read I/O* + 2 &times; *Write I/O* = *Total available disk I/O consumed*  

When the ratio of reads to writes and the number of spindles are known, the following equation can be derived from the above equation to identify the maximum I/O that can be supported by the array:  

> *Maximum IOPS per spindle* &times; 2 spindles &times; [(*%Reads* + *%Writes*) &divide; (*%Reads* + 2 &times; *%Writes*)] = *Total IOPS*

RAID 1+ 0, behaves exactly the same as RAID 1 regarding the expense of reading and writing. However, the I/O is now striped across each mirrored set. If  

> *Maximum IOPS per spindle* &times; 2 spindles &times; [(*%Reads* + *%Writes*) &divide; (*%Reads* + 2 &times; *%Writes*)] = *Total I/O*  

in a RAID 1 set, when a multiplicity (*N*) of RAID 1 sets are striped, the Total I/O that can be processed becomes N &times; I/O per RAID 1 set:  

> *N* &times; {*Maximum IOPS per spindle* &times; 2 spindles &times; [(*%Reads* + *%Writes*) &divide; (*%Reads* + 2 &times; *%Writes*)] } = *Total IOPS*

In RAID 5, sometimes referred to as *N* + 1 RAID, the data is striped across *N* spindles and parity information is written to the “+ 1” spindle. However, RAID 5 is much more expensive when performing a write I/O than RAID 1 or 1 + 0. RAID 5 performs the following process every time a write I/O is submitted to the array:

1. Read the old data
1. Read the old parity
1. Write the new data
1. Write the new parity

As every write I/O request that is submitted to the array controller by the operating system requires four I/O operations to complete, write requests submitted take four times as long to complete as a single read I/O. To derive a formula to translate I/O requests from the operating system perspective to that experienced by the spindles:  

> *Read I/O* + 4 &times; *Write I/O* = *Total I/O*  

Similarly in a RAID 1 set, when the ratio of reads to writes and the number of spindles are known, the following equation can be derived from the above equation to identify the maximum I/O that can be supported by the array (Note that total number of spindles does not include the “drive” lost to parity):  

> *IOPS per spindle* &times; (*Spindles* – 1) &times; [(*%Reads* + *%Writes*) &divide; (*%Reads* + 4 &times; *%Writes*)] = *Total IOPS*

### Introducing SANs

Expanding the complexity of the storage subsystem, when a SAN is introduced into the environment, the basic principles outlined do not change, however I/O behavior for all of the systems connected to the SAN needs to be taken into account. As one of the major advantages in using a SAN is an additional amount of redundancy over internally or externally attached storage, capacity planning now needs to take into account fault tolerance needs. Also, more components are introduced that need to be evaluated. Breaking a SAN down into the component parts:

- SCSI or Fibre Channel hard drive
- Storage unit channel backplane
- Storage units
- Storage controller module
- SAN switch(es)
- HBA(s)
- The PCI bus

When designing any system for redundancy, additional components are included to accommodate the potential of failure. It is very important, when capacity planning, to exclude the redundant component from available resources. For example, if the SAN has two controller modules, the I/O capacity of one controller module is all that should be used for total I/O throughput available to the system. This is due to the fact that if one controller fails, the entire I/O load demanded by all connected systems will need to be processed by the remaining controller. As all capacity planning is done for peak usage periods, redundant components should not be factored into the available resources and planned peak utilization should not exceed 80% saturation of the system (in order to accommodate bursts or anomalous system behavior). Similarly, the redundant SAN switch, storage unit, and spindles should not be factored into the I/O calculations.

When analyzing the behavior of the SCSI or Fibre Channel hard drive, the method of analyzing the behavior as outlined previously does not change. Although there are certain advantages and disadvantages to each protocol, the limiting factor on a per disk basis is the mechanical limitation of the hard drive.

Analyzing the channel on the storage unit is exactly the same as calculating the resources available on the SCSI bus, or bandwidth (such as 20 MB/s) divided by block size (such as 8 KB). Where this deviates from the simple previous example is in the aggregation of multiple channels. For example, if there are 6 channels, each supporting 20 MB/s maximum transfer rate, the total amount of I/O and data transfer that is available is 100 MB/s (this is correct, it is not 120 MB/s). Again, fault tolerance is a major player in this calculation, in the event of the loss of an entire channel, the system is only left with 5 functioning channels. Thus, to ensure continuing to meet performance expectations in the event of failure, total throughput for all of the storage channels should not exceed 100 MB/s (this assumes load and fault tolerance is evenly distributed across all channels). Turning this into an I/O profile is dependent on the behavior of the application. In the case of Active Directory Jet I/O, this would correlate to approximately 12,500 I/O per second (100 MB/s &divide; 8 KB per I/O).

Next, obtaining the manufacturer’s specifications for the controller modules is required in order to gain an understanding of the throughput each module can support. In this example, the SAN has two controller modules that support 7,500 I/O each. The total throughput of the system may be 15,000 IOPS if redundancy is not desired. In calculating maximum throughput in the case of failure, the limitation is the throughput of one controller, or 7,500 IOPS. This threshold is well below the 12,500 IOPS (assuming 4 KB block size) maximum that can be supported by all of the storage channels, and thus, is currently the bottleneck in the analysis. Still for planning purposes, the desired maximum I/O to be planned for would be 10,400 I/O.

When the data exits the controller module, it transits a Fibre Channel connection rated at 1 GB/s (or 1 Gigabit per second). To correlate this with the other metrics, 1 GB/s turns into 128 MB/s (1 GB/s &divide; 8 bits/byte). As this is in excess of the total bandwidth across all channels in the storage unit (100 MB/s), this will not bottleneck the system. Additionally, as this is only one of the two channels (the additional 1 GB/s Fibre Channel connection being for redundancy), if one connection fails, the remaining connection still has enough capacity to handle all the data transfer demanded.

En route to the server, the data will most likely transit a SAN switch. As the SAN switch has to process the incoming I/O request and forward it out the appropriate port, the switch will have a limit to the amount of I/O that can be handled, however, manufacturers specifications will be required to determine what that limit is. For example, if there are two switches and each switch can handle 10,000 IOPS, the total throughput will be 20,000 IOPS. Again, fault tolerance being a concern, if one switch fails, the total throughput of the system will be 10,000 IOPS. As it is desired not to exceed 80% utilization in normal operation, using no more than 8000 I/O should be the target.

Finally, the HBA installed in the server would also have a limit to the amount of I/O that it can handle. Usually, a second HBA is installed for redundancy, but just like with the SAN switch, when calculating maximum I/O that can be handled, the total throughput of *N* &ndash; 1 HBAs is what the maximum scalability of the system is.

### Caching considerations

Caches are one of the components that can significantly impact the overall performance at any point in the storage system. Detailed analysis about caching algorithms is beyond the scope of this article; however, some basic statements about caching on disk subsystems are worth illuminating:

- Caching does improved sustained sequential write I/O as it can buffer many smaller write operations into larger I/O blocks and de-stage to storage in fewer, but larger block sizes. This will reduce total random I/O and total sequential I/O, thus providing more resource availability for other I/O.
- Caching does not improve sustained write I/O throughput of the storage subsystem. It only allows for the writes to be buffered until the spindles are available to commit the data. When all the available I/O of the spindles in the storage subsystem is saturated for long periods, the cache will eventually fill up. In order to empty the cache, enough time between bursts, or extra spindles, need to be allotted in order to provide enough I/O to allow the cache to flush.

  Larger caches only allow for more data to be buffered. This means longer periods of saturation can be accommodated.

  In a normally operating storage subsystem, the operating system will experience improved write performance as the data only needs to be written to cache. Once the underlying media is saturated with I/O, the cache will fill and write performance will return to disk speed.

- When caching read I/O, the scenario where the cache is most advantageous is when the data is stored sequentially on the disk, and the cache can read-ahead (it makes the assumption that the next sector contains the data that will be requested next).
- When read I/O is random, caching at the drive controller is unlikely to provide any enhancement to the amount of data that can be read from the disk. Any enhancement is non-existent if the operating system or application-based cache size is greater than the hardware-based cache size.

  In the case of Active Directory, the cache is only limited by the amount of RAM.

### SSD considerations

SSDs are a completely different animal than spindle-based hard disks. Yet the two key criteria remain: “How many IOPS can it handle?” and “What is the latency for those IOPS?” In comparison to spindle-based hard disks, SSDs can handle higher volumes of I/O and can have lower latencies. In general and as of this writing, while SSDs are still expensive in a cost-per-Gigabyte comparison, they are very cheap in terms of cost-per-I/O and deserve significant consideration in terms of storage performance.

Considerations:

- Both IOPS and latencies are very subjective to the manufacturer designs and in some cases have been observed to be poorer performing than spindle based technologies. In short, it is more important to review and validate the manufacturer specs drive by drive and not assume any generalities.
- IOPS types can have very different numbers depending on whether it is read or write. AD DS services, in general, being predominantly read-based, will be less affected than some other application scenarios.
- “Write endurance” – this is the concept that SSD cells will eventually wear out. Various manufacturers deal with this challenge different fashions. At least for the database drive, the predominantly read I/O profile allows for downplaying the significance of this concern as the data is not highly volatile.

### Summary

One way to think about storage is picturing household plumbing. Imagine the IOPS of the media that the data is stored on is the household main drain. When this is clogged (such as roots in the pipe) or limited (it is collapsed or too small), all the sinks in the household back up when too much water is being used (too many guests). This is perfectly analogous to a shared environment where one or more systems are leveraging shared storage on an SAN/NAS/iSCSI with the same underlying media. Different approaches can be taken to resolve the different scenarios:

- A collapsed or undersized drain requires a full scale replacement and fix. This would be similar to adding in new hardware or redistributing the systems using the shared storage throughout the infrastructure.
- A “clogged” pipe usually means identification of one or more offending problems and removal of those problems. In a storage scenario this could be storage or system level backups, synchronized antivirus scans across all servers, and synchronized defragmentation software running during peak periods.

In any plumbing design, multiple drains feed into the main drain. If anything stops up one of those drains or a junction point, only the things behind that junction point back up. In a storage scenario, this could be an overloaded switch (SAN/NAS/iSCSI scenario), driver compatibility issues (wrong driver/HBA Firmware/storport.sys combination), or backup/antivirus/defragmentation. To determine if the storage “pipe” is big enough, IOPS and I/O size needs to be measured. At each joint add them together to ensure adequate “pipe diameter.”

## Appendix D - Discussion on storage troubleshooting - Environments where providing at least as much RAM as the database size is not a viable option

It is helpful to understand why these recommendations exist so that the changes in storage technology can be accommodated. These recommendations exist for two reasons. The first is isolation of IO, such that performance issues (that is, paging) on the operating system spindle do not impact performance of the database and I/O profiles. The second is that log files for AD DS (and most databases) are sequential in nature, and spindle-based hard drives and caches have a huge performance benefit when used with sequential I/O as compared to the more random I/O patterns of the operating system and almost purely random I/O patterns of the AD DS database drive. By isolating the sequential I/O to a separate physical drive, throughput can be increased. The challenge presented by today’s storage options is that the fundamental assumptions behind these recommendations are no longer true. In many virtualized storage scenarios, such as iSCSI, SAN, NAS, and Virtual Disk image files, the underlying storage media is shared across multiple hosts, thus completely negating both the “isolation of IO” and the “sequential I/O optimization” aspects. In fact these scenarios add an additional layer of complexity in that other hosts accessing the shared media can degrade responsiveness to the domain controller.

In planning storage performance, there are three categories to consider: cold cache state, warmed cache state, and backup/restore. The cold cache state occurs in scenarios such as when the domain controller is initially rebooted or the Active Directory service is restarted and there is no Active Directory data in RAM. Warm cache state is where the domain controller is in a steady state and the database is cached. These are important to note as they will drive very different performance profiles, and having enough RAM to cache the entire database does not help performance when the cache is cold. One can consider performance design for these two scenarios with the following analogy, warming the cold cache is a “sprint” and running a server with a warm cache is a “marathon.”

For both the cold cache and warm cache scenario, the question becomes how fast the storage can move the data from disk into memory. Warming the cache is a scenario where, over time, performance improves as more queries reuse data, the cache hit rate increases, and the frequency of needing to go to disk decreases. As a result the adverse performance impact of going to disk decreases. Any degradation in performance is only transient while waiting for the cache to warm and grow to the maximum, system-dependent allowed size. The conversation can be simplified to how quickly the data can be gotten off of disk, and is a simple measure of the IOPS available to Active Directory, which is subjective to IOPS available from the underlying storage. From a planning perspective, because warming the cache and backup/restore scenarios happen on an exceptional basis, normally occur off hours, and are subjective to the load of the DC, general recommendations do not exist except in that these activities be scheduled for non-peak hours.

AD DS, in most scenarios, is predominantly read IO, usually a ratio of 90% read/10% write. Read I/O often tends to be the bottleneck for user experience, and with write IO, causes write performance to degrade. As I/O to the NTDS.dit is predominantly random, caches tend to provide minimal benefit to read IO, making it that much more important to configure the storage for read I/O profile correctly.

For normal operating conditions, the storage planning goal is minimize the wait times for a request from AD DS to be returned from disk. This essentially means that the number of outstanding and pending I/O is less than or equivalent to the number of pathways to the disk. There are a variety of ways to measure this. In a performance monitoring scenario, the general recommendation is that LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read be less than 20 ms. The desired operating threshold must be much lower, preferably as close to the speed of the storage as possible, in the 2 to 6 millisecond (.002 to .006 second) range depending on the type of storage.

Example:

![Storage latency chart](media/capacity-planning-considerations-storage-latency.png)

Analyzing the chart:

- **Green oval on the left –** The latency remains consistent at 10 ms. The load increases from 800 IOPS to 2400 IOPS. This is the absolute floor to how quickly an I/O request can be processed by the underlying storage. This is subject to the specifics of the storage solution.
- **Burgundy oval on the right –** The throughput remains flat from the exit of the green circle through to the end of the data collection while the latency continues to increase. This is demonstrating that when the request volumes exceed the physical limitations of the underlying storage, the longer the requests spend sitting in the queue waiting to be sent out to the storage subsystem.

Applying this knowledge:

- **Impact to a user querying membership of a large group –** Assume this requires reading 1 MB of data from the disk, the amount of I/O and how long it takes can be evaluated as follows:
  - Active Directory database pages are 8 KB in size. 
  - A minimum of 128 pages need to be read in from disk. 
  - Assuming nothing is cached, at the floor (10 ms) this is going to take a minimum 1.28 seconds to load the data from disk in order to return it to the client. At 20 ms, where the throughput on storage has long since maxed out and is also the recommended maximum, it will take 2.5 seconds to get the data from disk in order to return it to the end user.  
- **At what rate will the cache be warmed –** Making the assumption that the client load is going to maximize the throughput on this storage example, the cache will warm at a rate of 2400 IOPS &times; 8 KB per IO. Or, approximately 20 MB/s per second, loading about 1 GB of database into RAM every 53 seconds.

> [!NOTE]
> It is normal for short periods to observe the latencies climb when components aggressively read or write to disk, such as when the system is being backed up or when AD DS is running garbage collection. Additional head room on top of the calculations should be provided to accommodate these periodic events. The goal being to provide enough throughput to accommodate these scenarios without impacting normal function.

As can be seen, there is a physical limit based on the storage design to how quickly the cache can possibly warm. What will warm the cache are incoming client requests up to the rate that the underlying storage can provide. Running scripts to “pre-warm” the cache during peak hours will provide competition to load driven by real client requests. That can adversely affect delivering data that clients need first because, by design, it will generate competition for scarce disk resources as artificial attempts to warm the cache will load data that is not relevant to the clients contacting the DC.Processor Information(_Total)\\` Processor Utility Domain Services
description: Detailed discussion of the factors to consider during capacity planning for AD DS.
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; kenbrunf
author: Teresa-Motiv
ms.date: 7/3/2019
---

# Capacity planning for Active Directory Domain Services

This topic is originally written by Ken Brumfield, Senior Premier Field Engineer at Microsoft, and provides recommendations for capacity planning for Active Directory Domain Services (AD DS).

## Goals of capacity planning

Capacity planning is not the same as troubleshooting performance incidents. They are closely related, but quite different. The goals of capacity planning are:  

- Properly implement and operate an environment 
- Minimize the time spent troubleshooting performance issues.  
  
In capacity planning, an organization might have a baseline target of 40% processor utilization during peak periods in order to meet client performance requirements and accommodate the time necessary to upgrade the hardware in the datacenter. Whereas, to be notified of abnormal performance incidents, a monitoring alert threshold might be set at 90% over a 5 minute interval.

The difference is that when a capacity management threshold is continually exceeded (a one-time event is not a concern), adding capacity (that is, adding in more or faster processors) would be a solution or scaling the service across multiple servers would be a solution. Performance alert thresholds indicate that client experience is currently suffering and immediate steps are needed to address the issue.

As an analogy: capacity management is about preventing a car accident (defensive driving, making sure the brakes are working properly, and so on) whereas performance troubleshooting is what the police, fire department, and emergency medical professionals do after an accident. This is about “defensive driving,” Active Directory-style.

Over the last several years, capacity planning guidance for scale-up systems has changed dramatically. The following changes in system architectures have challenged fundamental assumptions about designing and scaling a service:

- 64-bit server platforms  
- Virtualization  
- Increased attention to power consumption  
- SSD storage  
- Cloud scenarios  

Additionally, the approach is shifting from a server-based capacity planning exercise to a service-based capacity planning exercise. Active Directory Domain Services (AD DS), a mature distributed service that many Microsoft and third-party products use as a backend, becomes one the most critical products to plan correctly to ensure the necessary capacity for other applications to run.

### Baseline requirements for capacity planning guidance

Throughout this article, the following baseline requirements are expected:

- Readers have read and are familiar with [Performance Tuning Guidelines for Windows Server 2012 R2](https://docs.microsoft.com/previous-versions//dn529133(v=vs.85)).
- The Windows Server platform is an x64 based architecture. But even if your Active Directory environment is installed on Windows Server 2003 x86 (now beyond the end of the support lifecycle) and has a directory information tree (DIT) that is less 1.5 GB in size and that can easily be held in memory, the guidelines from this article are still applicable.
- Capacity planning is a continuous process and you should regularly review how well the environment is meeting expectations.
- Optimization will occur over multiple hardware lifecycles as hardware costs change. For example, memory becomes cheaper, the cost per core decreases, or the price of different storage options change.
- Plan for the peak busy period of the day. It is recommended to look at this in either 30 minute or hour intervals. Anything greater may hide the actual peaks and anything less may be distorted by “transient spikes.”
- Plan for growth over the course of the hardware lifecycle for the enterprise. This may include a strategy of upgrading or adding hardware in a staggered fashion, or a complete refresh every three to five years. Each will require a “guess” as how much the load on Active Directory will grow. Historical data, if collected, will help with this assessment. 
- Plan for fault tolerance. Once an estimate *N* is derived, plan for scenarios that include *N* &ndash; 1, *N* &ndash; 2, *N* &ndash; *x*.
  - Add in additional servers according to organizational need to ensure that the loss of a single or multiple servers does not exceed maximum peak capacity estimates.
  - Also consider that the growth plan and fault tolerance plan need to be integrated. For example, if one DC is required to support the load, but the estimate is that the load will be doubled in the next year and require two DCs total, there will not be enough capacity to support fault tolerance. The solution would be to start with three DCs. One could also plan to add the third DC after 3 or 6 months if budgets are tight.

    >[!NOTE]
    >Adding Active Directory-aware applications might have a noticeable impact on the DC load, whether the load is coming from the application servers or clients.

### Three-step process for the capacity planning cycle

In capacity planning, first decide what quality of service is needed. For example, a core datacenter supports a higher level of concurrency and requires more consistent experience for users and consuming applications, which requires greater attention to redundancy and minimizing system and infrastructure bottlenecks. In contrast, a satellite location with a handful of users does not need the same level of concurrency or fault tolerance. Thus, the satellite office might not need as much attention to optimizing the underlying hardware and infrastructure, which may lead to cost savings. All recommendations and guidance herein are for optimal performance, and can be selectively relaxed for scenarios with less demanding requirements.

The next question is: virtualized or physical? From a capacity planning perspective, there is no right or wrong answer; there is only a different set of variables to work with. Virtualization scenarios come down to one of two options:

- “Direct mapping” with one guest per host (where virtualization exists solely to abstract the physical hardware from the server)
- “Shared host”

Testing and production scenarios indicate that the “direct mapping” scenario can be treated identically to a physical host. “Shared host,” however, introduces a number of considerations spelled out in more detail later. The “shared host” scenario means that AD DS is also competing for resources, and there are penalties and tuning considerations for doing so.

With these considerations in mind, the capacity planning cycle is an iterative three-step process:

1. Measure the existing environment, determine where the system bottlenecks currently are, and get environmental basics necessary to plan the amount of capacity needed.
1. Determine the hardware needed according to the criteria outlined in step 1.
1. Monitor and validate that the infrastructure as implemented is operating within specifications. Some data collected in this step becomes the baseline for the next cycle of capacity planning.

### Applying the process

To optimize performance, ensure these major components are correctly selected and tuned to the application loads:

1. Memory
1. Network
1. Storage
1. Processor
1. Net Logon

The basic storage requirements of AD DS and the general behavior of well written client software allow environments with as many as 10,000 to 20,000 users to forego heavy investment in capacity planning with regards to physical hardware, as almost any modern server class system will handle the load. That said, the following table summarizes how to evaluate an existing environment in order to select the right hardware. Each component is analyzed in detail in subsequent sections to help AD DS administrators evaluate their infrastructure using baseline recommendations and environment-specific principals.

In general:

- Any sizing based on current data will only be accurate for the current environment.
- For any estimates, expect demand to grow over the lifecycle of the hardware.
- Determine whether to oversize today and grow into the larger environment, or add capacity over the lifecycle.
- For virtualization, all the same capacity planning principals and methodologies apply, except that the overhead of the virtualization needs to be added to anything domain related.
- Capacity planning, like anything that attempts to predict, is NOT an accurate science. Do not expect things to calculate perfectly and with 100% accuracy. The guidance here is the leanest recommendation; add in capacity for additional safety and continuously validate that the environment remains on target.

### Data collection summary tables

#### New environment

| Component | Estimates |
|-|-|
|Storage/Database Size|40 KB to 60 KB for each user|
|RAM|Database Size<br />Base operating system recommendations<br />Third-party applications|
|Network|1 GB|
|CPU|1000 concurrent users for each core|

#### High-level evaluation criteria

| Component | Evaluation criteria | Planning considerations |
|-|-|-|
|Storage/Database size|The section entitled “To activate logging of disk space that is freed by defragmentation” in [Storage Limits](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10))| |
|Storage/ Database performance|<ul><li>"LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read," "LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Write," "LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Transfer"</li><li>"LogicalDisk(*\<NTDS Database Drive\>*)\Reads/sec," "LogicalDisk(*\<NTDS Database Drive\>*)\Writes/sec," "LogicalDisk(*\<NTDS Database Drive\>*)\Transfers/sec"</li></ul>|<ul><li>Storage has two concerns to address<ul><li>Space available, which with the size of today’s spindle based and SSD based storage is irrelevant for most AD environments.</li> <li>Input/Output (IO) Operations available – In many environments, this is often overlooked. But it is important to evaluate only environments where there is not enough RAM to load the entire NTDS Database into memory.</li></ul><li>Storage can be a complex topic and should involve hardware vendor expertise for proper sizing. Particularly with more complex scenarios such as SAN, NAS, and iSCSI scenarios. However, in general, cost per Gigabyte of storage is often in direct opposition to cost per IO:<ul><li>RAID 5 has lower cost per Gigabyte than Raid 1, but Raid 1 has lower cost per IO</li><li>Spindle-based hard drives have lower cost per Gigabyte, but SSDs have a lower cost per IO</li></ul><li>After a restart of the computer or the Active Directory Domain Services service, the Extensible Storage Engine (ESE) cache is empty and performance will be disk bound while the cache warms.</li><li>In most environments AD is read intensive I/O in a random pattern to disks, negating much of the benefit of caching and read optimization strategies.  Plus, AD has a way larger cache in memory than most storage system caches.</li></ul>
|RAM|<ul><li>Database size</li><li>Base operating system recommendations</li><li>Third-party applications</li></ul>|<ul><li>Storage is the slowest component in a computer. The more that can be resident in RAM, the less it is necessary to go to disk.</li><li>Ensure enough RAM is allocated to store the operating system, Agents (antivirus, backup, monitoring), NTDS Database and growth over time.</li><li>For environments where maximizing the amount of RAM is not cost effective (such as a satellite locations) or not feasible (DIT is too large), reference the Storage section to ensure that storage is properly sized.</li></ul>|
|Network|<ul><li>“Network Interface(\*)\Bytes Received/sec”</li><li>“Network Interface(\*)\Bytes Sent/sec”|<ul><li>In general, traffic sent from a DC far exceeds traffic sent to a DC.</li><li>As a switched Ethernet connection is full-duplex, inbound and outbound network traffic need to be sized independently.</li><li>Consolidating the number of DCs will increase the amount of bandwidth used to send responses back to client requests for each DC, but will be close enough to linear for the site as a whole.</li><li>If removing satellite location DCs, don’t forget to add the bandwidth for the satellite DC into the hub DCs as well as use that to evaluate how much WAN traffic there will be.</li></ul>|
|CPU|<ul><li>“Logical Disk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read”</li><li>“Process(lsass)\\% Processor Time”</li></ul>|<ul><li>After eliminating storage as a bottleneck, address the amount of compute power needed.</li><li>While not perfectly linear, the number of processor cores consumed across all servers within a specific scope (such as a site) can be used to gauge how many processors are necessary to support the total client load. Add the minimum necessary to maintain the current level of service across all the systems within the scope.</li><li>Changes in processor speed, including power management related changes, impact numbers derived from the current environment. Generally, it is impossible to precisely evaluate how going from a 2.5 GHz processor to a 3 GHz processor will reduce the number of CPUs needed.</li></ul>|
|NetLogon|<ul><li>“Netlogon(\*)\Semaphore Acquires”</li><li>“Netlogon(\*)\Semaphore Timeouts”</li><li>“Netlogon(\*)\Average Semaphore Hold Time”</li></ul>|<ul><li>Net Logon Secure Channel/MaxConcurrentAPI only affects environments with NTLM authentications and/or PAC Validation. PAC Validation is on by default in operating system versions before Windows Server 2008. This is a client setting, so the DCs will be impacted until this is turned off on all client systems.</li><li>Environments with significant cross trust authentication, which includes intra-forest trusts, have greater risk if not sized properly.</li><li>Server consolidations will increase concurrency of cross-trust authentication.</li><li>Surges need to be accommodated, such as cluster fail-overs, as users re-authenticate en masse to the new cluster node.</li><li>Individual client systems (such as a cluster) might need tuning too.</li></ul>|

## Planning

For a long time, the community’s recommendation for sizing AD DS has been to “put in as much RAM as the database size.” For the most part, that recommendation is all that most environments needed to be concerned about. But the ecosystem consuming AD DS has gotten much bigger, as have the AD DS environments themselves, since its introduction in 1999. Although the increase in compute power and the switch from x86 architectures to x64 architectures has made the subtler aspects of sizing for performance irrelevant to a larger set of customers running AD DS on physical hardware, the growth of virtualization has reintroduced the tuning concerns to a larger audience than before.

The following guidance is thus about how to determine and plan for the demands of Active Directory as a service regardless of whether it is deployed in a physical, a virtual/physical mix, or a purely virtualized scenario. As such, we will break down the evaluation to each of the four main components: storage, memory, network, and processor. In short, in order to maximize performance on AD DS, the goal is to get as close to processor bound as possible.

## RAM

Simply, the more that can be cached in RAM, the less it is necessary to go to disk. To maximize the scalability of the server the minimum amount of RAM should be the sum of the current database size, the total SYSVOL size, the operating system recommended amount, and the vendor recommendations for the agents (antivirus, monitoring, backup, and so on). An additional amount should be added to accommodate growth over the lifetime of the server. This will be environmentally subjective based on estimates of database growth based on environmental changes.

For environments where maximizing the amount of RAM is not cost effective (such as a satellite locations) or not feasible (DIT is too large), reference the Storage  section to ensure that storage is properly designed.

A corollary that comes up in the general context in sizing memory is sizing of the page file. In the same context as everything else memory related, the goal is to minimize going to the much slower disk. Thus the question should go from, “how should the page file be sized?” to “how much RAM is needed to minimize paging?” The answer to the latter question is outlined in the rest of this section. This leaves most of the discussion for sizing the page file to the realm of general operating system recommendations and the need to configure the system for memory dumps, which are unrelated to AD DS performance.

### Evaluating

The amount of RAM that a domain controller (DC) needs is actually a complex exercise for these reasons:

- High potential for error when trying to use an existing system to gauge how much RAM is needed as LSASS will trim under memory pressure conditions, artificially deflating the need.
- The subjective fact that an individual DC only needs to cache what is “interesting” to its clients. This means that the data that needs to be cached on a DC in a site with only an Exchange server will be very different than the data that needs to be cached on a DC that only authenticates users.
- The labor to evaluate RAM for each DC on a case-by-case basis is prohibitive and changes as the environment changes.
- The criteria behind the recommendation will help to make informed decisions: 
- The more that can be cached in RAM, the less it is necessary to go to disk. 
- Storage is by far the slowest component of a computer. Access to data on spindle-based and SSD storage media is on the order of 1,000,000x slower than access to data in RAM.

Thus, in order to maximize the scalability of the server, the minimum amount of RAM is the sum of the current database size, the total SYSVOL size, the operating system recommended amount, and the vendor recommendations for the agents (antivirus, monitoring, backup, and so on). Add additional amounts to accommodate growth over the lifetime of the server. This will be environmentally subjective based on estimates of database growth. However, for satellite locations with a small set of end users, these requirements can be relaxed as these sites will not need to cache as much to service most of the requests.

For environments where maximizing the amount of RAM is not cost effective (such as a satellite locations) or not feasible (DIT is too large), reference the Storage section to ensure that storage is properly sized.

> [!NOTE]
> A corollary while sizing memory is sizing of the page file. Because the goal is to minimize going to the much slower disk, the question goes from “how should the page file be sized?” to “how much RAM is needed to minimize paging?” The answer to the latter question is outlined in the rest of this section. This leaves most of the discussion for sizing the page file to the realm of general operating system recommendations and the need to configure the system for memory dumps, which are unrelated to AD DS performance.

### Virtualization considerations for RAM

Avoid memory over-commit at the host. The fundamental goal behind optimizing the amount of RAM is to minimize the amount of time spent going to disk. In virtualization scenarios, the concept of memory over-commit exists where more RAM is allocated to the guests then exists on the physical machine. This in and of itself is not a problem. It becomes a problem when the total memory actively used by all the guests exceeds the amount of RAM on the host and the underlying host starts paging. Performance becomes disk-bound in cases where the domain controller is going to the NTDS.dit to get data, or the domain controller is going to the page file to get data, or the host is going to disk to get data that the guest thinks is in RAM.

### Calculation summary example

|Component|Estimated memory (example)|
|-|-|
|Base operating system recommended RAM (Windows Server 2008)|2 GB|
|LSASS internal tasks|200 MB|
|Monitoring agent|100 MB|
|Antivirus|100 MB|
|Database (Global Catalog)|8.5 GB are you sure ???|
|Cushion for backup to run, administrators to log on without impact|1 GB|
|Total|12 GB|

**Recommended: 16 GB**

Over time, the assumption can be made that more data will be added to the database and the server will probably be in production for 3 to 5 years. Based on an estimate of growth of 33%, 16 GB would be a reasonable amount of RAM to put in a physical server. In a virtual machine, given the ease with which settings can be modified and RAM can be added to the VM, starting at 12 GB with the plan to monitor and upgrade in the future is reasonable.

## Network

### Evaluating
This section is less about evaluating the demands regarding replication traffic, which is focused on traffic traversing the WAN and is thoroughly covered in [Active Directory Replication Traffic](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10)), than it is about evaluating total bandwidth and network capacity needed, inclusive of client queries, Group Policy applications, and so on. For existing environments, this can be collected by using performance counters “Network Interface(\*)\Bytes Received/sec,” and “Network Interface(\*)\Bytes Sent/sec.” Sample intervals for Network Interface counters in either 15, 30, or 60 분utes. Anything less will generally be too volatile for good measurements; anything greater will smooth out daily peeks excessively.

> [!NOTE]
> Generally, the majority of network traffic on a DC is outbound as the DC responds to client queries. This is the reason for the focus on outbound traffic, though it is recommended to evaluate each environment for inbound traffic also. The same approaches can be used to address and review inbound network traffic requirements. For more information, see Knowledge Base article [929851: The default dynamic port range for TCP/IP has changed in Windows Vista and in Windows Server 2008](http://support.microsoft.com/kb/929851).

### Bandwidth needs

Planning for network scalability covers two distinct categories: the amount of traffic and the CPU load from the network traffic. Each of these scenarios is straight-forward compared to some of the other topics in this article.

In evaluating how much traffic must be supported, there are two unique categories of capacity planning for AD DS in terms of network traffic. The first is replication traffic that traverses between domain controllers and is covered thoroughly in the reference [Active Directory Replication Traffic](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10)) and is still relevant to current versions of AD DS. The second is the intrasite client-to-server traffic. One of the simpler scenarios to plan for, intrasite traffic predominantly receives small requests from clients relative to the large amounts of data sent back to the clients. 100 MB will generally be adequate in environments up to 5,000 users per server, in a site. Using a 1 GB network adapter and Receive Side Scaling (RSS) support is recommended for anything above 5,000 users. To validate this scenario, particularly in the case of server consolidation scenarios, look at Network Interface(\*)\Bytes/sec across all the DCs in a site, add them together, and divide by the target number of domain controllers to ensure that there is adequate capacity. The easiest way to do this is to use the “Stacked Area” view in Windows Reliability and Performance Monitor (formerly known as Perfmon), making sure all of the counters are scaled the same.

Consider the following example (also known as, a really, really complex way to validate that the general rule is applicable to a specific environment). The following assumptions are made:

- The goal is to reduce the footprint to as few servers as possible. Ideally, one server will carry the load and an additional server is deployed for redundancy (*N* + 1 scenario). 
- In this scenario, the current network adapter supports only 100 MB and is in a switched environment.  
  The maximum target network bandwidth utilization is 60% in an N scenario (loss of a DC).
- Each server has about 10,000 clients connected to it.

Knowledge gained from the data in the chart (Network Interface(\*)\Bytes Sent/sec):

1. The business day starts ramping up around 5:30 and winds down at 7:00 PM.
1. The peak busiest period is from 8:00 AM to 8:15 AM, with greater than 25 Bytes sent/sec on the busiest DC.  
   > [!NOTE]
   > All performance data is historical. So the peak data point at 8:15 indicates the load from 8:00 to 8:15.
1. There are spikes before 4:00 AM, with more than 20 Bytes sent/sec on the busiest DC, which could indicate either load from different time zones or background infrastructure activity, such as backups. Since the peak at 8:00 AM exceeds this activity, it is not relevant.
1. There are five Domain Controllers in the site.
1. The max load is about 5.5 MB/s per DC, which represents 44% of the 100 MB connection. Using this data, it can be estimated that the total bandwidth needed between 8:00 AM and 8:15 AM is 28 MB/s.
   >[!NOTE]
   >Be careful with the fact that Network Interface sent/receive counters are in bytes and network bandwidth is measured in bits. 100 MB &divide; 8 = 12.5 MB, 1 GB &divide; 8 = 128 MB.
  
Conclusions:

1. This current environment does meet the N+1 level of fault tolerance at 60% target utilization. Taking one system offline will shift the bandwidth per server from about 5.5 MB/s (44%) to about 7 MB/s (56%).
1. Based on the previously stated goal of consolidating to one server, this both exceeds the maximum target utilization and theoretically the possible utilization of a 100 MB connection.
1. With a 1 GB connection this will represent 22% of the total capacity.
1. Under normal operating conditions in the *N* + 1 scenario, client load will be relatively evenly distributed at about 14 MB/s per server or 11% of total capacity.
1. To ensure that capacity is adequate during unavailability of a DC, the normal operating targets per server would be about 30% network utilization or 38 MB/s per server. Failover targets would be 60% network utilization or 72 MB/s per server.  
  
In short, the final deployment of systems must have a 1 GB network adapter and be connected to a network infrastructure that will support said load. A further note is that given the amount of network traffic generated, the CPU load from network communications can have a significant impact and limit the maximum scalability of AD DS. This same process can be used to estimate the amount of inbound communication to the DC. But given the predominance of outbound traffic relative to inbound traffic, it is an academic exercise for most environments. Ensuring hardware support for RSS is important in environments with greater than 5,000 users per server. For scenarios with high network traffic, balancing of interrupt load can be a bottleneck. This can be detected by Processor(\*)\% Interrupt Time being unevenly distributed across CPUs. RSS enabled NICs can mitigate this limitation and increase scalability.

> [!NOTE]
> A similar approach can be used to estimate the additional capacity necessary when consolidating data centers, or retiring a domain controller in a satellite location. Simply collect the outbound and inbound traffic to clients and that will be the amount of traffic that will now be present on the WAN links.  
>  
> In some cases, you might experience more traffic than expected because traffic is slower, such as when certificate checking fails to meet aggressive time-outs on the WAN. For this reason, WAN sizing and utilization should be an iterative, ongoing process.

### Virtualization considerations for network bandwidth

It is easy to make recommendations for a physical server: 1 GB for servers supporting greater than 5000 users. Once multiple guests start sharing an underlying virtual switch infrastructure, additional attention is necessary to ensure that the host has adequate network bandwidth to support all the guests on the system, and thus requires the additional rigor. This is nothing more than an extension of ensuring the network infrastructure into the host machine. This is regardless whether the network is inclusive of the domain controller running as a virtual machine guest on a host with the network traffic going over a virtual switch, or whether connected directly to a physical switch. The virtual switch is just one more component where the uplink needs to support the amount of data being transmitted. Thus the physical host physical network adapter linked to the switch should be able to support the DC load plus all other guests sharing the virtual switch connected to the physical network adapter.

### Calculation summary example

|System|Peak bandwidth|
|-|-|
DC 1|6.5 MB/s|
DC 2|6.25 MB/s|
|DC 3|6.25 MB/s|
|DC 4|5.75 MB/s|
|DC 5|4.75 MB/s|
|Total|28.5 MB/s|

**Recommended: 72 MB/s** (28.5 MB/s divided by 40%)

|Target system(s) count|Total bandwidth (from above)|
|-|-|
|2|28.5 MB/s|
|Resulting normal behavior|28.5 &divide; 2 = 14.25 MB/s|

As always, over time the assumption can be made that client load will increase and this growth should be planned for as best as possible. The recommended amount to plan for would allow for an estimated growth in network traffic of 50%.

## Storage

Planning storage constitutes two components:

- Capacity, or storage size
- Performance

A great amount of time and documentation is spent on planning capacity, leaving performance often completely overlooked. With current hardware costs, most environments are not large enough that either of these is actually a concern, and the recommendation to “put in as much RAM as the database size” usually covers the rest, though it may be overkill for satellite locations in larger environments.

### Sizing

#### Evaluating for storage

Compared to 13 years ago when Active Directory was introduced, a time when 4 GB and 9 GB drives were the most common drive sizes, sizing for Active Directory is not even a consideration for all but the largest environments. With the smallest available hard drive sizes in the 180 GB range, the entire operating system, SYSVOL, and NTDS.dit can easily fit on one drive. As such, it is recommended to deprecate heavy investment in this area.

The only recommendation for consideration is to ensure that 110% of the NTDS.dit size is available in order to enable defrag. Additionally, accommodations for growth over the life of the hardware should be made.

The first and most important consideration is evaluating how large the NTDS.dit and SYSVOL will be. These measurements will lead into sizing both fixed disk and RAM allocation. Due to the (relatively) low cost of these components, the math does not need to be rigorous and precise. Content about how to evaluate this for both existing and new environments can be found in the [Data Storage](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961771(v=technet.10)) series of articles. Specifically, refer to the following articles:

- **For existing environments &ndash;** The section titled “To activate logging of disk space that is freed by defragmentation” in the article [Storage Limits](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10)).
- **For new environments &ndash;** The article titled [Growth Estimates for Active Directory Users and Organizational Units](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961779(v=technet.10)).

  > [!NOTE]
  > The articles are based on data size estimates made at the time of the release of Active Directory in Windows 2000. Use object sizes that reflect the actual size of objects in your environment.

When reviewing existing environments with multiple domains, there may be variations in database sizes. Where this is true, use the smallest global catalog (GC) and non-GC sizes.  

The database size can vary between operating system versions. DCs that run earlier operating systems such as Windows Server 2003 has a smaller database size than a DC that runs a later operating system such as Windows Server 2008 R2, especially when features such Active Directory Recycle Bin or Credential Roaming are enabled.

> [!NOTE]  
  >
>- For new environments, notice that the estimates in Growth Estimates for Active Directory Users and Organizational Units indicate that 100,000 users (in the same domain) consume about 450 MB of space. Please note that the attributes populated can have a huge impact on the total amount. Attributes will be populated on many objects by both third-party and Microsoft products, including Microsoft Exchange Server and Lync. An evaluation based on the portfolio of the products in the environment is preferred, but the exercise of detailing out the math and testing for precise estimates for all but the largest environments may not actually be worth significant time and effort.
>- Ensure that 110% of the NTDS.dit size is available as free space in order to enable offline defrag, and plan for growth over a three to five year hardware lifespan. Given how cheap storage is, estimating storage at 300% the size of the DIT as storage allocation is safe to accommodate growth and the potential need for offline defrag.

#### Virtualization considerations for storage

In a scenario where multiple Virtual Hard Disk (VHD) files are being allocated on a single volume use a fixed sized disk of at least 210% (100% of the DIT + 110% free space) the size of the DIT to ensure that there is adequate space reserved.  

#### Calculation summary example

|Data collected from evaluation phase| |
|-|-|
|NTDS.dit size|35 GB|
|Modifier to allow for offline defrag|2.1|
|Total storage needed|73.5 GB|

> [!NOTE]
> This storage needed is in addition to the storage needed for SYSVOL, operating system, page file, temporary files, local cached data (such as installer files), and applications.

### Storage performance

#### Evaluating performance of storage

As the slowest component within any computer, storage can have the biggest adverse impact on client experience. For those environments large enough for which the RAM sizing recommendations are not feasible, the consequences of overlooking planning storage for performance can be devastating.  Also, the complexities and varieties of storage technology further increase the risk of failure as the relevance of long standing best practices of “put operating system, logs, and database” on separate physical disks is limited in it’s useful scenarios.  This is because the long standing best practice is based on the assumption that is that a “disk” is a dedicated spindle and this allowed I/O to be isolated.  This assumptions that make this true are no longer relevant with the introduction of:

- New storage types and virtualized and shared storage scenarios
- Shared spindles on a Storage Area Network (SAN)
- VHD file on a SAN or network-attached storage
- Solid State Drives
- Tiered storage architectures (i.e. SSD storage tier caching larger spindle based storage)

In short, the end goal of all storage performance efforts, regardless of underlying storage architecture and design, is to ensure the needed amount of Input/Output Operations per Second (IOPS) are available and that those IOPS happen within an acceptable time frame. This section covers how to evaluate what AD DS demands of the underlying storage in order to ensure storage solutions are properly designed.  Given the variability of today’s storage technologies, it is best to work with the storage vendors to ensure adequate IOPS.  For those scenarios with locally attached storage, reference the Appendix C for the basics in how to design traditional local storage scenarios.  This principals are generally applicable to more complex storage tiers and will also help in dialog with the vendors supporting backend storage solutions.

- Given the wide breadth of storage options available, it is recommended to engage the expertise of hardware support teams or vendors to ensure that the specific solution meets the needs of AD DS. The following numbers are the information that would be provided to the storage specialists.

For environments where the database is too large to be held in RAM, use the performance counters to determine how much I/O needs to be supported:

- LogicalDisk(\*)\Avg Disk sec/Read (for example, if NTDS.dit is stored on the D:/ drive, the full path would be LogicalDisk(D:)\Avg Disk sec/Read)
- LogicalDisk(\*)\Avg Disk sec/Write
- LogicalDisk(\*)\Avg Disk sec/Transfer
- LogicalDisk(\*)\Reads/sec
- LogicalDisk(\*)\Writes/sec
- LogicalDisk(\*)\Transfers/sec

These should be sampled in 15/30/60 minute intervals to benchmark the demands of the current environment.

#### Evaluating the results

> [!NOTE]
> The focus is on reads from the database as this is usually the most demanding component, the same logic can be applied to writes to the log file by substituting LogicalDisk(*\<NTDS Log\>*)\Avg Disk sec/Write and LogicalDisk(*\<NTDS Log\>*)\Writes/sec):
>  
> - LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read indicates whether or not the current storage is adequately sized.  If the results are roughly equal to the Disk Access Time for the disk type, LogicalDisk(*\<NTDS\>*)\Reads/sec is a valid measure.  Check the manufacturer specifications for the storage on the back end, but good ranges for LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read would roughly be:
>   - 7200 – 9 to 12.5 milliseconds (ms)
>   - 10,000 – 6 to 10 ms
>   - 15,000 – 4 to 6 ms  
>   - SSD – 1 to 3 ms  
>   - >[!NOTE]
>     >Recommendations exist stating that storage performance is degraded at 15ms to 20ms (depending on source).  The difference between the above values and the other guidance is that the above values are the normal operating range.  The other recommendations are troubleshooting guidance to identify when client experience significantly degrades and becomes noticeable.  Reference Appendix C for a deeper explanation.
> - LogicalDisk(*\<NTDS\>*)\Reads/sec is the amount of I/O that is being performed.
>   - If LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read is within the optimal range for the backend storage, LogicalDisk(*\<NTDS\>*)\Reads/sec can be used directly to size the storage.
>   - If LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read is not within the optimal range for the backend storage, additional I/O is needed according to the following formula:
>     > (LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read) &divide; (Physical Media Disk Access Time) &times; (LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read)

Considerations:

- Note that if the server is configured with a sub-optimal amount of RAM, these values will be inaccurate for planning purposes.  They will be erroneously on the high side and can still be used as a worst case scenario.
- Adding/Optimizing RAM specifically will drive a decrease in the amount of read I/O (LogicalDisk(*\<NTDS\>*)\Reads/Sec.  This means the storage solution may not have to be as robust as initially calculated.  Unfortunately, anything more specific than this general statement is environmentally dependent on client load and general guidance cannot be provided.  The best option is to adjust storage sizing after optimizing RAM.

#### Virtualization considerations for performance

Similar to all of the preceding virtualization discussions, the key here is to ensure that the underlying shared infrastructure can support the DC load plus the other resources using the underlying shared media and all pathways to it. This is true whether a physical domain controller is sharing the same underlying media on a SAN, NAS, or iSCSI infrastructure as other servers or applications, whether it is a guest using pass through access to a SAN, NAS, or iSCSI infrastructure that shares the underlying media, or if the guest is using a VHD file that resides on shared media locally or a SAN, NAS, or iSCSI infrastructure. The planning exercise is all about making sure that the underlying media can support the total load of all consumers.

Also, from a guest perspective, as there are additional code paths that must be traversed, there is a performance impact to having to go through a host to access any storage. Not surprisingly, storage performance testing indicates that the virtualizing has an impact on throughput that is subjective to the processor utilization of the host system (see Appendix A: CPU Sizing Criteria), which is obviously influenced by the resources of the host demanded by the guest. This contributes to the virtualization considerations regarding processing needs in a virtualized scenario (see [Virtualization considerations for processing](#virtualization-considerations-for-processing)).

Making this more complex is that there are a variety of different storage options that are available that all have different performance impacts. As a safe estimate when migrating from physical to virtual, use a multiplier of 1.10 to adjust for different storage options for virtualized guests on Hyper-V, such as pass-through storage, SCSI Adapter, or IDE. The adjustments that need to be made when transferring between the different storage scenarios are irrelevant as to whether the storage is local, SAN, NAS, or iSCSI.

#### Calculation summary example

Determining the amount of I/O needed for a healthy system under normal operating conditions:

- LogicalDisk(*\<NTDS Database Drive\>*)\Transfers/sec during the peak period 15 minute period 
- To determine the amount of I/O needed for storage where the capacity of the underlying storage is exceeded:
  >*Needed IOPS* = (LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read &divide; *\<Target Avg Disk sec/Read\>*) &times; LogicalDisk(*\<NTDS Database Drive\>*)\Read/sec

|Counter|Value|
|-|-|
|Actual LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Transfer|.02 seconds (20 milliseconds)|
|Target LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Transfer|.01 seconds|
|Multiplier for change in available IO|0.02 &divide; 0.01 = 2|  
  
|Value name|Value|
|-|-|
|LogicalDisk(*\<NTDS Database Drive\>*)\Transfers/sec|400|
|Multiplier for change in available IO|2|
|Total IOPS needed during peak period|800|

To determine the rate at which the cache is desired to be warmed:

- Determine the maximum acceptable time to warm the cache. It is either the amount of time that it should take to load the entire database from disk, or for scenarios where the entire database cannot be loaded in RAM, this would be the maximum time to fill RAM.
- Determine the size of the database, excluding white space.  For more information, see [Evaluating for storage](#evaluating-for-storage).  
- Divide the database size by 8 KB; that will be the total IOs necessary to load the database.
- Divide the total IOs by the number of seconds in the defined time frame.

Note that the rate calculated, while accurate, will not be exact because previously loaded pages are evicted if ESE is not configured to have a fixed cache size, and AD DS by default uses variable cache size.

|Data points to collect|Values
|-|-|
|Maximum acceptable time to warm|10 minutes (600 seconds)
|Database size|2 GB|  
  
|Calculation step|Formula|Result|
|-|-|-|
|Calculate size of database in pages|(2 GB &times; 1024 &times; 1024) = *Size of database in KB*|2,097,152 KB|
|Calculate number of pages in database|2,097,152 KB &divide; 8 KB = *Number of pages*|262,144 pages|
|Calculate IOPS necessary to fully warm the cache|262,144 pages &divide; 600 seconds = *IOPS needed*|437 IOPS|

## Processing

### Evaluating Active Directory processor usage

For most environments, after storage, RAM, and networking are properly tuned as described in the Planning section, managing the amount of processing capacity will be the component that deserves the most attention. There are two challenges in evaluating CPU capacity needed:

- Whether or not the applications in the environment are being well-behaved in a shared services infrastructure, and is discussed in the section titled “Tracking Expensive and Inefficient Searches” in the article Creating More Efficient Microsoft Active Directory-Enabled Applications or migrating away from down-level SAM calls to LDAP calls.  
  
  In larger environments, the reason this is important is that poorly coded applications can drive volatility in CPU load, “steal” an inordinate amount of CPU time from other applications, artificially drive up capacity needs, and unevenly distribute load against the DCs.  
- As AD DS is a distributed environment with a large variety of potential clients, estimating the expense of a “single client” is environmentally subjective due to usage patterns and the type or quantity of applications leveraging AD DS. In short, much like the networking section, for broad applicability, this is better approached from the perspective of evaluating the total capacity needed in the environment.

For existing environments, as storage sizing was discussed previously, the assumption is made that storage is now properly sized and thus the data regarding processor load is valid. To reiterate, it is critical to ensure that the bottleneck in the system is not the performance of the storage. When a bottleneck exists and the processor is waiting, there are idle states that will go away once the bottleneck is removed.  As processor wait states are removed, by definition, CPU utilization increases as it no longer has to wait on the data. Thus, collect performance counters “Logical Disk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read” and “Process(lsass)\\% Processor Time”. The data in “Process(lsass)\\% Processor Time” will be artificially low if “Logical Disk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read” exceeds 10 to 15 ms, which is a general threshold that Microsoft support uses for troubleshooting storage-related performance issues. As before, it is recommended that sample intervals be either 15, 30, or 60 minutes. Anything less will generally be too volatile for good measurements; anything greater will smooth out daily peeks excessively.

### Introduction

In order to plan capacity planning for domain controllers, processing power requires the most attention and understanding. When sizing systems to ensure maximum performance, there is always a component that is the bottleneck and in a properly sized Domain Controller this will be the processor.

Similar to the networking section where the demand of the environment is reviewed on a site-by-site basis, the same must be done for the compute capacity demanded. Unlike the networking section, where the available networking technologies far exceed the normal demand, pay more attention to sizing CPU capacity.  As any environment of even moderate size; anything over a few thousand concurrent users can put significant load on the CPU.

Unfortunately, due to the huge variability of client applications that leverage AD, a general estimate of users per CPU is woefully inapplicable to all environments. Specifically, the compute demands are subject to user behavior and application profile. Therefore, each environment needs to be individually sized.

#### Target site behavior profile

As mentioned previously, when planning capacity for an entire site, the goal is to target a design with an *N* + 1 capacity design, such that failure of one system during the peak period will allow for continuation of service at a reasonable level of quality. That means that in an “*N*” scenario, load across all the boxes should be less than 100% (better yet, less than 80%) during the peak periods.

Additionally, if the applications and clients in the site are using best practices for locating domain controllers (that is, using the [DsGetDcName function](http://msdn.microsoft.com/en-us/library/windows/desktop/ms675983(v=vs.85).aspx)), the clients should be relatively evenly distributed with minor transient spikes due to any number of factors.

In the next example, the following assumptions are made:

- Each of the five DCs in the site has four of CPUs.
- Total target CPU usage during business hours is 40% under normal operating conditions (“*N* + 1”) and 60% otherwise (“*N*”). During non-business hours, the target CPU usage is 80% because backup software and other maintenance are expected to consume all available resources.

![CPU usage chart](media/capacity-planning-considerations-cpu-chart.png)

Analyzing the data in the chart (Processor Information(_Total)\% Processor Utility) for each of the DCs:

- For the most part, the load is relatively evenly distributed which is what would be expected when clients use DC locator and have well written searches. 
- There are a number of five-minute spikes of 10%, with some as large as 20%. Generally, unless they cause the capacity plan target to be exceeded, investigating these is not worthwhile.  
- The peak period for all systems is between about 8:00 AM and 9:15 AM. With the smooth transition from about 5:00 AM through about 5:00 PM, this is generally indicative of the business cycle. The more randomized spikes of CPU usage on a box-by-box scenario between 5:00 PM and 4:00 AM would be outside of the capacity planning concerns.

  >[!NOTE]
  >On a well-managed system, said spikes are might be backup software running, full system antivirus scans, hardware or software inventory, software or patch deployment, and so on. Because they fall outside the peak user business cycle, the targets are not exceeded.

- As each system is about 40% and all systems have the same numbers of CPUs, should one fail or be taken offline, the remaining systems would run at an estimated 53% (System D's 40% load is evenly split and added to System A's and System C’s existing 40% load). For a number of reasons, this linear assumption is NOT perfectly accurate, but provides enough accuracy to gauge.  

  **Alternate scenario –** Two domain controllers running at 40%: One domain controller fails, estimated CPU on the remaining one would be an estimated 80%. This far exceeds the thresholds outlined above for capacity plan and also starts to severely limit the amount of head room for the 10% to 20% seen in the load profile above, which means that the spikes would drive the DC to 90% to 100% during the “*N*” scenario and definitely degrade responsiveness.

### Calculating CPU demands

The “Process\\% Processor Time” performance object counter sums the total amount of time that all of the threads of an application spend on the CPU and divides by the total amount of system time that has passed. The effect of this is that a multi-threaded application on a multi-CPU system can exceed 100% CPU time, and would be interpreted VERY differently than “Processor Information\\% Processor Utility”. In practice the “Process(lsass)\\% Processor Time” can be viewed as the count of CPUs running at 100% that are necessary to support the process’s demands. A value of 200% means that 2 CPUs, each at 100%, are needed to support the full AD DS load. Although a CPU running at 100% capacity is the most cost efficient from the perspective of money spent on CPUs and power and energy consumption, for a number of reasons detailed in Appendix A, better responsiveness on a multi-threaded system occurs when the system is not running at 100%.

To accommodate transient spikes in client load, it is recommended to target a peak period CPU of between 40% and 60% of system capacity. Working with the example above, that would mean that between 3.33 (60% target) and 5 (40% target) CPUs would be needed for the AD DS (lsass process) load. Additional capacity should be added in according to the demands of the base operating system and other agents required (such as antivirus, backup, monitoring, and so on). Although the impact of agents needs to be evaluated on a per environment basis, an estimate of between 5% and 10% of a single CPU can be made. In the current example, this would suggest that between 3.43 (60% target) and 5.1 (40% target) CPUs are necessary during peak periods.

The easiest way to do this is to use the “Stacked Area” view in Windows Reliability and Performance Monitor (perfmon), making sure all of the counters are scaled the same.

Assumptions:

- Goal is to reduce footprint to as few servers as possible. Ideally, one server would carry the load and an additional server added for redundancy (*N* + 1 scenario).

![Processor time chart for lsass process (over all processors)](media/capacity-planning-considerations-proc-time-chart.png)

Knowledge gained from the data in the chart (Process(lsass)\\% Processor Time):

- The business day starts ramping up around 7:00 and decreases at 5:00 PM.
- The peak busiest period is from 9:30 AM to 11:00 AM. 
  > [!NOTE]
  > All performance data is historical. The peak data point at 9:15 indicates the load from 9:00 to 9:15.
- There are spikes before 7:00 AM which could indicate either load from different time zones or background infrastructure activity, such as backups. Because the peak at 9:30 AM exceeds this activity, it is not relevant.
- There are three domain controllers in the site.

At maximum load, lsass consumes about 485% of one CPU, or 4.85 CPUs running at 100%. As per the math earlier, this means the site needs about 12.25 CPUs for AD DS. Add in the above suggestions of 5% to 10% for background processes and that means replacing the server today would need approximately 12.30 to 12.35 CPUs to support the same load. An environmental estimate for growth now needs to be factored in.

### When to tune LDAP weights

There are several scenarios where tuning [LdapSrvWeight](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc957291(v=technet.10)) should be considered. Within the context of capacity planning, this would be done when the application or user loads are not evenly balanced, or the underlying systems are not evenly balanced in terms of capability. Reasons to do so beyond capacity planning are outside of the scope of this article.

There are two common reasons to tune LDAP Weights:

- The PDC emulator is an example that affects every environment for which user or application load behavior is not evenly distributed. As certain tools and actions target the PDC emulator, such as the Group Policy management tools, second attempts in the case of authentication failures, trust establishment, and so on, CPU resources on the PDC emulator may be more heavily demanded than elsewhere in the site.
  - It is only useful to tune this if there is a noticeable difference in CPU utilization in order  to reduce the load on the PDC emulator and increase the load on other domain controllers will allow a more even distribution of load.
  - In this case, set LDAPSrvWeight between 50 and 75 for the PDC emulator.
- Servers with differing counts of CPUs (and speeds) in a site.  For example, say there are two eight-core servers and one four-core server.  The last server has half the processors of the other two servers.  This means that a well distributed client load will increase the average CPU load on the four-core box to roughly twice that of the eight-core boxes.
  - For example, the two eight-core boxes would be running at 40% and the four-core box would be running at 80%.
  - Also, consider the impact of loss of one eight-core box in this scenario, specifically the fact that the four-core box would now be overloaded.

#### Example 1 - PDC

| |Utilization with defaults|New LdapSrvWeight|Estimated new utilization|
|-|-|-|-|
|DC 1 (PDC emulator)|53%|57|40%|
|DC 2|33%|100|40%|
|DC 3|33%|100|40%|

The catch here is that if the PDC emulator role is transferred or seized, particularly to another domain controller in the site, there will be a dramatic increase on the new PDC emulator.

Using the example from the section [Target site behavior profile](#target-site-behavior-profile), an assumption was made that all three domain controllers in the site had four CPUs. What should happen, under normal conditions, if one of the domain controllers had eight CPUs? There would be two domain controllers at 40% utilization and one at 20% utilization. While this is not bad, there is an opportunity to balance the load a little bit better. Leverage LDAP weights to accomplish this.  An example scenario would be:

#### Example 2 - Differing CPU counts

| |Processor Information\\ %&nbsp;Processor Utility(_Total)<br />Utilization with defaults|New LdapSrvWeight|Estimated new utilization|
|-|-|-|-|
|4-CPU DC 1|40|100|30%|
|4-CPU DC 2|40|100|30%|
|8-CPU DC 3|20|200|30%|

Be very careful with these scenarios though. As can be seen above, the math looks really nice and pretty on paper. But throughout this article, planning for an “*N* + 1” scenario is of paramount importance. The impact of one DC going offline must be calculated for every scenario. In the immediately preceding scenario where the load distribution is even, in order to ensure a 60% load during an “*N*” scenario, with the load balanced evenly across all servers, the distribution will be fine as the ratios stay consistent. Looking at the PDC emulator tuning scenario, and in general any scenario where user or application load is unbalanced, the effect is very different:

| |Tuned Utilization|New LdapSrvWeight|Estimated New Utilization|
|-|-|-|-|
|DC 1 (PDC emulator)|40%|85|47%|
|DC 2|40%|100|53%|
|DC 3|40%|100|53%|

### Virtualization considerations for processing

There are two layers of capacity planning that need to be done in a virtualized environment. At the host level, similar to the identification of the business cycle outlined for the domain controller processing previously, thresholds during the peak period need to be identified. Because the underlying principals are the same for a host machine scheduling guest threads on the CPU as for getting AD DS threads on the CPU on a physical machine, the same goal of 40% to 60% on the underlying host are recommended. At the next layer, the guest layer, since the principals of thread scheduling have not changed, the goal within the guest remains in the 40% to 60% range.

In a direct mapped scenario, one guest per host, all the capacity planning done to this point needs to be added to the requirements (RAM, disk, network) of the underlying host operating system. In a shared host scenario, testing indicates that there is 10% impact on the efficiency of the underlying processors. That means if a site needs 10 CPUs at a target of 40%, the recommended amount of virtual CPUs to allocate across all the “*N*” guests would be 11. In a site with a mixed distribution of physical servers and virtual servers, the modifier only applies to the VMs. For example, if a site has an “*N* + 1” scenario, one physical or direct-mapped server with 10 CPUs would be about equivalent to one guest with 11 CPUs on a host, with 11 CPUs reserved for the domain controller.

Throughout the analysis and calculation of the CPU quantities necessary to support AD DS load, the numbers of CPUs that map to what can be purchased in terms physical hardware do not necessarily map cleanly. Virtualization eliminates the need to round up. Virtualization decreases the effort necessary to add compute capacity to a site, given the ease with which a CPU can be added to a VM. It does not eliminate the need to accurately evaluate the compute power needed so that the underlying hardware is available when additional CPUs need to be added to the guests.  As always, remember to plan and monitor for growth in demand.

### Calculation summary example

|System|Peak CPU|
|-|-|-|
|DC 1|120%|
|DC 2|147%|
|Dc 3|218%|
|Total CPU being used|485%|  
  
|Target system(s) count|Total bandwidth (from above)|
|-|-|
|CPUs needed at 40% target|4.85 &divide; .4 = 12.25|

Repeating due to the importance of this point, *remember to plan for growth*. Assuming 50% growth over the next three years, this environment will need 18.375 CPUs (12.25 &times; 1.5) at the three-year mark. An alternate plan would be to review after the first year and add in additional capacity as needed.

### Cross-trust client authentication load for NTLM

#### Evaluating cross-trust client authentication load

Many environments may have one or more domains connected by a trust. An authentication request for an identity in another domain that does not use Kerberos authentication needs to traverse a trust using the domain controller’s secure channel to another domain controller either in the destination domain or the next domain in the path to the destination domain. The number of concurrent calls using the secure channel that a domain controller can make to a domain controller in a trusted domain is controlled by a setting known as **MaxConcurrentAPI**. For domain controllers, ensuring that the secure channel can handle the amount of load is accomplished by one of two approaches: tuning **MaxConcurrentAPI** or, within a forest, creating shortcut trusts. To gauge the volume of traffic across an individual trust, refer to [How to do performance tuning for NTLM authentication by using the MaxConcurrentApi setting](https://support.microsoft.com/kb/2688798).

During data collection, this, as with all the other scenarios, must be collected during the peak busy periods of the day for the data to be useful.

> [!NOTE]
> Intraforest and interforest scenarios may cause the authentication to traverse multiple trusts and each stage would need to be tuned.

#### Planning

There are a number of applications that use NTLM authentication by default, or use it in a certain configuration scenario. Application servers grow in capacity and service an increasing number of active clients. There is also a trend that clients keep sessions open for a limited time and rather reconnect on a regular basis (such as email pull sync). Another common example for high NTLM load is web proxy servers that require authentication for Internet access.

These applications can cause a significant load for NTLM authentication, which can put significant stress on the DCs, especially when users and resources are in different domains.

There are multiple approaches to managing cross-trust load, which in practice are used in conjunction rather than in an exclusive either/or scenario. The possible options are:

- Reduce cross-trust client authentication by locating the services that a user consumes in the same domain that the user is resident in.
- Increase the number of secure-channels available. This is relevant to intraforest and cross-forest traffic and are known as shortcut trusts.
- Tune the default settings for **MaxConcurrentAPI**.

For tuning **MaxConcurrentAPI** on an existing server, the equation is:

> *New_MaxConcurrentApi_setting* &ge; (*semaphore_acquires* + *semaphore_time-outs*) &times; *average_semaphore_hold_time* &divide; *time_collection_length*

For more information, see [KB article 2688798: How to do performance tuning for NTLM authentication by using the MaxConcurrentApi setting](http://support.microsoft.com/kb/2688798).

## Virtualization considerations

None, this is an operating system tuning setting.

### Calculation summary example

|Data type|Value|
|-|-|
|Semaphore Acquires (Minimum)|6,161|
|Semaphore Acquires (Maximum)|6,762|
|Semaphore Timeouts|0|
|Average Semaphore Hold Time|0.012|
|Collection Duration (seconds)|1:11 minutes (71 seconds)|
|Formula (from KB 2688798)|((6762 &ndash; 6161) + 0) &times; 0.012 /|
|Minimum value for **MaxConcurrentAPI**|((6762 &ndash; 6161) + 0) &times; 0.012 &divide; 71 = .101|

For this system for this time period, the default values are acceptable.

## Monitoring for compliance with capacity planning goals

Throughout this article, it has been discussed that planning and scaling go towards utilization targets. Here is a summary chart of the recommended thresholds that must be monitored to ensure the systems are operating within adequate capacity thresholds. Keep in mind that these are not performance thresholds, but capacity planning thresholds. A server operating in excess of these thresholds will work, but is time to start validating that all the applications are well behaved. If said applications are well behaved, it is time to start evaluating hardware upgrades or other configuration changes.

|Category|Performance counter|Interval/Sampling|Target|Warning|
|-|-|-|-|-|
|Processor|Processor Information(_Total)\\% Processor Utility|60 min|40%|60%|
|RAM (Windows Server 2008 R2 또는 이전 버전)|메모리 (mb)|< 100MB|해당 사항 없음|< 100MB|
|RAM (Windows Server 2012)|Memory\Long 장기 대기 캐시 Lifetime(s) 평균|30 분|테스트 해야 합니다.|테스트 해야 합니다.|
|네트워크|Network Interface(\*)\Bytes Sent/sec<br /><br />Network Interface(\*)\Bytes Received/sec|30 분|40%|60%|
|스토리지|LogicalDisk( *\<NTDS Database Drive\>* )\Avg Disk sec/Read<br /><br />LogicalDisk( *\<NTDS Database Drive\>* )\Avg Disk sec/Write|60 분|10 밀리초|15ms|
|AD 서비스|Netlogon(\*)\Average Semaphore Hold Time|60 분|0|1 초|

## <a name="appendix-a-cpu-sizing-criteria"></a>부록 A: CPU 크기 조정 조건

### <a name="definitions"></a>정의

**프로세서 (마이크로프로세서) –** 읽고 프로그램 명령을 실행 하는 구성 요소  

**CPU-** 중앙 처리 장치  

**다중 코어 프로세서** 같은 집적 회로에 여러 Cpu  

**다중 CPU –** 동일한 통합 회로에 없는 여러 Cpu  

**논리 프로세서 –** 운영 체제의 관점에서 단일 논리적 컴퓨팅 엔진  

여기에 하이퍼스레딩, 다중 코어 프로세서, 단일 코어 프로세서에서 1 개 코어입니다.  

오늘날의 서버 시스템 다중 프로세서, 여러 다중 코어 프로세서 및 하이퍼 스레딩 동일 시나리오 모두에이 정보는 일반화 됩니다. 따라서 운영 체제 및 응용 프로그램 관점 가능한 컴퓨팅 엔진을 나타냄으로 용어 논리적 프로세서 사용 됩니다.

### <a name="thread-level-parallelism"></a>스레드 수준 병렬 처리

각 스레드는 독립적인 작업은 각 스레드가 자체 스택 및 지침입니다. AD DS는 다중 스레드 및 사용 하 여 사용 가능한 스레드 수를 조정할 수 있으므로 [보고 Ntdsutil.exe를 사용 하 여 Active Directory에서 LDAP 정책을 설정 하는 방법을](http://support.microsoft.com/kb/315071), 여러 개의 논리적 프로세서에서 잘 확장 합니다.

### <a name="data-level-parallelism"></a>데이터 수준 병렬 처리

데이터를 하나의 프로세스 (의 경우만 AD DS 프로세스) 내에서 여러 스레드 및 여러 프로세스에서 여러 스레드 간에 일반적으로 공유 해야 합니다. 데이터 변경 내용이 반영 되었는지 즉 과도 하 게 대/소문자를 간소화 하는 데 문제가 사용 하 여 공유 메모리를 업데이트할 수 있을 뿐만 아니라 모든 코어 (L1, L2, L3) 캐시의 모든 다양 한 수준에서 실행 중인 모든 스레드를 언급된 스레드를 실행 합니다. 명령 처리를 계속할 수 보다 먼저 다양 한 메모리 위치를 모두 일관 된 상태가 되는 동안 쓰기 작업 동안 성능이 저하 될 수 있습니다.

### <a name="cpu-speed-vs-multiple-core-considerations"></a>CPU 속도와 다중 코어 고려 사항

일반적인 경험상 빠릅니다 논리적 프로세서는 일련의 더 많은 작업이 동시에 실행할 수 있는 더 많은 논리 프로세서 의미 하는 동안 명령 처리 하는 데 걸리는 기간을 축소 합니다. 이러한 규칙이 시나리오의 공유 메모리, 데이터 수준 병렬 처리 및 다중 스레드 관리 오버 헤드가 대기에서 데이터를 가져오고를 고려 하 여 본질적으로 복잡 해지면 세분화 합니다. 또한 이것이 다중 코어 시스템의 확장성은 선형 이유입니다.

이러한 고려 사항에서 다음 정보를 제공 하는 것이 좋습니다: 되는 개별 자동차에는 코어 및 속도 한계 클럭 속도 되 고 각 레인 각 스레드를 사용 하 여 고속도로 생각해 보세요.

1. 고속도로에 자동차 하나만 있으면 두 레인 또는 12 레인 있을 경우 중요 하지 않습니다. 해당 자동차 속도 제한을 사용 하면 만큼 빠릅니다만 것입니다.
1. 스레드가 필요한 데이터를 즉시 사용할 수 없는 것으로 가정 합니다. 비유는 road 세그먼트가 종료 되는 것입니다. 속도 제한 이란 중요 하지 않습니다 고속도로에 하나의 자동차 있으면 레인 다시 열릴 때까지 (데이터는 메모리에서 가져옴).
1. 자동차의 수를 늘리면 자동차 수를 관리 하는 오버 헤드가 증가 합니다. 주의가 필요한 양에 거의 때 빈 (예:으로 늦은 저녁) 트래픽은 많이 (예: 중간 들어오므로 하지만 하지 혼잡 시 교통량)와 및 주행 경험을 비교 합니다. 또한 양을 고려해 주의가 필요한 두 레인 고속도로 구동 하는 경우 드라이버를 수행 하는 것에 대 한 걱정 다른 레인을 하나만 있으면 여기서는 많은 다른 드라이버에 대 한 걱정 하나에 6 레인 고속도로 및 수행 하는 합니다.
   > [!NOTE]
   > 혼잡 시 교통량 시나리오에 대 한 예를 들어 다음 섹션에서 확장 됩니다. 응답 시간/시스템 바빠서 성능에 미치는 영향을 합니다.

결과적으로 더 많은 또는 더 빠른 프로세서에 대 한 세부 정보는 AD DS는 경전철 매우 다르며도 서버 간 환경 내에서 응용 프로그램 동작에 항상 주관적인 됩니다. 이 인해 문서의 앞부분에서 참조 되는 과도 하 게 정확한에 많이 투자 하지 않습니다 하 고 보안의 여백을 계산에 포함 됩니다. 예산 중심 구매 의사 결정 시는 더 빠른 프로세서를 구입을 고려 하기 전에 먼저 발생 40% (또는 환경에 대해 원하는 수 만큼)에서 프로세서 사용량을 최적화 하는 것이 좋습니다. 더 많은 프로세서에서 향상 된 동기화 선형 진행에서 더 많은 프로세서의 진정한 장점은 줄어듭니다 (2&times; 프로세서 수가 2 보다 작은 제공&times; 사용할 수 있는 추가 계산 능력).

> [!NOTE]
> Amdahl의 법칙과 Gustafson의 법칙은 관련 개념 이며

### <a name="response-timehow-the-system-busyness-impacts-performance"></a>응답 시간/시스템 바빠서 성능에 미치는 영향을

큐 이론 (큐) 대기 선의 수학 연구입니다. 큐 이론적으로 사용률 사유가 수식으로 표현 됩니다.

*U* k = *B* &divide; *T*

여기서 *U* k 사용 백분율입니다 *B* 기간을 사용량이 및 *T* 시스템 관찰 된 총 시간입니다. Windows의 컨텍스트로 변환, 즉, 100 나노초 (ns) 수가 간격에 있는 스레드는 실행 중 상태인 100 ns 간격 수가 된 시간 간격 지정에서 사용할 수로 나눈 값. 이 정확 하 게 % 프로세서 유틸리티를 계산 하는 것에 대 한 수식 (참조 [프로세서 개체](https://docs.microsoft.com/previous-versions/ms804036(v=msdn.10)) 하 고 [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/previous-versions/windows/embedded/ms901169(v=msdn.10))).

또한 큐 이론에 수식을 제공합니다. *N* = *U* k &divide; (1 &ndash; *U* k) 사용률에 따라 대기 중인 항목의 수를 계산 하려면 ( *N* 되는 큐 길이)입니다. 모든 사용률 간격에 걸쳐이 차트는 프로세서의 가져올 큐를 모든 지정 된 CPU 로드 시 기간에 다음과 같은 예상 값을 제공 합니다.

![큐 길이](media/capacity-planning-considerations-queue-length.png)

가 관찰 되는 50 %CPU 로드 후 평균 대기 하는 항상 큐에서 다른 하나의 항목, 눈에 띄게 신속한 늘릴 약 70 %CPU 사용률입니다.

이 단원의 이전에 사용한 주행 비유를 반환 합니다.

- "중간 오후"의 바쁜 시간이 마찬가지로 가설적으로 되지 않는 환경의 중간쯤 40 ~ 70% 범위에 있습니다. 충분 한 트래픽을 모든 레인을 선택할 수 있는 1의 기능을 majorly 제하지 없는 되며 높음, 하는 동안에 방식에는 다른 드라이버의 가능성 "찾기" 이동 중에 다른 자동차 사이의 간격을 안전 하 게 하기 위한 활동 수준이 필요가 없습니다.
- 트래픽 혼잡 시 교통량 다가오면 road 시스템 가까워지면 100% 용량 하나 바뀝니다. 레인 변경 되므로 자동차 따라서 닫기 함께 향상 된 주의가 그러려면 것이 매우 어려울 될 수 있습니다.

이것이 급증 (예: 몇 분 동안 실행 되는 잘못 코딩 된 쿼리) 일시적인 있다고 여부를 로드 하거나 비정상적인 급증 일반적 부하 (아침의 비정상적인 급증에 대 한 헤드 방에 대 한 허용 되는 신중 하 게 40%로 예상 용량에 대 한 장기간의 평균을 계산 하는 이유 첫 번째 날 긴 주말).

위의 문은 % 프로세서 시간 계산 사용률 사유가 일반 판독기는 편의 위해 간소화의 비트는 같은 것을 인식 합니다. 이러한 수학적으로 더 엄격한에 대 한:  
- 변환 된 [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10))
  - *B* = 100 ns 간격 "Idle" 스레드가 논리 프로세서의 수입니다. 변경 된 "*X*" 변수를 [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10)) 계산
  - *T* = 지정된 된 시간 범위에서 100-ns 간격의 총 수입니다. 변경 된 "*Y*" 변수를 [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10)) 계산 합니다.
  - *U* k = "유휴 스레드" 또는 %는 논리적 프로세서의 사용률이 \ % 유휴 시간입니다.  
- 수학 산출 합니다.
  - *U* k = 1-% 프로세서 시간
  - % Processor Time = 1 – *U* k
  - %Processor Time = 1 – *B* / *T*
  - %Processor Time = 1 – *X1* – *X0* / *Y1* – *Y0*

### <a name="applying-the-concepts-to-capacity-planning"></a>용량 계획 개념을 적용합니다.

위의 계산을 만들 수는 시스템에 필요한 논리 프로세서의 수에 관한 결정 반응은 놀라울 정도로 복잡 한 것 같습니다. 이 때문에 현재에 기반 하는 최대 대상 사용률을 확인 하는 시스템 크기 조정 하는 방법은 포커스가 로드 및 구현할 수 있었다는 하는 데 필요한 논리 프로세서의 수를 계산 합니다. 또한 논리 프로세서 속도 성능, 캐시 효율성, 메모리 일관성 요구 사항, 스레드 예약 및 동기화에 상당한 영향을 미칠 빨라질 분산 된 클라이언트를 로드 하는 동안은 모두에 큰 영향을 성능을 서버 간 별로 달라 집니다. 계산 능력의 상대적으로 저렴 한 비용을 분석 하 고 필요한 Cpu 완벽 하 게 수를 결정 하는 동안 자세한 교육 연습 보다 비즈니스 가치 제공 됩니다.

40% 엄격한 요구 사항은 아닙니다.는 적절 한 시작 합니다. Active Directory의 다양 한 소비자는 다양 한 수준의 응답성 필요합니다. 프로세서에 대 한 액세스에 대 한 향상 된 대기 시간이 눈에 띄게 영향을 주지 것입니다 클라이언트 성능으로 환경을 지속적으로 평균을 80% 또는 90% 사용률에서 실행할 수 있는 시나리오 수 있습니다. 훨씬 더 느리기 논리 프로세서 보다 RAM에 대 한 액세스를 포함 하 여 시스템에는 시스템의 다양 한 측면은 다시 반복, 디스크 및 네트워크를 통해 응답을 전송에 대 한 액세스 하는 것이 반드시 합니다. 이러한 모든 항목을 함께에서 조정 해야 합니다. 예를 들면 다음과 같습니다.

- 디스크 바인딩된 90%를 실행 하는 시스템에 더 많은 프로세서를 추가 하지 않을 것 이므로 성능이 크게 향상 합니다. 아마도 시스템 심층적으로 분석도 받지 못한 프로세서의 i/o 완료를 기다리면서 스레드 많이 있는지를 식별 합니다.
- I/o 대기 상태의 스레드가 대기 상태에서 시간이 많이 소비 하 고 이전에 있었습니다는 더 이상 즉 될 및 이전 90% 사용률 즉 CPU 시간에 대 한 자세한 대회 될 디스크 바인딩된 문제 해결 예제 (때문에 더 높은 넘어가면) 100%로 이동 됩니다. 두 구성 요소를 함께에서 조정 해야 합니다.
  > [!NOTE]
  > 프로세서 Information(*)\\% 프로세서 유틸리티 "터보" 모드에 있는 시스템을 사용 하 여 100%를 초과할 수 있습니다.  CPU 짧은 기간에 대 한 등급이 지정 된 프로세서 속도 초과 하는 위치입니다.  참조 CPU 제조업체 설명서 및 큰 카운터의 설명입니다.  

전체 시스템 사용률 고려 사항 설명 부분도 대화 도메인 컨트롤러에 가상화 된 게스트도 합니다. [응답 시간/시스템 바빠서 성능에 미치는 영향을](#response-timehow-the-system-busyness-impacts-performance) 호스트와 게스트 가상화 시나리오에서에 적용 됩니다. 이 인해 하나의 게스트와 호스트에서 실제 하드웨어에서 동일한 성능 근처에 도메인 컨트롤러 (및 모든 시스템에 일반적으로). 이전에 설명한 대로 프로세서에 액세스 하는 대기 시간이 높입니다 기본 호스트의 사용률을 증가 호스트에 추가 게스트를 추가 합니다. 즉, 논리 프로세서 사용률 모두 호스트 및 게스트 수준에서 관리 해야 합니다.

확장 이전 기반, 고속도로 물리적 하드웨어와 게스트로 남겨 두는 VM (rider를 대상으로 바로 이동 하는 빠른 버스를 원하는) 버스를 사용 하 여 analogized 수 됩니다. 다음 네가지 시나리오를 가정해 보겠습니다.

- 시간, 거의 비어 있는 버스는 rider 가져옵니다 이므로 거의 비어 있는로에 bus를 가져옵니다. 많이 고민해 야 트래픽이 없는 경우는 rider는 훌륭한 쉽게 승객 있으며는 rider 대신 고정 했습니다 하는 경우 빨리 바로 수 있습니다. Rider의 이동 시간 속도 제한으로 계속 제한 됩니다.
- 이므로 시간 버스 거의 비어 있지만 재택 레인의 대부분 닫혀 있으므로 고속도로 혼잡도 됩니다. rider는 거의 비어 있지 버스 혼잡된도 켜져 있습니다. rider 보관 위치에 대 한 버스에서 대회 많은 수 없는 동안 총 여정에 나머지 외부 트래픽 계속 결정 됩니다.
- 이므로 혼잡 시 교통량 고속도로 및 버스 정체 됩니다. 뿐만 아니라는 여정 더 오래 걸릴. 이지만 버스를 켜거나 시작 문제일 사람들 어깨에 자격 증명 입력은 자동차가 고속도로 훨씬 더 나은 없기 때문에 있습니다. 자세한 버스 (게스트에 논리 프로세서)를 추가 해도 수에서 작동 하는 이동 중 하나라도 더 쉽게 또는 여정 축소 되는 의미 하지 않습니다.
- 마지막 시나리오에서는 해당 있습니다 수 늘이기 비유를 하지만 여기서 버스가 아닌 재택 정체 되어 있습니다. rider는 여전히가 켜고 버스를 가져오는 동안 문제가 발생 하는 동안 버스는 후에 여정 효율적인 없게 됩니다. 여기서 자세한 버스 (게스트에 논리 프로세서)를 추가 게스트 하면 성능이 향상 됩니다 유일한 시나리오입니다.

여기에서 비교적 쉽게 다양 한 시나리오는 0% 활용 사이 및도 속도인 100% 사용 상태와 다양 한 수준의 영향 있는 버스의 0% 및 100% 사용 상태는 예측할 수는 있습니다.

게스트 뿐만 아니라 호스트에 대 한 적절 한 대상으로 CPU 큐 용량 이상으로 같은 추론에 대 한 적절 한 시작을는 40%의 위에 보안 주체를 적용 합니다.

## <a name="appendix-b-considerations-regarding-different-processor-speeds-and-the-effect-of-processor-power-management-on-processor-speeds"></a>부록 B: 서로 다른 프로세서 속도 및 프로세서 속도의 프로세서 전원 관리의 영향에 대 한 고려 사항

전체 프로세서 선택 단원에서 데이터를 수집 하는 동안 프로세서 클럭 속도의 100%로 실행 되 고 대체 시스템 동일한 속도 프로세서에는 가정이 됩니다. 여기서 기본 전원 관리 옵션은 false, 특히 Windows Server 2008 R2 이상에서는 되는 실제로 두 가정을 불구 하 고 **균형**, 방법론은 여전히 보존 적인 접근 방법은 그대로 나타냅니다. 잠재적 오류 비율을 늘릴 수 있습니다, 프로세서 속도 향상으로 안전성 여백을 증가 합니다.

- 예를 들어, 11.25 Cpu를 요청할 데이터를 수집 하는 경우 프로세서 절반 속도로 실행 된 경우 여기서 시나리오를 보다 정확 하 게 예측할 수 있습니다 5.125 &divide; 2입니다.
- 지정 된 시간 동안 발생 하는 처리의 두 배의 클럭 속도 두 배로 높일 경우 보장 하는 것이 불가능 합니다. 때문 프로세서 소비 RAM에서 대기 하는 시간 또는 다른 시스템 구성 요소는 동일 하 게 유지 수 없습니다. 최종적 이며 더 빠른 프로세서 큰 비율로 가져올 데이터를 기다리는 동안 유휴 시간을 보낼 수 있습니다. 마찬가지로 보수적 되는 최소 공통 분모를 사용 하 여 고정 및 프로세서 속도 간의 선형 비교를 가정 하 여 잠재적으로 false 수준의 정확도 계산 하려고 하지 마세요 하는 것이 좋습니다.

또는 대체 하드웨어에서 프로세서 속도 현재 설치 된 하드웨어 보다 낮은 경우 것 비례 크기에 필요한 프로세서의 예상 증가 해도 안전 합니다. 예를 들어는 10 개의 프로세서를 사이트의 부하를 유지 하는 데 필요한 및 3.3 ghz 현재 프로세서를 실행 하는 대체 프로세서 2.6ghz에서 실행될지를 속도 21% 감소 계산 됩니다. 이 경우 12 프로세서 권장 되는 것입니다.

즉, 이러한 가변성 용량 관리 프로세서 사용률 대상 변경 되지 않습니다. 더 높은 부하에서 시스템을 실행 하는 요구를 부하에 따라 동적으로 프로세서의 클럭 속도 조정 될 때 CPU 자주 사용 되는 시간이 더 높은 클록 속도 상태의 100%에서 40% 사용률에 궁극적인 목표를 수행 하는 시나리오를 생성 합니다. 최대 클럭 속도 상태입니다. CPU 속도와 전력 절감 생성 보다 작으면 아무 것도 제한 됩니다 다시 중 최대 시나리오 해제 합니다.

> [!NOTE]
> 옵션에서 프로세서 전원 관리를 해제 하는 것 (전원 관리 설정 **고성능**) 데이터를 수집 하는 동안. 대상 서버에서 CPU 사용량 보다 정확한 표현을 제공 합니다.

서로 다른 프로세서에 대 한 예측을 조정 하는 프로세서 속도 두 배로 높일 경우 처리 수행 될 수 있는 양이 두 배를 위에서 설명한 다른 시스템 병목 현상을 제외 하 고 안전한 것으로 사용 합니다.  현재 프로세서의 내부 아키텍처 충분히 간에 다릅니다 표준 성능 평가에서 SPECint_rate2006 벤치 마크를 활용 하 여 계기에서 데이터를 가져왔습니다 보다 다른 프로세서를 사용 하 여의 효과를 더욱 안전 하 게 되는 프로세서 Corporation입니다.

1. 사용할 계획 하는 프로세서 사용에 대 한 SPECint_rate2006 점수를 찾습니다.
    1. 표준 성능 평가 Corporation의 웹 사이트를 선택 **결과**, 강조 표시 **CPU2006**를 선택 하 고 **모든 SPECint_rate2006 결과 검색**.
    1. 아래 **간단한 요청**, 예를 들어 대상 프로세서에 대 한 검색 조건을 입력 **프로세서 일치 E5-2630 (baselinetarget)** 및 **프로세서 일치 E5-2650(기준)** .
    1. 사용할 서버 및 프로세서 구성을 찾습니다 (또는 항목 닫기, 정확한 일치를 사용할 수 없는 경우) 값을 확인 하 고는 **결과** 하 고 **# 코어** 열입니다.
1. 한정자를 확인 하려면 다음 수식을 사용 하 여:
   >((*대상 플랫폼 코어당 점수 값*) &times; (*MHz 코어당 기준 플랫폼*)) &divide; ((*기준 당 코어 점수 값*) &times; (*MHz 코어당 대상 플랫폼의*))  

    위의 예제를 사용합니다.
   >(35.83 &times; 2000) &divide; (33.75 &times; 2300) = 0.92
1. 한정자 프로세서의 예상된 수를 곱하십시오.  E5-2650에서 이동 하려면 위의 경우에 프로세서 E5 2630 프로세서를 곱하는 계산된 11.25 Cpu &times; 0.92 = 10.35 프로세서가 필요 합니다.

## <a name="appendix-c-fundamentals-regarding-the-operating-system-interacting-with-storage"></a>부록 C: 저장소와 상호 작용 하는 운영 체제에 대 한 기본 사항

에 설명 된 큐 이론적 개념 [응답 시간/시스템 바빠서 성능에 미치는 영향을](#response-timehow-the-system-busyness-impacts-performance) 저장소에 해당 됩니다. I/O 운영 체제 핸들을를 이러한 개념을 적용 해야 하는 방법에 대 한 지식이 필요 합니다. Microsoft Windows 운영 체제에서 I/O 요청이 보관할 큐를 각 실제 디스크에 대해 만들어집니다. 그러나 물리적 디스크에 설명이로 설정 해야 합니다. 배열 컨트롤러 및 San 운영 체제에 포함 된 스핀 집계 단일 실제 디스크를 제공합니다. 또한 배열 컨트롤러 및 San 배열 집합에 여러 디스크를 집계를 다음 분할이 배열은 여러 실제 디스크 (그림 참조)으로 운영 체제에서 제공 되는 여러 개의 "파티션"으로 설정 합니다.

![블록 스핀 들](media/capacity-planning-considerations-block-spindles.png)  

이 그림에서 2 개의 스핀 들 미러된 되며 데이터 저장소 (데이터 2 및 Data 1)에 대 한 논리 영역으로 분할 합니다. 이러한 논리 영역 운영 체제에서 별도 물리적 디스크로 표시 됩니다.

항상 혼동을 줄 수 있습니다 하지만 다음과 같은 용어는 다양 한 엔터티를 식별 하이 부록 전체에서 사용 됩니다.

- **스핀 들 –** 물리적 서버에 설치 된 장치입니다.
- **배열-** 컨트롤러 별로 집계 된 스핀 들의 컬렉션입니다.
- **파티션-배열** 집계 된 배열의 분할
- **LUN –** 를 참조할 때 사용 되는 배열, San
- **디스크-** 운영 체제는 단일 실제 디스크를 관찰 합니다.
- **파티션-** 어떤 운영 체제에 게 실제 디스크의 논리적 분할 합니다.

### <a name="operating-system-architecture-considerations"></a>운영 체제 아키텍처 고려 사항

운영 체제; 관찰 되는 각 디스크에 대 한 In/First FIFO (선입 선출) I/O 큐를 만듭니다. 이 디스크는 스핀 들, 배열, 또는 배열 파티션을 나타내는 수 수 있습니다. I/O 처리와 관련 하 여 운영 체제 관점에서 더 많은 큐에 좋습니다. FIFO 큐도 serialize 하는 대로 요청이 도착 의미는 저장소 하위 시스템에 발급 된 모든 I/o를 순서 대로 처리 되어야 합니다. 관찰 된 스핀 들/배열을 사용 하 여 운영 체제에서 각 디스크를 상호 연결 하 여 운영 체제를 보유 하 고 있으므로 디스크 부족 한 I/O 리소스에 대 한 경합을 제거 하 고 단일 I/O 요구를 격리 디스크의 각 고유 집합에 대 한 I/O 큐를 디스크입니다. 예외로, Windows Server 2008 I/O 우선 순위 지정의 개념을 소개 하 고 "낮음" 우선 순위를 사용 하도록 디자인 된 응용 프로그램 일반 순서가 범주에 속하지 백 앉아. "Normal입니다."를 "낮음" 우선 순위 기본값을 활용 하 여 명시적으로 코딩 된 응용 프로그램

### <a name="introducing-simple-storage-subsystems"></a>단순한 저장소 하위 시스템을 소개

간단한 예 (컴퓨터 내에서 단일 하드 드라이브)를 사용 하 여 시작 하는 구성 요소 분석을 제공 됩니다. 분할이 주요 저장소 하위 시스템 구성 요소에, 시스템 구성 됩니다.

- **1 –** 10,000 RPM Ultra 빠른 SCSI HD (울트라 빠른 SCSI 20 MB/s 전송 속도 있음)
- **1-** SCSI 버스 (케이블)
- **1 –** ultra 빠른 SCSI 어댑터
- **1-** 32 비트 33 MHz PCI 버스

구성 요소 식별 되 면 데이터의 양을 시스템을 전송할 수 또는 얼마나 많은 I/O를 처리할 수 있습니다, 아이디어를 계산할 수 있습니다. I/O의 양 및 시스템을 전송할 수 있는 데이터의 양에 상관 된 참고 하지만 동일 하지는 않습니다. 이 상관 관계는 디스크 I/O 난수 또는 순차적 인지 및 블록 크기에 따라 달라 집니다. (모든 데이터 블록으로 디스크에 기록 되지만 다른을 사용 하 여 다른 응용 프로그램 블록 크기.) 요소 별로 기준:

- **하드 드라이브 –** 평균 10,000 RPM 하드 드라이브에는 7 (밀리초) (ms) 시간 및 3ms 액세스를 검색 합니다. 검색 시간은 플래터에서 위치를 이동 하려면 읽기/쓰기 헤드에 걸리는 평균 기간입니다. 액세스 시간은 읽거나 헤드를 올바른 위치에 있으면 디스크에 데이터를 작성 하는 데 걸리는 평균 기간입니다. 따라서 10, 000 RPM HD에서 데이터의 고유 블록을 읽는 데 필요한 평균 시간 데이터 블록당를 검색 하 고 약 10 밀리초 (또는.010 초)의 합계에 대 한 액세스를 구성 합니다.

  디스크에 대 한 액세스 권한을 모든 디스크에서 새 위치로 헤드의 이동에 필요한 경우 읽기/쓰기 동작 이라고 "임의"입니다. 따라서 모든 I/O 임의 경우 10,000 RPM HD 처리할 수 있는 약 100 IOPS (초당) I/O (공식은 1000ms 10ms I/O 또는 1000/10으로 나눈 초당 100 IOPS =) 합니다.

  또는 모든 I/O는 HD에 인접 한 섹터에서 발생 하면이 라고 순차 I/O입니다. 순차적 I/O가 없는 이므로 첫 번째 I/O가 완료 되 면 읽기/쓰기 헤드는 HD에서 데이터의 다음 블록 저장 된 시작 시간을 검색 합니다. 따라서 10,000 RPM HD는 약 333 처리할 수 있는 I/O / 초 (I/O 당 밀리초를 3으로 나눈 초당 1000 밀리초)입니다.

  >[!NOTE]
  >이 예제에서는 하나의 원기둥의 데이터를 보관할 일반적으로 디스크 캐시에 반영 되지 않습니다. 이 경우 첫 번째 I/O에서 10 밀리초가 필요 하 고 디스크 전체 원기둥을 읽습니다. 다른 모든 순차 I/O는 캐시에서 충족 됩니다. 결과적으로 디스크에 캐시 순차 I/O 성능이 향상 될 수 있습니다.
  
  지금 하드 드라이브의 전송 속도 관련 되었습니다 수 있습니다. 하드 드라이브 인지 20 MB/s Ultra 전각 또는 Ultra3 160 MB/s, IOPS 수의 실제 량 처리할 10,000 RPM HD가 ~ 100 임의 또는 순차 I/O ~ 300입니다. 드라이브에 작성 하는 응용 프로그램에 따라 크기를 변경 하는 블록으로 I/O 당 가져오는 데이터의 양이 다릅니다. 예를 들어 블록 크기가 8KB를 100 I/O 작업은에서 읽거나 쓸 하드 드라이브 총 800 KB입니다. 그러나 블록 크기는 32KB 100 경우 I/O는 읽기/쓰기 3,200 KB (3.2MB) 하드 드라이브에 있습니다. SCSI 전송 속도 전송 하는 데이터의 총 크기를 초과 하는, "빠른" 전송 속도 드라이브 가져오기 얻게 됩니다 아무 작업도 수행 합니다. 다음 비교 표를 참조 하세요.

  | |7200 RPM 9ms seek 4ms 액세스|10,000 RPM 되었고 seek 보냈습니다 액세스|15,000 RPM 4ms seek 2ms 액세스
  |-|-|-|-|
  |임의 I/O|80|100|150|
  |순차 I/O|250|300|500|  
  
  |10,000RPM 드라이브|8KB 블록 크기 (Active Directory Jet)|
  |-|-|
  |임의 I/O|800 (KB/s)|
  |순차 I/O|2400 (KB/s)|

- **SCSI 백플레인에서 (버스) –** 이해 하는 방법 "SCSI 백플레인에서 (버스)", 또는 리본 케이블이이 시나리오에서는 블록 크기의 기술 자료에 따라 다릅니다 저장소 하위 시스템의 처리량에 영향을 줍니다. I/O 8KB 블록에 있으면 I/O 버스 핸들 수 얼마나 기본적으로 질문 수는? 이 시나리오에서는 SCSI 버스 되었거나 20 MB/s, 20480 (KB/s). 8KB 블록 나눈 20480 KB/s는 약 2500 IOPS의 SCSI 버스에서 지 원하는 최대를 생성 합니다.

  >[!NOTE]
  >다음 표에 있는 수치는 예를 나타냅니다. 대부분의 연결 된 저장소 장치는 현재 훨씬 높은 처리량을 제공 하는 PCI Express 사용 합니다.  
  
  |I/O 블록 크기당 SCSI 버스에서 지 원하는|2KB 블록 크기|8KB 블록 크기 (AD Jet) (SQL Server 7.0/SQL Server 2000)
  |-|-|-|
  |20 MB/s|10,000|2,500|
  |40 MB/s|20,000|5,000|
  |128 MB/s|65,536|16,384|
  |320 MB/s|160,000|40,000|

  어떤 사용에 관계 없이 버스 병목 상태가 되지 것입니다를 설명 하는 시나리오에서이 차트에서 확인할 수 있게 스핀 들으로 최대값은 100 위의 임계값 중 하나 보다 훨씬 I/O입니다.

  >[!NOTE]
  >이 SCSI 버스 100% 효율적 이라고 가정 합니다.
  
- **SCSI 어댑터 –** 이 처리할 수 있는 I/O의 양에 결정 하는 것에 대 한 제조업체의 사양을 확인 해야 합니다. 일종의를 처리 해야 하는 적절 한 장치, 따라서 처리할 수 있는 i/o 용량은 SCSI 어댑터 (또는 배열 컨트롤러)에 따라 달라 집니다 프로세서.

  이 예제에서는 가정 1,000 I/O 수 있는 처리 됩니다.

- **PCI 버스 –** 흔히 간과 되는 구성 요소입니다. 이 예제에서는이 되지 병목 상태가 발생 합니다. 그러나 시스템을 강화 하는 대로 병목 상태가 될 수 있습니다. 참조에 대 한 33 Mhz에서 작동 하는 32 비트 PCI 버스 수 이론 전송에서 133 MB/s 데이터의 합니다. 다음은 수식입니다.  
  > 32 비트 &divide; 바이트 당 8 비트 &times; 33 MHz = 133 MB/s입니다.  

  이론적 제한;는 실제로 최대 약 50% 실제로 도달 하지만 특정 버스트 시나리오 75% 효율성 짧은 기간에 대 한 가져올 수 있습니다.

  66 Mhz 64-bit PCI 버스 이론적으로 최대 수 (64 비트 &divide; 바이트 당 8 비트 &times; 66 Mhz) 또한 528 MB 초당 = 다른 모든 장치 (예: 네트워크 어댑터, 두 번째 SCSI 컨트롤러 및 등)에 사용 가능한 대역폭이 줄어듭니다 대역폭을 공유 하 고 장치 제한 된 리소스에 대 한 경쟁 하 게 합니다.

이 저장소 하위 시스템의 구성 요소 분석 후 스핀 들을 요청할 수 있는 I/O 및 결과적으로 시스템을 전송할 수 있는 데이터의 양이 많음을 제한 요소입니다. 특히 AD DS 시나리오에서이 개체는 8KB 단위로 초당 100 임의 I/O 총 800 KB 당 두 번째 경우 Jet 데이터베이스에 액세스 합니다. 또는 로그 파일에 독점적으로 할당 되는 한 스핀 들에 대 한 최대 처리량이 저하 될 수는 다음과 같은 제한이: 초당 총 2400 KB (2.4 MB)의 8KB 단위로 초당 300 순차 I/O입니다.

이제 간단한 구성을 분석, 다음 표에 나와 저장소 하위 시스템의 구성 요소는 변경 되거나 추가 병목 상태가 발생 합니다.

|참고|병목 상태 분석|Disk|버스|어댑터|PCI 버스|
|-|-|-|-|-|-|
|두 번째 디스크를 추가한 후 도메인 컨트롤러 구성입니다. 디스크 구성 800 KB/s에서 병목 상태를 나타냅니다.|1 디스크 추가 (총 = 2)<br /><br />임의 I/O가<br /><br />4KB 블록 크기<br /><br />10,000RPM HD|총 200 I/o<br />800 KB/s 총액입니다.| | | |
|7 디스크를 추가한 후 디스크 구성을 계속 3200 KB/s에서 병목 상태를 나타냅니다.|**7 디스크 추가 (총 = 8)**  <br /><br />임의 I/O가<br /><br />4KB 블록 크기<br /><br />10,000RPM HD|총 I/o 800 합니다.<br />3200 KB/s 합계| | | |
|순차적 I/O를 변경한 후 네트워크 어댑터에 병목 상태가 발생 1000 IOPS로 제한 되어 있습니다.|7 디스크 추가 (총 = 8)<br /><br />**순차 I/O가**<br /><br />4KB 블록 크기<br /><br />10,000RPM HD| | |2400 I/O 수 초 읽기/쓸 수 디스크, 컨트롤러 1000 IOPS로 제한| |
|10,000 개의 IOPS를 지 원하는 SCSI 어댑터를 사용 하 여 네트워크 어댑터를 바꾸면 병목 디스크 구성을 반환 합니다.|7 디스크 추가 (총 = 8)<br /><br />임의 I/O가<br /><br />4KB 블록 크기<br /><br />10,000RPM HD<br /><br />**SCSI 어댑터 (이제 지원 10,000 I/O)를 업그레이드 합니다.**|총 I/o 800 합니다.<br />3,200 KB/s 합계| | | |
|블록 크기를 32KB로 증가 후 버스 20 MB/s만 지원 하므로 병목 상태가 됩니다.|7 디스크 추가 (총 = 8)<br /><br />임의 I/O가<br /><br />**32KB 블록 크기**<br /><br />10,000RPM HD| |총 I/o 800 합니다. 25,600 KB/s (25 MB/s)를 디스크에 읽기/쓰기 수입니다.<br /><br />버스 20 MB/s 지원| | |
|버스를 업그레이드 하 고 더 많은 디스크를 추가한, 디스크에 병목 상태가 유지 됩니다.|**13 디스크 추가 (총 = 14)**<br /><br />14 디스크를 사용 하 여 두 번째 SCSI 어댑터를 추가 합니다.<br /><br />임의 I/O가<br /><br />4KB 블록 크기<br /><br />10,000RPM HD<br /><br />**320 MB/s SCSI 버스로 업그레이드**|2800 I/Os<br /><br />11,200 KB/s (10.9 MB/s)| | | |
|순차적 I/O를 변경한 후 디스크에 병목 상태가 유지 됩니다.|13 디스크 추가 (총 = 14)<br /><br />14 디스크를 사용 하 여 두 번째 SCSI 어댑터를 추가 합니다.<br /><br />**순차 I/O가**<br /><br />4KB 블록 크기<br /><br />10,000RPM HD<br /><br />320 MB/s SCSI 버스로 업그레이드|8,400 I/o<br /><br />33,600 KB\s<br /><br />(32.8 MB\s)| | | |
|빠른 하드 드라이브를 추가한 후 디스크에 병목 상태가 유지 됩니다.|13 디스크 추가 (총 = 14)<br /><br />14 디스크를 사용 하 여 두 번째 SCSI 어댑터를 추가 합니다.<br /><br />순차 I/O가<br /><br />4KB 블록 크기<br /><br />**15,000 RPM HD**<br /><br />320 MB/s SCSI 버스로 업그레이드|14000 I/o<br /><br />56, 000 KB/s<br /><br />(54.7 MB/s)| | | |
|블록 크기를 32KB로 증가 후 PCI 버스에 병목 상태가 발생 합니다.|13 디스크 추가 (총 = 14)<br /><br />14 디스크를 사용 하 여 두 번째 SCSI 어댑터를 추가 합니다.<br /><br />순차 I/O가<br /><br />**32KB 블록 크기**<br /><br />15,000 RPM HD<br /><br />320 MB/s SCSI 버스로 업그레이드| | | |14000 I/o<br /><br />448,000 KB/s<br /><br />(437 MB/s)에 스핀 들에 읽기/쓰기 제한입니다.<br /><br />PCI 버스 이론적으로 최대 133 MB/s (가장 효율적 75%)을 지원합니다.|

### <a name="introducing-raid"></a>RAID를 소개합니다.

배열 컨트롤러 도입 되었습니다; 저장소 하위 시스템의 특성은 크게 변경 되지 않습니다. 방금 계산에 SCSI 어댑터를 대체합니다. 변경 내용에 읽기 및 다양 한 배열 수준 (예: RAID 0, RAID 5 또는 RAID 1)를 사용 하는 경우 데이터 디스크에 쓰기의 비용입니다.

Raid 0, 데이터에 스트라이프된 모든 디스크는 RAID에서 설정 합니다. 즉,는 읽기 또는 쓰기 작업 동안 데이터 부분에서 가져온 되었거나 동일한 기간 동안 시스템을 전송할 수 있는 데이터의 양이 증가 하는 각 디스크에 푸시됩니다. 따라서 1 초에서 (10, 000 RPM 드라이브 가정 다시), 각 스핀 들에 100 개의 I/O 작업 수행할 수 있습니다. 지원할 수 있는 I/O의 총 용량은 100 번 N 스핀 스핀 들 (초당 100 * N 생성 I/O) 초당 I/O입니다.

![논리 d: 드라이브](media/capacity-planning-considerations-logical-d-drive.png)

RAID 1에서 데이터 중복성을 위해 포함 된 스핀 쌍에 걸쳐 (복제) 미러 됩니다. 따라서 읽기 I/O 작업을 수행 하면 데이터 집합에 포함 된 스핀을 둘 다에서 읽을 수 있습니다. 이 효과적으로 사용 가능 두 디스크의 I/O 용량 읽기 작업 중입니다. 중요 한 점은 쓰기에 대 한 작업 성능 이점이 없습니다 RAID 1에서 것입니다. 이 같은 데이터 중복성을 위해 두 드라이브에 쓸 때문입니다. 데이터 쓰기 발생 동시에 두 개의 스핀 들에 두 개의 스핀 들의 데이터 중복이 꽉 찼을 때문에 더 긴 경우 고려 하지 않습니다, 하지만 쓰기 I/O 작업을 기본적으로 발생 하는 두 가지 읽기 작업을 방지 합니다. 따라서 모든 쓰기 I/O 비용 두 읽기 I/O입니다. 발생 하는 I/O 작업의 총 수를 확인 하는 정보에서 수식을 만들 수 있습니다.  

> *읽기 I/O* + 2 &times; *쓰기 I/O* = *총 사용 가능한 디스크 I/O 사용*  

때 쓰기 읽기 비율 및 스핀 들 수를 알고 있는 경우 다음 수식을 배열에서 지원할 수 있는 최대 I/O를 식별 하려면 위의 방정식에서 파생 될 수 있습니다.  

> *스핀 들 당 최대 IOPS* &times; 2 스핀 &times; [( *% 읽기* +  *% 쓰기*) &divide; ( *% 읽기* + 2 &times; *% 쓰기*)] = *총 IOPS*

RAID 1 + 0, 읽기 및 쓰기의 비용에 대 한 RAID 1 정확히 동일 하 게 동작 합니다. 그러나 I/O 이제 스트라이프된 미러된 각 집합입니다. If  

> *스핀 들 당 최대 IOPS* &times; 2 스핀 &times; [( *% 읽기* +  *% 쓰기*) &divide; ( *% 읽기* + 2 &times; *% 쓰기*)] = *총 I/O*  

RAID 1 집합 때 다중성에에서 (*N*) 처리할 수 있는 총 I/O가 집합 스트라이프 되 RAID 1 N &times; RAID 1 집합당 I/O:  

> *N* &times; {*스핀 들 당 최대 IOPS* &times; 2 스핀 &times; [( *% 읽기* +  *% 쓰기*) &divide; ( *% 읽기* + 2 &times; *% 쓰기*)]을 (를) = *총 IOPS*

RAID 5에서 라고도 *N* + 1 RAID의 데이터에 스트라이프된 *N* 스핀 들 및 패리티 "+ 1" 스핀 들에 정보가 기록 됩니다. 그러나 RAID 5는 RAID 1 또는 1 + 0 보다 쓰기 I/O를 수행 하는 경우 훨씬 더 비쌉니다. RAID 5 배열에 쓰기 I/O 제출 될 때마다 다음 프로세스를 수행 합니다.

1. 이전 데이터 읽기
1. 이전 패리티 읽기
1. 새 데이터를 작성 합니다.
1. 새 패리티를 작성 합니다.

운영 체제에서 배열 컨트롤러에 전송 된 모든 쓰기 I/O 요청이 4 개 I/O 작업 완료에 필요한 대로 쓰기 요청을 제출 걸릴 4 번 단일 읽기 I/O를 완료 합니다. 변환 하는 스핀 들로 인해 발생 하는 운영 체제 관점에서 I/O 요청 수식을 파생 됩니다.  

> *읽기 I/O* + 4 &times; *쓰기* = *총 I/O*  

마찬가지로 RAID 1 집합에서 읽기 쓰기 및 스핀 들 수의 비율에 알고 있는 경우 다음 수식을 파생 될 수 있습니다 (참고 스핀 들의 총 수를 포함 하지 않는 배열에서 지원할 수 있는 최대 I/O를 식별 하려면 위의 방정식에서 e "drive" 패리티를 손실):  

> *스핀 들 당 IOPS* &times; (*스핀* – 1) &times; [( *% 읽기* +  *% 쓰기*) &divide; ( *% 읽기* + 4 &times; *% 쓰기*)] = *총 IOPS*

### <a name="introducing-sans"></a>San 소개

SAN을 환경에 도입할 때 저장소 하위 시스템의 복잡성을 확장 합니다 설명한 기본 원칙은 변경 되지 않습니다를 모든 시스템에 대 한 I/O 동작 SAN에 연결 하는 단 고려해 야 합니다. 내부 또는 외부에서 연결 된 저장소를 통해 추가 중복 된 SAN을 사용 하 여 주요 이점 중 하나는 용량 계획 이제 계정 내결함성 요구 사항을 고려 되도록 해야 합니다. 또한 자세한 구성 요소 도입 된 평가 해야 하는 합니다. SAN 구성 요소 부분으로 분할 합니다.

- SCSI 또는 파이버 채널 하드 드라이브
- 저장소 단위 채널 백플레인
- 저장소 단위
- 저장소 컨트롤러 모듈
- SAN 스위치가
- HBA(s)
- PCI 버스

중복성을 위해 모든 시스템을 설계할 때 추가 구성 요소 오류의 가능성을 수용할 수 포함 되어 있습니다. 것이 매우 중요 한 경우 용량 계획, 사용 가능한 리소스의 중복 구성 요소는 제외 합니다. 예를 들어, SAN에 두 개의 컨트롤러 모듈을 하나의 컨트롤러 모듈의 I/O 용량은 시스템에 사용할 수 있는 총 I/O 처리량에 대 한 사용 해야 하는 모든입니다. 하나의 컨트롤러에 실패 하면 연결 된 모든 시스템에서 요구 하 여 전체 I/O 로드 해야 나머지 컨트롤러가에서 처리할 수 있는 것 때문입니다. 모든 용량 계획는 피크 사용 기간에 대 한 것 처럼 중복 구성 요소는 사용 가능한 리소스 없습니다 팩터링 해야 하 고 계획 된 최고 사용률이 (수용할 버스트 또는 비정상적인 시스템의 채도 80%를 넘지 않아야 합니다. 동작)입니다. 마찬가지로, 중복 SAN 스위치, 저장소 단위 및 스핀 하지에 포함 시켜야 I/O 계산 합니다.

SCSI 또는 파이버 채널 하드 드라이브의 동작을 분석 하는 경우 설명 된 대로 동작을 분석 하는 방법은 이전에 변경 되지 않습니다. 특정 장점 및 단점 각 프로토콜에 있더라도 당 디스크 제한 요소는 하드 드라이브의 기계적 제한입니다.

저장소 단위에 있는 채널 분석 같습니다 정확 하 게 블록 크기 (예: 8KB)로 나눈 값 (예: 20 MB/s) 대역폭을 SCSI 버스에 있는 리소스를 계산 합니다. 간단한 이전 예제에서 이것 여러 채널의 집계입니다. 예를 들어 6 채널의 경우 20 MB/s 최대 전송 속도 지 원하는 각 총 I/O 및 데이터 전송 사용할 수 있는 경우 100 MB/s (이것은 올바른 것이 없습니다 120 MB/s) 마찬가지로 내결함성은 전체 채널의 손실이 발생할 경우이 계산에서 중요 한 역할을 시스템에만 왼쪽 5 작동 채널. 따라서 지속적으로 오류가 발생할 경우 성능 기대치를 충족을 위해 모든 저장소 채널에 대 한 총 처리량 초과할 수 없습니다 100 MB/s (이 가정 부하 및 내결함성을 모든 채널에서 균등 하 게 분산 됩니다). I/O 프로필을로 설정 하는이 응용 프로그램의 동작에 따라 달라 집니다. Active Directory Jet I/O의 경우이 상관 관계를 대략 12,500 초당 I/O (100 MB/s &divide; I/O 당 8KB).

다음으로, 컨트롤러 모듈에 대 한 제조업체의 사양을 가져오는 필요 각 모듈 수 처리량을 파악 합니다. 이 예제에서는 SAN에 두 개의 컨트롤러 모듈 각 지원 7500 I/O 중복성을 원하지 않는 경우 시스템의 총 처리량 15,000 IOPS를 수 있습니다. 실패 한 경우 최대 처리량을 계산을 하나의 컨트롤러 또는 7,500 IOPS의 처리량 제한은입니다. 이 임계값 보다 훨씬 아래에 모든 저장소 채널에서 지원할 수 있는 12,500 IOPS (4KB 블록 크기를 가정) 최대 이며 따라서 현재 분석의 병목 상태. 여전히 계획 상으로 원하는 최대 I/O에 대 한 계획 됩니다 10,400 I/O입니다.

데이터 컨트롤러 모듈을 종료 하는 경우에 1 GB/s (또는 초당 1 기가 비트)에 등급을 지정 하는 파이버 채널 연결을 자신입니다. 이 다른 메트릭을 사용 하 여 상관 관계를 지정 하려면 1 GB/s 128 MB/s로 변환 (1 GB/s &divide; 8 비트/바이트)입니다. 저장소 단위 (100 MB/s)에서 모든 채널에서 총 대역폭을 초과 하는이 시스템을 하지 병목는이 합니다. 또한,이 두 채널 (추가 1 GB/s 파이버 채널 연결 중복성에 대 한 중)을 하나만 한 연결이 실패 하더라도 나머지 연결 여전히 충분 한 용량이 요구 되는 모든 데이터 전송을 처리 합니다.

En 경로 데이터를 서버에 SAN 스위치를 전송 중 대부분은 합니다. 들어오는 I/O 요청을 처리 하기에 SAN 스위치와 앞으로 적절 한 포트를 찾기, 스위치 더 처리할 수 있는 I/O의 양에 제한이 있지만 제조업체 사양 해야 결정 하는 제한 됩니다. 예를 들어 두 스위치를 각 스위치 10,000 개의 IOPS를 처리할 수 있는 총 처리량에 20,000 개의 IOPS 됩니다. 스위치를 두 개 실패, 시스템의 총 처리량은 10000 IOPS 되 면 문제가 되는 허용 오차를 다시 오류입니다. 이 정상적인 작업의 사용률이 80%를 넘지 원하는 대로 8000 개를 사용 하 여 I/O 있어야 대상 합니다.

마지막으로 서버에 설치 된 HBA 처리할 수 있는 I/O의 양 제한을 해야 합니다. 일반적으로 중복성을 위해 두 번째 HBA 설치 되지만 최대 I/O 처리 될 수 있는의 총 처리량을 계산할 때 해당 SAN 스위치와 마찬가지로 *N* &ndash; 1 Hba는 시스템의 최대 확장성.

### <a name="caching-considerations"></a>캐싱 고려 사항

캐시는 저장소 시스템에서 언제 든 지 전체 성능에 큰 영향 수는 구성 요소 중 하나입니다. 캐싱 알고리즘에 대 한 자세한 분석;이 문서의 범위를 벗어납니다. 그러나 디스크 하위 시스템에 캐시 하는 방법에 대 한 몇 가지 기본 문을 비추기 필요가 있습니다.

- 캐시 되는 지속적인된 향상 된 순차 쓰기 I/O 많은 작은 쓰기 작업 보다 큰 I/O 블록으로 버퍼링 하 고 적지만 크기가 큰 블록 크기의 저장소를 준비 취소 수 있습니다. 이렇게 하면 총 임의 I/O 및 기타 I/O에 대 한 자세한 리소스 가용성을 제공 하므로 총 순차 I/O를 줄일 수 있습니다.
- 캐시 저장소 하위 시스템의 지속적인된 쓰기 I/O 처리량을 향상 되지 않습니다. 스핀 들이 데이터를 커밋할 수 없을 때까지 버퍼링 쓰기만 허용 합니다. 저장소 하위 시스템에 포함 된 스핀을 사용할 수 있는 모든 I/O를 오랜 기간 포화 상태, 캐시 최종적으로 채워집니다. 캐시에 갑작스러운 증가 또는 추가 스핀 들 간에 충분 한 시간을 비워 캐시를 플러시할 수 있도록 충분 한 I/O를 제공 하기 위해 할당 될 해야 합니다.

  자세한 데이터를 버퍼링 시킬 캐시가 크면 캐시로 허용 합니다. 즉, 더 오랫동안 채도 수용할 수 있습니다.

  일반적으로 운영 저장소 하위 시스템에서 데이터를 캐시에 쓸 수만 요구 운영 체제 쓰기 성능이 향상된에 발생 합니다. I/O를 사용 하 여 기본 미디어를 포화 상태, 캐시를 채울 후 쓰기 성능은 디스크 속도를 반환 합니다.

- I/O 읽기 캐싱, 데이터 디스크에서 순차적으로 저장 되 고 캐시 수 미리 읽기 (있도록 다음 섹터 다음에 요청할 수 있는 데이터에 가정) 하는 경우 여기서 캐시는 가장 유용한 시나리오가입니다.
- 읽을 때 I/O가 임의의 드라이브 컨트롤러에 캐시 되지 않을 디스크에서 읽을 수 있는 데이터 양에 대 한 모든 향상 된 기능을 제공 합니다. 존재 하지 않는 운영 체제 또는 응용 프로그램 기반 캐시 크기를 하드웨어 기반 캐시 크기 보다 큰 경우의 모든 향상이입니다.

  Active Directory의 경우 캐시 RAM의 양이 제한 됩니다.

### <a name="ssd-considerations"></a>SSD 고려 사항

SSDs는 전혀 다른 체질 하드 디스크 스핀 들 기반 이며 아직 두 키 기준 남아 있습니다. "얼마나 많은 IOPS를 처리할 수 있습니까"? "해당 IOPS에 대 한 대기 시간 이란?" 및 스핀 들 기반 하드 디스크를 비교 하 여 Ssd의 더 높은 볼륨을 처리할 수 있습니다 및 짧은 대기 시간을 가질 수 있습니다. 일반적 및이 문서의 작성 시점 현재 SSDs는 1gb 당 비용으로 비교에서 여전히 비용이 많이 듭니다, 비용-당-I/O 측면에서 매우 저렴 되며 저장소 성능 측면에서 중요 한 고려 사항은 것이 좋습니다.

고려 사항:

- IOPS 및 대기 시간이 매우 제조업체 디자인에 대 한 주관적인 되며 경우도 관찰 수 기반된 기술을 스핀 들 보다 성능이 떨어집니다. 즉, 검토 및 제조업체 사양 드라이브에서 드라이브의 유효성을 검사 하 고 모든 일반적인 원칙을 가정 하지에 더욱 중요 한 것입니다.
- IOPS 형식 읽기 또는 쓰기 여부에 따라 매우 다른 번호를 가질 수 있습니다. AD DS 서비스를 일반적으로 주로 읽기 기반 됩니다 일부 다른 응용 프로그램 시나리오 보다 덜 영향을 받는.
- "지속 시간과 쓰기" –이 하는 개념 SSD 셀은 결국 밖에 되지 않습니다. 이 문제를 사용 하 여 다른 방식 처리 하는 다양 한 제조업체입니다. 이상 데이터베이스 드라이브 주로 읽기 I/O 프로필 데이터 휘발성 아니므로 이러한 문제의 중요성을 downplaying에 대 한 허용 됩니다.

### <a name="summary"></a>요약

저장소에 대해 생각 하는 한 가지 방법은 가구 배관을 그림 됩니다. 데이터에 저장 된 미디어의 IOPS는 가구 주 드레이닝 한다고 가정 합니다. 경우 (예: 파이프의 루트) 막혀서는이 또는 제한 (축소 또는 너무 작은 경우), 너무 많은 물 되는 경우 백업은 가족 모두가 각자의 모든 싱크로 (너무 많은 게스트)를 사용 합니다. 이 하나 이상의 시스템 SAN/NAS/iSCSI에 동일한 기본 미디어를 사용 하 여 공유 저장소 활용 하는 공유 환경에 완벽 하 게 유사 합니다. 다양 한 시나리오를 해결 하려면 다른 접근 방식은 사용할 수 있습니다.:

- 축소 또는 크기가 드레이닝 전체 규모 바꾸기 및 수정에 필요합니다. 이 새 하드웨어에서 추가 인프라 전체에서 공유 저장소를 사용 하 여 시스템을 재배포 또는 비슷한 것입니다.
- "복잡된" 파이프는 일반적으로 하나 이상의 잘못 된 문제의 식별 및 제거 문제를 의미합니다. Storage 시나리오에서이 저장소 또는 시스템 수준 백업의 모든 서버와 동기화 된 조각 모음 소프트웨어 실행 사용량이 많은 기간 동안 동기화 된 바이러스 백신 검사를 수 있습니다.

여러 나옴과 동시에 주 드레이닝 공급 하는 모든 내부 디자인. 아무 것도 이러한에서 나옴과 동시 또는 연결 지점 중 하나를 중지 되 면 해당 동기 분 기화 뒤 것만 백업 지점입니다. 저장소 시나리오에서는 스위치 (SAN/NAS/iSCSI 시나리오)를 오버 로드 된, 드라이버 호환성 문제 (잘못 된 드라이버/HBA Firmware/storport.sys 조합), 또는 백업/바이러스 백신/조각 모음 수 있습니다. 저장소 "파이프 로" 충분 한 크기 인지를 확인 하려면 IOPS 및 I/O 크기를 측정 해야 합니다. 각이 음에 협력 적절 한 추가할 "파이프 지름입니다."

## <a name="appendix-d---discussion-on-storage-troubleshooting---environments-where-providing-at-least-as-much-ram-as-the-database-size-is-not-a-viable-option"></a>여기서 제공 만큼 이상 RAM 데이터베이스 크기가 유용한 옵션이 아니므로 부록 D-storage 문제 해결에 대 한 논의-환경

이러한 권장 사항은 저장소 기술에서 변경 내용을 수용할 수 있도록 존재 하는 이유를 이해 하는 것이 유용 합니다. 이러한 권장 사항은 두 가지 이유로 존재 합니다. 첫 번째는 IO의 격리 성능 문제 (즉, 페이징) 운영 체제 스핀 들에 데이터베이스 및 I/O 프로필의 성능 영향을 주지 않습니다. 두 번째는 AD DS (및 대부분의 데이터베이스)에 대 한 로그 파일은 기본적으로 순차을 스핀 들 기반 하드 드라이브 및 캐시에 더 임의 I/O 패턴의 운영 체제 및 거의 비교 하 여 순차 I/O를 사용 하는 경우 큰 성능 이점은 AD DS의 순수한 임의 I/O 패턴 데이터베이스 드라이브입니다. 별도 실제 드라이브에 대 한 순차 I/O를 격리 하 여 처리량을 늘릴 수 있습니다. 오늘날의 저장소 옵션으로 표시 문제는 이러한 권장 사항 뒤 기본 가정이 더 이상 true. 대부분에서 iSCSI SAN, NAS에 및 가상 디스크 이미지 파일, 기본 미디어 여러 호스트 간에 공유 되는 저장소, 따라서 "IO 격리" 및 "순차 I/O 최적화" 측면을 완전히 부정 하는 등의 저장소 시나리오를 가상화 합니다. 사실 이러한 시나리오는 공유 미디어에 액세스 하는 다른 호스트에 도메인 컨트롤러에 대 한 응답성이 저하 될 수 있습니다 복잡성이 추가 계층을 추가 합니다.

저장소 성능 계획의 세 가지 범주 고려해 야 할: 콜드 캐시 상태, 캐시 준비 상태 및 백업/복원 합니다. 도메인 컨트롤러를 처음으로 다시 부팅 등의 시나리오에서 콜드 캐시 상태 발생 또는 Active Directory 서비스를 다시 시작 하 고 RAM의 Active Directory 데이터가 없습니다. 웜 캐시 상태 위치 이며 안정적인 상태에서 도메인 컨트롤러는 데이터베이스에 캐시 됩니다. 이들은 매우 다른 성능 프로필에 게와 전체 데이터베이스를 캐시에 충분 한 RAM을 가진 도움이 되지 않고 성능 캐시 콜드 때 명심 해야 합니다. 콜드 캐시를 준비, 다음 비유를 사용 하 여 이러한 두 시나리오에 대 한 성능 디자인은 "스 프린트" 및 "marathon." 웜 캐시를 사용 하 여 서버를 실행 하는 생각할 수 있습니다.

콜드 캐시와 웜 캐시 시나리오에 대 한 질문을 얼마나 빨리 저장소 데이터를 이동할 수는 디스크에서 메모리로 됩니다. 캐시를 준비 합니다. 여기서 시간이 지남에 따라 성능이 향상 됩니다와 더 많은 쿼리 데이터를 다시 사용, 캐시 적중 비율 증가 하는 경우 디스크를 이동할 필요가의 빈도 감소 시나리오입니다. 결과적으로 디스크에 이동의 성능에 나쁜 영향 감소 합니다. 만 캐시를 준비 하 고 시스템을 최대한 허용 된 크기 만큼 증가를 대기 하는 동안 성능 저하는 일시적입니다. 대화는 디스크에서 데이터를 받았으면 수는 얼마나 빨리 단순화할 수 있습니다 및은 주관적 사용할 수 있는 IOPS를 내부 저장소에서 Active Directory를 사용할 수 있는 IOPS의 단순 측정값 인지 합니다. 계획 측면에서 이기 때문에 준비 캐시 및 백업/복원 시나리오 예외 단위로 발생 일반적으로 시간을 발생은 DC의 부하에 대 한 주관적인 일반 권장 사항 없는 제외 하 고 이러한 작업을 예약할 수는 사용량이 많지 않은 시간입니다.

대부분의 시나리오에서 AD DS와 90 %read/10% 쓰기의 비율을 일반적으로 IO 읽기 주로입니다. 읽기 I/O 대개 사용자 경험에 대 한 병목 상태가 발생 하는 경향이 있습니다 쓰고 쓰기 IO를 통한 하면 성능이 저하 됩니다. 캐시 읽기 IO는 있도록 최소한의 이점을 제공 하는 경향이 있습니다는 주로 임의 I/O NTDS.dit가 그대로 훨씬 더 중요 구성에 대 한 저장소 프로필을 읽을 I/O 올바르게 합니다.

정상 작동 상태에 대 한 저장소 계획 목적은 디스크에서 반환할 AD DS에서 요청에 대 한 대기 시간을 최소화 합니다. 이 기본적으로 대기 중인 주소 및 보류 중인 I/O 숫자 보다 작거나 경로가 디스크의 수에 해당 하는 의미 합니다. 이 측정 하는 방법의 여러 가지가 있습니다. 성능 모니터링 시나리오, 일반적인 권장 사항에서는 해당 논리 디스크 ( *\<NTDS 데이터베이스 드라이브\>* ) \Avg Disk sec/Read 수 20 밀리초 미만입니다. 원하는 작업 임계값 가능한 저장소의 유형에 따라 2 ~ 6 밀리초 (.002를.006 초) 범위에서 훨씬 더 낮은, 가급적으로 저장소의 속도 가까운 이어야 합니다.

예:

![저장소 대기 시간 차트](media/capacity-planning-considerations-storage-latency.png)

차트를 분석 합니다.

- **– 왼쪽에 녹색 아이콘** 대기 시간이 10ms에서 일관성을 유지 합니다. 800 IOPS에서 2400 IOPS 부하를 증가합니다. 이 절대 최소 I/O 요청을 기본 저장소에서 얼마나 빨리 처리할 수 있습니다. 이 저장소 솔루션의 세부 사항 적용 됩니다.
- **– 오른쪽 포도주 oval** 처리량의 대기 시간이 계속 증가 하는 동안 들이 데이터 컬렉션의 끝에 녹색 원을 통해 종료에서 플랫 유지 됩니다. 이 때 기본 저장소의 물리적 제한을 초과 하는 요청 볼륨 길수록 요청을 보냅니다 저장소 하위 시스템에 전송 대기 중인 큐 대기 설명 하는 합니다.

이 기술 자료를 적용 합니다.

- **대규모 그룹 –의 사용자 쿼리 멤버 자격에 대 한 영향** 디스크 I/O의 양에에서 1 MB의 데이터를 읽는 필요 하며 시간이 얼마나 걸리는지 평가할 수 있습니다 다음과 같이 가정 합니다.
  - Active Directory 데이터베이스 페이지 크기 8KB는 있습니다. 
  - 최소 128 페이지의 디스크에서 읽은 수 해야 합니다. 
  - 아무 것도 가정 하 고 캐시 됩니다 하는 데 최소 1.28 초 클라이언트에 반환 하기 위해 디스크에서 데이터를 로드 하는 것이 floor (10 밀리초)에서. 20 밀리초, 여기서 저장소 처리량에 공룡의 최대값을 초과 및 권장 되는 최대 이기도에서 최종 사용자에 게 반환 하기 위해 디스크에서 데이터를 가져올 수 2.5 초가 걸립니다.  
- **속도 캐시 준비 –** 저장소 예제에 대 한 처리량을 최대화 하기 위해 클라이언트 부하 것 이라는 가정 하는 경우 캐시를 2400 IOPS의 속도로 준비는 &times; IO 당 8KB입니다. 또는 두 번째 약 1GB의 데이터베이스에 로드 RAM 53 초 마다 당 약 20 MB/s입니다.

> [!NOTE]
> 일반적으로 짧은 시간 동안 관찰 하는 구성 요소 적극적으로 읽거나 경우 시스템은 백업 또는 AD DS가 가비지 수집을 실행 하는 경우와 같은 디스크에 쓸 때 대기 시간 증가 합니다. 추가 헤드 공간을 계산을 기반으로 이러한 주기적 이벤트를 수용 하기 위해 제공 되어야 합니다. 일반 함수에 영향을 주지 않고 이러한 시나리오에 맞게 충분 한 처리량을 제공 되 고 목표입니다.

볼 수 있듯이 저장소 디자인을 얼마나 빨리 캐시 웜 가능한 수에 따라 물리적 제한이 있습니다. 들어오는 캐시를 준비 하는 새로운 기본 저장소를 제공할 수 있는 속도 최대 클라이언트 요청 합니다. "사전 준비" 캐시 사용량이 적은 시간 동안에 스크립트를 실행에 실제 클라이언트 요청에 따라 결정을 로드 하는 경쟁을 제공 합니다. 부정적인 영향을 기본적으로 생성 됩니다 캐시를 준비 하는 인위적인 하려고가 DC에 연결 하는 클라이언트와 관련 된 데이터를 로드 하는 대로 부족 한 디스크 리소스에 대 한 경쟁 때문에 클라이언트가 먼저 필요로 하는 데이터를 제공 합니다.
