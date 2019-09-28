---
ms.assetid: f88238ea-d851-4129-8b4e-a3a62b813614
title: 리소스 파트너에서 페더레이션 서버의 역할 검토
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: fd9f20eb7559f5862ee50bdd8364fa1604d3c1b6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358973"
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>리소스 파트너에서 페더레이션 서버의 역할 검토

리소스 파트너 조직의 페더레이션 서버는 계정 페더레이션 서버에서 전송 된 들어오는 보안 토큰을 가로채 고, 유효성을 검사 하 여 서명한 다음, 웹 @ no__t-0based 응용 프로그램을 대상으로 하는 자체 보안 토큰을 발급 합니다. .  
  
> [!NOTE]  
> 페더레이션된 사용자가 웹 브라우저를 사용 하 여 Web @ no__t-0based 응용 프로그램에 액세스 하는 경우 리소스 파트너 조직의 페더레이션 서버는 새 인증 쿠키를 작성 하 고 브라우저에 씁니다. 이 쿠키를 사용 하면 사용자가 리소스의 다른 웹 @ no__t-4 기반 응용 프로그램에 액세스 하려고 할 때 사용자가 계정 파트너의 페더레이션 서버에서 다시 로그온 할 필요가 없도록 단일 @ no__t-0sign @ no__t-1on \(SSO @ no__t-3 기능을 사용할 수 있습니다. 당사자.  
  
웹 SSO 디자인에서 하나 이상의 페더레이션 서버를 경계 네트워크에 설치 해야 합니다. 페더레이션된 웹 SSO 디자인에서는 계정 파트너 조직의 회사 네트워크에 하나 이상의 페더레이션 서버가 설치 되어 있어야 하 고 리소스 파트너 조직의 회사 네트워크에 하나 이상의 페더레이션 서버가 설치 되어 있어야 합니다.  
  
> [!NOTE]  
> 리소스 파트너 조직에서 페더레이션 서버 컴퓨터를 설정 하려면 먼저 리소스 파트너 조직의 Active Directory 도메인에 컴퓨터를 가입 시켜야 합니다. 자세한 내용은 [ 검사 목록을 참조 하세요. 페더레이션 서버 설정 @ no__t-0.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)

