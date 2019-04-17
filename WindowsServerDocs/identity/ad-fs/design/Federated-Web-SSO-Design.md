---
ms.assetid: 09f335bb-896a-45dd-adc2-f215b8fba828
title: "연결 된 웹 SSO 디자인"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b85f49ac0556bf9b3542a23514d7fcbf82d2d88e
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="federated-web-sso-design"></a>연결 된 웹 SSO 디자인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services \(AD FS\)에서 웹 Single\-Sign\-On 연방 \(SSO\) 디자인 통신이 보안 여러 방화벽, 주변 네트워크 및 name\ 해상도 서버에 걸쳐 있는-전체 인터넷 라우팅 인프라 외에도 있습니다.  
  
두 개의 조직 한 조직의 수 있도록 하려면 federation 신뢰 관계를 만드는 데 동의 하는 경우이 디자인 일반적으로 사용 \ (의 계정 파트너 organization\) Web\ 기반 응용 프로그램이 나 다른 조직의 Adfs에 의해 보호 되는 서비스에 액세스할 수 \ (리소스 파트너 organization\).  
  
즉, federation 보안 관계는 business\ 수준 계약 또는 두 조직 간에 간 산학 협동의 구현 합니다. 다음 그림와 같이 federation 신뢰 관계 end\ to\ 엔드 federation 시나리오에서 해당 하는 두 가지 비즈니스를 설정할 수 있습니다.  
  
![연결 된 웹 sso](media/adfs2_FederatedWebSSODesign.gif)  
  
그림에서 one\ 방향 화살표 방향으로 연합 의미 신뢰 하는 등 Windows 신뢰 방향을 같은-항상 숲 계정 측면을 가리킵니다. 즉, 인증은 계정 파트너 조직에서 리소스 파트너 조직에 배치 합니다.  
  
이 웹 SSO 연방 디자인 두 federation 서버 \ (Fabrikam에 1 하 고 다른 Contoso\) 인증의에서 요청 보낼 사용자 계정에 Fabrikam Web\ 기반 응용 프로그램이 나 Contoso에서 서비스에 있습니다.  
  
> [!NOTE]  
> 추가 보안에 대 한 federation 릴레이 서버에 요청을 federation 직접은 인터넷에서 액세스할 수 없는 프록시 서버를 사용할 수 있습니다.  
  
여기에서 Fabrikam는 id, 또는 계정 공급자입니다. 웹 SSO 연방 디자인 Fabrikam 부분이 다음 ADFS 배포 목표를 사용합니다.  
  
-   [응용 프로그램 및 서비스에서는 다른 조직의 Active Directory 사용자 액세스를 제공](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
Contoso는 리소스 공급자는 있습니다. 다음과 같은 ADFS 배포 목표를 달성 하는 웹 SSO 연방 디자인 Contoso 부분이:  
  
-   [조직에 대 한 또 다른 액세스에 사용자가 인식 클레임 응용 프로그램 및 서비스에 제공](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [인식 클레임 응용 프로그램 및 서비스에 사용자 Active Directory 사용자가 액세스할 수 있도록](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
계획 하 고 웹 SSO 연방 디자인 배포 사용할 수 있는 작업 자세한 목록은 [검사: 웹 SSO 연방 디자인을 구현](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
