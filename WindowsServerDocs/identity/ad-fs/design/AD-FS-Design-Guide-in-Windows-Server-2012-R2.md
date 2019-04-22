---
ms.assetid: a8558c9d-0606-4881-93b2-f2d2716b18e7
title: Windows Server 2012 R2의 AD FS 디자인 가이드
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 498b399818fb8c9e463f9990fa13c87648c0a33d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822154"
---
# <a name="ad-fs-design-guide-in-windows-server-2012-r2"></a>Windows Server 2012 R2의 AD FS 디자인 가이드

>적용 대상: Windows Server 2016, Windows Server 2012 R2

Active Directory Federation Services \(AD FS\) 간편 하 고 안전한 id 페더레이션 및 웹 single sign 제공\-온 \(SSO\) 응용 프로그램에 액세스 하려는 최종 사용자에 대 한 기능 AD FS 내의\-페더레이션 파트너 조직 또는 클라우드에서 엔터프라이즈 보호 합니다.  
  
Windows Server® 2012 R2 AD FS 페더레이션 서비스 역할 서비스를 id 공급자로 사용 되는 포함 되어 있습니다 \(AD FS를 신뢰 하는 응용 프로그램에 보안 토큰을 제공 하는 사용자를 인증\) 또는 페더레이션 공급자 \( 다른 id 공급자에서 토큰을 사용 하 여 AD FS를 신뢰 하는 응용 프로그램에 보안 토큰 제공\)합니다.  
  
이제 Windows Server 2012 R2에서 AD FS에 의해 보안되는 응용 프로그램 및 서비스에 대한 엑스트라넷 액세스 권한을 제공하는 기능은 웹 응용 프로그램 프록시라는 새 원격 액세스 역할 서비스에서 수행됩니다. 이는 AD FS 페더레이션 서버 프록시가 이 함수를 처리한 이전 버전의 Windows Server에서 시작되었습니다. 웹 응용 프로그램 프록시는 AD FS에 대 한 액세스를 제공 하도록 설계 된 서버 역할\-관련 엑스트라넷 시나리오 및 다른 엑스트라넷 시나리오입니다. 웹 응용 프로그램 프록시에 대 한 자세한 내용은 참조 하세요. [웹 응용 프로그램 프록시 연습 가이드](https://technet.microsoft.com/library/dn280944.aspx)합니다.  
  
## <a name="about-this-guide"></a>이 가이드 정보  
이 가이드에서는 조직의 요구 사항에 따라 AD FS의 새 배포를 계획 하기 위한 권장 사항을 제공 합니다. 이 가이드는 인프라 전문가 또는 시스템 설계자용으로 작성되었습니다. AD FS 배포를 계획할 때 필요한 주요 의사 결정 사항을 강조 합니다. 이 가이드를 읽기 전에 기능 수준에서 AD FS의 작동 방식을 이해를 해야 합니다. 자세한 내용은 [Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)를 참조하세요.  
  
## <a name="in-this-guide"></a>이 가이드의 내용  
  
-   [AD FS 배포 목표 식별](Identify-Your-AD-FS-Deployment-Goals.md)  
  
-   [AD FS 배포 토폴로지 계획](Plan-Your-AD-FS-Deployment-Topology.md)  
  
-   [AD FS 요구 사항](AD-FS-Requirements.md)  
  
  
## <a name="see-also"></a>관련 항목  
[AD FS 디자인](../../ad-fs/AD-FS-Design.md)  
  

