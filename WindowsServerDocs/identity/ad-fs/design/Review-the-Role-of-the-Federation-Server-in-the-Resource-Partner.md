---
ms.assetid: f88238ea-d851-4129-8b4e-a3a62b813614
title: 리소스 파트너에서 페더레이션 서버의 역할 검토
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b2ed7a09bbc50c83d3bf6f8f2688152ed5202abc
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190822"
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>리소스 파트너에서 페더레이션 서버의 역할 검토

리소스 파트너 조직의 페더레이션 서버 계정 페더레이션 서버에서 보낸 들어오는 보안 토큰을 가로채의 유효성을 검사 하 고, 서명 및 웹용 되는 자체 보안 토큰을 발급 합니다\-기반 응용 프로그램입니다.  
  
> [!NOTE]  
> 페더레이션된 사용자가 웹에 액세스 하는 웹 브라우저를 사용 하는 경우\-기반된 응용 프로그램, 리소스 파트너 조직의 페더레이션 서버는 새 인증 쿠키를 빌드하고 브라우저에 씁니다. 이 쿠키를 사용 하도록 설정 단일\-기호\-온 \(SSO\) 기능 사용자가 다시 로그온 계정 파트너에서 페더레이션 서버에서 사용자가 다른 웹에 액세스 하려고 할 때 하지 않아도 되도록\- 리소스 파트너에 따라 응용 프로그램입니다.  
  
웹 SSO 디자인에서는 하나 이상의 페더레이션 서버는 경계 네트워크에 설치 되어야 합니다. 페더레이션된 웹 SSO 디자인에서는 계정 파트너 조직의 회사 네트워크에 설치 된 하나 이상의 페더레이션 서버 및 리소스 파트너 조직의 회사 네트워크에 설치 하는 페더레이션 서버가 하나 이상 있어야 합니다.  
  
> [!NOTE]  
> 리소스 파트너 조직의 페더레이션 서버 컴퓨터를 설정할 수 있습니다, 전에 리소스 파트너 조직의 Active Directory 도메인에 컴퓨터를 연결 해야 합니다. 자세한 내용은 참조 하세요. [검사 목록: 페더레이션 서버를 설정할](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)

