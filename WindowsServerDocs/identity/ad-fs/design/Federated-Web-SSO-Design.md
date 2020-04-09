---
ms.assetid: 09f335bb-896a-45dd-adc2-f215b8fba828
title: 페더레이션된 웹 SSO 디자인
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9915a2942c9336d5aeb7776169d2e51491c22909
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853146"
---
# <a name="federated-web-sso-design"></a>페더레이션된 웹 SSO 디자인

Active Directory Federation Services \(AD FS\)의 SSO\) 디자인에서 페더레이션된 웹 Single\-Sign \(\-에는 전체 인터넷 라우팅 인프라 외에도 여러 방화벽, 경계 네트워크 및 이름\-확인 서버에 걸쳐 있는 보안 통신이 포함 됩니다.  
  
두 조직 동의 단일 조직에서 사용자를 허용 하도록 페더레이션 트러스트 관계를 만들려면이 디자인 일반적으로 사용 됩니다 \(계정 파트너 조직\) 웹에 액세스할\-응용 프로그램이 나 다른 조직에서 AD FS를 통해 보호 되는 서비스 기반 \(리소스 파트너 조직의\)합니다.  
  
즉, 페더레이션 트러스트 관계는 비즈니스의 전형\-수준 계약 또는 두 조직 간의 파트너 관계입니다. 다음 그림에 나와 있는 것 처럼 그는 최종 결과 두 개의 기업 간의 페더레이션 트러스트 관계를 설정할 수 있습니다\-를\-전체 페더레이션 시나리오입니다.  
  
![페더레이션된 웹 sso](media/adfs2_FederatedWebSSODesign.gif)  
  
한\-방향 화살표 그림에서 페더레이션의 방향을 나타냅니다 신뢰로 — Windows 트러스트 방향을 같은-항상 포리스트의 계정 쪽을 가리킵니다. 즉, 인증은 계정 파트너 조직에서 리소스 파트너 조직으로 흐릅니다.  
  
이 페더레이션된 웹 SSO 디자인에서는 두 명의 페더레이션 서버 \(Fabrikam과 Contoso의 다른에서\) 웹 Fabrikam의 사용자 계정에서 인증 요청을 라우팅할\-응용 프로그램 또는 Contoso에서 서비스를 기반으로 합니다.  
  
> [!NOTE]  
> 추가 보안을 위해 릴레이 요청을 인터넷에서 직접 액세스할 수 없는 페더레이션 서버에 페더레이션 서버 프록시를 사용할 수 있습니다.  
  
이 예제에서 Fabrikam은 ID 또는 계정 공급자입니다. 페더레이션된 웹 SSO 디자인의 Fabrikam 부분에서는 다음과 같은 AD FS 배포 목표를 사용합니다.  
  
-   [Active Directory 사용자에게 다른 조직의 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
Contoso는 리소스 공급자입니다. 다음과 같은 AD FS 배포 목표를 달성 하는 페더레이션된 웹 SSO 디자인의 Contoso 부분:  
  
-   [다른 조직의 사용자에게 클레임 인식 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Active Directory 사용자에게 클레임 인식 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
페더레이션된 웹 SSO 디자인 계획 및 배포에 사용할 수 있는 자세한 작업 목록은 [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
