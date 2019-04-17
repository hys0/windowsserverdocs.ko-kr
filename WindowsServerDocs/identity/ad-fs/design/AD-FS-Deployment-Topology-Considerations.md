---
ms.assetid: 4ef052f0-61a9-4912-b780-5c96187c850f
title: "광고 FS 배포 토폴로지 고려 사항"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: eee14ee7bb50e1a82f35caf9fbacda0b86d3a1ad
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-fs-deployment-topology-considerations"></a>광고 FS 배포 토폴로지 고려 사항

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 계획 및 생산 환경에서 사용 하는 Active Directory Federation Services \(AD FS\) 배포가 디자인를 위해 중요 한 사항을 설명 합니다. 이 항목은 시작 지점 검토 하 고 평가 어떤 기능 또는 기능 제공 됩니다을 ADFS 배포한 후에 영향을 고려 합니다. 예를 들어,는 데이터베이스에 따라 유형이 ADFS 구성 데이터베이스를 저장 하도록 선택 하면 됩니다 결국 결정 SQL Server 해야 하는 특정 보안 설정 Markup Language \(SAML\) 기능 여부를 구현할 수 있습니다.  
  
## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>사용 하 여 ADFS 구성 데이터베이스 유형을 확인  
ADFS 데이터베이스를 사용 하 여 구성 저장 하 고-경우에 따라-트랜잭션 데이터 Federation 서비스와 관련 된 합니다. built\ Windows 내부 데이터베이스 \(WID\) 또는 Microsoft SQL Server 2005 또는 최신 Federation 서비스의 데이터를 저장 하도록 선택 하는 ADFS 소프트웨어를 사용할 수 있습니다.  
  
대부분의 경우 두 가지 데이터베이스 유형 상대적으로 동일합니다. 그러나 Adfs에 사용할 수 있는 다양 한 배포 토폴로지에 대해 자세히 읽기 시작 하기 전에 주의 해야 할 몇 가지 차이점이 있습니다. 다음 표에서 WID 데이터베이스와 SQL Server 데이터베이스 간의 차이점 지원 되는 기능에 설명합니다.  
  
광고 FS 기능  
  
|기능|WID 지원 하나요?|SQL Server 지원 하나요?|이 기능에 대 한 자세한 정보|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|Federation 서버 농장 배포|예, 각 농장에 대해 5 federation 서버 제한|예입니다. 단일 팜에 배포할 수 있는 federation 서버 수에 제한이 없습니다 적용 되어|[해당 AD FS 배포가 확인](Determine-Your-AD-FS-Deployment-Topology.md)|  
|SAML 아티팩트 해상도 **참고:** 이 기능은 Microsoft Online Services, Microsoft Office 365, Microsoft Exchange 또는 SharePoint 시나리오 Microsoft Office에 대 한 필요 하지 않습니다.|아니요|예|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[보안 및 배포 Adfs의에 대 한 유용한](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
|토큰 연합-WS\ SAML\/재생 검색|아니요|예|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[보안 및 배포 Adfs의에 대 한 유용한](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
  
데이터베이스 기능  
  
|기능|WID 지원 하나요?|SQL Server 지원 하나요?|이 기능에 대 한 자세한 정보|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|사용 하 여 위치를 read\ 전용 원본 서버에 대 한 데이터베이스 요청 변경 호스트 하는 하나 이상의 서버 호스트 하는 데이터베이스의 read\/쓰기 복사본 방향으로 빼냅니다 복제 기본 데이터베이스 중복|예|아니요|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|데이터베이스 중복 장애 클러스터링 또는 미러링 같은 high\ 가용성 솔루션을 사용 하 여 \ (데이터베이스 계층 only\)에서 **참고:** 모든 ADFS 배포 토폴로지 ADFS 서비스 계층 클러스터링을 지원 합니다.|아니요|예|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[높은 가용성 솔루션 개요](https://go.microsoft.com/fwlink/?LinkId=179853)|  
  
### <a name="sql-server-considerations"></a>SQL Server 고려 사항  
ADFS 배포를 위해 구성 데이터베이스와 SQL Server를 선택 하는 경우 다음 배포 사실 고려해 야 합니다.  
  
-   **SAML 기능과 데이터베이스 크기와 성장에 미치는 영향**합니다. SAML 아티팩트 해상도 또는 SAML 토큰 재생 감지 기능이 활성화 되어 있으면 ADFS 정보 발생 하는 각 ADFS 토큰 SQL Server 구성 데이터베이스에 저장 합니다. 이 활동으로 인해 SQL Server 데이터베이스의 증가, 중요 한 것으로 간주 되지 않습니다 및 토큰 구성 된 재생 보존 기간에 따라 달라 집니다. 각 아티팩트 레코드 약 30 킬로바이트 \(KB\)의 크기를 있습니다.  
  
-   **서버에 배포 하는 데 필요한 수가**합니다. 하나 이상의 추가 서버에 추가 해야 합니다 \ 서버 ADFS infrastructure\ 배포 하는 데 필요한의 총) (를 있는 SQL Server 인스턴스 전용된 호스트 처럼 작동 합니다. 무결성 및 확장성 SQL Server 구성 데이터베이스를 제공 하기 위해 장애 클러스터링 사용 하거나 사용 하려는 경우 두 가지 SQL server 최소 공간이 필요 합니다.  
  
### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>선택한 구성 데이터베이스 형식 있습니다 어떤 영향을 주나요 하드웨어 리소스  
중요 한 하드웨어 리소스 WID federation 서버 SQL Server 데이터베이스를 사용 하 여 팜에 배포 되는 것이 아니라 사용 하 여 팜에 배포 되는 federation 서버에 영향을 않습니다. 그러나이 그룹에 대 한 WID를 사용 하는 경우 해당 농장의 각 federation 서버 해야 저장, 관리 및도 계속 Federation 서비스에 필요한 기본 작업을 제공 하는 동안 복제 변경 ADFS 구성 데이터베이스의 로컬 복사본을 유지 고려해 야 할 중요 합니다.  
  
비교, SQL Server 데이터베이스를 사용 하는 농장에 배포 되는 federation 서버가 ADFS 구성 데이터베이스의 로컬 인스턴스를 반드시 포함 되지 않습니다. 따라서 하드웨어 리소스에 약간 더 적은 수의 요구를 만들 수 있습니다.  
  
## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>프로덕션 환경 ADFS 배포 지원할 수 있는지 확인  
을 배포할 federation 서버와 함께 하 고 기존 생산 환경 설정한 방식에 따라 다음과 같은 추가 서버 새 ADFS 배포를 지원 하기 위해 필요한 인프라를 제공 하기 위해 해야 수 있습니다.  
  
-   Active Directory 도메인 컨트롤러  
  
-   인증 기관 \(CA\)  
  
-   웹 서버를 호스트 federation 메타 데이터  
  
-   네트워크 부하 분산 \(NLB\)  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
