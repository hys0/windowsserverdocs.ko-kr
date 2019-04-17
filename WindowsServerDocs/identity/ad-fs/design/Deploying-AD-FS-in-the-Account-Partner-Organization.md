---
ms.assetid: 8c3536b7-d091-4ee6-ad04-24713f070862
title: "계정 파트너 조직에서 ADFS 배포"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5b4ba00aa9fed1022d9c0137d05ac6240b44b276
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="deploying-ad-fs-in-the-account-partner-organization"></a>계정 파트너 조직에서 ADFS 배포

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

계정 파트너 Active Directory Federation Services \(AD FS\)에서 지원 되는 특성 스토어에서 사용자 계정 물리적으로 저장 하는 federation 신뢰 관계에는 조직을 나타냅니다. 스토어 지원 되는 특성에 대 한 자세한 내용은 참조 [The 역할의 특성을 저장](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)합니다.  
  
계정 파트너 조직에서 federation 서버 인증 하는 로컬 사용자 하 고 승인 결정을 내리는 리소스 파트너에 사용 되는 보안 토큰 만듭니다. 신뢰 당사자 쉽게 federation 서버에 등록할 하 고 사용할 수 있는 웹 사이트와 웹 서비스와 같은 인증과 액세스 제어 토큰 발생 합니다.  
  
여러 연결 된 응용 프로그램이 나 서비스에 액세스할 수 있는 사용자에 게 제공 하기 위해 필요한 경우 등 다른 조직 하 여 각 응용 프로그램 또는 서비스 호스트 때-여러 신뢰 당사자 배포할 수 있도록 계정 파트너 federation 서버를 구성할 수 있습니다.  
  
설정 하 고 계정 파트너 조직 구성 하는 방법에 대 한 자세한 내용은 참조 [검사: 계정 파트너 조직 구성](../../ad-fs/deployment/Checklist--Configuring-the-Account-Partner-Organization.md)합니다.  
  
## <a name="in-this-section"></a>이 섹션에서  
  
-   [계정 파트너에 해당 Federation 서버의 역할을 검토](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)  
  
-   [계정 파트너의 Federation 서버 프록시 역할을 검토](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md)  
  
-   [클라이언트 컴퓨터에 계정 파트너 준비](Prepare-Client-Computers-in-the-Account-Partner.md)  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
