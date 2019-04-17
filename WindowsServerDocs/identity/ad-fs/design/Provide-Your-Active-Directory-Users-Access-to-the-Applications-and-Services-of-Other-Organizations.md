---
ms.assetid: 2d62386c-b466-4a54-b6fa-5d16cda120d8
title: "응용 프로그램 및 서비스에서는 다른 조직의 Active Directory 사용자 액세스를 제공"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d50d26c5c654e5c91b82f6f209e21f257221c12d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="provide-your-active-directory-users-access-to-the-applications-and-services-of-other-organizations"></a>응용 프로그램 및 서비스에서는 다른 조직의 Active Directory 사용자 액세스를 제공

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 Active Directory Federation Services \(AD FS\) 배포 목표에 목표에 빌드 [제공 나만의 Active Directory 사용자에 대 한 액세스 클레임 인식 나만의 응용 프로그램과 서비스](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)합니다.  
  
관리자 계정 파트너 조직에는 직원 연합된 액세스를 제공 하도록 하는 시간과 호스트 리소스 다른 조직에서:  
  
-   회사 네트워크에서 Active Directory 도메인에 로그인 되어 있는 직원 \(SSO\) 기능 single\ sign\-켜 짐 사용 여러 Web\ 기반 응용 프로그램이 나 다른 조직에는 응용 프로그램 또는 서비스가 때 Adfs에 의해 보호할 서비스에 액세스할 수 있습니다. 자세한 내용은 참조 [웹 SSO 디자인 연방](Federated-Web-SSO-Design.md)합니다.  
  
    예를 들어, Fabrikam 회사 네트워크 직원 Contoso에서 호스트 하는 웹 서비스에 액세스할 수 있는 연결 된 하 않도록 할 수 있습니다.  
  
-   원격 직원에 게 Active Directory 도메인 로그온 ADFS 토큰 federation 서버 AD FS-보안 Web\ 기반 응용 프로그램이 나 다른 조직에서 호스트 되는 서비스에 연결 된 액세스할 조직에서 얻을 수 있습니다.  
  
    예를 들어, Fabrikam Fabrikam 회사 네트워크에 연결 해야 Fabrikam 직원을 않고도 호스트 되는 광고 FS-보안 서비스에 액세스할 수 있는 연방 원격 직원이 않도록 할 수 있습니다.  
  
외에 대해 설명 하는 기본 구성 요소 [제공 나만의 Active Directory 사용자에 대 한 액세스 클레임 인식 나만의 응용 프로그램 및 서비스](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md) 다음 그림에서 회색으로 표시 되는, 다음과 같은 구성 요소가 필요이 배포 목표에 대해 다음과 같습니다.  
  
-   **파트너 federation 서버 프록시 계정:** 직원에 연결 된 서비스 또는 응용 프로그램은 인터넷에서 액세스 하는 인증을 수행 하려면이 ADFS 구성 요소를 사용할 수 있습니다. 기본적으로이 구성 요소 양식 인증을 수행 하지만 기본 인증 수행할 수도 있습니다. 이 구성 요소 경우를 수행할 주소 \(SSL\) 클라이언트 인증 직원 조직에서 제공 하는 인증서가 구성할 수 있습니다. 자세한 내용은 참조 [Federation 서버 프록시 위치](Where-to-Place-a-Federation-Server-Proxy.md)합니다.  
  
-   **주변 DNS:** Domain Name System \(DNS\)이 구현 주변 네트워크에 대 한 호스트 이름을 제공 합니다. 주변 DNS federation 프록시 서버에 대 한 구성 하는 방법에 대 한 자세한 내용은 참조 [이름 해상도 요구 사항을 Federation 서버 프록시](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)합니다.  
  
-   **원격 직원:** 원격 직원 Web\ 기반 응용 프로그램에 액세스 \ (지원 되는 웹 browser\)을 통해 또는 Web\ 기반 서비스 \ 직원은 오프 인터넷을 사용 하는 동안 (된 application\)를 통해 회사 네트워크에서 유효한 자격 증명을 사용 합니다. 원격 위치에는 직원 클라이언트 컴퓨터 federation 서버 프록시 토큰 생성 하 고 인증 응용 프로그램이 나 서비스를 사용 하 여 직접 통신 합니다.  
  
연결 된 항목에 대 한 정보를 검토 한 후 하기에 나와 있는 단계에 따라이 목표를 배포 [검사: 웹 SSO 연방 디자인을 구현](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)합니다.  
  
다음은 각각의이 ADFS 배포 목표에 필요한 구성 요소입니다.  
  
![앱에 대 한 액세스](media/50af4837-31e0-451f-a942-e705c2300065.gif)  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
