---
ms.assetid: 1b3a03c0-5558-4177-9b2f-e9d6ce3271cd
title: "계정 파트너의 Federation 서버 프록시 역할을 검토"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d2b60ce593c2ca7eb902595ee6a42850cb7605d9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-account-partner"></a>계정 파트너의 Federation 서버 프록시 역할을 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기본 역할로 주변 Active Directory Federation Services \(AD FS\)에서 계정 파트너 회사의 네트워크에 federation 서버 프록시 인증 자격 증명은 인터넷을 통해 로그온 하는 클라이언트 컴퓨터에서 수집 하 고 해당 자격 증명 회사 계정 파트너 회사의 네트워크 안에 있는 federation 서버에 전달 하입니다. 컴퓨터에 대 한 계정은 계정 파트너의 특성 스토어에 저장 됩니다.  
  
Federation 서버 프록시 계정 파트너 회사의 요구를 충족 하 고 구성 하는 방법에 따라 다음과 같은 역할을 한 곳 이상에 작동할 수 있습니다.  
  
-   보안 토큰 릴레이-federation 서버 보안 토큰 클라이언트 컴퓨터로 토큰을 릴레이 federation 프록시 서버에 문제가 있습니다. 보안 토큰 특정 당사자에 해당 클라이언트 컴퓨터에 대 한 액세스를 제공 하기 위해 사용 됩니다.  
  
-   수집 자격 증명을 federation 서버 프록시 기본 클라이언트 로그온 웹 양식 \(clientlogon.aspx\) password\ 기반 자격 증명 forms\ 기반 인증을 통해 수집을 사용 하 여 합니다. 그러나이 양식 지원 되는 다른 유형의 주소 \(SSL\) 클라이언트 인증와 같이 인증을 수락 사용자 지정할 수 있습니다. 이 페이지를 사용자 지정 하는 방법에 대 한 자세한 내용은 참조 클라이언트 로그온 사용자 지정 하 고 영역 검색 페이지 정의 \ ([http:///\/go.microsoft.com\/fwlink\/ 있나요? LinkId\ 104275 =](https://go.microsoft.com/fwlink/?LinkId=104275)\). Federation 서버 프록시 Windows 통합 인증 통해 자격 증명을 받지 않습니다.  
  
요약 계정 파트너는 federation 서버 프록시 회사 네트워크에 있는 federation 서버에 대 한 클라이언트 로그온에 대 한 프록시 역할을 합니다. 또한 federation 서버 프록시 인터넷 클라이언트 신뢰 당사자에 대 한로 전송 된 보안 토큰 배포 쉽게 수 있습니다.  
  
> [!CAUTION]  
> 익스트라넷 계정 파트너에는 federation 서버 프록시 노출 클라이언트 로그온 인터넷 있는 사용자가 액세스할 수 있는 웹 양식에 액세스 합니다. 이 수 있는 잠재적 조직에 감염 일부 password\ 기반 등의 공격을 사전 공격이 나 공격 계정 잠금을 Active Directory Domain Services 회사 저장 되어 있는 사용자 계정에 대 한 시작할 수 있는 \ (AD DS \).  
  

## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
