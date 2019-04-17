---
ms.assetid: 7013fc21-9ced-4f9d-9588-cb04d6d60924
title: "Federation 서버 용량에 대 한 계획"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 618dc9419be965dedaaf7dc946da436a5001f121
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="planning-for-federation-server-capacity"></a>Federation 서버 용량에 대 한 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

용량 federation 서버에 대 한 계획을 평가할 수 있습니다.  
  
-   어떤은 ADFS 구성 데이터베이스의 크기를 성장 합니다.  
  
-   각 federation 서버에 대 한 적절 한 하드웨어 요구 합니다.  
  
-   각 조직에 배치 federation 서버의 수 있습니다.  
  
Federation 서버는 사용자에 게 보안 토큰 발행 합니다. 이 토큰 사용량에 대해 당사자에 표시 됩니다. Federation 서버 발급 한 후 사용자 인증 또는 보안 토큰 연합 서비스 파트너가 이전에 발행를 받은 후 보안 토큰 합니다. 사용자가 처음 연결 된 응용 프로그램에 로그인 하거나 해당 보안 토큰 연합된 응용 프로그램에 액세스 하는 동안 만료 되 면 보안 토큰 연합 서비스에서 요청 됩니다.  
  
Federation 서버는 high\ 가용성 Microsoft 네트워크 부하 분산 \(NLB\) 기술을 사용 하는 서버 농장 구성에 맞게 설계 되어 있습니다. 팜 구성에서 federation 서버 수 요청을 처리 하지 독립적으로 각 요청에 대 한 일반적인 팜 구성 요소에 액세스 하지 않고 합니다. 따라서 헤드가 작은 federation 서버 배포 확장에 참여 합니다.  
  
**추천을 제공 합니다.**  
  
-   에 대 한 중요 한 mission\ 하거나 증명을 생성 작은 federation 서버 팜 오류 확보 하기 위해 농장 별로 두 개 이상의 federation 서버와 함께 각 파트너 조직의 추천 high\ 가용성 배포 했습니다.  
  
-   높은 가용성 및 federation 서버 확장 접근성에 대 한 필요성을 확장 된 많아지면 초당 특정 Federation 서비스에 대 한 요청을 처리 하기 위한 권장 되는 방법입니다. 이 가이드 기본 구성 이상 내부 확장를 향상 처리 중요 한 용량을 생성할 가능성이있지 않습니다.  
  
## <a name="ad-fs-configuration-database-size-and-growth"></a>광고 FS 구성 데이터베이스 크기 및 증가  
ADFS 구성 데이터베이스의 크기는 일반적으로 작고 있는 것으로 간주 하 고 데이터베이스 크기 ADFS 배포 주요 고려 하지 경향이 합니다.  ADFS 구성 데이터베이스의 정확 하 게 크기의 수와 연결 된 trust\ 관련 메타 데이터 보안 관계 대체로에 따라 달라질 수-청구 등 규칙 주장 및 설정에 대해 각 신뢰 구성 모니터링 합니다. 구성 데이터베이스에 신뢰 항목 수가 증가 디스크 공간에 대 한 필요성을 마찬가지입니다.  
  
추가 배포 ADFS 구성 데이터베이스에 대 한 정보를 참조 하세요. [광고 FS 배포 토폴로지 고려](AD-FS-Deployment-Topology-Considerations.md)합니다.  
  
## <a name="memory-cpu-and-disk-space-requirements"></a>메모리, CPU 디스크 공간 요구 사항  
다행히도 federation 서버에 대 한 메모리, CPU 및 디스크 공간이 필요는 어느 정도의와 하드웨어 결정의 운전 원인이 되 발생 하지 않습니다. 하드웨어 요구 사항에 대 한 자세한 내용은 참조 [FS 요구 부록 a: 검토 AD](Appendix-A--Reviewing-AD-FS-Requirements.md)합니다.  
  
> [!NOTE]  
> ADFS 제품 팀 전용된 SQL Server로 구성 federation 서버 팜 ADFS 구성 데이터베이스를 저장 하기 위해 사용 하 여 수행 된 테스트에서 경향이 SQL Server 전반적인 로드 부족 한 것입니다. 단일 SQL Server를 사용 하도록 구성 된 팜 four\ federation\ 서버를 사용 하 여 테스트 하나 cpu 대상 사용량에 federation 서버 주는 테스트 불구 하 고 10%를 초과 하지 않습니다.  
  
## <a name="bk_estimatefs"></a>조직에 대 한 federation 서버 횟수 예측  
계획 프로세스 federation 서버에 대 한 하드웨어 간소화 하기 위해, ADFS 제품 팀 AD FS 용량 계획 크기 조정 스프레드시트 개발 되었습니다. 이 Excel 스프레드시트 하는 데 필요한 사용자에 대 한 조직에서 제공 하 고 ADFS 생산 환경에 대 한 federation 서버 권장된 최적의 번호를 반환 예상된 사용 현황 데이터 calculator\ 같은 기능이 포함 되어 있습니다.  
  
> [!NOTE]  
> 이 스프레드시트는 추천 federation 서버 수 ADFS 제품 팀을 테스트 하는 동안 사용 하는 하드웨어 및 네트워크 사양을 기반으로 합니다. 따라서 스프레드시트는 추천 federation 서버 수이 여기서 내 이해할 수 있어야 합니다.  항목을 테스트 하는 동안 사용 사양에 대 한 자세한 내용은 참조 [광고 FS 서버 용량에 대 한 계획](Planning-for-AD-FS-Server-Capacity.md)합니다.  
  
### <a name="using-the-ad-fs-capacity-planning-sizing-spreadsheet"></a>크기 조정 스프레드시트 계획 AD FS 용량을 사용 하 여  
이 스프레드시트를 사용 하면 값을 선택 해야 합니다 \ (중 **40%**, **60%**, 또는 **80%**\) 가장 원하는 총 사용자 백분율을 나타내는 인증 요청을 보냅니다 federation 서버의 사용량이 중입니다.  
  
그런 다음 값을 선택 해야 합니다 \ (중 **1 분**, **15 분**, 또는 **1 시간**\) 가장 마지막에 최대 사용 시간을 원하는 시간을 나타냅니다. 예를 들어 또는 1 시간 동안 내 60%의 사용자가 로그인 15 분 동안 내에서 로그인 하는 사용자의 총에 대 한 값으로 40% 예상할 수 있습니다. 이 값 크기 조정 권장을 계산 최고 부하 프로필을 정의 합니다.  
  
그런 다음 대상 claims\ 인식 응용 프로그램에 사용자가 있는지 여부에 따라 단일 sign\에 액세스 해야 하는 사용자의 총 지정 해야 합니다.  
  
-   실제로 회사 네트워크에 연결 되어 있는 로컬 컴퓨터에서 Active Directory에 로그인 \ (통해 Windows 통합된 authentication\)  
  
-   실제로 회사 네트워크에 연결 되어 있지 않은 한 컴퓨터에서 원격 Active Directory에 로그인 \ (창을 통해 통합 인증 또는 사용자명과 password\)  
  
-   다른 조직과 액세스 하려는 대상 claims\ 인식 응용 프로그램 신뢰할 수 있는 파트너 로부터  
  
-   SAML 2.0 id 공급자와은에서 액세스 하려는 대상 claims\ 인식 응용 프로그램  
  
#### <a name="how-to-use-this-spreadsheet"></a>이 스프레드시트 사용 하는 방법  
각 federation 서버 농장 인스턴스 federation 서버 추천된 수를 확인 하려면 배포할 계획에 대 한 다음 단계를 사용할 수 있습니다.  
  
1.  다운로드 한 다음 엽니다는 [Windows Server 2012 r 2 용 광고 FS 용량이 계획 크기 조정 스프레드시트](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacityPlanning.xlsx) 또는 [광고 FS 용량 계획 크기 조정 스프레드시트에 대 한 Windows Server 2016](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)합니다.
  
2.  오른쪽에 있는 셀에서는 **되나요 인증을 사용자에 게이 비율 최고 시스템 사용 기간 동안** 셀 셀 클릭 한 다음 drop\ 아래쪽 화살표를 사용 하 여 예상된 시스템 사용률이 수준을 선택할 **40%**, **60%** 또는 **80%** 배포 합니다.  
  
3.  오른쪽에 있는 셀에서는 **다음 기간 내에서** 셀 셀 클릭 한 다음 drop\ 아래쪽 화살표를 사용 하 여 중 하나를 선택 **1 분**, **15 분**, 또는 **1 시간** 최고 로드의 지속 시간을 선택 합니다.  
  
4.  오른쪽에 있는 셀에서는 **Enter 예상 수 내부 응용 프로그램의 \ (SharePoint 등 \(2007 or 2010\) 인식 웹 applications\ 주장 또는)** 셀 조직에서 사용 하는 내부 응용 프로그램의 번호를 입력 합니다.  
  
5.  오른쪽에 있는 셀에서는 **Enter 예상 수 온라인 응용 프로그램의 \ (Office 365 Exchange Online, SharePoint Online 또는 등 Lync Online\)** 셀 온라인 응용 프로그램 또는 조직에서 사용 되는 서비스는 사용자의 번호를 입력 합니다.  
  
6.  라는 제목의 셀 아래 **번호와 사용자의**, 입력에 사용자가 들어 응용 시나리오에 적용 되는 각 행 숫자가 sign\에 액세스 하 단일 필요 합니다. 이 열 하지 초당 최고 사용자 정의 된 사용자의 수가 있어야 합니다. 응용 프로그램에 대 한 액세스 시도 홈 영역 검색 페이지를 통해 길을 먼저 해야 하는 경우 입력 **Y**합니다. 이 옵션을이 선택 잘 모르는 경우 입력 **Y**합니다.  
  
7.  제공 되는 값 권장 하는 다음을 검토 합니다.  
  
    1.  권장된 federation 서버 총 오른쪽 셀 회색으로 표시 되는 아래를 참조 하세요.  
  
    2.  각 예 응용 프로그램 시나리오에 대 한 권장 서버 수가 셀 회색으로 표시 된 행에서 참조 합니다.  
  
> [!NOTE]  
> 라는 제목의 셀의 오른쪽에 있는 셀에서 자동으로 계산 값 **총 추천 federation 서버** 스프레드시트 맨 아래에서 각 개별 행 앞에 있는 모든 값 총에 추가 20% 버퍼가 추가 하는 수식을 포함 됩니다. 에 추가 수식에서 **총 추천 federation 서버** 셀 권장 하는 농장의 전반적인 로드 채도 지점 발생할 개가 될 가능성이 배포 federation 서버 수 금액이이 버퍼가이 빌드입니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
