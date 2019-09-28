---
ms.assetid: d254fca3-85a1-424d-ac22-d6687ec3798e
title: Active Directory 사용자에게 클레임 인식 응용 프로그램 및 서비스에 대한 액세스 제공
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 48436f8e98af965f2bc2b38d296c4a15924e4db1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407954"
---
# <a name="provide-your-active-directory-users-access-to-your-claims-aware-applications-and-services"></a>Active Directory 사용자에게 클레임 인식 응용 프로그램 및 서비스에 대한 액세스 제공

Active Directory Federation Services \(AD FS @ no__t 배포의 계정 파트너 조직의 관리자이 고, \(SSO @ no__t-5에 대 한 단일 @ no__t-2sign @ no__t에 대 한 액세스를 제공 하는 배포 목표가 있는 경우 호스트 된 리소스에 대 한 회사 네트워크:  
  
-   회사 네트워크의 Active Directory 포리스트에 로그온한 직원이 SSO를 사용하여 해당 조직의 경계 네트워크에 있는 여러 응용 프로그램이나 서비스에 액세스할 수 있습니다. 이러한 응용 프로그램 및 서비스는 AD FS에서 보안이 유지 됩니다.  
  
    예를 들어, Fabrikam 웹에 대 한 액세스를 페더레이션 하는 직원이 회사 네트워크를 할 수\-Fabrikam에 대 한 경계 네트워크에서 호스팅되는 응용 프로그램을 기반으로 합니다.  
  
-   Active Directory 도메인에 로그온 한 원격 직원은 조직의 페더레이션 서버에서 AD FS 토큰을 가져와 AD FS @ no__t-0secured 적용 된 웹 @ no__t 기반 응용 프로그램 또는 서비스에 대 한 페더레이션 액세스 권한을 얻을 수 있습니다. 직.  
  
-   Active Directory 특성 저장소의 정보를 직원의 AD FS 토큰에 채울 수 있습니다.  
  
이 배포 목표를 달성하려면 다음 구성 요소가필요 합니다.  
  
-   **Active Directory Domain Services \(AD DS @ no__t-2:** AD DS에는 AD FS 토큰을 생성하는 데 사용되는 직원의 사용자 계정이 포함되어 있습니다. 그룹 구성원 자격 및 특성과 같은 정보는 그룹 클레임 및 사용자 지정 클레임으로 AD FS 토큰에 채워집니다.  
  
    > [!NOTE]  
    > Lightweight Directory Access Protocol \(LDAP @ no__t-1을 사용 하거나 구조적 쿼리 언어 \(SQL @ no__t-3을 사용 하 여 AD FS 토큰 생성을 위한 id를 포함할 수도 있습니다.  
  
-   **회사 DNS:** 이 도메인 이름 시스템 구현 \(DNS @ no__t-1은 인트라넷 클라이언트가 계정 페더레이션 서버를 찾을 수 있도록 간단한 호스트 \(A @ no__t-3 리소스 레코드를 포함 합니다. DNS 구현에서 회사 네트워크에 필요한 다른 DNS 레코드를 호스트할 수도 있습니다. 자세한 내용은 참조 [페더레이션 서버에 대 한 이름 확인 요구 사항](Name-Resolution-Requirements-for-Federation-Servers.md)합니다.  
  
-   **계정 파트너 페더레이션 서버:** 이 페더레이션 서버는 계정 파트너 포리스트의 도메인에 가입 됩니다. 직원 사용자 계정을 인증하고 AD FS 토큰을 생성합니다. 직원의 클라이언트 컴퓨터는이 페더레이션 서버에 대해 Windows 통합 인증을 수행 하 여 AD FS 토큰을 생성 합니다. 자세한 내용은 참조 [검토 하는 계정 파트너의 페더레이션 서버 역할을](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)합니다.  
  
    계정 파트너 페더레이션 서버는 다음 사용자를 인증할 수 있습니다.  
  
    -   이 도메인의 사용자 계정을 가진 직원  
  
    -   이 포리스트의 사용자 계정을 가진 직원  
  
    -   이 포리스트에서 신뢰할 수 있는 포리스트에 있는 사용자 계정이 있는 직원 (\( ~ 2 @ no__t-1 방향 Windows trust @ no__t-2)  
  
-   **직원:** 직원이 회사 네트워크에 로그온 되어 있는 동안 지원 되는 웹 브라우저 @ no__t-5를 통해 Web @ no__t-0based service \(을 사용 하 여 Web @ no__t-2 또는 Web @ no__t 기반 응용 @no__t 프로그램에 액세스 합니다. 회사 네트워크에서 직원의 클라이언트 컴퓨터 인증을 위해 페더레이션 서버와 직접 통신합니다.  
  
연결 된 항목의 정보를 검토 한 후 [Checklist 목록의 단계에 따라이 목표 배포를 시작할 수 있습니다. 페더레이션된 웹 SSO 디자인 @ no__t-0을 구현 합니다.  
  
다음 그림에서는이 AD FS 배포 목표에 대 한 필수 구성 요소 각각을 보여 줍니다.  
  
![사용자 클레임에 대 한 액세스](media/31394ea8-fecb-4372-ac3f-cc3cf566ffc9.gif)  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
