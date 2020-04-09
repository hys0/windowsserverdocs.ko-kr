---
ms.assetid: d254fca3-85a1-424d-ac22-d6687ec3798e
title: Active Directory 사용자에게 클레임 인식 응용 프로그램 및 서비스에 대한 액세스 제공
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0cb530eacfa8239f3a2a135397e54becfadb602b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858576"
---
# <a name="provide-your-active-directory-users-access-to-your-claims-aware-applications-and-services"></a>Active Directory 사용자에게 클레임 인식 응용 프로그램 및 서비스에 대한 액세스 제공

\(Active Directory Federation Services에서 계정 파트너 조직의 관리자가\) 배포를 AD FS 하 고\-SSO\-에 대 한 단일 \(sign-on을 제공 하는 배포 목표가 있는 경우 회사 네트워크의 직원 들에 게 호스트 된 리소스에 대 한\) 액세스를 제공 합니다.  
  
-   회사 네트워크의 Active Directory 포리스트에 로그온한 직원이 SSO를 사용하여 해당 조직의 경계 네트워크에 있는 여러 애플리케이션이나 서비스에 액세스할 수 있습니다. 이러한 애플리케이션 및 서비스는 AD FS에서 보안이 유지 됩니다.  
  
    예를 들어, Fabrikam 웹에 대 한 액세스를 페더레이션 하는 직원이 회사 네트워크를 할 수\-Fabrikam에 대 한 경계 네트워크에서 호스팅되는 응용 프로그램을 기반으로 합니다.  
  
-   Active Directory 도메인에 로그온 한 원격 직원은 조직의 페더레이션 서버에서 AD FS 토큰을 가져와 조직에도 있는 보안 웹\-기반 응용 프로그램 또는 서비스\-AD FS에 대 한 페더레이션 액세스 권한을 얻을 수 있습니다.  
  
-   Active Directory 특성 저장소의 정보를 직원의 AD FS 토큰에 채울 수 있습니다.  
  
이 배포 목표를 달성하려면 다음 구성 요소가필요 합니다.  
  
-   **Active Directory Domain Services \(AD DS\):** AD DS에는 AD FS 토큰을 생성 하는 데 사용 되는 직원의 사용자 계정이 포함 되어 있습니다. 그룹 구성원 자격 및 특성과 같은 정보는 그룹 클레임 및 사용자 지정 클레임으로 AD FS 토큰에 채워집니다.  
  
    > [!NOTE]  
    > 또한\) 토큰 생성을 위한 id를 포함 하는 LDAP\) 또는 구조적 쿼리 언어 \(SQL AD FS에 대 한 LDAP (Lightweight Directory Access Protocol \()를 사용할 수 있습니다.  
  
-   **회사 DNS:** Domain Name System이이 구현 \(DNS\) 간단한 호스트 포함 \(A\) 인트라넷 클라이언트가 계정 페더레이션 서버를 찾을 수 있도록 리소스를 기록 합니다. DNS 구현에서 회사 네트워크에 필요한 다른 DNS 레코드를 호스트할 수도 있습니다. 자세한 내용은 [페더레이션 서버에 대한 이름 확인 요구 사항](Name-Resolution-Requirements-for-Federation-Servers.md)을 참조하세요.  
  
-   **계정 파트너 페더레이션 서버:** 이 페더레이션 서버는 계정 파트너 포리스트에 있는 도메인에 가입 합니다. 직원 사용자 계정을 인증하고 AD FS 토큰을 생성합니다. 직원의 클라이언트 컴퓨터는이 페더레이션 서버에 대해 Windows 통합 인증을 수행 하 여 AD FS 토큰을 생성 합니다. 자세한 내용은 참조 [검토 하는 계정 파트너의 페더레이션 서버 역할을](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)합니다.  
  
    계정 파트너 페더레이션 서버는 다음 사용자를 인증할 수 있습니다.  
  
    -   이 도메인의 사용자 계정을 가진 직원  
  
    -   이 포리스트의 사용자 계정을 가진 직원  
  
    -   이 포리스트에서 신뢰 하는 포리스트의 어디에서 나 사용자 계정을 가진 직원은 Windows 트러스트를 두\-방식 \(\)  
  
-   **직원:** 웹 액세스 하는 직원\-기반 서비스 \(응용 프로그램을 통해\) 또는 웹\-기반 응용 프로그램 \(지원 되는 웹 브라우저를 통해\) 대금은 로그온 한 상태에서 회사 네트워크에 있습니다. 회사 네트워크에서 직원의 클라이언트 컴퓨터 인증을 위해 페더레이션 서버와 직접 통신합니다.  
  
링크된 항목의 정보를 검토한 후 [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)의 단계를 따라 이 목표 배포를 시작할 수 있습니다.  
  
다음 그림에서는이 AD FS 배포 목표에 대 한 필수 구성 요소 각각을 보여 줍니다.  
  
![사용자 클레임에 대 한 액세스](media/31394ea8-fecb-4372-ac3f-cc3cf566ffc9.gif)  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
