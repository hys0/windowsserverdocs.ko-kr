---
ms.assetid: 8c3536b7-d091-4ee6-ad04-24713f070862
title: 계정 파트너 조직에서 AD FS 배포
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 93f61bc7fd147b2e0220178bcd163b6ca56279cf
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191573"
---
# <a name="deploying-ad-fs-in-the-account-partner-organization"></a>계정 파트너 조직에서 AD FS 배포

Active Directory Federation Services를 사용 하는 계정 파트너 \(AD FS\) 지원 되는 특성 저장소에 사용자 계정을 실제로 저장 하는 페더레이션 트러스트 관계의 조직을 나타냅니다. 저장소 지원 되는 특성에 대 한 자세한 내용은 참조 하세요. [The 특성 저장소의 역할](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)입니다.  
  
계정 파트너 조직의 페더레이션 서버는 로컬 사용자를 인증 하 고 권한 부여 결정을 내리는 리소스 파트너에서 사용 되는 보안 토큰을 만듭니다. 웹 사이트 및 웹 서비스와 같은 신뢰 당사자 쉽게 페더레이션 서버를 사용 하 여 자신을 등록 하 고 인증 및 액세스 제어에 발급 된 토큰을 사용할 수 있게 됩니다.  
  
여러 페더레이션된 응용 프로그램 또는 서비스에 대 한 액세스를 사용 하 여 사용자에 게 제공 해야 하는 시나리오에서-다른 조직에서 각 응용 프로그램 또는 서비스 호스트 되는 경우-배포할 수 있도록 계정 파트너 페더레이션 서버를 구성할 수 있습니다 여러 신뢰 당사자입니다.  
  
설정 및 계정 파트너 조직의 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [검사 목록: 계정 파트너 조직 구성](../../ad-fs/deployment/Checklist--Configuring-the-Account-Partner-Organization.md)합니다.  
  
## <a name="in-this-section"></a>단원 내용  
  
-   [계정 파트너에서 페더레이션 서버의 역할 검토](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)  
  
-   [계정 파트너에서 페더레이션 서버 프록시의 역할 검토](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md)  
  
-   [계정 파트너에서 클라이언트 컴퓨터 준비](Prepare-Client-Computers-in-the-Account-Partner.md)  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
