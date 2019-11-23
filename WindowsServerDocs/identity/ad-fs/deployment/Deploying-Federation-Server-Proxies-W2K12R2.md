---
ms.assetid: 222e9f93-7c41-4527-8a98-8f7fbc7a58af
title: 페더레이션 서버 프록시 배포
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 34d2a15d5ad4f2563beffbce6ae5e729cf72c3ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359679"
---
# <a name="deploying-federation-server-proxies"></a>페더레이션 서버 프록시 배포

Windows Server 2012 r 2에서\) \(AD FS Active Directory Federation Services 페더레이션 서버 프록시의 역할은 웹 응용 프로그램 프록시 라는 새 원격 액세스 역할 서비스에 의해 처리 됩니다. 회사 네트워크 외부에서의 접근성에 대 한 AD FS를 사용 하도록 설정 하려면 Windows Server 2012의 AD FS 2.0 및 AD FS와 같이 AD FS의 레거시 버전에서 페더레이션 서버 프록시를 배포 하기 위한 것입니다. D FS in Windows Server 2012 R2.  
  
AD FS 컨텍스트에서 웹 응용 프로그램 프록시는 AD FS 페더레이션 서버 프록시로 작동 합니다. 이 외에도 웹 응용 프로그램 프록시는 회사 네트워크 내부의 웹 응용 프로그램에 대해 역방향 프록시 기능을 제공하여 모든 장치의 사용자가 회사 네트워크 권역을 벗어나서도 해당 네트워크에 접근할 수 있습니다. 웹 응용 프로그램 프록시 역할 서비스에 대한 자세한 내용은 웹 응용 프로그램 프록시 개요를 참조하세요.  
  
웹 응용 프로그램 프록시 배포를 계획하려면 다음 항목의 정보를 검토하면 됩니다.  
  
-   [웹 응용 프로그램 프록시 인프라 (WAP) 계획](https://technet.microsoft.com/library/dn383648.aspx)  
  
-   [웹 응용 프로그램 프록시 서버 계획](https://technet.microsoft.com/library/dn383647.aspx)  
  
웹 응용 프로그램 프록시를 배포하려면 다음 항목의 절차를 따르면 됩니다.  
  
-   [웹 응용 프로그램 프록시 인프라 구성](https://technet.microsoft.com/library/dn383644.aspx)  
  
-   [웹 응용 프로그램 프록시 서버 설치 및 구성](https://technet.microsoft.com/library/dn383662.aspx)  
  
 
## <a name="see-also"></a>참고 항목 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[페더레이션 서버 팜 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

