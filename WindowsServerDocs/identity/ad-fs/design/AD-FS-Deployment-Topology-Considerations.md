---
ms.assetid: 4ef052f0-61a9-4912-b780-5c96187c850f
title: AD FS 배포 토폴로지 고려 사항
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 260d86c0feae0179620ece09e06f12729691b5a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359216"
---
# <a name="ad-fs-deployment-topology-considerations"></a>AD FS 배포 토폴로지 고려 사항

이 항목에서는 프로덕션 환경에서 사용할 배포 토폴로지\) AD FS \(Active Directory Federation Services을 계획 하 고 설계 하는 데 도움이 되는 중요 한 고려 사항을 설명 합니다. 이 항목은 AD FS를 배포한 후에 사용할 수 있는 기능에 영향을 주는 고려 사항을 검토 하 고 평가 하는 시작점입니다. 예를 들어 AD FS 구성 데이터베이스를 저장 하기 위해 선택한 데이터베이스 유형에 따라 궁극적으로 SQL Server 필요한 SAML\) 기능을 \(특정 Security Assertion Markup Language를 구현할 수 있는지 여부가 결정 됩니다.  

## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>사용할 AD FS 구성 데이터베이스의 유형 결정  
AD FS는 데이터베이스를 사용 하 여 구성을 저장 하며, 경우에 따라 페더레이션 서비스와 관련 된 트랜잭션 데이터를 저장 합니다. AD FS 소프트웨어를 사용 하 여 Windows 내부 데이터베이스 \(WID\) 또는 Microsoft SQL Server 2005 이상에서 빌드된\-를 선택 하 여 페더레이션 서비스에 데이터를 저장할 수 있습니다.  

대부분의 용도에는 두 가지 데이터베이스 유형이 비교적 동일합니다. 그러나 AD FS에서 사용할 수 있는 다양 한 배포 토폴로지에 대 한 읽기를 시작 하기 전에 알아두어야 할 몇 가지 차이점이 있습니다. 다음 표에서는 WID 데이터베이스와 SQL Server 데이터베이스 간에 지원 되는 기능의 차이점을 설명 합니다.  

AD FS 기능  

|기능|WID에서 지원?|SQL Server에서 지원?|이 기능에 대한 자세한 정보|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|페더레이션 서버 팜 배포|예. 각 팜에 대 한 페더레이션 서버를 30 개로 제한 합니다.|예. 단일 팜에 배포할 수 있는 페더레이션 서버 수에 대한 제한 없음|[AD FS 배포 토폴로지 결정](Determine-Your-AD-FS-Deployment-Topology.md)|  
|SAML 아티팩트 확인 **참고:** Microsoft Online Services, Microsoft Office 365, microsoft Exchange 또는 Microsoft Office SharePoint 시나리오에는이 기능이 필요 하지 않습니다.|아니요|예|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[AD FS 보안 계획 및 배포 모범 사례](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
|SAML\/WS\-페더레이션 토큰 재생 검색|아니요|예|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[AD FS 보안 계획 및 배포 모범 사례](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  

데이터베이스 기능  

|기능|WID에서 지원?|SQL Server에서 지원?|이 기능에 대한 자세한 정보|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|끌어오기 복제를 사용 하는 기본 데이터베이스 중복성-읽기\-를 호스트 하는 하나 이상의 서버가 데이터베이스의 복사본\/읽기를 호스트 하는 원본 서버에서 수행 된 변경 내용을 요청 합니다.|예|아니요|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|데이터베이스 계층 에서만 장애 조치 (failover) 클러스터링 또는 미러링 \(와 같은 높은\-가용성 솔루션을 사용 하는 데이터베이스 중복성\) **참고:** 모든 AD FS 배포 토폴로지는 AD FS 서비스 계층에서 클러스터링을 지원 합니다.|아니요|예|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[고가용성 솔루션 개요](https://go.microsoft.com/fwlink/?LinkId=179853)|  

### <a name="sql-server-considerations"></a>SQL Server 고려 사항  
AD FS 배포에 대 한 구성 데이터베이스로 SQL Server를 선택 하는 경우 다음과 같은 배포 팩트를 고려해 야 합니다.  

-   **SAML 기능과 해당 기능이 데이터베이스 크기 및 증가에 미치는 영향**. SAML 아티팩트 확인 또는 SAML 토큰 재생 검색 기능을 사용 하도록 설정 하면 AD FS는 발급 된 각 AD FS 토큰에 대 한 정보를 SQL Server 구성 데이터베이스에 저장 합니다. 이 작업의 결과로 SQL Server 데이터베이스의 증가는 중요 한 것으로 간주 되지 않으며, 구성 된 토큰 재생 보존 기간에 따라 달라 집니다. 각 아티팩트 레코드의 크기는 약 30kb \(KB\)입니다.  

-   **배포에 필요한 서버 수**. SQL Server 인스턴스의 전용 호스트 역할을 하는 AD FS 인프라\)를 배포 하는 데 필요한 총 서버 수에 추가 서버 \(를 하나 이상 추가 해야 합니다. 장애 조치 (failover) 클러스터링 또는 미러링을 사용 하 여 SQL Server 구성 데이터베이스에 대 한 내결함성 및 확장성을 제공 하려는 경우 최소한 두 개의 SQL server가 필요 합니다.  

### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>선택한 구성 데이터베이스 유형이 하드웨어 리소스에 미치는 영향  
SQL Server 데이터베이스를 사용 하는 팜에 배포 된 페더레이션 서버와 달리, WID를 사용 하는 팜에 배포 된 페더레이션 서버의 하드웨어 리소스에 미치는 영향은 중요 하지 않습니다. 그러나 팜에 대해 WID를 사용 하는 경우 해당 팜의 각 페더레이션 서버는 AD FS 구성 데이터베이스의 로컬 복사본에 대 한 복제 변경 내용을 저장, 관리 및 유지 관리 하 고 계속 해 서 정상 제공 페더레이션 서비스에 필요한 작업입니다.  

반면 SQL Server 데이터베이스를 사용 하는 팜에 배포 된 페더레이션 서버는 AD FS 구성 데이터베이스의 로컬 인스턴스를 포함할 필요가 없습니다. 따라서 하드웨어 리소스에 대한 수요가 조금 더 적습니다.  

## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>프로덕션 환경에서 AD FS 배포를 지원할 수 있는지 확인 하는 중  
배포할 페더레이션 서버 외에 기존 프로덕션 환경이 설정 된 방식에 따라 다음과 같은 추가 서버가 새 AD FS 배포를 지 원하는 데 필요한 인프라를 제공 해야 할 수 있습니다.  

-   Active Directory 도메인 컨트롤러  

-   인증 기관 \(CA\)  

-   페더레이션 메타데이터를 호스트할 웹 서버  

-   NLB\) \(네트워크 부하 분산  

## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
