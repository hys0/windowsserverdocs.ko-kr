---
ms.assetid: 1b3a03c0-5558-4177-9b2f-e9d6ce3271cd
title: 계정 파트너에서 페더레이션 서버 프록시의 역할 검토
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: eb0547ac1d84fffed31360f0ee510504510c24ce
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867673"
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-account-partner"></a>계정 파트너에서 페더레이션 서버 프록시의 역할 검토

Active Directory Federation Services \(ADFS\) 의 계정 파트너 조직의 경계 네트워크에 있는 페더레이션 서버 프록시의 주 역할은 로그온 하는 클라이언트 컴퓨터에서 인증 자격 증명을 수집 하는 것입니다. 인터넷을 통해 및 계정 파트너 조직의 회사 네트워크 내부에 있는 페더레이션 서버에 이러한 자격 증명을 전달 합니다. 클라이언트 컴퓨터의 계정은 계정 파트너의 특성 저장소에 저장 됩니다.  
  
또한 페더레이션 서버 프록시는 계정 파트너 조직의 요구를 충족 하도록 구성 하는 방법에 따라 다음 역할 중 하나 이상으로 작동할 수 있습니다.  
  
-   릴레이 보안 토큰-페더레이션 서버는 페더레이션 서버 프록시에 보안 토큰을 발급 합니다. 그러면 페더레이션 서버는이 토큰을 클라이언트 컴퓨터에 릴레이 합니다. 보안 토큰은 해당 클라이언트 컴퓨터에 특정 신뢰 당사자에 대한 액세스 권한을 제공하기 위해 사용됩니다.  
  
-   자격 증명 수집-페더레이션 서버 프록시는 기본 \(클라이언트 로그온 웹 폼\) 을 사용 하 여 폼\-기반 인증을\-통해 암호 기반 자격 증명을 수집 합니다. 그러나 SSL(Secure Sockets Layer) \(SSL\) 클라이언트 인증 등의 지원 되는 다른 인증 형식을 허용 하도록이 양식을 사용자 지정할 수 있습니다. 이 페이지를 사용자 지정 하는 방법에 대 한 자세한 내용은 클라이언트 로그온 및 홈 영역 검색 \(페이지 사용자 지정 [http\/: go.microsoft.com\/fwlink\/?를 참조 하세요.\/ LinkId\=104275](https://go.microsoft.com/fwlink/?LinkId=104275).\) 페더레이션 서버 프록시는 Windows 통합 인증을 통해 자격 증명을 허용 하지 않습니다.  
  
요약 하면 계정 파트너의 페더레이션 서버 프록시는 회사 네트워크에 있는 페더레이션 서버에 대 한 클라이언트 로그온을 위한 프록시 역할을 합니다. 또한 페더레이션 서버 프록시는 신뢰 당사자를 대상으로 하는 인터넷 클라이언트에 대 한 보안 토큰 배포를 용이 하 게 합니다.  
  
> [!CAUTION]  
> 계정 파트너 엑스트라넷에서 페더레이션 서버 프록시를 노출 하면 인터넷에 액세스할 수 있는 모든 사용자가 클라이언트 로그온 웹 폼에 액세스할 수 있습니다. 이렇게 하면 조직이 회사에 저장 된 사용자 계정에\-대 한 계정 잠금을 트리거할 수 있는 사전 공격 또는 무차별 암호 대입 공격과 같은 일부 암호 기반 공격에 취약 해질 수 있습니다 Active Directory 도메인 서비스 \(ADDS\)입니다.  
  

## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
