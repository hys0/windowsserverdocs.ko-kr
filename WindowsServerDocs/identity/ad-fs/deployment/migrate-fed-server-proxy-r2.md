---
title: AD FS 2.0 페더레이션 프록시 서버를 마이그레이션하십시오.
description: AD FS 프록시 서버를 Windows Server 2012 R2로 마이그레이션하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a2eb6c670e704564bed49486b8950dab96da8a80
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444574"
---
# <a name="migrate-the-active-directory-federation-services-proxy-server-to-windows-server-2012-r2"></a>Active Directory 페더레이션 서비스 프록시 서버를 Windows Server 2012 R2로 마이그레이션

Active Directory Federation Services (AD FS) Windows Server 2012 r2에서에서 페더레이션 서버 프록시의 역할은 웹 응용 프로그램 프록시 라는 새 원격 액세스 역할 서비스에서 처리 됩니다. 회사 네트워크 외부에서 내게 필요한 옵션에 대 한 AD FS를 사용 하도록 설정 하려면 Windows Server 2012 R2에서 하나 이상의 웹 응용 프로그램 프록시 배포할 수 있습니다. 그러나 Windows Server 2012 R2에서 실행 중인 웹 응용 프로그램 프록시를 Windows Server 2008 R2 또는 Windows Server 2012에서 실행 되는 페더레이션 서버 프록시를 마이그레이션할 수 없습니다.  
  
> [!IMPORTANT]
>  Windows Server 2012 R2에서 실행 되는 웹 응용 프로그램 프록시를 Windows Server 2008, Windows Server 2008 R2 또는 Windows Server 2012에서 실행 되는 페더레이션 서버 프록시 마이그레이션 지원 되지 않습니다.  
  
엑스트라넷 액세스에 대 한 Windows Server 2012 R2 마이그레이션된 팜의 AD FS를 구성 하려는 경우에 하나 이상의 웹 응용 프로그램 프록시 컴퓨터의 AD FS 인프라의 일부로 새로 배포를 수행 해야 합니다.  
  
웹 응용 프로그램 프록시 배포를 계획하려면 다음 항목의 정보를 검토하면 됩니다.  
  
- [웹 응용 프로그램 프록시 인프라 계획](https://technet.microsoft.com/library/dn383648.aspx)  
  
- [웹 응용 프로그램 프록시 서버 계획](https://technet.microsoft.com/library/dn383647.aspx)  
  
  웹 응용 프로그램 프록시를 배포하려면 다음 항목의 절차를 따르면 됩니다.  
  
- [웹 응용 프로그램 프록시 인프라 구성](https://technet.microsoft.com/library/dn383644.aspx)  
  
- [웹 응용 프로그램 프록시 서버 설치 및 구성](https://technet.microsoft.com/library/dn383662.aspx)  
  
## <a name="next-steps"></a>다음 단계
 [Windows Server 2012 R2로 Active Directory Federation Services 역할 서비스 마이그레이션](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS 페더레이션 서버 마이그레이션 준비](prepare-migrate-ad-fs-server-r2.md)   
 [AD FS 페더레이션 서버 마이그레이션](migrate-ad-fs-fed-server-r2.md)    
 [Windows Server 2012 R2로 AD FS 마이그레이션 확인](verify-ad-fs-migration.md)

