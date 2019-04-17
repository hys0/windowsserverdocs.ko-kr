---
ms.assetid: de7e1e4a-f96d-4b59-ac9b-f65f5d37a96f
title: "조직에 대 한 또 다른 액세스에 사용자가 인식 클레임 응용 프로그램 및 서비스에 제공"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b4ec08182e2523b0fcb16088ec9c1d094a5923fe
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="provide-users-in-another-organization-access-to-your-claims-aware-applications-and-services"></a>조직에 대 한 또 다른 액세스에 사용자가 인식 클레임 응용 프로그램 및 서비스에 제공

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

리소스 파트너 조직의 Active Directory Federation Services \(AD FS\)의 관리자 인 다른 조직에는 사용자에 대 한 연합된 액세스를 제공 하도록 하는 시간과 \ (계정 파트너 organization\) claims\ 인식 응용 프로그램 또는 조직에 있는 Web\ 기반 서비스에 \ (리소스 파트너 organization\):  
  
-   사용자가 연합 구성한 있는 조직이 및 조직에서 둘 다에 안전 하 게 조직 연방 \ 응용 프로그램 또는 서비스가 조직 하 여 호스팅된 보안 ADFS (파트너 organizations\ 계정)에 액세스할 수 있습니다. 자세한 내용은 참조 [웹 SSO 디자인 연방](Federated-Web-SSO-Design.md)합니다.  
  
    예를 들어, Fabrikam Contoso에서 호스트 하는 웹 서비스에 액세스할 수 있는 연방 회사 네트워크 직원이 않도록 할 수 있습니다.  
  
-   사용자에 게 직접 연결 된 신뢰할 수 있는 조직 연방 \ (예: 개별 customers\), 로그온 주변 네트워크에서 호스트 하는 여러 광고 FS\ 보안 응용 프로그램에도 인터넷에 있는 하는 컴퓨터에서 한 번에 로그인 하 여 주변 네트워크에 호스팅된에 액세스할 수 있는 특성 스토어에 있습니다. 즉, 응용 프로그램 또는 주변 네트워크의 서비스에 액세스할 수 있도록 하기 위해 고객 계정을 개최 특성 스토어에서 호스트 하는 고객 액세스할 수 응용 프로그램 또는 서비스 주변 네트워크에 한 번에 로그인 하 여. 자세한 내용은 참조 [웹 SSO 디자인](Web-SSO-Design.md)합니다.  
  
    예를 들어, Fabrikam 여러 응용 프로그램이 나 주변 네트워크에서 호스트 되는 서비스에 \(SSO\) 액세스 single\ sign\-켜 짐 고객 않도록 할 수 있습니다.  
  
다음과 같은 구성 요소는이 배포 목표에 대해 필요 합니다.  
  
-   **Active Directory Domain Services \ (AD DS \):** 리소스 파트너 federation 서버 Active Directory 도메인에 가입 있어야 합니다.  
  
-   **주변 DNS:** 도메인 Name System \(DNS\) 클라이언트 컴퓨터 리소스 파트너 federation 서버와 웹 서버를 찾을 수 있도록 간단한 호스트 \(A\) 리소스 레코드를 포함 해야 합니다. DNS 서버 주변 네트워크에도 필요 다른 DNS 레코드 개최 될 수 있습니다. 자세한 내용은 참조 [이름을 확인 요구 사항을 Federation 서버에 대 한](Name-Resolution-Requirements-for-Federation-Servers.md)합니다.  
  
-   **리소스 파트너 federation 서버:** 리소스 파트너 federation 서버 계정 파트너 보내기 ADFS 토큰의 유효성을 검사 합니다. 계정 파트너 검색이 federation 서버를 통해 수행 됩니다. 자세한 내용은 참조 [리소스 파트너에 해당 Federation 서버의 역할 검토](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)합니다.  
  
-   **웹 서버:** 웹 응용 프로그램 또는 웹 서비스의 웹 서버 호스트할 수 있습니다. 웹 서버 보호 웹 응용 프로그램 또는 웹 서비스에 액세스할 수 있게 하기 전에 유효한 ADFS 토큰 연합된 사용자 로부터 수신 있는지 확인 합니다.  
  
    Windows 신원을 파운데이션 \(WIF\)를 사용 하 여 사용자 이름 및 암호 등 모든 표준 로그온 방법을 사용 하 여 수행 된 연합된 사용자 로그온 요청을 수락 하 않도록 웹 응용 프로그램 또는 서비스가 개발할 수 있습니다.  
  
연결 된 항목에 대 한 정보를 검토 한 후 하기에 나와 있는 단계에 따라이 목표를 배포 [검사: 웹 SSO 연방 디자인을 구현](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md) 및 [검사: 웹 SSO 디자인을 구현](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)합니다.  
  
다음은 각각의이 ADFS 배포 목표에 필요한 구성 요소입니다.  
  
![사용자 청구에 대 한 액세스](media/75358b16-2a6f-4e16-9cc4-b0e614480305.gif)  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
