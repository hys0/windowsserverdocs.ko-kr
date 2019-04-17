---
ms.assetid: d0ba3c0d-869f-4e24-89d7-499da7576f22
title: "계정 파트너에 해당 Federation 서버의 역할을 검토"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0914d32e8f24d5e7db0a25c733342c1bde3e0329
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="review-the-role-of-the-federation-server-in-the-account-partner"></a>계정 파트너에 해당 Federation 서버의 역할을 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Federation 서버 Active Directory Federation Services \(AD FS\)에서 보안 토큰 발행인이으로 작동합니다. Federation 서버 클레임 특성을 로컬에 있는 값 스토어 계정에 따라 생성 하 고 사용자가 Web\ browser\ 기반 응용 프로그램을 원활 하 게 액세스할 수 있도록 토큰 보안으로 패키지 \ (단일 sign\ 켜 짐 \(SSO\)\) 리소스 파트너 조직에서 호스트 하는 사용 합니다.  
  
> [!NOTE]  
> 사용자 액세스 웹 브라우저를 사용 하 여 응용 프로그램 연결을 federation 서버 자동으로 쿠키 Web\ browser\ 기반 응용 프로그램에 대 한 자신의 로그온 상태를 유지 하기 위해 사용자에 게 발급 합니다. 이 쿠키는 사용자에 대 한 주장 포함 되어 있습니다. 쿠키는 사용자가 리소스 파트너의 서로 다른 Web\ browser\ 기반 응용 프로그램 방문할 때마다 자격 증명을 입력할 필요가 없습니다 되도록 SSO 기능을 사용 합니다.  
  
웹 SSO 디자인 조직 주변 네트워크와 응용 프로그램에 대 한 액세스를 사용자가 인터넷에는 federation 서버 프록시 주변 네트워크에 설치 해야 합니다. 웹 SSO 연방 디자인에 회사 계정 파트너 회사의 네트워크에 설치 된 하나 이상 federation 서버 및 리소스 파트너 회사의 회사 네트워크에 설치 된 하나 이상 federation 서버 있어야 합니다.  
  
> [!NOTE]  
> 계정 파트너 조직에서 federation 서버 컴퓨터를 설정 하기 전에 해당 숲에서 사용자를 인증 federation 서버는 사용할 Active Directory 숲 속의 모든 도메인에 있는 컴퓨터를 연결 해야 합니다. 자세한 내용은 참조 [검사: Federation 서버 설정을](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
