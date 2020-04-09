---
ms.assetid: f88238ea-d851-4129-8b4e-a3a62b813614
title: 리소스 파트너에서 페더레이션 서버의 역할 검토
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 8cda394800bf0554e00e2897d240e2c08a72a00b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858556"
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>리소스 파트너에서 페더레이션 서버의 역할 검토

리소스 파트너 조직의 페더레이션 서버는 계정 페더레이션 서버에서 전송 된 들어오는 보안 토큰을 가로채 고 유효성을 검사 하 여 서명한 다음 웹\-기반 응용 프로그램을 대상으로 하는 자체 보안 토큰을 발급 합니다.  
  
> [!NOTE]  
> 페더레이션 사용자가 웹 브라우저를 사용 하 여 웹\-기반 응용 프로그램에 액세스 하는 경우 리소스 파트너 조직의 페더레이션 서버는 새 인증 쿠키를 빌드하여 브라우저에 씁니다. 이 쿠키를 사용 하면 사용자가 리소스 파트너의 다른 웹\-기반 응용 프로그램에 액세스 하려고 할 때 사용자가 계정 파트너의 페더레이션 서버에서 다시 로그온 할 필요가 없도록 SSO\) 기능 \(에서 단일\-기호\-를 사용할 수 있습니다.  
  
웹 SSO 디자인에서 하나 이상의 페더레이션 서버를 경계 네트워크에 설치 해야 합니다. 페더레이션된 웹 SSO 디자인에서는 계정 파트너 조직의 회사 네트워크에 하나 이상의 페더레이션 서버가 설치 되어 있어야 하 고 리소스 파트너 조직의 회사 네트워크에 하나 이상의 페더레이션 서버가 설치 되어 있어야 합니다.  
  
> [!NOTE]  
> 리소스 파트너 조직에서 페더레이션 서버 컴퓨터를 설정 하려면 먼저 리소스 파트너 조직의 Active Directory 도메인에 컴퓨터를 가입 시켜야 합니다. 자세한 내용은 [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)

