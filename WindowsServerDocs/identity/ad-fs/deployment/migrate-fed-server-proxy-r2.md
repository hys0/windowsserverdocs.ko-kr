---
title: AD FS 2.0 페더레이션 프록시 서버 마이그레이션
description: AD FS 프록시 서버를 Windows Server 2012 r 2로 마이그레이션하는 방법에 대 한 정보를 제공 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 57367cadd3c7ce3d031c6eb3a53c333422543dae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359374"
---
# <a name="migrate-the-active-directory-federation-services-proxy-server-to-windows-server-2012-r2"></a>Active Directory Federation Services 프록시 서버를 Windows Server 2012 r 2로 마이그레이션

Windows Server 2012 r 2의 Active Directory Federation Services (AD FS)에서 페더레이션 서버 프록시의 역할은 웹 응용 프로그램 프록시 라는 새 원격 액세스 역할 서비스에 의해 처리 됩니다. Windows Server 2012 r 2에서 회사 네트워크 외부의 접근성에 대 한 AD FS를 사용 하도록 설정 하기 위해 웹 응용 프로그램 프록시를 하나 이상 배포할 수 있습니다. 그러나 windows server 2008 R2 또는 Windows Server 2012에서 실행 되는 페더레이션 서버 프록시를 Windows Server 2012 r 2에서 실행 되는 웹 응용 프로그램 프록시로 마이그레이션할 수는 없습니다.  
  
> [!IMPORTANT]
>  Windows server 2008, Windows Server 2008 R2 또는 Windows Server 2012에서 실행 되는 페더레이션 서버 프록시를 Windows Server 2012 r 2에서 실행 되는 웹 응용 프로그램 프록시로 마이그레이션하는 기능은 지원 되지 않습니다.  
  
엑스트라넷 액세스를 위해 Windows Server 2012 R2 마이그레이션된 팜에서 AD FS을 구성 하려면 AD FS 인프라의 일부로 하나 이상의 웹 응용 프로그램 프록시 컴퓨터를 새로 배포 해야 합니다.  
  
웹 응용 프로그램 프록시 배포를 계획하려면 다음 항목의 정보를 검토하면 됩니다.  
  
- [웹 응용 프로그램 프록시 인프라 계획](https://technet.microsoft.com/library/dn383648.aspx)  
  
- [웹 응용 프로그램 프록시 서버 계획](https://technet.microsoft.com/library/dn383647.aspx)  
  
  웹 응용 프로그램 프록시를 배포하려면 다음 항목의 절차를 따르면 됩니다.  
  
- [웹 응용 프로그램 프록시 인프라 구성](https://technet.microsoft.com/library/dn383644.aspx)  
  
- [웹 응용 프로그램 프록시 서버 설치 및 구성](https://technet.microsoft.com/library/dn383662.aspx)  
  
## <a name="next-steps"></a>다음 단계
 [Active Directory Federation Services 역할 서비스를 Windows Server 2012 r 2로 마이그레이션](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS 페더레이션 서버 마이그레이션을 준비 하는 중](prepare-migrate-ad-fs-server-r2.md)   
 [AD FS 페더레이션 서버 마이그레이션](migrate-ad-fs-fed-server-r2.md)    
 [Windows Server 2012 r 2로 AD FS 마이그레이션 확인](verify-ad-fs-migration.md)

