---
ms.assetid: 4ef052f0-61a9-4912-b780-5c96187c850f
title: AD FS 배포 토폴로지 고려 사항
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c5a3c85d40baee137ecdf7a1a5507b25361cac6d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191766"
---
# <a name="ad-fs-deployment-topology-considerations"></a>AD FS 배포 토폴로지 고려 사항

이 항목에서는 계획 하 고는 Active Directory Federation Services를 디자인 하는 데 중요 한 고려 사항 설명 \(AD FS\) 프로덕션 환경에서 사용 하는 배포 토폴로지입니다. 이 항목은 검토 하 고 어떤 기능 또는 기능 됩니다 할 수 있는 AD FS를 배포한 후에 영향을 주는 고려 사항을 평가 대 한 시작 지점입니다. 예를 들어 데이터베이스에 따라 AD FS 구성 데이터베이스를 저장 하도록 선택 하면 형식이 결정 됩니다 있는지 여부를 특정 Security Assertion Markup Language를 구현할 수 있습니다 \(SAML\) SQL을 필요로 하는 기능 서버입니다.  
  
## <a name="determining-which-type-of-adfs-configuration-database-to-use"></a>사용할 AD FS 구성 데이터베이스의 유형 결정  
AD FS는 데이터베이스를 사용 하 여 구성을 저장 하 고-경우도-페더레이션 서비스와 관련 된 트랜잭션 데이터입니다. AD FS 소프트웨어를 사용 하 여 선택 하거나 기본 제공\-Windows 내부 데이터베이스에 \(WID\) 또는 Microsoft SQL Server 2005 이상 페더레이션 서비스에 데이터를 저장 합니다.  
  
대부분의 용도에는 두 가지 데이터베이스 유형이 비교적 동일합니다. 그러나 AD FS와 함께 사용할 수 있는 다양 한 배포 토폴로지를 추가로 읽기를 시작 하기 전에 알아야 할 몇 가지 차이점이 있습니다. 다음 표에서는 WID 데이터베이스와 SQL Server 데이터베이스 간에 지원되는 기능의 차이점을 설명합니다.  
  
AD FS 기능  
  
|기능|WID에서 지원?|SQL Server에서 지원?|이 기능에 대한 자세한 정보|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|페더레이션 서버 팜 배포|예, 팜의 각 페더레이션 서버를 30 개로 제한|예 단일 팜에 배포할 수 있는 페더레이션 서버 수에 대한 제한 없음|[AD FS 배포 토폴로지 결정](Determine-Your-AD-FS-Deployment-Topology.md)|  
|SAML 아티팩트 확인 **참고 합니다.** 이 기능은 Microsoft Online Services, Microsoft Office 365, Microsoft Exchange 또는 Microsoft Office SharePoint 시나리오에는 필요하지 않습니다.|아니요|예|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[AD FS 보안 계획 및 배포 모범 사례](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
|SAML\/WS\-페더레이션 토큰 재생 검색|아니요|예|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[AD FS 보안 계획 및 배포 모범 사례](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
  
데이터베이스 기능  
  
|기능|WID에서 지원?|SQL Server에서 지원?|이 기능에 대한 자세한 정보|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|하나 또는 읽기 호스팅 서버를 더 끌어오기 복제를 사용 하 여 기본 데이터베이스 중복성\-읽기를 호스트 하는 원본 서버에 적용 된 데이터베이스 요청 변경의 전용 복사본\/데이터베이스의 복사본을 작성|예|아니요|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|고가용성을 사용 하 여 데이터베이스 중복성\-장애 조치 클러스터링 또는 미러링을 같은 가용성 솔루션 \(데이터베이스 계층 에서만\) **참고:** 모든 AD FS 배포 토폴로지는 AD FS 서비스 계층의 클러스터링을 지원 합니다.|아니요|예|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[고가용성 솔루션 개요](https://go.microsoft.com/fwlink/?LinkId=179853)|  
  
### <a name="sql-server-considerations"></a>SQL Server 고려 사항  
AD FS 배포를 위한 구성 데이터베이스로 SQL Server를 선택한 경우 다음 배포 정보를 고려해야 합니다.  
  
-   **SAML 기능과 해당 기능이 데이터베이스 크기 및 증가에 미치는 영향**. SAML 아티팩트 확인 또는 SAML 토큰 재생 검색 기능을 사용하는 경우 AD FS는 발급된 각 AD FS 토큰에 대한 정보를 SQL Server 구성 데이터베이스에 저장합니다. 이 활동의 결과로 인한 SQL Server 데이터베이스의 증가는 중요한 것으로 간주되지 않으며, 구성된 토큰 재생 보존 기간에 따라 다릅니다. 각 아티팩트 레코드 크기가 약 30 킬로바이트 \(KB\)합니다.  
  
-   **배포에 필요한 서버 수**. 하나 이상의 추가 서버를 추가 해야 합니다 \(AD FS 인프라를 배포 하는 데 필요한 서버의 총 수\) SQL Server 인스턴스의 전용된 호스트 역할을 할 합니다. 장애 조치(failover) 클러스터링 또는 미러링을 사용하여 SQL Server 구성 데이터베이스에 대한 내결함성 및 확장성을 제공하려면 두 대 이상의 SQL Server가 필요합니다.  
  
### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>선택한 구성 데이터베이스 유형이 하드웨어 리소스에 미치는 영향  
SQL Server 데이터베이스를 사용하는 팜에 배포된 페더레이션 서버와 달리, WID를 사용하는 팜에 배포된 페더레이션 서버의 하드웨어 리소스에 대한 영향은 중요하지 않습니다. 그러나 팜에 WID를 사용할 경우 해당 팜의 각 페더레이션 서버는 페더레이션 서비스에 필요한 정상 작업을 계속 제공하는 동시에 AD FS 구성 데이터베이스의 로컬 복사본에 대한 복제 변경 내용을 저장, 관리 및 유지해야 합니다.  
  
반면, SQL Server 데이터베이스를 사용하는 팜에 배포된 페더레이션 서버는 AD FS 구성 데이터베이스의 로컬 인스턴스를 포함할 필요가 없습니다. 따라서 하드웨어 리소스에 대한 수요가 조금 더 적습니다.  
  
## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>프로덕션 환경에 AD FS 배포를 지원할 수 있는지 확인 합니다.  
페더레이션 서버를 배포 하는 것 외에도 하 고 기존 프로덕션 환경이 설정 방법에 따라 다음과 같은 추가 서버가 새 AD FS 배포를 지원 하기 위해 필요한 인프라를 제공 해야 할 수 있습니다.  
  
-   Active Directory 도메인 컨트롤러  
  
-   인증 기관 \(CA\)  
  
-   페더레이션 메타데이터를 호스트할 웹 서버  
  
-   네트워크 로드 균형 조정 \(NLB\)  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
