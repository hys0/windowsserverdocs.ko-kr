---
ms.assetid: 2d62386c-b466-4a54-b6fa-5d16cda120d8
title: Active Directory 사용자에게 다른 조직의 응용 프로그램 및 서비스에 대한 액세스 제공
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: bcf9b9ec91c1757ad060747a6aa1589012c1ec14
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359034"
---
# <a name="provide-your-active-directory-users-access-to-the-applications-and-services-of-other-organizations"></a>Active Directory 사용자에게 다른 조직의 응용 프로그램 및 서비스에 대한 액세스 제공

이 Active Directory Federation Services \(\) AD FS [Active Directory 사용자에 게 클레임 인식 응용 프로그램 및 서비스에 대 한 액세스를 제공](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)합니다.  
  
계정 파트너 조직의 관리자이고 직원들에게 다른 조직의 호스트된 리소스에 대한 페더레이션 액세스 권한을 제공하려는 배포 목표가 있는 경우:  
  
-   회사 네트워크의 Active Directory 도메인에 로그온 한 직원은 \(SSO\) 기능에서 단일\-sign\-을 사용 하 여 응용 프로그램이 나 서비스가 다른 조직에 있는 경우\-으로 보안이 유지 되는 여러 웹 AD FS 기반 응용 프로그램 또는 서비스에 액세스할 수 있습니다. 자세한 내용은 참조 [페더레이션된 웹 SSO 디자인](Federated-Web-SSO-Design.md)합니다.  
  
    예를 들어 Fabrikam이 회사 네트워크 직원에게 Contoso에서 호스트된 웹 서비스에 대해 페더레이션 액세스 권한을 갖게 하고 싶을 수 있습니다.  
  
-   Active Directory 도메인에 로그온 한 원격 직원은 조직의 페더레이션 서버에서 AD FS 토큰을 얻어 다른 조직에서 호스트 되는 AD FS 보안 웹\-기반 응용 프로그램이 나 서비스에 대 한 페더레이션 액세스 권한을 얻을 수 있습니다.  
  
    예를 들어 Fabrikam 원격 직원은 Fabrikam 직원이 Fabrikam 회사 네트워크에 있는 것을 요구 하지 않고, Contoso에서 호스트 되는 AD FS 보안 서비스에 대 한 액세스를 페더레이션 하는 경우가 있습니다.  
  
이 배포 목표에는 [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md) 에서 설명하고 다음 일러스트레이션에서 음영 처리된 기본 구성 요소 외에 다음 구성 요소가 필요합니다.  
  
-   **파트너 페더레이션 서버 프록시 계정:** 인터넷에서 페더레이션된 서비스 또는 응용 프로그램에 액세스 하는 직원 인증을 수행 하도록이 AD FS 구성 요소를 사용할 수 있습니다. 기본적으로 이 구성 요소는 폼 인증을 수행하지만 또한 기본 인증도 수행할 수 있습니다. 또한 Secure Sockets Layer를 수행 하려면이 구성 요소를 구성할 수 있습니다 \(SSL\) 사용자의 조직에서 직원 들이 인증서를 제공 하는 경우 클라이언트 인증입니다. 자세한 내용은 참조 [페더레이션 서버 프록시 배치 위치](Where-to-Place-a-Federation-Server-Proxy.md)합니다.  
  
-   **경계 DNS:** Domain Name System이이 구현 \(DNS\) 경계 네트워크에 대 한 호스트 이름을 제공 합니다. 페더레이션 서버 프록시에 대 한 경계 DNS를 구성 하는 방법에 대 한 자세한 내용은 참조 [페더레이션 서버 프록시에 대 한 이름 확인 요구 사항](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)합니다.  
  
-   **원격 직원:** 웹 액세스 하는 원격 직원\-기반 응용 프로그램 \(지원 되는 웹 브라우저를 통해\) 또는 웹\-기반 서비스 \(응용 프로그램을 통해\), 직원은 인터넷을 사용 하 여 오프 사이트를 회사 네트워크에서 유효한 자격 증명을 사용 하 여 합니다. 직원의 클라이언트 컴퓨터는 원격 위치에서 토큰을 생성 하 고 응용 프로그램이 나 서비스에 인증 하는 페더레이션 서버 프록시가와 직접 통신 합니다.  
  
링크된 항목의 정보를 검토한 후 [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)의 단계를 따라 이 목표 배포를 시작할 수 있습니다.  
  
다음 그림에서는이 AD FS 배포 목표에 대 한 필수 구성 요소 각각을 보여 줍니다.  
  
![응용 프로그램에 대 한 액세스](media/50af4837-31e0-451f-a942-e705c2300065.gif)  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
