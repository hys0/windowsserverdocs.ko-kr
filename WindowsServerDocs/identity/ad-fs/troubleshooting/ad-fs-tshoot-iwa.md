---
title: 통합 Windows 인증을 AD FS 문제 해결-
description: 이 문서에서는 windows 통합된 인증 문제를 해결 하는 방법 설명
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9703a8652b0e0bbafe48858cbfbcc8aa9aa31ef8
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812052"
---
# <a name="ad-fs-troubleshooting---integrated-windows-authentication"></a>통합 Windows 인증을 AD FS 문제 해결-
통합된 Windows 인증 사용자가 Windows 자격 증명 및 환경 single sign-on (SSO), Kerberos 또는 NTLM을 사용 하 여 로그인 할 수 있습니다.

## <a name="reason-integrated-windows-authentication-fails"></a>따라서 windows 통합된 인증에 실패
Windows 통합된 인증에 실패 하는 이유 세 가지 주요 이유가 있습니다. 구현되지 않은 것은 다음과 같습니다.
    - Spn (서비스 주체 (이름) 잘못 된 구성
    - 채널 바인딩 토큰
    - Internet Explorer 구성

## <a name="spn-misconfiguration"></a>SPN 구성 오류
서비스 사용자 이름 (SPN)에 서비스 인스턴스는 고유 식별자입니다. Spn은 서비스 로그온 계정을 사용 하 여 서비스 인스턴스 연결에 Kerberos 인증에서 사용 됩니다. 이렇게 하면 클라이언트에 계정 이름이 없는 경우에 서비스가 계정을 인증을 요청 하려면 클라이언트 응용 프로그램을 수 있습니다.

사용 하 여 SPN이 사용 됩니다 하는 방법의 예로 AD FS는 다음과 같습니다.
1. 웹 브라우저는 서비스 계정: sts.contoso.com 실행 중인지 확인 하려면 Active Directory 쿼리
2. Active Directory AD FS 서비스 계정에는 브라우저를 알립니다.
3. 브라우저에는 AD FS 서비스 계정에 대 한 Kerberos 티켓을 받게 됩니다.

AD FS 서비스 계정에는 잘못 구성 되거나 잘못 된 SPN 문제가 발생할 수 있습니다이 있습니다.  네트워크 추적을 살펴보면 KRB 오류와 같은 오류가 표시 될 수 있습니다. KRB5KDC_ERR_S_PRINCIPAL_UNKNOWN.

네트워크 추적 (예: Wireshark)를 사용 하 여 확인할 수 있습니다 어떤 브라우저를 확인 하려고 합니다. SPN 및 명령줄을 사용 하 여 다음 도구를 setspn-Q <spn>, SPN 조회 하는 조회를 수행할 수 있습니다.  찾을 수 있습니다 또는 AD FS 서비스 계정이 아닌 다른 계정을 할당할 수 있습니다.

![통합](media/ad-fs-tshoot-iwa/iwa3.png)

AD FS 서비스 계정의 속성을 확인 하 여 SPN을 확인할 수 있습니다.

![통합](media/ad-fs-tshoot-iwa/iwa1.png)

## <a name="channel-binding-token"></a>채널 바인딩 토큰
현재 클라이언트 응용 프로그램에 자체 인증 Kerberos, Digest 또는 HTTPS를 사용 하 여 NTLM을 사용 하 여 서버에 전송 수준 보안 (TLS) 채널이 먼저 설정 되며 및이 채널을 사용해 인증이 진행 됩니다. 

채널 바인딩 토큰은 TLS로 보호 되는 외부 채널의, 속성 및 클라이언트를 인증 하는 내부 채널을 통해 대화에 외부 채널을 바인딩하는 데 사용 됩니다.

없을 경우 발생 하는 "man-에--the-middle" 공격 되며 de 암호화 및 SSL 트래픽을 다시 암호화 한 다음 키 일치 하지 않게 됩니다.  AD FS 웹 찾아보기 r 자체 사이의 중간에 앉아 항목 인지 결정 됩니다.  이렇게 하면 실패에 대 한 Kerberos 인증 및 SSO 환경 대신 401 대화 상자를 사용 하 여 묻는 메시지가 사용자입니다.

이 인해 발생할 수 있습니다.
 - 모든 AD FS 브라우저 사이의 작업할 것입니다.
 - Fiddler
 - SSL 브리징을 수행 하는 역방향 프록시

기본적으로 AD FS의 "허용"으로 설정 합니다.  PowerShell cmdlt을 사용 하 여이 설정을 변경할 수 있습니다. `Set-ADFSProperties -ExtendProtectionTokenCheck`

이 참조에 대 한 자세한 내용은 [AD FS의 보안 계획 및 배포에 대 한 모범 사례](../../ad-fs/design/best-practices-for-secure-planning-and-deployment-of-ad-fs.md)합니다.

## <a name="internet-explorer-configuration"></a>Internet Explorer 구성
기본적으로 Internet explorer 같은 방식으로 적용 됩니다.

1. Internet explorer에는 헤더에 있는 단어 협상을 사용 하 여 AD FS에서 401 응답을 받습니다.
2. 그러면 웹 브라우저를 AD FS에 다시 전송할 NTLM 또는 Kerberos 티켓을 가져옵니다.
3. 기본적으로 IE 단어 협상에에서 있으면 헤더 (SPNEGO)이 사용자 상호 작용 없이 수행 하려고 합니다.  인트라넷 사이트에만 작동 합니다.

두 가지 주요 happeing에서이 방지할 수는 있습니다.
   - 통합된 Windows 인증 사용 IE의 속성에서 확인 하지 않습니다.  -> 인터넷 옵션 아래에 있는이 고급-> 보안 합니다.
   
   ![통합](media/ad-fs-tshoot-iwa/iwa4.png)
   
   - 보안 영역 올바르게 구성 되지 않습니다.
       - Fqdn은 인트라넷 영역에 있지 않습니다.
       - AD FS URL을 인트라넷 영역에 없는 경우

      ![통합](media/ad-fs-tshoot-iwa/iwa5.png)
## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)
