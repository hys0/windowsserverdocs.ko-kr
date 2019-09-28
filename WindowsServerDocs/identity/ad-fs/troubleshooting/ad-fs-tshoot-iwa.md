---
title: AD FS 문제 해결-Windows 통합 인증
description: 이 문서에서는 windows 통합 인증 문제를 해결 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 98f6c2e39b2a5eeab76103c1ae477dde785a0e04
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385387"
---
# <a name="ad-fs-troubleshooting---integrated-windows-authentication"></a>AD FS 문제 해결-Windows 통합 인증
Windows 통합 인증을 사용 하면 사용자가 Windows 자격 증명을 사용 하 여 로그인 하 고 Kerberos 또는 NTLM을 사용 하 여 SSO (single sign-on)를 경험할 수 있습니다.

## <a name="reason-integrated-windows-authentication-fails"></a>Windows 통합 인증이 실패 하는 이유
Windows 통합 인증이 실패 하는 세 가지 주요 이유가 있습니다. 구현되지 않은 것은 다음과 같습니다.
    - SPN (서비스 사용자 이름)이 잘못 구성 되었습니다.
    - 채널 바인딩 토큰
    - Internet Explorer 구성

## <a name="spn-misconfiguration"></a>SPN 잘못 구성
SPN (서비스 사용자 이름)은 서비스 인스턴스의 고유 식별자입니다. Spn은 Kerberos 인증에서 서비스 인스턴스를 서비스 로그온 계정과 연결 하는 데 사용 됩니다. 이를 통해 클라이언트 응용 프로그램은 클라이언트에 계정 이름이 없는 경우에도 서비스에서 계정을 인증 하도록 요청할 수 있습니다.

SPN을 AD FS와 함께 사용 하는 방법의 예는 다음과 같습니다.
1. Sts.contoso.com를 실행 하는 서비스 계정을 결정 하는 웹 브라우저 Active Directory 쿼리
2. Active Directory는 브라우저에 AD FS 서비스 계정 임을 알립니다.
3. 브라우저는 AD FS 서비스 계정에 대 한 Kerberos 티켓을 가져옵니다.

AD FS 서비스 계정에 잘못 구성 되었거나 잘못 된 SPN이 있는 경우 문제가 발생할 수 있습니다.  네트워크 추적을 살펴보면 KRB 오류와 같은 오류가 표시 될 수 있습니다. KRB5KDC_ERR_S_PRINCIPAL_UNKNOWN.

네트워크 추적 (예: Wireshark)을 사용 하 여 브라우저에서 해결 하려고 하는 SPN을 확인 하 고 명령줄 도구인 setspn-Q <spn>을 사용 하 여 해당 SPN을 조회할 수 있습니다.  찾을 수 없거나 AD FS 서비스 계정이 아닌 다른 계정에 할당할 수 있습니다.

![통합형](media/ad-fs-tshoot-iwa/iwa3.png)

AD FS 서비스 계정의 속성을 확인 하 여 SPN을 확인할 수 있습니다.

![통합형](media/ad-fs-tshoot-iwa/iwa1.png)

## <a name="channel-binding-token"></a>채널 바인딩 토큰
현재 클라이언트 응용 프로그램이 Kerberos, 다이제스트 또는 HTTPS를 사용 하는 NTLM을 사용 하 여 서버에 인증 하는 경우 TLS (전송 수준 보안) 채널이 먼저 설정 되 고이 채널을 사용 하 여 인증이 수행 됩니다. 

채널 바인딩 토큰은 TLS 보안 외부 채널의 속성 이며, 외부 채널을 클라이언트 인증 내부 채널을 통해 대화에 바인딩하는 데 사용 됩니다.

"메시지 가로채기 (man-in-the-middle)" 공격이 발생 하 고 crypting 하 여 SSL 트래픽을 다시 암호화 하는 경우 키가 일치 하지 않습니다.  AD FS는 웹 찾아보기 r과 자체 사이에 있는 내용이 있음을 확인 합니다.  이로 인해 Kerberos 인증이 실패 하 고 사용자에 게 SSO 환경 대신 401 대화 상자가 표시 됩니다.

이는 다음과 같은 경우에 발생할 수 있습니다.
 - 브라우저와 AD FS 사이에 있는 모든 항목
 - Fiddler
 - SSL 브리징을 수행 하는 역방향 프록시

기본적으로 AD FS는 "허용"으로 설정 되어 있습니다.  PowerShell cmdlet `Set-ADFSProperties -ExtendProtectionTokenCheck`을 사용 하 여이 설정을 변경할 수 있습니다.

이에 대 한 자세한 내용은 [AD FS의 보안 계획 및 배포에 대 한 모범 사례](../../ad-fs/design/best-practices-for-secure-planning-and-deployment-of-ad-fs.md)를 참조 하세요.

## <a name="internet-explorer-configuration"></a>Internet Explorer 구성
기본적으로 Internet explorer는 다음과 같은 방식으로 수행 됩니다.

1. Internet explorer는 헤더에서 NEGOTIATE 이라는 단어를 사용 하 여 AD FS에서 401 응답을 받게 됩니다.
2. 그러면 웹 브라우저에서 Kerberos 또는 NTLM 티켓을 가져와 AD FS으로 다시 보낼 수 있습니다.
3. 기본적으로 IE는 헤더에 단어 NEGOTIATE가 있는 경우 사용자 개입 없이이 작업을 수행 하려고 합니다 (SPNEGO).  인트라넷 사이트에만 적용 됩니다.

Happeing에서이를 방지할 수 있는 두 가지 주요 작업이 있습니다.
   - IE의 속성에서는 Windows 통합 인증 사용이 선택 되어 있지 않습니다.  인터넷 옵션-> 고급 > 보안에 있습니다.
   
   ![통합형](media/ad-fs-tshoot-iwa/iwa4.png)
   
   - 보안 영역이 제대로 구성 되지 않았습니다.
       - Fqdn이 인트라넷 영역에 없습니다.
       - AD FS URL이 인트라넷 영역에 없습니다.

      ![통합형](media/ad-fs-tshoot-iwa/iwa5.png)
## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)
