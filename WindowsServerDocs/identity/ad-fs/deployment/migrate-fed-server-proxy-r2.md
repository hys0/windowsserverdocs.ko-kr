---
title: "마이그레이션 ADFS 2.0 federation 프록시 서버"
description: "Windows Server 2012 r 2에는 ADFS 프록시 서버에 정보를 제공 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 33ab29fd5efdb0bdd1fe25580e3f4434071e1c7d
ms.sourcegitcommit: 03ce78a1624dbd7f4e6abf2ec1ef185b55de29a1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2017
---
# <a name="migrate-the-active-directory-federation-services-proxy-server-to-windows-server-2012-r2"></a>Windows Server 2012 r 2 마이그레이션을 Active Directory Federation Services 프록시 서버

Active Directory Federation Services (ADFS) Windows Server 2012 r 2에서를 federation 서버 프록시 역할 웹 응용 프로그램 프록시 라는 새로운 원격 액세스 역할 서비스에 의해 처리 됩니다. 회사 네트워크 외부에서 접근성에 대 한 사용자 ADFS 수 있도록 Windows Server 2012 r 2의 하나 이상 웹 응용 프로그램 프록시 배포할 수 있습니다. 그러나 웹 응용 프로그램 프록시 Windows Server 2012 r 2에서 실행 중인 Windows Server 2008 R2 또는 Windows Server 2012에서 실행 되는 federation 서버 프록시를 마이그레이션할 수 없습니다.  
  
> [!IMPORTANT]
>  웹 응용 프로그램 프록시 Windows Server 2012 r 2에서 실행 중인 Windows Server 2008, Windows Server 2008 R2 또는 Windows Server 2012에서 실행 되는 federation 서버 프록시 마이그레이션을 지원 되지 않습니다.  
  
ADFS 익스트라넷 액세스를 위해 Windows Server 2012 r 2 마이그레이션된 농장 구성할 하려는 경우 ADFS 인프라의 일환으로 하나 이상의 웹 응용 프로그램 프록시 컴퓨터의 새 배포를 수행 해야 합니다.  
  
웹 응용 프로그램 프록시 배포를 계획 하는 정보는 다음과 같은 항목에 검토할 수 있습니다.  
  
-   [웹 응용 프로그램 프록시 인프라 계획](https://technet.microsoft.com/en-us/library/dn383648.aspx)  
  
-   [웹 응용 프로그램 프록시 서버 계획](https://technet.microsoft.com/en-us/library/dn383647.aspx)  
  
 프록시 웹 응용 프로그램을 배포 하는 절차 다음 항목에 따라 수 있습니다.  
  
-   [웹 응용 프로그램 프록시 인프라 구성](https://technet.microsoft.com/en-us/library/dn383644.aspx)  
  
-   [설치 및 구성 웹 응용 프로그램 프록시 서버](https://technet.microsoft.com/en-us/library/dn383662.aspx)  
  
## <a name="next-steps"></a>다음 단계
 [Windows Server 2012 r 2 Active Directory Federation Services 역할 서비스 마이그레이션을](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [광고 FS Federation 서버 마이그레이션 준비](prepare-migrate-ad-fs-server-r2.md)   
 [마이그레이션 광고 FS Federation 서버](migrate-ad-fs-fed-server-r2.md)    
 [Windows Server 2012 r 2에 AD FS 마이그레이션 확인](verify-ad-fs-migration.md)

