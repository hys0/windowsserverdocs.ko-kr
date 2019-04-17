---
ms.assetid: f88238ea-d851-4129-8b4e-a3a62b813614
title: "해당 Federation 서버의 리소스 파트너에 역할을 검토"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6d4c7763d7204dd2340d10a234e48f47c96788dc
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>해당 Federation 서버의 리소스 파트너에 역할을 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Federation 서버 리소스 파트너 조직 가로챕니다 수신 보안 토큰을 계정 federation 서버, 전송에 유효성을 검사 하 고, 로그인을 표시 한 다음 Web\ 기반 응용 프로그램에 대 한로 전송 된 보안 토큰 고유한 합니다.  
  
> [!NOTE]  
> 연결 된 사용자가 웹 브라우저를 사용 하 여 Web\ 기반 응용 프로그램에 액세스를 리소스 파트너 조직에서 federation 서버 인증 쿠키를 새 빌드를 하 고 브라우저 기록 합니다. 이 쿠키는 사용자가 수행 하지 않도록에 로그온 할 다시 federation 서버 계정 파트너에는 사용자가 다른 Web\ 기반 응용 프로그램 리소스 파트너에 액세스 하려고 하면 \(SSO\) 기능 single\ sign\-켜 짐 수 있습니다.  
  
웹 SSO 디자인에서 하나 이상의 federation 서버 주변 네트워크에 설치 되어야 합니다. 웹 SSO 연방 디자인에 회사 계정 파트너 회사의 네트워크에 설치 된 하나 이상 federation 서버 및 리소스 파트너 회사의 회사 네트워크에 설치 된 하나 이상 federation 서버 있어야 합니다.  
  
> [!NOTE]  
> 리소스 파트너 조직에서 federation 서버 컴퓨터를 설정 하기 전에 리소스 파트너 조직에서 된 Active Directory 도메인 컴퓨터를 연결 해야 합니다. 자세한 내용은 참조 [검사: Federation 서버 설정을](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)

