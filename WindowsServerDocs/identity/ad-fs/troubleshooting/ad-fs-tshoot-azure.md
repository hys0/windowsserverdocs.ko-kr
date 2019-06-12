---
title: AD FS 문제 해결-Azure AD
description: 이 문서에서는 AD FS와 Azure AD의 다양 한 측면을 해결 하는 방법 설명
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/01/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 228ef34ab25276c1cf98f9b2b64e997390023c87
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444015"
---
# <a name="ad-fs-troubleshooting---azure-ad"></a>AD FS 문제 해결-Azure AD
클라우드의 증가 사용 하 여 많은 회사가 된 이동 다양 한 앱 및 서비스에 대 한 Azure AD를 사용 합니다.  Azure AD로 페더레이션 여러 조직과 방법이 되었습니다.  이 문서에서는이 페더레이션 사용 하 여 발생 하는 문제 해결의 측면 중 일부를 설명 합니다.  이 문서는 Azure AD 사용 하 여 단순히 세부 사항에 집중할 Azure로 페더레이션에 여전히 관련 일반 문제 해결 문서에서 항목의 여러 및 AD FS 상호 작용 합니다.

## <a name="redirection-to-ad-fs"></a>AD FS로 리디렉션
리디렉션은 Office 365와 같은 응용 프로그램에 로그인 하 고 "리디렉션됩니다" 하는 경우에 발생 조직의 AD FS 서버에 로그인 합니다.

![](media/ad-fs-tshoot-azure/azure1.png)


### <a name="first-things-to-check"></a>확인할 첫 번째 항목
리디렉션 되지 발생 하는 경우는 몇 가지 사항을 확인.

   1. Azure portal에 로그인 하 고 Azure AD Connect에서 확인 하 여 Azure AD 테 넌 트 페더레이션에 대해 활성화 되어 있는지 확인 합니다.

![](media/ad-fs-tshoot-azure/azure2.png)

1. Azure portal에서 페더레이션 옆에 있는 도메인을 클릭 하 여 사용자 지정 도메인이 확인 되는 있는지 확인 합니다.
   ![](media/ad-fs-tshoot-azure/azure3.png)

2. 마지막으로 확인 하려고 [DNS](ad-fs-tshoot-dns.md) WAP 서버나 AD FS 서버는 인터넷에서 해결 하 고 있는지 확인 합니다.  이 해결 되는지가 이미지로 이동할 수 있는지 확인 합니다.
3. PowerShell cmdlt을 사용할 수도 있습니다 `Get-AzureADDomain` 이 정보를 가져올 수도 있습니다.

![](media/ad-fs-tshoot-azure/azure6.png)

### <a name="you-are-receiving-an-unknown-auth-method-error"></a>알 수 없는 인증 메서드 오류가 나타났습니까
Azure에서 리디렉션되면 AuthnContext STS 또는 AD FS 수준에서 지원 되지 않습니다 없다는 "알 수 없는 인증 메서드" 오류가 발생할 수 있습니다. 

가장 일반적인 경우 Azure AD 인증 방법을 적용 하는 매개 변수를 사용 하 여 AD FS 또는 STS로 리디렉션합니다. 

인증 방법에 적용 하려면 다음 방법 중 하나를 사용 합니다.
- WS-페더레이션에 대 한 기본 인증 메서드를 WAUTH 쿼리 문자열을 사용 합니다.

- SAML2.0, 다음을 사용 합니다.
  ```
  <saml:AuthnContext>
  <saml:AuthnContextClassRef>
  urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport
  </saml:AuthnContextClassRef>
  </saml:AuthnContext>
  ```
  잘못 된 값을 사용 하 여 강제 인증 메서드를 보낼 때, AD FS STS에 인증 방법을 지원 되지 않는 경우 인증 된 전에 오류 메시지가 나타납니다.

|원하는 인증 방법|wauth URI|
|-----|-----|
|사용자 이름 및 암호 인증|urn:oasis:names:tc:SAML:1.0:am:password|
|SSL 클라이언트 인증|urn:ietf:rfc:2246|
|Windows 통합 인증|urn:federation:authentication:windows|

지원 되는 SAML 인증 컨텍스트 클래스

|인증 방법|인증 컨텍스트 클래스 URI|
|-----|-----| 
|사용자 이름 및 암호|urn:oasis:names:tc:SAML:2.0:ac:classes:Password|
|암호로 보호 된 전송|urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport|
|전송 계층 보안 (TLS) 클라이언트|urn:oasis:names:tc:SAML:2.0:ac:classes:TLSClient
|X.509 certificate(X.509 인증서)|urn:oasis:names:tc:SAML:2.0:ac:classes:X509
|통합된 Windows 인증|urn:federation:authentication:windows|
|Kerberos|urn:oasis:names:tc:SAML:2.0:ac:classes:Kerberos|

AD FS 수준에서 인증 방법을 지원 되는지 확인을 하려면 다음을 확인 합니다.

#### <a name="ad-fs-20"></a>AD FS 2.0 

아래 **/adfs/ls/web.config**, 인증 형식에 대 한 항목이 있는지 확인 합니다.

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

아래 **AD FS 관리**, 클릭 **인증 정책** 스냅인 AD FS에서.

에 **기본 인증** 섹션, 전역 설정 옆의 편집을 클릭 합니다. 또한 인증 정책을 마우스 오른쪽 단추로 클릭 수 있으며 전역 기본 인증 편집을 선택 합니다. 또는 작업 창에서 전역 기본 인증 편집을 선택 합니다.

전역 인증 정책 편집 창에서 탭의 기본 설정을 전역 인증 정책의 일부로 구성할 수 있습니다. 예를 들어, 기본 인증에 대 한 엑스트라넷 및 인트라넷에서 사용 가능한 인증 방법으로 선택할 수 있습니다.

* * 확인 메서드에 필요한 인증 확인란을 선택 합니다. 

#### <a name="ad-fs-2016"></a>AD FS 2016

아래 **AD FS 관리**, 클릭 **서비스** 하 고 **인증 방법을** 스냅인 AD FS에서.

에 **기본 인증** 섹션에서 편집을 클릭 합니다.

에 **인증 방법을 편집** 창 탭의 기본 설정을 인증 정책의 일부로 구성할 수 있습니다.

![](media/ad-fs-tshoot-azure/azure4.png)

## <a name="tokens-issued-by-ad-fs"></a>AD FS에서 발급 된 토큰

### <a name="azure-ad-throws-error-after-token-issuance"></a>Azure AD 토큰 발급 후 오류가 throw 됩니다.
AD FS 토큰을 발급 한 후 Azure AD는 오류가 발생할 수 있습니다. 이 경우 다음 사항을 확인 합니다.
- 클레임 토큰에서 AD FS에서 발급 한 Azure AD에서 사용자의 해당 특성을 일치 해야 합니다.
- Azure AD에 대 한 토큰에 다음 필수 클레임이 있어야 합니다.
    - WSFED: 
        - UPN: 이 클레임은 Azure AD에서 사용자의 UPN을 일치 해야 합니다.
        - ImmutableID: 이 클레임의 값에는 Azure AD에서 사용자의 ImmutableID를 sourceAnchor 일치 해야 합니다.

Azure AD의 사용자 특성 값을 검색할 다음 명령줄을 실행 합니다. `Get-AzureADUser –UserPrincipalName <UPN>`

![](media/ad-fs-tshoot-azure/azure5.png)

   - SAML 2.0:
       - IDPEmail: 이 클레임의 값에는 Azure AD에서 사용자의 사용자 계정 이름을 일치 해야 합니다.
       - NAMEID: 이 클레임의 값에는 Azure AD에서 사용자의 ImmutableID를 sourceAnchor 일치 해야 합니다.

자세한 내용은 [single sign-on을 구현 하는 SAML 2.0 id 공급자를 사용 하 여](https://technet.microsoft.com/library/dn641269.aspx)입니다.

### <a name="token-signing-certificate-mismatch-between-ad-fs-and-azure-ad"></a>AD FS와 Azure AD 간의 토큰 서명 인증서 불일치

AD FS 토큰 서명 인증서를 사용 하 여 사용자 또는 응용 프로그램에 전송 되는 토큰에 서명 합니다. AD FS와 Azure AD 간의 트러스트는이 토큰 서명 인증서에 기반 하는 페더레이션된 트러스트를 합니다.

그러나 일부 개입 하거나 자동 인증서 롤오버로 인해 AD FS 쪽에서 토큰 서명 인증서 변경 되 면 페더레이션된 도메인에 대 한 Azure AD 쪽에서 새 인증서의 세부 정보 업데이트 되어야 합니다. 기본 토큰 서명 인증서를 AD FS에서 Azure Ad와 다른 경우 AD FS에서 발급 한 토큰이 Azure AD에 의해 신뢰 되지 않습니다. 따라서 페더레이션된 사용자가 로그온 할 수 없습니다.

따르면이 문제를 해결 하는 단계에서 설명 [Office 365 및 Azure Active Directory에 대 한 페더레이션 인증서 갱신](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs)합니다.

## <a name="other-common-things-to-check"></a>확인할 기타 공통 사항
다음은 빠른 목록을 확인 하는 경우 AD FS와 Azure AD 상호 작용을 사용 하 여 문제가 있는 것입니다.
- 부실 또는 캐시 된 관리자의 자격 증명이 Windows 자격 증명
- Office 365에 대 한 신뢰 당사자 트러스트에 구성 되어 있는 보안 해시 알고리즘은 SHA1로 설정

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)