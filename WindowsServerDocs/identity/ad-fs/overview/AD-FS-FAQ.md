---
ms.assetid: acc9101b-841c-4540-8b3c-62a53869ef7a
title: AD FS FAQ
description: AD FS에 대한 질문과 대답
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 04/17/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a1041bdc189238c7da32896e6f867f730e392d24
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814433"
---
# <a name="ad-fs-frequently-asked-questions-faq"></a>AD FS FAQ(질문과 대답)


다음 설명서는 Active Directory Federation Services와 관련하여 자주 묻는 질문과 대답입니다.  이 문서는 질문 유형에 따라 그룹으로 분할되어 있습니다.

## <a name="deployment"></a>배포

### <a name="how-can-i-upgrademigrate-from-previous-versions-of-ad-fs"></a>이전 버전의 AD FS에서 업그레이드/마이그레이션하는 방법
다음 중 하나를 사용하여 AD FS를 업그레이드할 수 있습니다.


- Windows Server 2012 R2 AD FS에서 Windows Server 2016 AD FS 이상으로 업그레이드. 이 방법론은 Windows Server 2016 AD FS에서 Windows Server 2019 AD FS로 업그레이드하는 경우에도 동일합니다. 
    - [WID 데이터베이스를 사용하여 Windows Server 2016에서 AD FS로 업그레이드](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)
    - [SQL 데이터베이스를 사용하여 Windows Server 2016에서 AD FS로 업그레이드](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL.md)
- Windows Server 2012 AD FS에서 Windows Server 2012 R2 AD FS로 업그레이드
    - [Windows Server 2012 R2에서 AD FS로 마이그레이션](https://technet.microsoft.com/library/dn486815.aspx)
- AD FS 2.0에서 Windows Server 2012 AD FS로 업그레이드
    - [Windows Server 2012에서 AD FS로 마이그레이션](https://technet.microsoft.com/library/jj647765.aspx)
- AD FS 1.x에서 AD FS 2.0으로 업그레이드
    - [AD FS 1.x에서 AD FS 2.0으로 업그레이드](https://technet.microsoft.com/library/ff678035.aspx)

AD FS 2.0 또는 2.1(Windows Server 2008 R2 또는 Windows Server 2012)에서 업그레이드하려면 기본 제공 스크립트(C:\Windows\ADFS에 있음)를 사용해야 합니다.

### <a name="why-does-ad-fs-installation-require-a-reboot-of-the-server"></a>AD FS 설치에서 서버를 다시 부팅해야 하는 이유는 무엇인가요?

HTTP/2 지원이 Windows Server 2016에 추가되었지만, 클라이언트 인증서 인증에는 HTTP/2를 사용할 수 없습니다.  많은 AD FS 시나리오에서 클라이언트 인증서 인증을 사용하고 상당한 수의 클라이언트에서 HTTP/1.1을 사용하여 요청을 다시 시도하도록 지원하지 않으므로 AD FS 팜 구성에서는 로컬 서버의 HTTP 설정을 HTTP/1.1로 다시 구성합니다.  이로 인해 서버를 다시 부팅해야 합니다.  

### <a name="is-using-windows-2016-wap-servers-to-publish-the-ad-fs-farm-to-the-internet-without-upgrading-the-back-end-ad-fs-farm-supported"></a>지원되는 백 엔드 AD FS 팜을 업그레이드하지 않고 Windows 2016 WAP 서버를 사용하여 AD FS 팜을 인터넷에 게시하나요?
예, 이 구성은 지원되지만, 새로운 AD FS 2016 기능이 이 구성에 지원되지 않습니다.  이 구성은 AD FS 2012 R2에서 AD FS 2016으로 마이그레이션하는 단계 중에 일시적으로 수행되며 장기간 배포하면 안 됩니다.

### <a name="is-it-possible-to-deploy-ad-fs-for-office-365-without-publishing-a-proxy-to-office-365"></a>프록시를 Office 365에 게시하지 않고 Office 365용 AD FS를 배포할 수 있나요?
예, 지원됩니다. 하지만 다음과 같이 부작용이 있습니다.

1. Azure AD에서 페더레이션 메타데이터에 액세스할 수 없으므로 토큰 서명 인증서 업데이트를 수동으로 관리해야 합니다. 토큰 서명 인증서를 수동으로 업데이트하는 방법에 대한 자세한 내용은 [Office 365 및 Azure Active Directory에 대한 페더레이션 인증서 갱신](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs)을 참조하세요.
2. 레거시 인증 흐름(예: ExO 프록시 인증 흐름)을 사용할 수 없습니다.

### <a name="what-are-load-balancing-requirements-for-ad-fs-and-wap-servers"></a>AD FS 및 WAP 서버에 대한 부하 분산 요구 사항은 무엇인가요?

AD FS는 상태 비저장 시스템입니다. 따라서 로그인에 대한 부하 분산은 매우 간단합니다. 부하 분산 시스템에 대한 주요 추천 사항은 다음과 같습니다.


- 부하 분산 장치는 IP 선호도를 사용하여 구성하면 안 됩니다. 이로 인해 특정 Exchange Online 시나리오에서 서버의 하위 세트에 과도한 부하가 발생할 수 있습니다.
- 부하 분산 장치는 HTTPS 연결을 종료하고 ADFS 서버에 대한 새 연결을 다시 시작하면 안 됩니다.
- 부하 분산 장치는 ADFS로 보낼 때 HTTP 패킷에서 연결 IP 주소를 원본 IP로 변환해야 합니다. 부하 분산 장치가 HTTP 패킷에서 원본 IP를 보낼 수 없는 경우 부하 분산 장치에서 IP 주소를 x-forwarded-for 헤더에 추가(또는 기존의 경우 추가)해야 합니다. 이는 특정 IP 관련 기능(금지된 IP, 엑스트라넷 스마트 잠금,...)을 올바르게 처리하는 데 필요하며, 부적절하게 구성되면 보안이 저하될 수 있습니다.
- 부하 분산 장치는 SNI를 지원해야 합니다. 그렇지 않으면 AD FS에서 HTTPS 바인딩을 만들어 SNI를 지원하지 않는 클라이언트를 처리하도록 구성되어 있는지 확인합니다.
- 부하 분산 장치는 AD FS HTTP 상태 프로브 엔드포인트를 사용하여 AD FS 또는 WAP 서버가 작동되는지 여부를 확인하고, 200 OK가 반환되지 않으면 해당 서버를 제외해야 합니다.

### <a name="what-multi-forest-configurations-are-supported-by-ad-fs"></a>AD FS에서 지원하는 다중 포리스트 구성은 무엇인가요?

AD FS는 여러 개의 다중 포리스트 구성을 지원하며, 기본 AD DS 트러스트 네트워크를 사용하여 여러 신뢰할 수 있는 영역에서 사용자를 인증합니다. 이는 트러스트 하위 시스템이 문제 없이 제대로 작동하도록 하기 위한 더 간단한 설정이므로 양방향 포리스트 트러스트를 사용하는 것이 좋습니다. 또한

- 파트너 ID가 포함된 DMZ 포리스트와 같은 단방향 포리스트 트러스트의 경우 ADFS를 회사 포리스트에 배포하고, DMZ 포리스트를 LDAP를 통해 연결된 다른 로컬 클레임 공급자 트러스트로 처리하는 것이 좋습니다. 이 경우 Windows 통합 인증은 DMZ 포리스트 사용자에게 작동하지 않으며, LDAP에 유일하게 지원되는 메커니즘이므로 암호 인증을 수행해야 합니다. 이 옵션을 수행할 수 없는 경우 다른 ADFS를 DMZ 포리스트에 설정하고, 이를 클레임 공급자 트러스트로 회사 포리스트의 ADFS에 추가해야 합니다. 사용자는 홈 영역 검색을 수행해야 하지만 Windows 통합 인증 및 암호 인증은 모두 작동합니다. 회사 포리스트의 ADFS는 DMZ 포리스트에서 사용자에 대한 추가 사용자 정보를 가져올 수 없으므로 DMZ 포리스트에 있는 ADFS의 발급 규칙을 적절하게 변경하세요.
- 도메인 수준 트러스트가 지원되며 작동할 수 있지만 포리스트 수준 트러스트 모델로 이동하는 것이 좋습니다. 또한 이름에 대한 UPN 라우팅 및 NETBIOS 이름 확인이 정확하게 작동해야 합니다.

>[!NOTE]  
>선택적 인증이 양방향 트러스트 구성에 사용되는 경우 호출자 사용자에게 대상 서비스 계정에 대한 "인증 허용" 권한이 부여되어야 합니다. 


## <a name="design"></a>디자인

### <a name="what-third-party-multi-factor-authentication-providers-are-available-for-ad-fs"></a>AD FS에 사용할 수 있는 타사 다단계 인증 공급자는 무엇인가요?
AD FS는 타사 MFA 공급자에서 통합할 수 있는 확장 가능한 메커니즘을 제공합니다. 이에 대해 설정된 인증 프로그램이 없습니다. 공급업체에서 릴리스하기 전에 필요한 유효성 검사를 수행했다고 가정합니다. 

Microsoft에 통지한 공급업체 목록은 [AD FS에 대한 MFA 공급자](../operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)에 게시됩니다.  언제든지 알 수 없는 공급자가 있을 수 있으며, 이에 대해 확인되는 대로 이 목록이 업데이트됩니다.

### <a name="are-third-party-proxies-supported-with-ad-fs"></a>타사 프록시가 AD FS에 지원되나요?
예, 타사 프록시는 웹 애플리케이션 프록시 앞에 배치할 수 있지만, 타사 프록시에서 웹 애플리케이션 프록시 대신 사용할 [MS-ADFSPIP 프로토콜](https://msdn.microsoft.com/library/dn392811.aspx)을 지원해야 합니다.

알고 있는 타사 공급자 목록은 아래와 같습니다.  언제든지 알 수 없는 공급자가 있을 수 있으며, 이에 대해 확인되는 대로 이 목록이 업데이트됩니다.

- [F5 액세스 정책 관리자](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-third-party-integration-13-1-0/12.html#guid-1ee8fbb3-1b33-4982-8bb3-05ae6868d9ee)


### <a name="where-is-the-capacity-planning-sizing-spreadsheet-for-ad-fs-2016"></a>AD FS 2016의 용량 계획 크기 조정 스프레드시트는 어디에 있나요?
AD FS 2016 버전의 스프레드시트는 [여기](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)서 다운로드할 수 있습니다.
이는 Windows Server 2012 R2의 AD FS에도 사용할 수 있습니다.

### <a name="how-can-i-ensure-my-ad-fs-and-wap-servers-support-apples-atp-requirements"></a>AD FS 및 WAP 서버에서 Apple의 ATP 요구 사항을 지원하도록 하려면 어떻게 해야 하나요?

Apple은 AD FS를 인증하는 iOS 앱의 호출에 영향을 줄 수 있는 ATS(App Transport Security)라는 일단의 요구 사항을 발표했습니다.  AD FS 및 WAP 서버에서 [ATS를 사용한 연결 요구 사항](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)을 지원하는지 확인하여 해당 서버에서 준수하는지 확인할 수 있습니다.  
특히 AD FS 및 WAP 서버에서 TLS 1.2를 지원하고 TLS 연결의 협상된 암호 그룹에서 완벽한 전달 보안을 지원하는지 확인해야 합니다.

[AD FS의 SSL 프로토콜 관리](../operations/Manage-SSL-Protocols-in-AD-FS.md)를 사용하여 SSL 2.0 및 3.0 과 TLS 버전 1.0, 1.1 및 1.2를 사용하거나 사용하지 않도록 설정할 수 있습니다.

AD FS 및 WAP 서버에서 ATP를 지원하는 TLS 암호 그룹만 협상하도록 하려면 [ATP 규격 암호 그룹 목록](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)에 없는 모든 암호 그룹을 사용하지 않도록 설정할 수 있습니다.  이렇게 하려면 [Windows TLS PowerShell cmdlet](https://technet.microsoft.com/itpro/powershell/windows/tls/index)을 사용합니다.

## <a name="developer"></a>Developer

### <a name="when-generating-an-id_token-with-adfs-for-a-user-authenticated-against-ad-how-is-the-sub-claim-generated-in-the-id_token"></a>ADFS를 사용하여 AD에 대해 인증된 사용자에 대한 id_token을 생성하는 경우 "sub" 클레임은 id_token에서 어떻게 생성되나요?
"sub" 클레임의 값은 클라이언트 ID + 앵커 클레임 값의 해시입니다.

### <a name="what-is-the-lifetime-of-the-refresh-tokenaccess-token-when-the-user-logs-in-via-a-remote-claims-provider-trust-over-ws-fedsaml-p"></a>사용자가 WS-Fed/SAML-P에 대한 원격 클레임 공급자 트러스트를 통해 로그인하는 경우 새로 고침 토큰/액세스 토큰의 수명은 어떻게 되나요?
새로 고침 토큰의 수명은 ADFS에서 원격 클레임 공급자 트러스트로부터 가져온 토큰의 수명입니다. 액세스 토큰의 수명은 액세스 토큰을 발급하는 신뢰 당사자의 토큰 수명입니다.

### <a name="i-need-to-return-profile-and-email-scopes-as-well-in-addition-to-the-openid-scope-can-i-obtain-additional-information-using-scopes-how-to-do-it-in-ad-fs"></a>OpenId 범위뿐만 아니라 프로필과 이메일 범위도 반환해야 합니다. 범위를 사용하여 추가 정보를 가져올 수 있나요? AD FS에서는 어떻게 해야 하나요?
사용자 지정된 id_token을 사용하여 id_token 자체에 관련 정보를 추가할 수 있습니다. 자세한 내용은 [id_token에서 내보낼 클레임 사용자 지정](../development/Custom-Id-Tokens-in-AD-FS.md) 문서를 참조하세요.

### <a name="how-to-issue-json-blobs-inside-jwt-tokens"></a>JWT 토큰 내에서 json Blob을 발급하는 방법은 어떻게 되나요?
이를 위해 특수한 ValueType("<http://www.w3.org/2001/XMLSchema#json>") 및 이스케이프 문자(\x22)가 AD FS 2016에 추가되었습니다. 발급 규칙에 대해 아래 샘플을 확인하고, 액세스 토큰의 최종 출력도 확인하세요.

발급 규칙 샘플:

    => issue(Type = "array_in_json", ValueType = "http://www.w3.org/2001/XMLSchema#json", Value = "{\x22Items\x22:[{\x22Name\x22:\x22Apple\x22,\x22Price\x22:12.3},{\x22Name\x22:\x22Grape\x22,\x22Price\x22:3.21}],\x22Date\x22:\x2221/11/2010\x22}");

액세스 토큰에서 발급된 클레임:

    "array_in_json":{"Items":[{"Name":"Apple","Price":12.3},{"Name":"Grape","Price":3.21}],"Date":"21/11/2010"}

### <a name="can-i-pass-resource-value-as-part-of-the-scope-value-like-how-requests-are-done-against-azure-ad"></a>Azure AD에 대한 요청 수행 방식과 같이 리소스 값을 범위 값의 일부로 전달할 수 있나요?
서버 2019에서 AD FS를 사용하면 이제 범위 매개 변수에 포함된 리소스 값을 전달할 수 있습니다. 이제 범위 매개 변수를 공백으로 구분된 목록으로 구성할 수 있습니다. 여기서 각 항목은 리소스/범위로 구조화됩니다. 예를 들면 다음과 같습니다.  
**<올바른 샘플 요청 만들기>**

### <a name="does-ad-fs-support-pkce-extension"></a>AD FS에서 PKCE 확장을 지원하나요?
서버 2019의 AD FS는 OAuth 인증 코드 부여 흐름에 대한 PKCE(코드 교환용 증명 키)를 지원합니다.

### <a name="what-permitted-scopes-are-supported-by-ad-fs"></a>AD FS는 어떤 허용 범위를 지원하나요?
- aza - [broker 클라이언트용 OAuth 2.0 프로토콜 확장](https://docs.microsoft.com/openspecs/windows_protocols/ms-oapxbc/2f7d8875-0383-4058-956d-2fb216b44706)을 사용하고 "aza" 범위가 범위 매개 변수에 포함된 경우 서버에서 새 주 새로 고침 토큰을 발급하고, 이를 응답의 refresh_token 필드에 설정합니다. 또한 새 주 새로 고침 토큰이 강제로 적용되는 경우 refresh_token_expires_in 필드를 이 토큰의 수명으로 설정합니다.
- openid - 이 범위를 사용하면 애플리케이션에서 OpenID Connect 권한 부여 프로토콜을 사용하도록 요청할 수 있습니다.
- logon_cert - logon_cert 범위를 사용하면 애플리케이션에서 로그온 인증서를 요청할 수 있습니다. 이 인증서는 인증된 사용자를 대화형으로 로그온하는 데 사용할 수 있습니다. AD FS 서버는 응답에서 access_token 매개 변수를 생략하는 대신, base64로 인코딩된 CMS 인증서 체인 또는 CMC 전체 PKI 응답을 제공합니다. 자세한 내용은 [여기](https://docs.microsoft.com/openspecs/windows_protocols/ms-oapx/32ce8878-7d33-4c02-818b-6c9164cc731e)서 확인할 수 있습니다. 
- user_impersonation - AD FS에서 On-Behalf-Of 액세스 토큰을 성공적으로 요청하려면 user_imperation 범위가 필요합니다. 이 범위를 사용하는 방법에 대한 자세한 내용은 [AD FS 2016에서 OAuth를 사용하는 OBO(On-Behalf-Of)를 통해 다중 계층 애플리케이션 빌드](../../ad-fs/development/ad-fs-on-behalf-of-authentication-in-windows-server.md)를 참조하세요.
- vpn_cert - vpn_cert 범위를 사용하면 애플리케이션에서 VPN 인증서를 요청할 수 있습니다. 이 인증서는 EAP-TLS 인증을 사용하여 VPN 연결을 설정하는 데 사용할 수 있습니다. 이 범위는 더 이상 지원되지 않습니다.
- email - 이 범위를 사용하면 애플리케이션에서 로그인한 사용자에 대한 이메일 클레임을 요청할 수 있습니다. 이 범위는 더 이상 지원되지 않습니다. 
- profile - 이 범위를 사용하면 애플리케이션에서 로그인 사용자에 대한 프로필 관련 클레임을 요청할 수 있습니다. 이 범위는 더 이상 지원되지 않습니다. 


## <a name="operations"></a>작업

### <a name="how-do-i-replace-the-ssl-certificate-for-ad-fs"></a>AD FS용 SSL 인증서를 바꾸려면 어떻게 해야 하나요?
AD FS SSL 인증서는 AD FS 관리 스냅인에 있는 AD FS 서비스 통신 인증서와 다릅니다.  AD FS SSL 인증서를 변경하려면 PowerShell을 사용해야 합니다. 아래 문서의 지침을 따르세요.

[AD FS 및 WAP 2016의 SSL 인증서 관리](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)

### <a name="how-can-i-enable-or-disable-tlsssl-settings-for-ad-fs"></a>AD FS에 대한 TLS/SSL 설정을 사용하거나 사용하지 않도록 설정하려면 어떻게 해야 하나요?
SSL 프로토콜 및 암호 그룹을 사용하거나 사용하지 않도록 설정하려면 다음을 사용하세요.

[AD FS의 SSL 프로토콜 관리](../operations/Manage-SSL-Protocols-in-AD-FS.md)

### <a name="does-the-proxy-ssl-certificate-have-to-be-the-same-as-the-ad-fs-ssl-certificate"></a>프록시 SSL 인증서는 AD FS SSL 인증서와 동일해야 하나요?  
프록시 SSL 인증서 및 AD FS SSL 인증서와 관련하여 다음 지침을 사용하세요.


- 프록시를 사용 하는 경우 Windows 통합 인증을 프록시 SSL 인증서를 사용 하는 AD FS 프록시 요청 동일 해야 (동일한 키를 사용 하 여) 페더레이션 서버 SSL 인증서로
- "ExtendedProtectionTokenCheck"는 AD FS 속성 설정 (기본 AD FS에서 설정), 프록시 SSL 인증서 동일 해야 (동일한 키를 사용 하 여) 페더레이션 서버 SSL 인증서로
- 그렇지 않으면 AD FS SSL 인증서와 다른 키가 프록시 SSL 인증서에 있을 수 있지만 동일한 [요구 사항](../overview/AD-FS-2016-Requirements.md)을 충족해야 합니다.

### <a name="why-do-i-only-see-a-password-login-on-ad-fs-and-not-my-other-authentication-methods-that-i-have-configured"></a>AD FS에서만 암호 로그인이 표시되고 구성한 다른 인증 방법이 표시되지 않는 이유는 무엇인가요? 
구성되고 사용하도록 설정된 인증 방법에 매핑되는 특정 인증 URI가 애플리케이션에 명시적으로 필요한 경우에만 AD FS에서 단일 인증 방법을 로그인 화면에 표시합니다. 이는 WS-Federation 요청의 'wauth' 매개 변수와 SAML 프로토콜 요청의 'RequestedAuthnCtxRef' 매개 변수로 전달됩니다. 따라서 요청된 인증 방법(예: 암호 로그인)만 표시됩니다.

Azure AD에서 AD FS를 사용하는 경우 애플리케이션에서 prople=login 매개 변수를 Azure AD로 보내는 것이 일반적입니다. Azure AD는 기본적으로 이 매개 변수에서 AD FS에 대한 새 암호 기반 로그인을 요청하도록 변환합니다. 이는 네트워크 내의 AD FS에서 암호 로그인을 확인하거나 인증서를 사용하여 로그인하는 옵션이 표시되지 않는 가장 일반적인 이유입니다. 이 문제는 Azure AD의 페더레이션된 도메인 설정을 변경하여 쉽게 해결할 수 있습니다. 

이를 구성하는 방법에 대한 자세한 내용은 [Active Directory Federation Services prompt=login 매개 변수 지원](../operations/AD-FS-Prompt-Login.md)을 참조하세요.

### <a name="how-can-i-change-the-ad-fs-service-account"></a>AD FS 서비스 계정을 변경하려면 어떻게 해야 하나요?
AD FS 서비스 계정을 변경하려면 AD FS 도구 상자인 [서비스 계정 Powershell 모듈](https://github.com/Microsoft/adfsToolbox/tree/master/serviceAccountModule)을 사용하는 지침을 따르세요.

### <a name="how-can-i-configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>AD FS에서 WIA(Windows 통합 인증)를 사용하도록 브라우저를 구성하려면 어떻게 해야 하나요?

브라우저를 구성하는 방법에 대한 자세한 내용은 [AD FS에서 WIA(Windows 통합 인증)를 사용하도록 브라우저 구성](../operations/Configure-AD-FS-Browser-WIA.md)을 참조하세요.

### <a name="can-i-turn-off-browserssoenabled"></a>BrowserSsoEnabled를 해제할 수 있나요?
ADFS의 디바이스 또는 ADFS를 사용하는 비즈니스용 Windows Hello 인증서 등록을 기반으로 하는 액세스 제어 정책이 없는 경우 BrowserSsoEnabled를 해제할 수 있습니다. BrowserSsoEnabled를 사용하면 ADFS에서 디바이스 정보가 포함된 클라이언트로부터 PRT(주 새로 고침 토큰)를 수집할 수 있습니다. 해당 디바이스가 없으면 ADFS의 인증이 Windows 10 디바이스에서 작동하지 않습니다.

### <a name="how-long-are-ad-fs-tokens-valid"></a>AD FS 토큰의 유효 기간은 얼마인가요?

이 질문은 종종 '새 자격 증명을 입력하지 않고도 사용자가 SSO(Single Sign-On)를 얼마나 오래 사용할 수 있나요?, 그리고 관리자 권한으로 이를 어떻게 제어할 수 있나요?'를 의미합니다.  이 동작 및 이를 제어하는 구성 설정은 [AD FS Single Sign-On 설정](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-2016-single-sign-on-settings) 문서에서 설명하고 있습니다.

아래에는 다양한 쿠키 및 토큰의 기본 수명과 이 수명을 제어하는 매개 변수가 나와 있습니다.

**등록된 디바이스**

- PRT 및 SSO 쿠키: 최대 90일이며, PSSOLifeTimeMins로 관리됩니다. (제공된 디바이스는 최소 14일마다 사용되며, DeviceUsageWindow로 제어됩니다.)

- 새로 고침 토큰: 일관된 동작을 제공하기 위해 위 항목을 기준으로 계산됩니다.

- access_token: 기본적으로 1시간이며,신뢰 당사자를 기준으로 합니다.

- id_token: access_token과 동일

**등록 취소된 디바이스**

- SSO 쿠키: 기본적으로 8시간이며, SSOLifetimeMins로 제어됩니다.  KMSI(로그인 유지)를 사용하도록 설정되면 기본값이 24시간이며, KMSILifetimeMins를 통해 구성할 수 있습니다.


- 새로 고침 토큰: 기본적으로 8시간입니다. KMSI를 사용하도록 설정되면 24시간입니다.

- access_token: 기본적으로 1시간이며,신뢰 당사자를 기준으로 합니다.

- id_token: access_token과 동일

### <a name="does-ad-fs-support-http-strict-transport-security-hsts"></a>AD FS에서 HSTS(HTTP Strict Transport Security)를 지원하나요?  

HTTP HSTS(HTTP Strict Transport Security)는 HTTP 및 HTTPS 엔드포인트를 모두 사용하는 서비스에 대한 프로토콜 다운그레이드 공격 및 쿠키 하이재킹을 완화하는 데 도움이 되는 웹 보안 정책 메커니즘입니다. 이를 통해 웹 서버에서 웹 브라우저(또는 기타 준수 사용자 에이전트)가 HTTP 프로토콜이 아니라 HTTPS를 통해서만 상호 작용해야 한다고 선언할 수 있습니다.

웹 인증 트래픽에 대한 모든 AD FS 엔드포인트는 HTTPS를 통해서만 열립니다.  결과적으로 AD FS는 HTTP Strict Transport Security 정책 메커니즘에서 제공하는 위협을 효과적으로 완화합니다(설계상 HTTP에는 수신기가 없으므로 HTTP로 다운그레이드하지 않음). 또한 AD FS는 모든 쿠키를 보안 플래그로 표시하여 쿠키가 HTTP 프로토콜 엔드포인트를 사용하는 쿠키를 다른 서버로 보내지 않도록 방지합니다.

따라서 다운그레이드할 수 없으므로 AD FS 서버에서 HSTS를 구현할 필요가 없습니다.  AD FS 서버는 규정 준수를 위해 HTTP를 사용할 수 없고 모든 쿠키가 안전한 것으로 표시되므로 이러한 요구 사항을 충족합니다.

또한 AD FS 2016(최신 패치 포함) 및 AD FS 2019는 HSTS 헤더를 내보낼 수 있습니다. 이를 구성하려면 [AD FS를 사용하여 HTTP 보안 응답 헤더 사용자 지정](../operations/customize-http-security-headers-ad-fs.md)을 참조하세요.

### <a name="x-ms-forwarded-client-ip-does-not-contain-the-ip-of-the-client-but-contains-ip-of-the-firewall-in-front-of-the-proxy-where-can-i-get-the-right-ip-of-the-client"></a>x-ms-forwarded-client-ip는 클라이언트의 IP를 포함하지 않지만 프록시 앞에 방화벽의 IP를 포함합니다. 클라이언트의 올바른 IP는 어디서 가져올 수 있나요?
WAP 앞에서 SSL 종료를 수행하지 않는 것이 좋습니다. SSL 종료가 WAP 앞에서 수행되는 경우 x-ms-forwarded-client-ip에는 WAP 앞에 있는 네트워크 디바이스의 IP가 포함됩니다. AD FS에서 지원하는 다양한 IP 관련 클레임에 대한 간단한 설명은 다음과 같습니다.
 - x-ms-client-ip: STS에 연결된 디바이스의 네트워크 IP입니다.  엑스트라넷 요청의 경우 이 클레임에는 항상 WAP의 IP가 포함됩니다.
 - x-ms-forwarded-client-ip: Exchange Online을 통해 ADFS에 전달된 값과 WAP에 연결된 디바이스의 IP 주소를 포함하는 다중 값 클레임입니다.
 - Userip: 엑스트라넷 요청의 경우 이 클레임에는 x-ms-forwarded-client-ip 값이 포함됩니다.  인트라넷 요청의 경우 이 클레임에는 x-ms-client-ip와 동일한 값이 포함됩니다.

 또한 AD FS 2016(최신 패치 포함) 이상 버전에서는 x-forwarded-for 헤더 캡처도 지원합니다. 계층 3에서 전달하지 않는 부하 분산 장치 또는 네트워크 디바이스(IP가 유지됨)는 들어오는 클라이언트 IP를 업계 표준 x-forwarded-for 헤더에 추가해야 합니다. 

### <a name="i-am-trying-to-get-additional-claims-on-the-user-info-endpoint-but-its-only-returning-subject-how-can-i-get-additional-claims"></a>userinfo 엔드포인트에서 추가 클레임을 가져오려고 했지만 주체만 반환됩니다. 추가 클레임을 가져오려면 어떻게 해야 하나요?
AD FS userinfo 엔드포인트는 항상 OpenID 표준에 지정된 대로 주체 클레임을 반환합니다. AD FS는 userinfo 엔드포인트를 통해 요청된 추가 클레임을 제공하지 않습니다. ID 토큰에 추가 클레임이 필요한 경우 [AD FS의 사용자 지정 ID 토큰](../development/custom-id-tokens-in-ad-fs.md)을 참조하세요.

### <a name="why-do-i-see-a-lot-of-1021-errors-on-my-ad-fs-servers"></a>AD FS 서버에서 1021 오류가 많이 표시되는 이유는 무엇인가요?
이 이벤트는 일반적으로 00000003-0000-0000-c000-000000000000 리소스에 대한 AD FS의 잘못된 리소스 액세스에 대해 기록됩니다. 이 오류는 Azure AD Graph 서비스에 대한 액세스 토큰을 가져오려는 클라이언트의 잘못된 동작으로 인해 발생합니다. 리소스가 AD FS에 없으므로 이 경우 AD FS 서버에서 1021 이벤트 ID가 생성됩니다. AD FS의 00000003-0000-0000-c000-000000000000 리소스에 대한 경고 또는 오류는 무시해도 안전합니다.

### <a name="why-am-i-seeing-a-warning-for-failure-to-add-the-ad-fs-service-account-to-the-enterprise-key-admins-group"></a>AD FS 서비스 계정을 엔터프라이즈 키 관리 그룹에 추가하지 못했다는 경고가 표시되는 이유는 무엇인가요?
이 그룹은 FSMO PDC 역할이 있는 Windows 2016 도메인 컨트롤러가 도메인에 있는 경우에만 만들어집니다. 이 오류를 해결하려면 그룹을 수동으로 만들고 아래 절차에 따라 서비스 계정을 그룹의 멤버로 추가한 후 필요한 권한을 부여할 수 있습니다.
1.    **Active Directory 사용자 및 컴퓨터**를 엽니다.
2.    탐색 창에서 도메인 이름을 **마우스 오른쪽 단추로 클릭**하고 [속성]을 **클릭**합니다.
3.    [보안]을 **클릭**합니다([보안] 탭이 없으면 [보기] 메뉴에서 [고급 기능]을 켭니다).
4.    [고급]을 **클릭**합니다. [추가]를 **클릭**합니다. [보안 주체 선택]을 **클릭**합니다.
5.    [사용자, 컴퓨터, 서비스 계정 또는 그룹 선택] 대화 상자가 표시됩니다.  [선택할 개체 이름 입력] 텍스트 상자에서 '키 관리 그룹'을 입력합니다.  확인을 클릭합니다.
6.    [적용 대상] 목록 상자에서 **하위 사용자 개체**를 선택합니다.
7.    스크롤 막대를 사용하여 페이지 아래쪽으로 스크롤하고, [모두 지우기]를 **클릭**합니다.
8.    **속성** 섹션에서 **msDS-KeyCredentialLink 읽기** 및 **msDS-KeyCredentialLink 쓰기**를 선택합니다.

### <a name="why-does-modern-authentication-from-android-devices-fail-if-the-server-does-not-send-all-the-intermediate-certificates-in-the-chain-with-the-ssl-cert"></a>서버에서 SSL 인증서를 사용하여 체인의 모든 중간 인증서를 보내지 않는 경우 Android 디바이스의 최신 인증이 실패하는 이유는 무엇인가요?

페더레이션 사용자는 Android ADAL 라이브러리를 사용하는 앱에 대한 Azure AD 인증이 실패할 수 있습니다. 앱에서 로그인 페이지를 표시하려고 하면 **AuthenticationException**이 발생합니다. Chrome에서는 AD FS 로그인 페이지가 안전하지 않은 것으로 호출될 수 있습니다.

모든 버전과 모든 디바이스에서 Android는 인증서의 **authorityInformationAccess** 필드에서 추가 인증서 다운로드를 지원하지 않습니다. 이는 Chrome 브라우저에서도 마찬가지입니다. 전체 인증서 체인이 AD FS에서 전달되지 않으면 중간 인증서가 없는 서버 인증 인증서로 인해 이 오류가 발생합니다.

이 문제에 대한 적절한 해결 방법은 AD FS 및 WAP 서버에서 SSL 인증서와 함께 필요한 중간 인증서를 보내도록 구성하는 것입니다.

한 머신에서 컴퓨터(AD FS 및 WAP 서버)의 개인 저장소로 가져올 SSL 인증서를 내보내는 경우 프라이빗 키를 내보내고 **개인 정보 교환 - PKCS #12**를 선택해야 합니다.

**확장 속성 모두 내보내기**뿐만 아니라 **가능한 경우 인증 경로에 있는 인증서 모두 포함**에 대한 확인란도 선택해야 합니다.  

Windows Server에서 certlm.msc를 실행하고, *.PFX를 컴퓨터의 개인 인증서 저장소로 가져옵니다. 이로 인해 서버에서 전체 인증서 체인을 ADAL 라이브러리로 전달합니다.

>[!NOTE]
> 네트워크 부하 분산 장치의 인증서 저장소도 있는 경우 전체 인증서 체인을 포함하도록 업데이트해야 합니다.

### <a name="does-ad-fs-support-head-requests"></a>AD FS에서 HEAD 요청을 지원하나요?
AD FS는 HEAD 요청을 지원하지 않습니다.  애플리케이션에서 AD FS 엔드포인트에 대해 HEAD 요청을 사용하지 않아야 합니다.  이로 인해 예기치 않았거나 지연된 HTTP 오류 응답이 발생할 수 있습니다.  또한 AD FS 이벤트 로그에 예기치 않은 오류 이벤트가 표시될 수 있습니다.

### <a name="why-am-i-not-seeing-a-refresh-token-when-i-am-logging-in-with-a-remote-idp"></a>원격 IdP를 사용하여 로그인할 때 새로 고침 토큰이 표시되지 않는 이유는 무엇인가요?
IdP에서 발급한 토큰의 유효 기간이 1시간 미만인 경우 새로 고침 토큰이 발급되지 않습니다. 새로 고침 토큰이 발급되도록 하려면 IdP에서 발급한 토큰의 유효 기간을 1시간 넘게 늘립니다.

### <a name="do-we-have-any-way-to-change-rp-token-encryption-algorithm"></a>RP 토큰 암호화 알고리즘을 변경할 수 있는 방법이 있나요?
RP 토큰 암호화는 기본적으로 AES256으로 설정되며, 다른 값으로 변경할 수 없습니다.

### <a name="on-a-mixed-mode-farm-i-get-error-when-trying-to-set-the-new-ssl-certificate-using-set-adfssslcertificate--thumbprint-how-can-i-update-the-ssl-certificate-in-a-mixed-mode-ad-fs-farm"></a>혼합 모드 팜에서 Set-AdfsSslCertificate -Thumbprint를 사용하여 새 SSL 인증서를 설정하려고 하면 오류가 발생합니다. 혼합 모드 AD FS 팜에서 SSL 인증서를 업데이트하려면 어떻게 해야 하나요?
혼합 모드 AD FS 팜은 전환(transitionary) 상태가 됩니다. 계획하는 동안 업그레이드 프로세스 전에 SSL 인증서를 롤오버하거나, 프로세스를 완료하고 SSL 인증서를 업데이트하기 전에 팜 동작 수준을 높이는 것이 좋습니다. 이 작업이 수행되지 않은 경우 아래 지침에 따라 SSL 인증서를 업데이트할 수 있습니다. 

WAP 서버에서도 Set-WebApplicationProxySslCertificate를 계속 사용할 수 있습니다. ADFS 서버에서 netsh를 사용해야 합니다. 아래에 제공된 단계를 따르세요.

1. 유지 관리(예: 부하 분산 장치에서 제거)를 위해 ADFS 2016 서버의 하위 세트를 선택합니다.
2. #1에서 선택한 서버에서 MMC를 통해 새 인증서를 가져옵니다.
3. 기존 인증서를 삭제합니다.

    a. netsh http delete sslcert hostnameport=fs.contoso.com:443 b. netsh http delete sslcert hostnameport=localhost:443 c. netsh http delete sslcert hostnameport=fs.contoso.com:49443

4.  새 인증서를 추가합니다.

    a. netsh http add sslcert hostnameport=fs.contoso.com:443 certhash=CERTTHUMBPRINT appid={5d89a20c-beab-4389-9447-324788eb944a} certstorename=MY sslctlstorename=AdfsTrustedDevices

    b. netsh http add sslcert hostnameport=localhost:443 certhash=CERTTHUMBPRINT appid={5d89a20c-beab-4389-9447-324788eb944a} certstorename=MY sslctlstorename=AdfsTrustedDevices

    c. netsh http add sslcert hostnameport=fs.contoso.com:49443 certhash=CERTTHUMBPRINT appid={5d89a20c-beab-4389-9447-324788eb944a} certstorename=MY sslctlstorename=AdfsTrustedDevices

5. 선택한 서버에서 ADFS 서비스를 다시 시작합니다.
6. 유지 관리를 위해 WAP 서버의 하위 세트를 제거합니다.
7. 선택한 WAP 서버에서 MMC를 통해 새 인증서를 가져옵니다.
8. cmdlet을 사용하여 WAP에서 새 인증서를 설정합니다.

    a. Set-WebApplicationProxySslCertificate -Thumbprint " CERTTHUMBPRINT"

9. 선택한 WAP 서버에서 서비스를 다시 시작합니다.
10. 선택한 WAP 및 AD FS 서버를 프로덕션 환경에 다시 배치합니다.

나머지 AD FS 및 WAP 서버에서 비슷한 방식으로 업데이트를 수행합니다.

### <a name="is-adfs-supported-when-web-application-proxy-wap-servers-are-behind-azure-web-application-firewallwaf"></a>WAP(웹 애플리케이션 프록시) 서버가 Azure WAF(웹 애플리케이션 방화벽) 뒤에 있는 경우 ADFS가 지원되나요?
ADFS 및 웹 애플리케이션 서버는 엔드포인트에서 SSL 종료를 수행하지 않는 방화벽을 지원합니다. 또한 ADFS/WAP 서버에는 일반적인 웹 공격(예: 사이트 간 스크립팅, ADFS 프록시)을 방지하고 [MS-ADFSPIP 프로토콜](https://msdn.microsoft.com/library/dn392811.aspx)에 정의된 모든 요구 사항을 충족하는 메커니즘이 기본 제공되어 있습니다.

### <a name="i-am-seeing-an-event-441-a-token-with-a-bad-token-binding-key-was-found-what-should-i-do-to-resolve-this"></a>"이벤트 441: 토큰 바인딩 키가 잘못된 토큰을 발견했습니다."라는 메시지가 표시됩니다. 이 문제를 해결하려면 어떻게 해야 하나요?
AD FS 2016에서는 토큰 바인딩을 사용하도록 자동으로 설정되며, 프록시 및 페더레이션 시나리오에서 알려진 여러 문제가 발생하여 이 오류가 발생합니다. 이 문제를 해결하려면 다음 Powershell 명령을 실행하고 토큰 바인딩 지원을 제거합니다.

`Set-AdfsProperties -IgnoreTokenBinding $true`

### <a name="i-have-upgraded-my-farm-from-ad-fs-in-windows-server-2016-to-ad-fs-in-windows-server-2019-the-farm-behavior-level-for-the-ad-fs-farm-has-been-successfully-raised-to-2019-but-the-web-application-proxy-configuration-is-still-displayed-as-windows-server-2016"></a>팜을 Windows Server 2016의 AD FS에서 Windows Server 2019의 AD FS로 업그레이드했습니다. AD FS 팜의 팜 동작 수준이 성공적으로 2019로 높아졌지만 웹 애플리케이션 프록시 구성이 여전히 Windows Server 2016으로 표시되나요?
Windows Server 2019로 업그레이드한 후에도 웹 애플리케이션 프록시의 구성 버전은 계속 Windows Server 2016으로 표시됩니다. 웹 애플리케이션 프록시에는 Windows Server 2019에 대한 새로운 버전 관련 기능이 없으며, AD FS에서 팜 동작 수준이 성공적으로 높아진 경우 웹 애플리케이션 프록시는 설계상 Windows Server 2016으로 계속 표시됩니다.

### <a name="can-i-estimate-the-size-of-the-adfsartifactstore-before-enabling-esl"></a>ESL을 사용하도록 설정하기 전에 ADFSArtifactStore의 크기를 예측할 수 있나요?
ESL을 사용하도록 설정하면 AD FS는 ADFSArtifactStore 데이터베이스에서 사용자의 계정 활동과 알려진 위치를 추적합니다. 이 데이터베이스는 추적된 사용자 및 알려진 위치의 수를 기준으로 크기를 조정합니다. ESL을 사용하도록 계획하는 경우 ADFSArtifactStore 데이터베이스의 크기가 사용자 100,000명당 최대 1GB의 속도로 확장한다고 예측할 수 있습니다. AD FS 팜에서 WID(Windows 내부 데이터베이스)를 사용하는 경우 데이터베이스 파일의 기본 위치는 C:\Windows\WID\Data입니다. 이 드라이브를 채우지 않도록 방지하려면 ESL을 사용하도록 설정하기 전에 최소 5GB의 사용 가능한 스토리지가 있어야 합니다. 디스크 스토리지 외에도 500,000명 이하의 사용자 인구에 대해 최대 1GB의 RAM을 추가하여 ESL을 사용하도록 설정한 후 총 프로세스 메모리를 늘리도록 계획합니다.
