---
ms.assetid: acc9101b-841c-4540-8b3c-62a53869ef7a
title: AD FS FAQ
description: AD FS에 대 한 질문과 대답
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 04/17/2019
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8444e417fe089c1a3cf2acc2648b222ec5c9774c
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865465"
---
# <a name="ad-fs-frequently-asked-questions-faq"></a>AD FS FAQ (질문과 대답)


다음 설명서는 Active Directory Federation Services와 관련 하 여 자주 묻는 질문과 대답입니다.  문서는 질문 유형에 따라 그룹으로 분할 되었습니다.

## <a name="deployment"></a>배포

### <a name="how-can-i-upgrademigrate-from-previous-versions-of-ad-fs"></a>이전 버전의 AD FS에서 업그레이드/마이그레이션할 수 있는 방법
다음 중 하나를 사용 하 여 AD FS를 업그레이드할 수 있습니다.


- Windows Server 2012 R2 AD FS Windows Server 2016 AD FS 이상 Windows Server 2016 AD FS에서 Windows Server 2019 AD FS로 업그레이드 하는 경우 방법론은 동일 합니다. 
    - [WID 데이터베이스를 사용하여 Windows Server 2016에서 AD FS로 업그레이드](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)
    - [SQL 데이터베이스를 사용하여 Windows Server 2016에서 AD FS로 업그레이드](../deployment/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL.md)
- Windows server 2012 AD FS Windows Server 2012 R2 AD FS
    - [Windows Server 2012 r 2에서 AD FS로 마이그레이션](https://technet.microsoft.com/library/dn486815.aspx)
- 2\.0 AD FS Windows Server 2012 AD FS
    - [Windows Server 2012에서 AD FS로 마이그레이션](https://technet.microsoft.com/library/jj647765.aspx)
- 1\. x AD FS AD FS 2.0
    - [AD FS 1.x에서 AD FS 2.0로 업그레이드](https://technet.microsoft.com/library/ff678035.aspx)

AD FS 2.0 또는 2.1 (Windows Server 2008 R2 또는 Windows Server 2012)에서 업그레이드 해야 하는 경우에는 기본적으로 사용 하는 스크립트 (C:\fs에 있음)를 사용 해야 합니다.

### <a name="why-does-ad-fs-installation-require-a-reboot-of-the-server"></a>AD FS 설치에서 서버를 다시 부팅 해야 하는 이유는 무엇 인가요?

Windows Server 2016에는 HTTP/2 지원이 추가 되었지만 클라이언트 인증서 인증에는 h t t p/2를 사용할 수 없습니다.  많은 AD FS 시나리오에서 클라이언트 인증서 인증을 사용 하 고 상당한 수의 클라이언트가 HTTP/1.1을 사용 하 여 요청을 다시 시도 하는 것을 지원 하지 않기 때문에 AD FS 팜 구성은 로컬 서버의 HTTP 설정을 HTTP/1.1로 다시 구성 합니다.  이렇게 하려면 서버를 다시 부팅 해야 합니다.  

### <a name="is-using-windows-2016-wap-servers-to-publish-the-ad-fs-farm-to-the-internet-without-upgrading-the-back-end-ad-fs-farm-supported"></a>Windows 2016 WAP 서버를 사용 하 여 지원 되는 백 엔드 AD FS 팜을 업그레이드 하지 않고 인터넷에 AD FS 팜을 게시 합니까?
예,이 구성은 지원 되지만 새로운 AD FS 2016 기능이이 구성에서 지원 되지 않습니다.  이 구성은 AD FS 2012 R2에서 AD FS 2016로의 마이그레이션 단계 중에 일시적인 것 이며 장기간 배포 해서는 안 됩니다.

### <a name="is-it-possible-to-deploy-ad-fs-for-office-365-without-publishing-a-proxy-to-office-365"></a>Office 365에 프록시를 게시 하지 않고 Office 365에 대 한 AD FS를 배포할 수 있나요?
예, 지원 됩니다. 그러나 의도 하지 않은 결과

1. Azure AD는 페더레이션 메타 데이터에 액세스할 수 없으므로 수동으로 토큰 서명 인증서 업데이트를 관리 해야 합니다. 토큰 서명 인증서를 수동으로 업데이트 하는 방법에 대 한 자세한 내용은 [Office 365 및 Azure Active Directory에 대 한 페더레이션 인증서 갱신](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs) 을 참조 하세요.
2. 레거시 인증 흐름을 활용할 수 없습니다 (예: ExO 프록시 인증 흐름).

### <a name="what-are-load-balancing-requirements-for-ad-fs-and-wap-servers"></a>AD FS 및 WAP 서버에 대 한 부하 분산 요구 사항은 무엇 인가요?

AD FS 상태 비저장 시스템입니다. 따라서 부하 분산은 로그인에 매우 간단 합니다. 다음은 부하 분산 시스템에 대 한 주요 권장 사항입니다.


- 부하 분산 장치는 IP 선호도를 사용 하 여 구성 하면 안 됩니다. 이렇게 하면 특정 Exchange Online 시나리오에서 서버의 하위 집합에 과도 한 부하를 넣을 수 있습니다.
- 부하 분산 장치는 HTTPS 연결을 종료 하지 않고 ADFS 서버에 대 한 새 연결을 다시 시작 합니다.
- 부하 분산 장치는 ADFS로 전송 될 때 연결 하는 IP 주소를 HTTP 패킷에서 원본 IP로 변환 해야 하는지 확인 해야 합니다. 부하 분산 장치가 HTTP 패킷에서 원본 IP를 보낼 수 없는 경우에는 부하 분산 장치가 x 전달 된 헤더에 IP 주소를 추가 (또는 기존 경우에 추가) 해야 합니다. 특정 IP 관련 기능 (금지 된 IP, 엑스트라넷 스마트 잠금,...)을 올바르게 처리 하는 데 필요 하며, 부적절 하 게 구성 된 경우 보안이 약화 될 수 있습니다.
- 부하 분산 장치는 SNI를 지원 해야 합니다. 그렇지 않은 이벤트에서 SNI 가능 클라이언트를 처리 하는 HTTPS 바인딩을 만들도록 AD FS 구성 되어 있는지 확인 합니다.
- 부하 분산 장치는 AD FS HTTP 상태 프로브 끝점을 사용 하 여 AD FS 또는 WAP 서버가 실행 중인지 확인 하 고 200 확인이 반환 되지 않은 경우이를 제외 해야 합니다.

### <a name="what-multi-forest-configurations-are-supported-by-ad-fs"></a>AD FS에서 지 원하는 다중 포리스트 구성은 무엇입니까?

AD FS는 다중 포리스트 구성을 여러 개 지원 하며, 신뢰할 수 있는 여러 영역에서 사용자를 인증 하기 위해 기본 AD DS 신뢰 네트워크에 의존 합니다. 양방향 포리스트 트러스트를 사용 하는 것이 좋습니다 .이는 트러스트 하위 시스템이 문제 없이 제대로 작동 하도록 하기 위한 간단한 설정입니다. 게다가

- 파트너 id를 포함 하는 DMZ 포리스트와 같은 단방향 포리스트 트러스트의 경우, ADFS를 corp 포리스트에 배포 하 고 DMZ 포리스트를 LDAP를 통해 연결 된 다른 로컬 클레임 공급자 트러스트로 처리 하는 것이 좋습니다. 이 경우 DMZ 포리스트 사용자에 대해 Windows 통합 인증을 사용할 수 없으며, LDAP에 대해 지원 되는 유일한 메커니즘인 암호 인증을 수행 해야 합니다. 이 옵션을 사용할 수 없는 경우에는 DMZ 포리스트에 다른 ADFS를 설정 하 고이를 corp 포리스트의 ADFS에 클레임 공급자 트러스트로 추가 해야 합니다. 사용자는 홈 영역 검색을 수행 해야 하지만 Windows 통합 인증 및 암호 인증을 모두 사용할 수 있습니다. Corp 포리스트의 ADFS에서 DMZ 포리스트의 사용자에 대 한 추가 사용자 정보를 가져올 수 없기 때문에 DMZ 포리스트의 ADFS에 있는 발급 규칙을 적절 하 게 변경 하십시오.
- 도메인 수준 트러스트가 지원 되 고 작동할 수 있지만 포리스트 수준 트러스트 모델로 이동 하는 것이 좋습니다. 또한 이름의 UPN 라우팅 및 NETBIOS 이름 확인이 정확 하 게 작동 해야 하는지 확인 해야 합니다.



## <a name="design"></a>디자인

### <a name="what-third-party-multi-factor-authentication-providers-are-available-for-ad-fs"></a>AD FS에 대해 사용할 수 있는 타사 multi-factor authentication 공급자는 무엇입니까?
AD FS는 타사 MFA 공급자를 통합 하는 데 사용할 수 있는 확장 가능한 메커니즘을 제공 합니다. 이에 대 한 인증 프로그램은 설정 되지 않습니다. 공급 업체는 릴리스 전에 필요한 유효성 검사를 수행 했다고 가정 합니다. 

Microsoft에 알림이 제공 된 공급 업체 목록에는 [AD FS에 대 한 MFA 공급자](../operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)가 게시 됩니다.  언제 든 지 알 수 없는 공급자가 있을 수 있으며,이에 대해 알아볼 때 목록을 업데이트 합니다.

### <a name="are-third-party-proxies-supported-with-ad-fs"></a>타사 프록시가 AD FS 지원 되나요?
예, 타사 프록시를 웹 응용 프로그램 프록시 앞에 배치할 수 있지만 타사 프록시는 웹 응용 프로그램 프록시 대신 사용할 [MS ADFSPIP 프로토콜](https://msdn.microsoft.com/library/dn392811.aspx) 을 지원 해야 합니다.

다음은 알고 있는 타사 공급자 목록입니다.  언제 든 지 알 수 없는 공급자가 있을 수 있으며,이에 대해 알아볼 때 목록을 업데이트 합니다.

- [F5 액세스 정책 관리자](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-third-party-integration-13-1-0/12.html#guid-1ee8fbb3-1b33-4982-8bb3-05ae6868d9ee)


### <a name="where-is-the-capacity-planning-sizing-spreadsheet-for-ad-fs-2016"></a>AD FS 2016에 대 한 용량 계획 크기 조정 스프레드시트는 어디에 있나요?
AD FS 2016 버전의 스프레드시트는 [여기](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)에서 다운로드할 수 있습니다.
이는 Windows Server 2012 r 2의 AD FS에도 사용할 수 있습니다.

### <a name="how-can-i-ensure-my-ad-fs-and-wap-servers-support-apples-atp-requirements"></a>내 AD FS 및 WAP 서버에서 Apple ATP 요구 사항을 지원 하는지 확인 하려면 어떻게 해야 하나요?

Apple은 AD FS를 인증 하는 iOS 앱의 호출에 영향을 줄 수 있는 ATS (App Transport Security) 라는 요구 사항 집합을 릴리스 했습니다.  [ATS를 사용 하 여 연결 하는 데 필요한 요구 사항을](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)지원 하는지 확인 하 여 AD FS 및 WAP 서버가 준수 하는지 확인할 수 있습니다.  
특히 AD FS 및 WAP 서버에서 TLS 1.2을 지원 하 고 TLS 연결의 협상 된 암호 그룹에서 완벽 한 전달 보안을 지원 하는지 확인 해야 합니다.

[AD FS에서 Ssl 프로토콜 관리](../operations/Manage-SSL-Protocols-in-AD-FS.md)를 사용 하 여 ssl 2.0 및 3.0 및 TLS 버전 1.0, 1.1 및 1.2을 사용 하거나 사용 하지 않도록 설정할 수 있습니다.

AD FS 및 WAP 서버가 ATP를 지 원하는 TLS 암호 그룹만을 협상 하도록 하기 위해 [atp 규격 암호 그룹 목록](https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW57)에 없는 모든 암호 그룹을 사용 하지 않도록 설정할 수 있습니다.  이렇게 하려면 [WINDOWS TLS PowerShell cmdlet](https://technet.microsoft.com/itpro/powershell/windows/tls/index)을 사용 합니다.

## <a name="developer"></a>Developer

### <a name="when-generating-an-id_token-with-adfs-for-a-user-authenticated-against-ad-how-is-the-sub-claim-generated-in-the-id_token"></a>AD에 대해 인증 된 사용자에 대해 ADFS를 사용 하 여 id_token를 생성 하는 경우 id_token에서 "sub" 클레임이 어떻게 생성 되나요?
"Sub" 클레임의 값은 클라이언트 ID + 앵커 클레임 값의 해시입니다.

### <a name="what-is-the-lifetime-of-the-refresh-tokenaccess-token-when-the-user-logs-in-via-a-remote-claims-provider-trust-over-ws-fedsaml-p"></a>사용자가 WS-급지됨/SAML-P를 통해 원격 클레임 공급자 트러스트를 통해 로그인 하는 경우 새로 고침 토큰/액세스 토큰의 수명은 무엇 인가요?
새로 고침 토큰의 수명은 ADFS가 원격 클레임 공급자 트러스트에서 가져온 토큰의 수명입니다. 액세스 토큰의 수명은 액세스 토큰을 발급 하는 신뢰 당사자의 토큰 수명이 됩니다.

### <a name="i-need-to-return-profile-and-email-scopes-as-well-in-addition-to-the-openid-scope-can-i-obtain-additional-information-using-scopes-how-to-do-it-in-ad-fs"></a>Openid connect 범위 뿐만 아니라 프로필 및 전자 메일 범위만 반환 해야 합니다. 범위를 사용 하 여 추가 정보를 가져올 수 있나요? AD FS에서이 작업을 수행 하는 방법
사용자 지정 된 id_token를 사용 하 여 id_token 자체에 관련 정보를 추가할 수 있습니다. 자세한 내용은 [id_token에서 내보낼 클레임 사용자 지정](../development/Custom-Id-Tokens-in-AD-FS.md)문서를 참조 하세요.

### <a name="how-to-issue-json-blobs-inside-jwt-tokens"></a>JWT 토큰 내에서 json blob을 발급 하는 방법
이에 대 한 특수<http://www.w3.org/2001/XMLSchema#json>ValueType ("") 및 이스케이프 문자 (\x22)가 AD FS 2016에 추가 되었습니다. 발급 규칙에 대해 아래 샘플을 확인 하 고 액세스 토큰의 최종 출력도 확인 하세요.

샘플 발급 규칙:

    => issue(Type = "array_in_json", ValueType = "http://www.w3.org/2001/XMLSchema#json", Value = "{\x22Items\x22:[{\x22Name\x22:\x22Apple\x22,\x22Price\x22:12.3},{\x22Name\x22:\x22Grape\x22,\x22Price\x22:3.21}],\x22Date\x22:\x2221/11/2010\x22}");

액세스 토큰에서 발급 된 클레임:

    "array_in_json":{"Items":[{"Name":"Apple","Price":12.3},{"Name":"Grape","Price":3.21}],"Date":"21/11/2010"}

### <a name="can-i-pass-resource-value-as-part-of-the-scope-value-like-how-requests-are-done-against-azure-ad"></a>Azure AD에 대 한 요청이 수행 되는 방법과 같이 범위 값의 일부로 리소스 값을 전달할 수 있나요?
서버 2019에서 AD FS를 사용 하 여 이제 범위 매개 변수에 포함 된 리소스 값을 전달할 수 있습니다. 이제 범위 매개 변수를 공백으로 구분 된 목록으로 구성할 수 있습니다. 여기서 각 항목은 리소스/범위의 구조입니다. 예  
**< 올바른 샘플 요청을 만듭니다 >**

### <a name="does-ad-fs-support-pkce-extension"></a>PKCE 확장을 지원할 AD FS 있나요?
Server 2019의 AD FS는 OAuth 인증 코드 부여 흐름에 대 한 PKCE (코드 교환에 대 한 증명 키)를 지원 합니다.

### <a name="what-permitted-scopes-are-supported-by-ad-fs"></a>AD FS에서 지 원하는 허용 범위는 무엇입니까?
- aza- [Broker 클라이언트에 OAuth 2.0 프로토콜 확장](https://docs.microsoft.com/openspecs/windows_protocols/ms-oapxbc/2f7d8875-0383-4058-956d-2fb216b44706) 을 사용 하는 경우 범위 매개 변수에 "aza" 범위가 포함 되어 있으면 서버가 새 주 새로 고침 토큰을 발급 하 고 응답의 refresh_token 필드에 해당 토큰을 설정 하 고 refresh_token_를 설정 합니다. expires_in이 적용 되는 경우 새 주 새로 고침 토큰의 수명으로 필드를 유지 합니다.
- openid connect-응용 프로그램에서 Openid connect Connect 권한 부여 프로토콜의 사용을 요청할 수 있습니다.
- logon_cert-logon_cert 범위를 통해 응용 프로그램은 인증 된 사용자를 대화형으로 로그온 하는 데 사용할 수 있는 로그온 인증서를 요청할 수 있습니다. AD FS 서버는 응답에서 access_token 매개 변수를 생략 하 고 대신 b a s e 64로 인코딩된 CMS 인증서 체인 또는 CMC 전체 PKI 응답을 제공 합니다. 자세한 내용은 [여기](https://docs.microsoft.com/openspecs/windows_protocols/ms-oapx/32ce8878-7d33-4c02-818b-6c9164cc731e)에 있습니다. 
- user_impersonation-AD FS에서 온-액세스 토큰을 성공적으로 요청 하려면 user_impersonation 범위가 필요 합니다. 이 범위를 사용 하는 방법에 대 한 자세한 내용은 [AD FS 2016에서 OAuth를 사용 하 여 OBO (온-)를 사용 하는 다중 계층 응용 프로그램 빌드를](../../ad-fs/development/ad-fs-on-behalf-of-authentication-in-windows-server.md)참조 하세요.
- vpn_cert-vpn_cert 범위를 사용 하면 응용 프로그램에서 VPN 인증서를 요청할 수 있으며,이는 EAP-TLS 인증을 사용 하 여 VPN 연결을 설정 하는 데 사용할 수 있습니다. 이는 더 이상 지원 되지 않습니다.
- 전자 메일-응용 프로그램에서 로그인 한 사용자에 대 한 전자 메일 클레임을 요청할 수 있습니다. 이는 더 이상 지원 되지 않습니다. 
- 프로필-응용 프로그램에서 로그인 사용자에 대 한 프로필 관련 클레임을 요청할 수 있습니다. 이는 더 이상 지원 되지 않습니다. 


## <a name="operations"></a>작업

### <a name="how-do-i-replace-the-ssl-certificate-for-ad-fs"></a>AD FS에 대 한 SSL 인증서를 어떻게 할까요? 바꾸시겠습니까?
AD FS SSL 인증서는 AD FS 관리 스냅인에 있는 AD FS 서비스 통신 인증서와 동일 하지 않습니다.  AD FS SSL 인증서를 변경 하려면 PowerShell을 사용 해야 합니다. 아래 문서의 지침을 따르세요.

[AD FS 및 WAP 2016의 SSL 인증서 관리](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)

### <a name="how-can-i-enable-or-disable-tlsssl-settings-for-ad-fs"></a>AD FS에 대 한 TLS/SSL 설정을 사용 하거나 사용 하지 않도록 설정 하려면 어떻게 해야 하나요?
SSL 프로토콜 및 암호 그룹을 사용 하지 않거나 사용 하도록 설정 하려면 다음을 사용 합니다.

[AD FS에서 SSL 프로토콜 관리](../operations/Manage-SSL-Protocols-in-AD-FS.md)

### <a name="does-the-proxy-ssl-certificate-have-to-be-the-same-as-the-ad-fs-ssl-certificate"></a>프록시 SSL 인증서 AD FS SSL 인증서와 동일 해야 하나요?  
프록시 SSL 인증서 및 AD FS SSL 인증서와 관련 하 여 다음 지침을 사용 합니다.


- 프록시를 사용 하는 경우 Windows 통합 인증을 프록시 SSL 인증서를 사용 하는 AD FS 프록시 요청 동일 해야 (동일한 키를 사용 하 여) 페더레이션 서버 SSL 인증서로
- "ExtendedProtectionTokenCheck"는 AD FS 속성 설정 (기본 AD FS에서 설정), 프록시 SSL 인증서 동일 해야 (동일한 키를 사용 하 여) 페더레이션 서버 SSL 인증서로
- 그렇지 않으면 프록시 SSL 인증서 AD FS SSL 인증서와 다른 키를 사용할 수 있지만 동일한 [요구 사항을](../overview/AD-FS-2016-Requirements.md) 충족 해야 합니다.

### <a name="why-do-i-only-see-a-password-login-on-ad-fs-and-not-my-other-authentication-methods-that-i-have-configured"></a>구성 된 다른 인증 방법이 아닌 AD FS에 암호 로그인만 표시 되는 이유는 무엇 인가요? 
AD FS는 응용 프로그램에 구성 및 사용 인증 방법에 매핑되는 특정 인증 URI가 명시적으로 필요한 경우 로그인 화면에 단일 인증 방법만 표시 합니다. 이는 WS-FEDERATION 요청에 대 한 ' wauth ' 매개 변수와 SAML 프로토콜 요청에서 ' RequestedAuthnCtxRef ' 매개 변수로 전달 됩니다. 따라서 요청 된 인증 방법 (예: 암호 로그인)만 표시 됩니다.

Azure AD에서 AD FS를 사용 하는 경우 응용 프로그램에서 prompt = login 매개 변수를 Azure AD로 보내는 것이 일반적입니다. 기본적으로 Azure AD는 AD FS에 대 한 새 암호 기반 로그인 요청으로이를 변환 합니다. 이는 네트워크 내 AD FS에서 암호 로그인을 확인 하거나 인증서를 사용 하 여 로그인 하는 옵션이 표시 되지 않는 가장 일반적인 이유입니다. 이는 Azure AD에서 페더레이션된 도메인 설정을 변경 하 여 쉽게 해결할 수 있습니다. 

이를 구성 하는 방법에 대 한 자세한 내용은 [Active Directory Federation Services 프롬프트 = 로그인 매개 변수 지원](../operations/AD-FS-Prompt-Login.md)을 참조 하세요.

### <a name="how-can-i-change-the-ad-fs-service-account"></a>AD FS 서비스 계정을 변경 하려면 어떻게 해야 하나요?
AD FS 서비스 계정을 변경 하려면 AD FS 도구 상자 [서비스 계정 Powershell 모듈](https://github.com/Microsoft/adfsToolbox/tree/master/serviceAccountModule)을 사용 하는 지침을 따르세요.

### <a name="how-can-i-configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>AD FS에서 WIA (Windows 통합 인증)를 사용 하도록 브라우저를 구성 하려면 어떻게 해야 하나요?

브라우저를 구성 하는 방법에 대 한 자세한 내용은 [AD FS에서 WIA (Windows 통합 인증)를 사용 하도록 브라우저 구성을](../operations/Configure-AD-FS-Browser-WIA.md)참조 하세요.

### <a name="can-i-turn-off-browserssoenabled"></a>BrowserSsoEnabled를 끌 수 있나요?
Adfs의 장치 또는 ADFS를 사용 하는 비즈니스용 Windows Hello 인증서 등록을 기반으로 하는 액세스 제어 정책이 없는 경우 BrowserSsoEnabled를 해제할 수 있습니다. BrowserSsoEnabled를 사용 하면 ADFS가 장치 정보를 포함 하는 클라이언트에서 PRT (기본 새로 고침 토큰)를 수집할 수 있습니다. Windows 10 장치에서는 ADFS의 장치 인증이 작동 하지 않습니다.

### <a name="how-long-are-ad-fs-tokens-valid"></a>AD FS 토큰이 유효한 기간

이 질문은 일반적으로 사용자가 새 자격 증명을 입력 하지 않고도 SSO (single sign on)를 사용 하는 방법 및 관리 컨트롤을 어떻게 사용할 수 있나요? '를 의미 합니다.  이 동작 및이 동작을 제어 하는 구성 설정은 [AD FS Single Sign-on 설정](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-2016-single-sign-on-settings)문서에 설명 되어 있습니다.

다양 한 쿠키 및 토큰의 기본 수명은 다음과 같이 표시 됩니다 (수명을 제어 하는 매개 변수).

**등록 된 장치**

- PRT 및 SSO 쿠키: PSSOLifeTimeMins에 의해 관리 되는 90 일 최대값 제공 된 장치는 최소 14 일 마다 사용 되며 DeviceUsageWindow에 의해 제어 됩니다.

- 새로 고침 토큰: 일관 된 동작을 제공 하기 위해 위의을 기준으로 계산 됩니다.

- access_token: 기본적으로 신뢰 당사자를 기준으로 1 시간

- id_token: 액세스 토큰과 동일

**등록 취소 된 장치**

- SSO 쿠키: 기본적으로 8 시간으로, SSOLifetimeMins에 의해 제어 됩니다.  KMSI (로그인 유지)를 사용 하는 경우 기본값은 24 시간이 고 KMSILifetimeMins을 통해 구성할 수 있습니다.


- 새로 고침 토큰: 기본적으로 8 시간입니다. KMSI를 사용 하는 24 시간

- access_token: 기본적으로 신뢰 당사자를 기준으로 1 시간

- id_token: 액세스 토큰과 동일

### <a name="does-ad-fs-support-http-strict-transport-security-hsts"></a>는 HTTP HSTS (Strict Transport Security)를 지원 AD FS?  

HSTS (HTTP Strict Transport Security)는 HTTP 및 HTTPS 끝점이 모두 포함 된 서비스에 대 한 프로토콜 다운 그레이드 공격 및 쿠키 가로채기를 완화 하는 데 도움이 되는 웹 보안 정책 메커니즘입니다. 웹 서버에서 웹 브라우저 (또는 기타 준수 사용자 에이전트)가 HTTPS를 사용 하 여 HTTP 프로토콜을 통해 상호 작용 하는 경우에만 해당 웹 브라우저 또는 다른 사용자 에이전트를 선언할 수 있습니다.

웹 인증 트래픽에 대 한 모든 AD FS 끝점은 HTTPS를 통해서만 열 수 있습니다.  결과적으로 http 엄격한 전송 보안 정책 메커니즘이 제공 하는 위협을 효과적으로 완화 하는 AD FS (HTTP에 수신기가 없기 때문에 HTTP에 다운 그레이드를 하지 않음). 또한 AD FS는 보안 플래그를 사용 하 여 모든 쿠키를 표시 함으로써 쿠키가 HTTP 프로토콜 끝점을 사용 하는 다른 서버로 전송 되는 것을 방지 합니다.

따라서 AD FS 서버에서 HSTS를 구현 하는 것은 다운 그레이드할 수 없기 때문에 필요 하지 않습니다.  규정 준수를 위해 AD FS 서버는 HTTP를 사용할 수 없고 모든 쿠키가 안전 하 게 표시 되기 때문에 이러한 요구 사항을 충족 합니다.

또한 AD FS 2016 (최신 패치 사용) 및 AD FS 2019에서 HSTS 헤더를 내보낼 수 있습니다. 이를 구성 하려면 [AD FS 사용 하 여 HTTP 보안 응답 헤더 사용자 지정](../operations/customize-http-security-headers-ad-fs.md) 을 참조 하세요.

### <a name="x-ms-forwarded-client-ip-does-not-contain-the-ip-of-the-client-but-contains-ip-of-the-firewall-in-front-of-the-proxy-where-can-i-get-the-right-ip-of-the-client"></a>X-ms 전달-클라이언트 ip는 클라이언트의 IP를 포함 하지 않지만 프록시 앞에 방화벽의 IP를 포함 합니다. 클라이언트의 올바른 IP는 어디에서 얻을 수 있나요?
WAP 이전에는 SSL 종료를 수행 하지 않는 것이 좋습니다. WAP 앞에서 SSL 종료를 수행 하는 경우 X-ms로 전달 된-클라이언트 ip에는 WAP 앞에 네트워크 장치의 IP가 포함 됩니다. 다음은 AD FS에서 지 원하는 다양 한 IP 관련 클레임에 대 한 간단한 설명입니다.
 - x-m-클라이언트-ip: STS에 연결 된 장치의 네트워크 IP입니다.  엑스트라넷 요청의 경우이는 항상 WAP의 IP를 포함 합니다.
 - x------------ip: 다중 값 클레임-Exchange Online에서 ADFS에 전달 된 값과 WAP에 연결 된 장치의 IP 주소를 포함 합니다.
 - Userip: 엑스트라넷 요청에 대해이 클레임은 x-ms로 전달 된-클라이언트 ip 값을 포함 합니다.  인트라넷 요청의 경우이 클레임은 x-m s-i p--와 동일한 값을 포함 합니다.

 또한 AD FS 2016 (최신 패치 포함)에서 더 높은 버전은 x 전달 된 헤더 캡처도 지원 합니다. 계층 3에서 전달 되지 않는 모든 부하 분산 장치 또는 네트워크 장치 (IP가 유지 됨)는 들어오는 클라이언트 IP를 업계 표준 x 전달 됨 헤더에 추가 해야 합니다. 

### <a name="i-am-trying-to-get-additional-claims-on-the-user-info-endpoint-but-its-only-returning-subject-how-can-i-get-additional-claims"></a>사용자 정보 끝점에서 추가 클레임을 가져오려고 했지만 제목만 반환 합니다. 추가 클레임을 얻으려면 어떻게 해야 하나요?
AD FS userinfo 끝점은 항상 Openid connect 표준에 지정 된 대로 주체 클레임을 반환 합니다. AD FS는 UserInfo 끝점을 통해 요청 된 추가 클레임을 제공 하지 않습니다. ID 토큰에 추가 클레임이 필요한 경우 [AD FS에서 사용자 지정 ID 토큰](../development/custom-id-tokens-in-ad-fs.md)을 참조 하세요.

### <a name="why-do-i-see-a-lot-of-1021-errors-on-my-ad-fs-servers"></a>AD FS 서버에서 1021 오류가 많이 표시 되는 이유는 무엇 인가요?
이 이벤트는 일반적으로 리소스 00000003-0000-0000-c000-000000000000에 대 한 AD FS의 잘못 된 리소스 액세스에 대해 기록 됩니다. 이 오류는 Azure AD Graph 서비스에 대 한 액세스 토큰을 가져오려고 시도 하는 클라이언트의 잘못 된 동작으로 인해 발생 합니다. 리소스가 AD FS에 존재 하지 않기 때문에 AD FS 서버에서 이벤트 ID 1021이 발생 합니다. AD FS에서 리소스 00000003-0000-0000-c000-000000000000에 대 한 경고 또는 오류를 무시 해도 안전 합니다.

### <a name="why-am-i-seeing-a-warning-for-failure-to-add-the-ad-fs-service-account-to-the-enterprise-key-admins-group"></a>엔터프라이즈 키 관리자 그룹에 AD FS 서비스 계정을 추가 하는 데 실패 하는 경우 경고가 표시 되는 이유는 무엇 인가요?
이 그룹은 FSMO PDC 역할이 있는 Windows 2016 도메인 컨트롤러가 도메인에 있는 경우에만 생성 됩니다. 이 오류를 해결 하려면 그룹을 수동으로 만들고 아래를 따라 서비스 계정을 그룹 구성원으로 추가한 후 필요한 사용 권한을 부여할 수 있습니다.
1.  **Active Directory 사용자 및 컴퓨터**를 엽니다.
2.  탐색 창에서 도메인 이름을 **마우스 오른쪽 단추로 클릭** 하 고 속성을 **클릭** 합니다.
3.  **클릭** 합니다. 보안 (보안 탭이 없는 경우 보기 메뉴에서 고급 기능을 켭니다.)
4.  **클릭** 합니다. 고급. **클릭** 합니다. 추가. **클릭** 합니다. 보안 주체를 선택 합니다.
5.  사용자, 컴퓨터, 서비스 계정 또는 그룹 선택 대화 상자가 나타납니다.  선택할 개체 이름을 입력 하십시오. 텍스트 상자에 키 관리 그룹을 입력 합니다.  확인을 클릭합니다.
6.  적용 대상 목록 상자에서 **하위 사용자 개체**를 선택 합니다.
7.  스크롤 막대를 사용 하 여 페이지 아래쪽으로 스크롤한 다음 모두 지우기를 **클릭** 합니다.
8.  **속성** 섹션에서 **Read의 msds-primary-computer-KeyCredentialLink** 및 **Write의 msds-primary-computer-KeyCredentialLink**를 선택 합니다.

### <a name="why-does-modern-authentication-from-android-devices-fail-if-the-server-does-not-send-all-the-intermediate-certificates-in-the-chain-with-the-ssl-cert"></a>서버에서 SSL 인증서를 사용 하 여 체인의 모든 중간 인증서를 보내지 않는 경우 Android 장치에서 최신 인증이 실패 하는 이유는 무엇 인가요?

페더레이션 사용자는 Android ADAL 라이브러리를 사용 하지 못하는 앱에 대해 Azure AD에 대 한 인증을 경험할 수 있습니다. 앱은 로그인 페이지를 표시 하려고 할 때 **Authenticationexception** 을 받습니다. Chrome에서는 AD FS 로그인 페이지를 안전 하지 않은 것으로 호출할 수 있습니다.

Android-모든 버전 및 모든 장치에서-인증서의 **authorityInformationAccess** 필드에서 추가 인증서를 다운로드 하는 것을 지원 하지 않습니다. Chrome 브라우저의 경우에도 마찬가지입니다. 중간 인증서가 없는 모든 서버 인증 인증서는 AD FS에서 전체 인증서 체인이 전달 되지 않은 경우이 오류가 발생 합니다.

이 문제에 대 한 적절 한 해결 방법은 필요한 중간 인증서를 SSL 인증서와 함께 보내도록 AD FS 및 WAP 서버를 구성 하는 것입니다.

한 컴퓨터에서 컴퓨터의 개인 저장소 (AD FS 및 WAP 서버)로 가져올 SSL 인증서를 내보내는 경우 개인 키를 내보내고 **개인 정보 교환-PKCS #12**를 선택 해야 합니다.

**가능 하면 인증서 경로에 모든 인증서를 포함** 하는 확인란을 선택 하 고 **모든 확장 속성을 내보냅니다**.  

Windows 서버에서 a l m .msc를 실행 하 고 *를 가져옵니다. PFX를 컴퓨터의 개인 인증서 저장소로 복사 합니다. 이렇게 하면 서버에서 전체 인증서 체인을 ADAL 라이브러리로 전달 합니다.

>[!NOTE]
> 네트워크 부하 분산 장치의 인증서 저장소도 있는 경우 전체 인증서 체인을 포함 하도록 업데이트 해야 합니다.

### <a name="does-ad-fs-support-head-requests"></a>AD FS HEAD 요청을 지원 하나요?
AD FS는 HEAD 요청을 지원 하지 않습니다.  응용 프로그램은 AD FS 끝점에 대해 HEAD 요청을 사용 하지 않아야 합니다.  이로 인해 예기치 않은 HTTP 오류 응답이 발생 하거나 지연 될 수 있습니다.  또한 AD FS 이벤트 로그에 예기치 않은 오류 이벤트가 표시 될 수 있습니다.

### <a name="why-am-i-not-seeing-a-refresh-token-when-i-am-logging-in-with-a-remote-idp"></a>원격 IdP를 사용 하 여 로그인 할 때 새로 고침 토큰이 표시 되지 않는 이유는 무엇 인가요?
IdP에서 발급 한 토큰의 유효한 단위가 1 시간 미만인 경우에는 새로 고침 토큰이 발급 되지 않습니다. 새로 고침 토큰이 발급 되었는지 확인 하려면 IdP에서 발급 한 토큰의 유효성을 1 시간 이상으로 늘립니다.

### <a name="do-we-have-any-way-to-change-rp-token-encryption-algorithm"></a>RP 토큰 암호화 알고리즘을 변경 하는 방법이 있나요?
기본적으로 RP 토큰 암호화는 AES256로 설정 되며 다른 값으로 변경할 수 없습니다.

### <a name="on-a-mixed-mode-farm-i-get-error-when-trying-to-set-the-new-ssl-certificate-using-set-adfssslcertificate--thumbprint-how-can-i-update-the-ssl-certificate-in-a-mixed-mode-ad-fs-farm"></a>혼합 모드 팜에서 Set-adfssslcertificate-Thumbprint를 사용 하 여 새 SSL 인증서를 설정 하려고 하면 오류가 발생 합니다. 혼합 모드 AD FS 팜에서 SSL 인증서를 업데이트 하려면 어떻게 해야 하나요?
혼합 모드 AD FS 팜은 transitionary 상태가 됩니다. 업그레이드 프로세스 전에 SSL 인증서를 롤오버 하거나 프로세스를 완료 하 고 SSL 인증서를 업데이트 하기 전에 팜 동작 수준을 늘리는 것이 좋습니다. 이 작업을 수행 하지 않은 경우에는 아래 지침에 따라 SSL 인증서를 업데이트할 수 있는 기능이 제공 됩니다. 

WAP 서버에서 WebApplicationProxySslCertificate을 계속 사용할 수 있습니다. ADFS 서버에서 netsh를 사용 해야 합니다. 아래 지정 된 단계를 수행 합니다.

1. 유지 관리를 위해 ADFS 2016 서버의 하위 집합을 선택 합니다 (예: 부하 분산 장치에서 제거).
2. #1에서 선택한 서버에서 MMC를 통해 새 인증서를 가져옵니다.
3. 기존 인증서를 삭제 합니다.

    a. netsh http delete sslcert hostnameport: 443 b. netsh http delete sslcert hostnameport = localhost: 443 c. netsh http delete sslcert hostnameport = 49443

4.  새 인증서 추가

    a. netsh http add sslcert hostnameport: 443 certhash = CERTTHUMBPRINT appid = {5d89a20c-beab-4389-9447-324788eb944a} certstorename = MY sslctlstorename = AdfsTrustedDevices

    b. netsh http add sslcert hostnameport = localhost: 443 certhash = CERTTHUMBPRINT appid = {5d89a20c-beab-4389-9447-324788eb944a} certstorename = MY sslctlstorename = AdfsTrustedDevices

    c. netsh http add sslcert hostnameport: 49443 certhash = CERTTHUMBPRINT appid = {5d89a20c-beab-4389-9447-324788eb944a} certstorename = MY sslctlstorename = AdfsTrustedDevices

5. 선택한 서버에서 ADFS 서비스를 다시 시작 합니다.
6. 유지 관리를 위해 WAP 서버 하위 집합 제거
7. 선택한 WAP 서버에서 MMC를 통해 새 인증서를 가져옵니다.
8. Cmdlet을 사용 하 여 WAP에서 새 인증서 설정

    a. WebApplicationProxySslCertificate-지문 "CERTTHUMBPRINT"

9. 선택한 WAP 서버에서 서비스를 다시 시작 합니다.
10. 선택한 WAP 및 AD FS 서버를 프로덕션 환경에 다시 배치 합니다.

다른 AD FS 및 WAP 서버에 대 한 업데이트를 비슷한 방식으로 수행 합니다.

### <a name="is-adfs-supported-when-web-application-proxy-wap-servers-are-behind-azure-web-application-firewallwaf"></a>WAP (웹 응용 프로그램 프록시) 서버가 Azure WAF (웹 응용 프로그램 방화벽) 뒤에 있을 때 ADFS가 지원 되나요?
ADFS 및 웹 응용 프로그램 서버는 끝점에서 SSL 종료를 수행 하지 않는 모든 방화벽을 지원 합니다. 또한 ADFS/WAP 서버는 사이트 간 스크립팅, ADFS 프록시와 같은 일반적인 웹 공격을 방지 하는 메커니즘을 기본 제공 하며, [MS-ADFSPIP 프로토콜](https://msdn.microsoft.com/library/dn392811.aspx)에서 정의한 모든 요구 사항을 충족 합니다.

### <a name="i-am-seeing-an-event-441-a-token-with-a-bad-token-binding-key-was-found-what-should-i-do-to-resolve-this"></a>"이벤트 441: 토큰 바인딩 키가 잘못 된 토큰을 찾았습니다. " 이 문제를 해결 하려면 어떻게 해야 하나요?
AD FS 2016에서 토큰 바인딩이 자동으로 사용 하도록 설정 되 고이 오류가 발생 하는 프록시 및 페더레이션 시나리오에서 알려진 여러 문제가 발생 합니다. 이 문제를 해결 하려면 다음 Powershell 명령을 실행 하 고 토큰 바인딩 지원을 제거 합니다.

`Set-AdfsProperties -IgnoreTokenBinding $true`

### <a name="i-have-upgraded-my-farm-from-ad-fs-in-windows-server-2016-to-ad-fs-in-windows-server-2019-the-farm-behavior-level-for-the-ad-fs-farm-has-been-successfully-raised-to-2019-but-the-web-application-proxy-configuration-is-still-displayed-as-windows-server-2016"></a>내 팜을 windows Server 2016의 AD FS에서 Windows Server 2019의 AD FS로 업그레이드 했습니다. AD FS 팜에 대 한 팜 동작 수준이 2019에 성공적으로 발생 했지만 웹 응용 프로그램 프록시 구성이 Windows Server 2016로 계속 표시 되나요?
Windows Server 2019로 업그레이드 한 후에는 웹 응용 프로그램 프록시의 구성 버전이 Windows Server 2016로 계속 표시 됩니다. 웹 응용 프로그램 프록시에는 Windows Server 2019에 대 한 새로운 버전 관련 기능이 없으며, 팜 동작 수준이 AD FS에서 성공적으로 발생 한 경우에는 웹 응용 프로그램 프록시가 디자인을 통해 Windows Server 2016로 계속 표시 됩니다. 
