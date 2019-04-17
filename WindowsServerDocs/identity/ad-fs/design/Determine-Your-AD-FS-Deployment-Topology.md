---
ms.assetid: f67b0bc9-e5af-4891-9da0-d9be539af42d
title: "해당 AD FS 배포가 확인"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3300c16be6d516d7ec0bf4d0c3a025e59e6126b6
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="determine-your-ad-fs-deployment-topology"></a>해당 AD FS 배포가 확인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services \(AD FS\) 배포를 계획 하는 첫 번째 단계는 단일 sign\ 켜 짐 \(SSO\)에 맞게 오른쪽 배포가 확인 하는 조직의 필요 합니다. 이 섹션의 항목 Adfs에 사용할 수 있는 다양 한 배포 토폴로지에 설명 합니다. 또한 특정 비즈니스 요구에 가장 적합 한 토폴로지 선택할 수 있도록 각각 배포가와 관련 된 장단점 설명 합니다.  
  
이 배포 토폴로지 항목을 읽으려면 하기 전에 먼저 다음 표와 순서의 작업을 완료 하는 것이 좋습니다.  
  
|권장된 작업|설명|참조|  
|--------------------|---------------|-------------|  
|ADFS 데이터 저장 되 고 federation 서버 그룹의 다른 federation 서버에 복제 어떻게 검토 합니다.|목적 및 기본 ADFS 구성 데이터베이스에 저장 된 데이터에 사용할 수 있는 복제 방법을 파악 합니다. 이 항목 구성 데이터베이스의 개념을 소개 하 고 데이터베이스 두 종류에 설명 합니다: Windows 내부 데이터베이스 \(WID\) 및 Microsoft SQL Server 합니다.|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|조직에 배포할 ADFS 구성 데이터베이스 유형을 선택 합니다.|다양 한 혜택 및 WID 또는 SQL Server ADFS 구성 데이터베이스를 지 원하는 다양 한 응용 프로그램 시나리오 함께으로 사용과 관련 된 제한 검토 합니다.|[광고 FS 배포 토폴로지 고려 사항](AD-FS-Deployment-Topology-Considerations.md)|  
  
> [!NOTE]  
> 기본 중복, 부하 분산 Federation 서비스 \(if required\) 크기를 조정 하는 옵션을 구현을 두 개 이상의 federation 서버 federation 서버 팜 데이터베이스에 사용할 형식에 관계 없이 모든 생산 환경에 대 한 배포 하는 것이 좋습니다.  
  
위의 표에 콘텐츠를 검토이 섹션의 다음 항목으로 이동 합니다.  
  
-   [WID 사용 하 여 독립 실행형 Federation 서버](Stand-Alone-Federation-Server-Using-WID.md)  
  
-   [사용 하 여 WID federation 서버 농장](Federation-Server-Farm-Using-WID-2012.md)  
  
-   [Federation 서버 팜 WID 및 프록시 사용 하 여](Federation-Server-Farm-Using-WID-and-Proxies-2012.md)  
  
-   [Federation 서버 팜 SQL Server를 사용 하 여](Federation-Server-Farm-Using-SQL-Server-2012.md)  
  
선택 하 여 ADFS 배포가 마친 후 항목을 검토 하는 것이 좋습니다 [광고 FS 서버 용량에 대 한 계획](Planning-for-AD-FS-Server-Capacity.md) 이 토폴로지 지원 하기 위해 배포 해야 하는 서버 권장된 번호를 확인 합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)

