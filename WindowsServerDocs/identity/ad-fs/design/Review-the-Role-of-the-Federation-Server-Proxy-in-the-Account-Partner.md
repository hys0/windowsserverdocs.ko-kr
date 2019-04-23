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
ms.openlocfilehash: d2b60ce593c2ca7eb902595ee6a42850cb7605d9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870844"
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-account-partner"></a>계정 파트너에서 페더레이션 서버 프록시의 역할 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services에서 계정 파트너 조직의 경계 네트워크의 페더레이션 서버 프록시의 기본 역할 \(AD FS\) 로그온 하는 클라이언트 컴퓨터에서 인증 자격 증명을 수집 하는 것 인터넷을 통해 및 페더레이션 서버에 이러한 자격 증명을 전달 하는 계정 파트너 조직의 회사 네트워크 내부 있는 합니다. 클라이언트 컴퓨터용 계정은 계정 파트너의 특성 저장소에 저장됩니다.  
  
페더레이션 서버 프록시 계정 파트너 조직의 요구에 맞게 구성 하는 방법에 따라 다음 역할 중 하나 이상에서 작동할 수도 있습니다.  
  
-   보안 토큰 릴레이-페더레이션 서버는 다음 클라이언트 컴퓨터에 토큰을 릴레이 하는 페더레이션 서버 프록시에 보안 토큰을 발급 합니다. 보안 토큰은 해당 클라이언트 컴퓨터에 특정 신뢰 당사자에 대한 액세스 권한을 제공하기 위해 사용됩니다.  
  
-   자격 증명 수집-페더레이션 서버 프록시에 기본 클라이언트 로그온 웹 폼을 사용 하 여 \(clientlogon.aspx\) 암호를 수집 하도록\-기반 폼을 통해 자격 증명\-기반 인증. 지원 되는 다른 형식의 Secure Sockets Layer 같은 인증을 허용 하도록이 양식을 사용자 지정할 수는 있지만 \(SSL\) 클라이언트 인증입니다. 이 페이지를 사용자 지정 하는 방법에 대 한 자세한 내용은 사용자 지정 클라이언트 로그온 및 홈 영역 검색 페이지를 참조 하세요. \( [http:\/\/이 포트는 go.microsoft.com\/fwlink\/? LinkId\=104275](https://go.microsoft.com/fwlink/?LinkId=104275)\)합니다. 페더레이션 서버 프록시는 Windows 통합 인증을 통해 자격 증명을 허용 하지 않습니다.  
  
요약 하자면, 계정 파트너에서 페더레이션 서버 프록시를 회사 네트워크에 있는 페더레이션 서버에 로그온 하는 클라이언트에 대 한 프록시로 작동 합니다. 페더레이션 서버 프록시는 또한 신뢰 당사자에 대해 대상이 지정 된 인터넷 클라이언트에 보안 토큰의 배포를 지원 합니다.  
  
> [!CAUTION]  
> 인터넷을 사용 하 여 누구나 액세스할 수 있는 Web form 클라이언트 로그온 액세스 계정 파트너 엑스트라넷에서 페더레이션 서버 프록시를 노출 합니다. 이 잠재적으로 조직의 취약 한 상태로 몇 가지 암호\-기반 공격을 사전 공격 또는 무차별 대입 공격 회사 Active Directory 도메인에 저장 된 사용자 계정에 대 한 계정 잠금을 트리거할 수 있는 같은 서비스 \(AD DS\)합니다.  
  

## <a name="see-also"></a>관련 항목
[Windows Server 2012의에서 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
