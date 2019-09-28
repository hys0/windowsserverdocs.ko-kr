---
title: AD FS 문제 해결-Azure AD
description: 이 문서에서는 AD FS 및 Azure AD의 다양 한 측면을 해결 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/01/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 293618b3fe2a24caff8fd6b52c5528cc699f93de
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407285"
---
# <a name="ad-fs-troubleshooting---azure-ad"></a>AD FS 문제 해결-Azure AD
클라우드의 성장으로 많은 회사에서 다양 한 앱 및 서비스에 대해 Azure AD를 사용 하도록 이동 했습니다.  Azure AD를 사용 하 여 페더레이션 하는 것은 많은 조직에서 표준 관행으로 사용 됩니다.  이 문서에서는이 페더레이션에서 발생 하는 문제 해결에 대 한 몇 가지 측면을 다룹니다.  일반적인 문제 해결 문서의 몇 가지 항목은 여전히 Azure와의 페더레이션과 관련 되어 있으므로이 문서는 Azure AD 및 AD FS 상호 작용에 대 한 구체적인 내용만 중점적으로 다룹니다.

## <a name="redirection-to-ad-fs"></a>AD FS로 리디렉션
리디렉션은 Office 365와 같은 응용 프로그램에 로그인 하면 조직 AD FS 서버에 로그인 할 때 "리디렉션되"는 경우에 발생 합니다.

![](media/ad-fs-tshoot-azure/azure1.png)


### <a name="first-things-to-check"></a>먼저 확인 해야 할 사항
리디렉션이 발생 하지 않는 경우 확인할 몇 가지 항목이 있습니다.

   1. Azure Portal에 로그인 하 고 Azure AD Connect에서 확인 하 여 Azure AD 테 넌 트가 페더레이션을 사용 하도록 설정 되었는지 확인 합니다.

![](media/ad-fs-tshoot-azure/azure2.png)

1. Azure Portal의 페더레이션 옆에 있는 도메인을 클릭 하 여 사용자 지정 도메인을 확인 해야 합니다.
   ![](media/ad-fs-tshoot-azure/azure3.png)

2. 마지막으로 [DNS](ad-fs-tshoot-dns.md) 를 확인 하 고 AD FS 서버 또는 WAP 서버를 인터넷에서 확인 하 고 있는지 확인 합니다.  이를 확인 하 고 탐색할 수 있는지 확인 합니다.
3. PowerShell cmdlet `Get-AzureADDomain`을 사용 하 여이 정보를 가져올 수도 있습니다.

![](media/ad-fs-tshoot-azure/azure6.png)

### <a name="you-are-receiving-an-unknown-auth-method-error"></a>알 수 없는 인증 방법 오류를 수신 하 고 있습니다.
Azure에서 리디렉션되는 경우 AD FS 또는 STS 수준에서 Authn 컨텍스트가 지원 되지 않는다는 "알 수 없는 인증 방법" 오류가 발생할 수 있습니다. 

이는 인증 방법을 적용 하는 매개 변수를 사용 하 여 Azure AD가 AD FS 또는 STS로 리디렉션하는 경우 가장 일반적입니다. 

인증 방법을 적용 하려면 다음 방법 중 하나를 사용 합니다.
- WS-FEDERATION의 경우 WAUTH 쿼리 문자열을 사용 하 여 기본 인증 방법을 강제로 적용 합니다.

- SAML 2.0의 경우 다음을 사용 합니다.
  ```
  <saml:AuthnContext>
  <saml:AuthnContextClassRef>
  urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport
  </saml:AuthnContextClassRef>
  </saml:AuthnContext>
  ```
  적용 된 인증 방법이 잘못 된 값으로 전송 되거나 AD FS 또는 STS에서 해당 인증 방법이 지원 되지 않는 경우 인증 되기 전에 오류 메시지가 표시 됩니다.

|필요한 인증 방법|wauth URI|
|-----|-----|
|사용자 이름 및 암호 인증|urn:oasis:names:tc:SAML:1.0:am:password|
|SSL 클라이언트 인증|urn:ietf:rfc:2246|
|Windows 통합 인증|urn: 페더레이션: 인증: windows|

지원 되는 SAML 인증 컨텍스트 클래스

|인증 방법|인증 컨텍스트 클래스 URI|
|-----|-----| 
|사용자 이름 및 암호|urn: oasis: names: tc: SAML: 2.0: ac: 클래스: 암호|
|암호로 보호 된 전송|urn: oasis: names: tc: SAML: 2.0: ac: 클래스: PasswordProtectedTransport|
|TLS (전송 계층 보안) 클라이언트|urn: oasis: names: tc: SAML: 2.0: ac: 클래스: TLSClient
|X.509 certificate(X.509 인증서)|urn: oasis: names: tc: SAML: 2.0: ac: 클래스: X509
|Windows 통합 인증|urn: 페더레이션: 인증: windows|
|Kerberos|urn: oasis: names: tc: SAML: 2.0: ac: 클래스: Kerberos|

AD FS 수준에서 인증 방법이 지원 되는지 확인 하려면 다음을 확인 합니다.

#### <a name="ad-fs-20"></a>AD FS 2.0 

**/Adfs/ls/web.config**에서 인증 형식에 대 한 항목이 있는지 확인 합니다.

```
<microsoft.identityServer.web>
<localAuthenticationTypes>
<add name="Forms" page="FormsSignIn.aspx" />
<add name="Integrated" page="auth/integrated/" />
<add name="TlsClient" page="auth/sslclient/" />
<add name="Basic" page="auth/basic/" />
</localAuthenticationTypes>
```

#### <a name="ad-fs-2012-r2"></a>AD FS 2012 R2

**AD FS 관리**에서 AD FS 스냅인의 **인증 정책** 을 클릭 합니다.

**기본 인증** 섹션에서 전역 설정 옆의 편집을 클릭 합니다. 인증 정책을 마우스 오른쪽 단추로 클릭 한 다음 전역 기본 인증 편집을 선택할 수도 있습니다. 또는 작업 창에서 전역 기본 인증 편집을 선택 합니다.

전역 인증 정책 편집 창의 기본 탭에서 설정을 전역 인증 정책의 일부로 구성할 수 있습니다. 예를 들어 기본 인증의 경우 엑스트라넷 및 인트라넷에서 사용 가능한 인증 방법을 선택할 수 있습니다.

\* * 필수 인증 방법 확인란이 선택 되어 있는지 확인 합니다. 

#### <a name="ad-fs-2016"></a>AD FS 2016

**AD FS 관리**에서 AD FS 스냅인의 **서비스** 및 **인증 방법** 을 클릭 합니다.

**기본 인증** 섹션에서 편집을 클릭 합니다.

**인증 방법 편집** 창의 기본 탭에서 설정을 인증 정책의 일부로 구성할 수 있습니다.

![](media/ad-fs-tshoot-azure/azure4.png)

## <a name="tokens-issued-by-ad-fs"></a>AD FS에서 발급 한 토큰

### <a name="azure-ad-throws-error-after-token-issuance"></a>토큰 발급 후 Azure AD가 오류를 throw 합니다.
AD FS에서 토큰을 발급 한 후에는 Azure AD에서 오류를 throw 할 수 있습니다. 이 경우 다음과 같은 문제가 있는지 확인 하십시오.
- 토큰의 AD FS에서 발급 하는 클레임은 Azure AD에서 사용자의 각 특성과 일치 해야 합니다.
- Azure AD의 토큰은 다음과 같은 필수 클레임을 포함 해야 합니다.
    - WSFED 
        - UPN 이 클레임의 값은 Azure AD 사용자의 UPN과 일치 해야 합니다.
        - ImmutableID 이 클레임의 값은 Azure AD에서 사용자의 sourceAnchor 또는 ImmutableID와 일치 해야 합니다.

Azure AD에서 사용자 특성 값을 가져오려면 다음 명령줄을 실행 합니다. `Get-AzureADUser –UserPrincipalName <UPN>`

![](media/ad-fs-tshoot-azure/azure5.png)

   - SAML 2.0:
       - IDPEmail 이 클레임의 값은 Azure AD 사용자의 사용자 계정 이름과 일치 해야 합니다.
       - NAMEID 이 클레임의 값은 Azure AD에서 사용자의 sourceAnchor 또는 ImmutableID와 일치 해야 합니다.

자세한 내용은 [SAML 2.0 id 공급자를 사용 하 여 Single Sign-On 구현](https://technet.microsoft.com/library/dn641269.aspx)을 참조 하세요.

### <a name="token-signing-certificate-mismatch-between-ad-fs-and-azure-ad"></a>AD FS와 Azure AD 간에 토큰 서명 인증서가 일치 하지 않습니다.

AD FS는 토큰 서명 인증서를 사용 하 여 사용자 또는 응용 프로그램에 전송 된 토큰에 서명 합니다. AD FS와 Azure AD 간의 트러스트는이 토큰 서명 인증서를 기반으로 하는 페더레이션된 트러스트입니다.

그러나 자동 인증서 롤오버가 나 특정 작업으로 인해 AD FS 쪽의 토큰 서명 인증서가 변경 된 경우에는 페더레이션된 도메인에 대해 Azure AD 쪽에서 새 인증서의 세부 정보를 업데이트 해야 합니다. AD FS의 기본 토큰 서명 인증서가 Azure AD와 다른 경우 AD FS에서 발급 한 토큰은 Azure AD에서 신뢰할 수 없습니다. 따라서 페더레이션된 사용자는 로그온 할 수 없습니다.

이 문제를 해결 하려면 [Office 365에 대 한 페더레이션 인증서 갱신 및 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs)의 단계 개요를 사용할 수 있습니다.

## <a name="other-common-things-to-check"></a>확인할 다른 일반적인 사항
다음은 AD FS 및 Azure AD 상호 작용에 문제가 있는지 확인 하는 데 도움이 되는 빠른 목록입니다.
- Windows 자격 증명 관리자에서 부실 하거나 캐시 된 자격 증명
- Office 365에 대 한 신뢰 당사자 트러스트에 구성 된 보안 해시 알고리즘이 SHA1로 설정 되어 있습니다.

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)