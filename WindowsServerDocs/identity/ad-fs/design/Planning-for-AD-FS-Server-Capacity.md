---
ms.assetid: ef91f1d8-2991-4d90-b687-5fa189737c88
title: "광고 FS 서버 용량에 대 한 계획"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 484dd08edef85b91e777f8963f175a6172c75430
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="planning-for-ad-fs-server-capacity"></a>광고 FS 서버 용량에 대 한 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

  
> [!NOTE]  
> 이 항목에서 제공 하는 내용 Windows Server 2012를 실행 하는 서버에 수행 되는 실제 테스트를 반영 하지 않습니다. 이 항목 필수 테스트 수행 된 업데이트 됩니다.  
  
Active Directory Federation Services에 대 한 계획 용량 \(AD FS\) Federation 서비스에 대 한 사용량이 예측 및 계획 하는 과정은 또는 scaling\ 접속 사용자에 맞게 ADFS 서버 배포 로드 요구 합니다.  
  
이 섹션 배포 지침 federation 서버와 federation 서버 프록시 역할에 설명 하 고 Microsoft에서 ADFS 제품 팀에서 수행한 랩 테스트에 따라 합니다. 이 콘텐츠 목적은 수 있도록 다음과 같습니다.  
  
-   배포에 대 한 조직의 특정 ADFS, 서버 Adfs의 수와 같은 하드웨어 요구 예상 밀접 하 게 합니다.  
  
-   정확 하 게 예상된 사용량이 요청 sign\의 확장에 대 한 계획을 프로젝 팅 하 고 ADFS 배포 사용량이 예상 처리할 수 있는지 확인 합니다.  
  
이 용량 콘텐츠 계획 읽기용 진행 하기 전에 먼저 다음과 같은 두 가지 표에 나와 있는 순서 대로 작업을 완료 하는 것이 좋습니다. 첫 번째 표에 수 있도록 권장 되는 작업에 대 한 링크가이 용량 토론 계획에 대 한 관련 된 상황에 맞는 제공을 제공 합니다.  
  
|권장된 작업|설명|참조|  
|--------------------|---------------|-------------|  
|이해 ADFS federation 서버 및 federation 서버 프록시 배포를 위해 요구 사항|중요 한 하드웨어 및 소프트웨어 요구 사항이 federation 서버와 federation 서버 프록시 배포 하는 데 필요한 검토 합니다.|[부록 a: 검토 광고 FS 요구 사항](Appendix-A--Reviewing-AD-FS-Requirements.md)|  
|조직에 배포할 ADFS 구성 데이터베이스 유형 선택|먼저, 배포할 ADFS 구성 데이터베이스 유형을 확인 해야이 섹션의 용량 계획 데이터 사용을 시작 하기 전에 Windows 내부 데이터베이스 \(WID\) 또는 구조적 쿼리 언어 \(SQL\) 데이터베이스 합니다.|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md);<br /><br />[광고 FS 배포 토폴로지 고려 사항](AD-FS-Deployment-Topology-Considerations.md)|  
|새 ADFS 구성 데이터베이스 선택와 함께 사용 하려면 토폴로지 레이아웃 확인|배포에 사용 하 여 ADFS 구성 데이터베이스의 종류에 결정 했으면, 해야 합니다 고려해 어떤 배포가 가장 일치 하는 해야 하는 곳 federation 서버와 federation 프록시 서버 생산 환경 내에서 합니다.|[해당 AD FS 배포가 확인](Determine-Your-AD-FS-Deployment-Topology.md)|  
|주요 광고 FS 관련 용량 계획 계약을 이해 합니다.|일반적인 용량 ADFS 용량 토론 계획에서 사용 되는 서비스 계약 계획을 정의 검토 합니다.|섹션을 참조 [ADFS 용량 계획 계약](Planning-for-AD-FS-Server-Capacity.md#bk_terms) 이 항목에서|  
  
위의 표의 콘텐츠를 검토 한 후 이제 다음 표에서 필수 작업을 완료할 수 있습니다.  
  
|필수 작업|설명|참조|  
|---------------------|---------------|-------------|  
|AD FS 용량 크기 조정 스프레드시트 계획 다운로드|광고 FS 용량 계획 크기 조정 스프레드시트 ADFS federation 서버 농장 배포를 위해 필요한 federation 서버 수를 확인할 수 있습니다. 이 스프레드시트 사용 하는 방법에 대 한 지침 다음 작업에 대 한 아래 제공 된 링크에서 사용할 수 있습니다.|[광고 FS 용량 계획 스프레드시트](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacityPlanning.xlsx)|  
|액세스 해야 하는 하나의 sign\ 켜 짐 \(SSO\) 대상 claims\ 인식 응용 프로그램 및이 액세스와 관련 된 예상된 최고 사용 기간에는 사용자의 수에 대 한 데이터를 수집 합니다.|사용자 데이터를 수집할이 입력된 값 AD FS 용량 계획 크기 조정 스프레드시트의 컨텍스트에서 필요한에 대 한 사용 됩니다.|[조직에 대 한 federation 서버 횟수 예측](Planning-for-Federation-Server-Capacity.md#bk_estimatefs)|  
|Windows Server 2016 용 AD FS 용량 계획 스프레드시트|Windows Server 2016 용 업데이트 계획 워크시트|[ADFS Windows Server 2016 용량 계획](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)  
  
## <a name="bk_terms"></a>광고 FS 용량 계획 계약  
다음 표에이 기능 계획 AD FS 디자인 가이드의 섹션에서에서 자주 사용 되는 중요 조건을 다룹니다. ADFS 계약의 전체 목록을 보려면 [이해 키 광고 FS 개념](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)합니다.  
  
|용어|정의|  
|--------|--------------|  
|동시 사용자|시간을 최대 사용 활동 기간 일반적으로 특정된 기간 동안 서비스에 대 한 요청을 제출 하는 사용자의 예상된 수 있습니다.|  
|현재 사용자|시스템을 있지만 반드시 지정 된 기간 동안 요청을 제출에서 활성화 되어 있는 사용자의 대략적인 평균 수 있습니다.|  
|사용자 정의 된|일반적으로 계정을 시스템에 정의 된 사용자의 수에 따라 이론적 최대 사용자 수 있습니다.|  
|초당 요청|요청 하거나 클라이언트 제출한 수가 \ (경우에 system\ 로드에 대해 이야기) 서버에 의해 처리 또는 \ (throughput\ 서버에 대해 이야기) 경우 잠시에서 합니다. 이 메트릭 계획 메모리 용량 및 프로세서가 서버에서 사용 됩니다.|  
|대상 서버 응답성 및 활용|서버를 사용할 수 있는 성능 범위 바인딩된 성공 메트릭 합니다. 일반적으로 응답성 미만이 되 활용도 대상 위에서 이동 하거나, 시스템 지나치게으로 간주 되 고 용량이 더 큰 필요 합니다.|  
|Windows 내부 \(WID\) 데이터베이스|특정 ADFS 배포에서 SQL Server 하는 대신 사용할 수 있는 기본 AD FS 구성 데이터베이스 합니다.|  
  
## <a name="configuration-environment-used-during-ad-fs-testing"></a>ADFS 테스트 하는 동안 사용 되는 구성 환경  
이 섹션 ADFS 제품 팀의 테스트를 수행 하는 데 사용 되는 구성 환경을 설명 합니다. 팀은 사용 성능 및 federation 서버 테스트에서 확장성 데이터를 수집 하는 다음과 같은 컴퓨터 하드웨어, 소프트웨어 및 네트워크 구성 됩니다.  
  
-   듀얼 코어 2.27 4 개의 기가헤르쯔 \(GHz\) \(8 cores\)  
  
-   16\ 1GB RAM  
  
-   Windows Server 2008 R2 Enterprise Edition  
  
-   네트워크 기가 비트  
  
> [!NOTE]  
> 16GB의 RAM 테스트 하는 동안 federation 서버에 사용 된, 있지만 대부분의 ADFS 배포 4GB의 RAM federation 서버 당 같은 더 많은 보통 메모리 크기를 사용할 수 있습니다. 이 광고 FS 용량 계획 가정 각 federation 서버는 약 사용 하는 내용을 광고 FS 용량 계획 스프레드시트에서 제공 되는 결과 함께 기반에서 제공 되는 추천 4GB의 ram 대부분의 ADFS 생산 환경에 대 한입니다.  
  
다음과 같은 구성 테스트 federation 서버 프록시 성능과 확장성 데이터를 수집 하는 데 사용 하는 제품 팀은 다음과 같습니다.  
  
-   듀얼 코어 2.24 4 개의 g h z \(4 cores\)  
  
-   4\ 1GB RAM  
  
-   Windows Server 2008 R2 Enterprise Edition  
  
-   네트워크 기가 비트  
  
> [!NOTE]  
> 용량 추천 ADFS 서버에 대 한 해당된 환경에서 사용할 수 네트워크 및 하드웨어 구성에 대 한 선택 사양에 따라 상당히 다를 수 있습니다. 참조 지점으로이 콘텐츠를 제공 하는 크기 조정 지침 앞에서 언급 한 컴퓨터에서 80%의 활용도 대상에 따라 됩니다.  
  
## <a name="measure-ad-fs-server-capacity"></a>ADFS 측정 서버 용량  
일반적으로 확장성 서버 성능에 영향을 주는 하드웨어 구성 요소 CPU, 메모리, 디스크 및 네트워크 어댑터는 합니다. 다행히 각 ADFS 구성 요소 거의 수요 메모리 및 디스크 공간이 필요합니다. 네트워크 연결이 확실 한 요구 사항입니다. 따라서 로드 테스트에서 federation 서버 및 federation 서버 프록시 수행 하는 서버 용량 측정 하기 위한 두 주요 영역에 집중 합니다.  
  
-   **초당 ADFS 요청 피크:** federation 서버에 초당 처리 sign\에서 요청 수 있습니다. 이 단위 개수 동시 사용자 지정된 하는 서버에 로그인 할 수 판단 하는 데 도움이 됩니다. 이 단위 성능에이 영향을 알아보려면 CPU 소비 측정와 함께에서이 단위를 사용할 수 있습니다.  
  
-   **CPU 소비:** 용량이 측정 있는 CPU가 비율 합니다. 이 단위 발생 하는 전반적인 CPU 로드 수 초당 들어오는 sign\의 요청에 따라 결정 하는 데 도움이 됩니다.  
  
## <a name="continue-reading-more-about-ad-fs-capacity-planning"></a>계속 ADFS 용량 계획에 대해 자세히 읽기  
필수 작업을 완료 하 고 있는 익힐 관련 된 약관 및 하드웨어 요구 사항 후 ADFS 서버에 배포 하는 데 필요한 추천된 수를 확인 하는 데 도움이 되는 다음과 같은 추가 용량 콘텐츠 계획을 사용할 수 있습니다.  
  
-   [Federation 서버 용량에 대 한 계획](Planning-for-Federation-Server-Capacity.md)  
  
-   [Federation 서버 프록시 용량에 대 한 계획](Planning-for-Federation-Server-Proxy-Capacity.md)  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
