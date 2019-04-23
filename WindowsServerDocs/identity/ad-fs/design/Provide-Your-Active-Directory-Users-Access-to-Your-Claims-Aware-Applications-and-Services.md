---
ms.assetid: d254fca3-85a1-424d-ac22-d6687ec3798e
title: Active Directory 사용자에게 클레임 인식 응용 프로그램 및 서비스에 대한 액세스 제공
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f6fb37c16c20915c0051e3a24cdb0c147ae92d9c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835874"
---
# <a name="provide-your-active-directory-users-access-to-your-claims-aware-applications-and-services"></a>Active Directory 사용자에게 클레임 인식 응용 프로그램 및 서비스에 대한 액세스 제공

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory 페더레이션 서비스에서 계정 파트너 조직의 관리자 인 경우 \(AD FS\) 배포 하 고 있는 단일 제공 하려는 배포 목표가\-sign\-에서 \( SSO\) 호스 티 드 리소스에 회사 네트워크 직원에 대 한 액세스:  
  
-   회사 네트워크의 Active Directory 포리스트에 로그온한 직원이 SSO를 사용하여 해당 조직의 경계 네트워크에 있는 여러 응용 프로그램이나 서비스에 액세스할 수 있습니다. 이러한 응용 프로그램 및 서비스는 AD FS에서 보안이 유지 됩니다.  
  
    예를 들어, Fabrikam 웹에 대 한 액세스를 페더레이션 하는 직원이 회사 네트워크를 할 수\-Fabrikam에 대 한 경계 네트워크에서 호스팅되는 응용 프로그램을 기반으로 합니다.  
  
-   Active Directory 도메인에 로그온 한 원격 직원 AD FS로 페더레이션에 액세스 하기 위해 조직에서 페더레이션 서버에서 AD FS 토큰을 가져올 수 있습니다\-웹 보안\-기반 응용 프로그램 또는 서비스에 있는 조직입니다.  
  
-   Active Directory 특성 저장소의 정보를 직원의 AD FS 토큰에 채울 수 있습니다.  
  
이 배포 목표를 달성하려면 다음 구성 요소가필요 합니다.  
  
-   **Active Directory Domain Services \(AD DS\):** AD DS에는 AD FS 토큰을 생성하는 데 사용되는 직원의 사용자 계정이 포함되어 있습니다. 그룹 구성원 자격 및 특성과 같은 정보는 그룹 클레임 및 사용자 지정 클레임으로 AD FS 토큰에 채워집니다.  
  
    > [!NOTE]  
    > Lightweight Directory Access Protocol을 사용할 수도 있습니다 \(LDAP\) 또는 구조적 쿼리 언어 \(SQL\) 포함 하도록 AD FS에 대 한 id 토큰을 생성 합니다.  
  
-   **회사 DNS:** 이 구현의 Domain Name System \(DNS\) 간단한 호스트 포함 \(는\) 인트라넷 클라이언트가 계정 페더레이션 서버를 찾을 수 있도록 리소스를 기록 합니다. DNS 구현에서 회사 네트워크에 필요한 다른 DNS 레코드를 호스트할 수도 있습니다. 자세한 내용은 참조 [페더레이션 서버에 대 한 이름 확인 요구 사항](Name-Resolution-Requirements-for-Federation-Servers.md)합니다.  
  
-   **계정 파트너 페더레이션 서버:** 이 페더레이션 서버는 계정 파트너 포리스트의 도메인에 조인 됩니다. 직원 사용자 계정을 인증하고 AD FS 토큰을 생성합니다. 직원의 클라이언트 컴퓨터는 AD FS 토큰을 생성 하이 페더레이션 서버에 대해 Windows 통합 인증을 수행 합니다. 자세한 내용은 참조 [검토 하는 계정 파트너의 페더레이션 서버 역할을](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)합니다.  
  
    계정 파트너 페더레이션 서버는 다음 사용자를 인증할 수 있습니다.  
  
    -   이 도메인의 사용자 계정을 가진 직원  
  
    -   이 포리스트의 사용자 계정을 가진 직원  
  
    -   이 포리스트의에서 신뢰할 수 있는 포리스트 원격 사용자 계정 가진 직원 \(2를 통해\-방식으로 Windows 트러스트\)  
  
-   **직원:** 웹 액세스 하는 직원\-기반 서비스 \(응용 프로그램을 통해\) 또는 Web\-기반 응용 프로그램 \(지원 되는 웹 브라우저를 통해\) 자신이 로그온 하는 동안는 회사 네트워크입니다. 회사 네트워크에서 직원의 클라이언트 컴퓨터 인증을 위해 페더레이션 서버와 직접 통신합니다.  
  
연결 된 항목의 정보를 검토 한 후 시작할 수 있습니다이 목표의 단계를 수행 하 여 배포 [검사 목록: 페더레이션된 웹 SSO 디자인 구현](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)합니다.  
  
다음 그림에서는이 AD FS 배포 목표에 대 한 필수 구성 요소 각각을 보여 줍니다.  
  
![사용자 클레임에 대 한 액세스](media/31394ea8-fecb-4372-ac3f-cc3cf566ffc9.gif)  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의에서 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
