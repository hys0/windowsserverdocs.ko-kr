---
ms.assetid: d0ba3c0d-869f-4e24-89d7-499da7576f22
title: 계정 파트너에서 페더레이션 서버의 역할 검토
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0914d32e8f24d5e7db0a25c733342c1bde3e0329
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835134"
---
# <a name="review-the-role-of-the-federation-server-in-the-account-partner"></a>계정 파트너에서 페더레이션 서버의 역할 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services에서 페더레이션 서버 \(AD FS\) 보안 토큰 발급자로 작동 합니다. 페더레이션 서버 값 특성을 로컬에 상주 하는 저장소 계정에 따라 클레임을 생성 하 고 사용자가 웹을 원활 하 게 액세스할 수 있도록 보안 토큰에 패키지\-브라우저\-기반 응용 프로그램 \(를 사용 하 여 single\-대 \(SSO\) \) 리소스 파트너 조직에서 호스트 되는 합니다.  
  
> [!NOTE]  
> 페더레이션 서버는 웹에 대 한 로그온 상태를 유지 하기 위해 사용자에 게 쿠키를 자동으로 발급 사용자가 웹 브라우저를 사용 하 여 페더레이션된 응용 프로그램에 액세스할 때\-브라우저\-기반 응용 프로그램입니다. 이러한 쿠키는 사용자에 대한 클레임을 포함합니다. 사용자가 다른 웹을 방문할 때마다 자격 증명을 입력 하지 않아도 되도록 SSO 기능을 사용 하는 쿠키\-브라우저\-기반 리소스 파트너의 응용 프로그램입니다.  
  
웹 SSO 디자인에서는 경계 네트워크를 사용 하 여 인터넷 사용자가 응용 프로그램에 액세스할 수 있도록 하는 조직은 경계 네트워크의 페더레이션 서버 프록시를 설치 해야 합니다. 페더레이션된 웹 SSO 디자인에서는 계정 파트너 조직의 회사 네트워크에 설치 된 하나 이상의 페더레이션 서버 및 리소스 파트너 조직의 회사 네트워크에 설치 하는 페더레이션 서버가 하나 이상 있어야 합니다.  
  
> [!NOTE]  
> 계정 파트너 조직의 페더레이션 서버 컴퓨터를 설정할 수 있습니다, 전에 페더레이션 서버를 사용 하는 해당 포리스트에서 사용자를에서 인증 하는 위치 Active Directory 포리스트의 모든 도메인에 컴퓨터를 연결 해야 합니다. 자세한 내용은 참조 하세요. [검사 목록: 페더레이션 서버를 설정할](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의에서 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
