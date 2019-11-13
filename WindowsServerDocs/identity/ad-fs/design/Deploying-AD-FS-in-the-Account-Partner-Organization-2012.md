---
ms.assetid: 9aaca9c5-ce44-495c-aad6-61aede87a83f
title: 계정 파트너 조직에서 AD FS 배포
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 62d7549f124b96cd7addf7e54cc5d0c1d9897098
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408122"
---
# <a name="deploying-ad-fs-in-the-account-partner-organization"></a>계정 파트너 조직에서 AD FS 배포

Active Directory Federation Services \(AD FS\)의 계정 파트너는 지원 되는 특성 저장소에 사용자 계정을 실제로 저장 하는 페더레이션 트러스트 관계의 조직을 나타냅니다. 지원 되는 특성 저장소에 대 한 자세한 내용은 [특성 저장소의 역할](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)을 참조 하세요.  
  
계정 파트너 조직의 페더레이션 서버는 로컬 사용자를 인증 하 고 권한 부여 결정을 내리는 데 리소스 파트너가 사용 하는 보안 토큰을 만듭니다. 웹 사이트 및 웹 서비스와 같은 신뢰 당사자는 쉽게 페더레이션 서버에 등록 하 고 인증 및 액세스 제어를 위해 발급 된 토큰을 사용할 수 있습니다.  
  
사용자에 게 여러 페더레이션 응용 프로그램 또는 서비스에 대 한 액세스 권한을 제공 해야 하는 시나리오에서 (각 응용 프로그램 또는 서비스가 다른 조직에서 호스트 되는 경우), 배포할 수 있도록 계정 파트너 페더레이션 서버를 구성할 수 있습니다. 여러 신뢰 당사자  
  
계정 파트너 조직을 설정하고 구성하는 방법에 대한 자세한 내용은 [Checklist: Configuring the Account Partner Organization](../../ad-fs/deployment/Checklist--Configuring-the-Account-Partner-Organization.md)을 참조하세요.  
  
## <a name="in-this-section"></a>단원 내용  
  
-   [계정 파트너에서 페더레이션 서버의 역할 검토](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)  
  
-   [계정 파트너에서 페더레이션 서버 프록시의 역할 검토](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md)  
  
-   [계정 파트너에서 클라이언트 컴퓨터 준비](Prepare-Client-Computers-in-the-Account-Partner.md)  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
