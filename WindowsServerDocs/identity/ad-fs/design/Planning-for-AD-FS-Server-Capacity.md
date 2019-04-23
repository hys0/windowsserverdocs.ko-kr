---
ms.assetid: ef91f1d8-2991-4d90-b687-5fa189737c88
title: AD FS 서버 용량 계획
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 484dd08edef85b91e777f8963f175a6172c75430
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847394"
---
# <a name="planning-for-ad-fs-server-capacity"></a>AD FS 서버 용량 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

  
> [!NOTE]  
> 이 항목의 내용에는 Windows Server 2012를 실행 하는 서버에서 수행 된 실제 테스트는 반영 하지 않습니다. 이 항목은 필요한 테스트가 수행된 후 업데이트됩니다.  
  
Active Directory Federation Services를 위한 용량 계획 \(AD FS\) 페더레이션 서비스의 피크 사용 기간을 예측 및 계획 또는 크기 조정 프로세스\-사항에 AD FS 서버 배포 구성 로드 요구 사항입니다.  
  
이 섹션에서는 페더레이션 서버 및 페더레이션 서버 프록시 역할에 대 한 배포 지침을 설명 하 고 Microsoft의 AD FS 제품 팀에서 수행한 랩 테스트 기반으로 합니다. 이 내용의 목적은 다음을 지원하는 것입니다.  
  
-   조직의 특정 AD FS 배포에 대 한 AD FS 서버 수와 같은 하드웨어 사용 요구를 예상 밀접 하 게 합니다.  
  
-   로그인에 대 한 예상 된 피크 사용을 정확 하 게 프로젝트\-요청에서는 증가 계획 하 고 AD FS 배포는 예상 된 피크 사용을 처리할 수 있는지 확인 합니다.  
  
이 용량 계획 내용을 계속 읽기 전에 먼저 다음 두 표에 나와 있는 작업을 완료하는 것이 좋습니다. 첫 번째 표에는 이 용량 계획에 대한 관련 컨텍스트를 제공하는 데 도움이 되는 권장 작업의 링크가 나와 있습니다.  
  
|권장 작업|설명|참조|  
|--------------------|---------------|-------------|  
|AD FS 페더레이션 서버 및 페더레이션 서버 프록시를 배포 하기 위한 요구 사항 이해|페더레이션 서버 및 페더레이션 서버 프록시를 배포하는 데 필요한 중요한 하드웨어 및 소프트웨어 요구 사항을 검토합니다.|[부록 a: AD FS 요구 사항 검토](Appendix-A--Reviewing-AD-FS-Requirements.md)|  
|조직에서 배포할 AD FS 구성 데이터베이스의 유형 선택|이 섹션의 용량 계획 데이터를 사용 하 여를 시작 하기 전에 먼저 결정 해야 AD FS 구성 데이터베이스 유형, 배포 하거나 Windows 내부 데이터베이스 \(WID\) 또는 구조적 쿼리 언어 \(SQL\) 데이터베이스입니다.|[The Role of the AD FS Configuration Database](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[AD FS 배포 토폴로지 고려 사항](AD-FS-Deployment-Topology-Considerations.md)|  
|선택한 새 AD FS 구성 데이터베이스에서 사용할 토폴로지 레이아웃의 유형 결정|배포에 사용할 AD FS 구성 데이터베이스의 유형을 결정했으면 프로덕션 환경에서 페더레이션 서버 및 페더레이션 서버 프록시를 배치해야 하는 위치와 가장 일치하는 배포 토폴로지를 고려해야 합니다.|[AD FS 배포 토폴로지 결정](Determine-Your-AD-FS-Deployment-Topology.md)|  
|키 AD FS 관련 용량 계획 용어 이해|일반적인 용량 계획 AD FS 용량 계획 설명 전체에서 사용 되는 용어의 정의 검토 합니다.|이 항목의 [AD FS capacity planning terms](Planning-for-AD-FS-Server-Capacity.md#bk_terms) 섹션을 참조하세요.|  
  
위 표의 내용을 검토했으면 이제 다음 표의 사전 필수 작업을 완료할 수 있습니다.  
  
|사전 필수 작업|설명|참조|  
|---------------------|---------------|-------------|  
|AD FS 용량 계획 규모 산정 스프레드시트 다운로드|AD FS 용량 계획 규모 산정 스프레드시트를 AD FS 페더레이션 서버 팜 배포에 필요한 페더레이션 서버 수를 확인 하려면 도움이 됩니다. 이 스프레드시트를 사용하는 방법에 대한 지침은 아래에 제공된 다음 작업의 링크에서 확인할 수 있습니다.|[AD FS 용량 계획 스프레드시트](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacityPlanning.xlsx)|  
|단일 로그인 해야 하는 사용자 수에 대 한 데이터 수집\-대 \(SSO\) 대상 클레임에 대 한 액세스\-인식 응용 프로그램 및이 액세스와 관련 된 예상된 피크 사용 기간|수집한 이 사용자 데이터는 AD FS 용량 계획 규모 산정 스프레드시트의 컨텍스트 내에 필요한 입력 값에 사용됩니다.|[조직에 대 한 페더레이션 서버 수 추정](Planning-for-Federation-Server-Capacity.md#bk_estimatefs)|  
|Windows Server 2016 용 AD FS 용량 계획 스프레드시트|Windows Server 2016에 대 한 업데이트 된 계획 워크시트|[AD FS Windows Server 2016 용량 계획](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)  
  
## <a name="bk_terms"></a>AD FS 용량 계획 용어  
다음 표에서이 용량 계획 AD FS 디자인 가이드의 섹션에서에서 자주 사용 되는 중요 한 용어를 설명 합니다. 자세한 목록은 AD FS 용어를 참조 하세요 [Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)합니다.  
  
|용어|정의|  
|--------|--------------|  
|동시 사용자|지정된 기간(일반적으로 피크 활동 기간) 동안 서비스 요청을 제출할 것으로 예상되는 사용자 수|  
|활성 사용자|지정된 기간 동안 시스템에서 활성 상태(요청을 제출할 필요는 없음)로 있는 대략적인 평균 사용자 수|  
|정의된 사용자|일반적으로 시스템에 정의된 계정이 있는 사용자 수를 기반으로 하는 이론적 최대 사용자 수|  
|초당 요청 수|클라이언트에서 제출 하거나 요청 수가 \(시스템에서 부하를 이야기 하는 경우\) 서버에서 처리 또는 \(서버 처리량을 이야기할 때\) 초당에서 합니다. 이 메트릭은 서버 프로세서 및 메모리 용량 계획에 사용됩니다.|  
|목표 서버 응답성 및 사용률|허용되는 서버 성능 범위를 지정하는 성공 메트릭. 일반적으로 응답성이 목표를 미달하거나 사용률이 목표를 초과하는 경우 시스템이 오버로드되어 추가 용량이 필요한 것으로 간주됩니다.|  
|Windows 내부 데이터베이스 \(WID\)|기본 AD FS 구성 데이터베이스, 특정 AD FS 배포에서 SQL Server 대 안으로 사용할 수 있는입니다.|  
  
## <a name="configuration-environment-used-during-ad-fs-testing"></a>AD FS 테스트 중에 사용된 구성 환경  
이 섹션에서는 AD FS 제품 팀이 테스트를 수행 하는 구성 환경을 설명 합니다. 제품 팀은 페더레이션 서버 테스트에서 다음 컴퓨터 하드웨어, 소프트웨어 및 네트워크 구성을 사용하여 성능 및 확장성 데이터를 수집했습니다.  
  
-   듀얼 쿼드 코어 2.27 기가헤르쯔 \(GHz\) \(코어 8 개\)  
  
-   16\-GB RAM  
  
-   Windows Server 2008 R2, Enterprise Edition  
  
-   기가비트 네트워크  
  
> [!NOTE]  
> 테스트 하는 동안 16GB의 RAM이 페더레이션 서버에서 사용 되었지만는 보다 적정 한 메모리 크기, 4GB의 RAM 페더레이션 서버당 같은 대부분의 AD FS 배포에 사용할 수 있습니다. 대부분의 AD FS 프로덕션에 대 한 ram이 AD FS 용량 계획 AD FS 용량 계획 스프레드시트에서 제공 하는 결과 함께 콘텐츠 가정을 기반으로 각 페더레이션 서버에서 약 사용할에서 제공 되는 권장 사항을 4GB의 환경입니다.  
  
제품 팀은 페더레이션 서버 프록시 테스트에서 다음 구성을 사용하여 성능 및 확장성 데이터를 수집했습니다.  
  
-   듀얼 쿼드 코어 2.24 GHz \(4 개 코어\)  
  
-   4\-GB RAM  
  
-   Windows Server 2008 R2, Enterprise Edition  
  
-   기가비트 네트워크  
  
> [!NOTE]  
> AD FS 서버에 대 한 용량 권장 사항은 지정된 된 환경에서 사용할 하드웨어 및 네트워크 구성에 대 한 선택 사양에 따라 상당히 달라질 수 있습니다. 이 항목에 제공된 규모 산정 지침은 위에 언급된 컴퓨터에서 80%의 사용률 목표를 기반으로 합니다.  
  
## <a name="measure-ad-fs-server-capacity"></a>AD FS 서버 용량 측정  
일반적으로 서버 성능 및 확장성에 영향을 주는 하드웨어 구성 요소는 CPU, 메모리, 디스크 및 네트워크 어댑터입니다. 다행 스럽게도 각 AD FS 구성 요소는 메모리 및 디스크 공간은 매우 적습니다가 필요합니다. 네트워크 연결은 명확한 요구 사항입니다. 따라서 페더레이션 서버와 페더레이션 서버 프록시에서 수행된 부하 테스트는 서버 용량 측정의 두 가지 주요 영역에 중점을 둡니다.  
  
-   **초당 피크 AD FS 요청:** 로그인 수\-페더레이션 서버에서 초당 처리 되는 요청입니다. 이 측정을 통해 지정된 서버에 동시에 로그인할 수 있는 사용자 수를 파악할 수 있습니다. 이 측정을 CPU 사용 측정과 함께 사용하면 이 측정이 성능에 미치는 영향을 이해할 수 있습니다.  
  
-   **CPU 사용량:** CPU 용량을 측정된 백분율입니다. 이 측정을 통해 들어오는 로그인의 수를 기준으로 발생 하는 전체 CPU 부하를 확인할 수 있습니다\-초당 요청에서 합니다.  
  
## <a name="continue-reading-more-about-ad-fs-capacity-planning"></a>AD FS 용량 계획에 대한 추가 정보 확인  
필수 구성 요소 작업을 완료 하 고 관련된 용어 및 하드웨어 요구 사항에 익숙해 후 사용할 수는 다음 추가 용량 계획 내용을 AD FS 서버에 필요한 권장 되는 수를 결정 하는 데 사용자 배포:  
  
-   [페더레이션 서버 용량 계획](Planning-for-Federation-Server-Capacity.md)  
  
-   [페더레이션 서버 프록시 용량 계획](Planning-for-Federation-Server-Proxy-Capacity.md)  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의에서 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
