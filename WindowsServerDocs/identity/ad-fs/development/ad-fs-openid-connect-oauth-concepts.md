---
title: AD FS Openid connect Connect/OAuth 개념
description: 최신 인증 개념 AD FS에 대해 알아봅니다.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0e680e07ce1ee27a73791e310a71b85ad76d6318
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358764"
---
# <a name="ad-fs-openid-connectoauth-concepts"></a>AD FS Openid connect Connect/OAuth 개념
AD FS 2016 이상에 적용 됩니다.
 
## <a name="modern-authentication-actors"></a>최신 인증 행위자 

|행위자| 설명|
|-----|-----|
|최종 사용자|리소스에 액세스 해야 하는 보안 주체 (사용자, 응용 프로그램, 서비스 및 그룹)입니다.|  
|클라이언트|클라이언트 ID로 식별 되는 웹 응용 프로그램입니다. 클라이언트는 일반적으로 최종 사용자가 상호 작용 하는 당사자 이며 권한 부여 서버에서 토큰을 요청 합니다.
|권한 부여 서버/i d 공급자 (IdP)| AD FS 서버입니다. 조직의 디렉터리에 존재 하는 보안 주체의 id를 확인 하는 일을 담당 합니다. 보안 주체가 성공적으로 인증 되 면 보안 토큰 (전달자 액세스 토큰, ID 토큰, 새로 고침 토큰)이 발급 됩니다.
|리소스 서버/리소스 공급자/신뢰 당사자| 리소스 또는 데이터가 있는 위치입니다. 클라이언트를 안전 하 게 인증 하 고 권한을 부여 하는 권한 부여 서버를 신뢰 하 고 전달자 액세스 토큰을 사용 하 여 리소스에 대 한 액세스 권한을 부여할 수 있도록 합니다.

다음 다이어그램은 행위자 간의 가장 기본적인 관계를 제공 합니다.

![최신 인증 행위자](media/adfs-modern-auth-concepts/concept1.png)

## <a name="application-types"></a>응용 프로그램 종류 
 

|응용 프로그램 종류|설명|역할|
|-----|-----|-----|
|네이티브 응용 프로그램|**공용 클라이언트**라고도 하는이는 사용자가 상호 작용 하는 pc 또는 장치에서 실행 되는 클라이언트 앱이 될 수 있습니다.|리소스에 대 한 사용자 액세스 권한 부여 서버 (AD FS)의 토큰을 요청 합니다. HTTP 헤더와 토큰을 사용 하는 보호 된 리소스에 HTTP 요청을 보냅니다.| 
|서버 응용 프로그램 (웹 앱)|웹 응용 프로그램 서버에서 실행 되며 일반적으로 브라우저를 통해 사용자가 액세스할 수 있습니다. 자체 클라이언트 ' 암호 ' 또는 자격 증명을 유지할 수 있으므로 **기밀 클라이언트**라고도 합니다. |리소스에 대 한 사용자 액세스 권한 부여 서버 (AD FS)의 토큰을 요청 합니다. 토큰을 요청 하기 전에 클라이언트 (웹 앱)는 암호를 사용 하 여 인증 해야 합니다. | 
|Web API|최종 리소스는 사용자에 액세스 합니다. 이러한 "신뢰 당사자"의 새 표현으로 간주 합니다.|클라이언트에서 가져온 전달자 액세스 토큰을 사용 합니다.| 

## <a name="application-group"></a>응용 프로그램 그룹 
 
AD FS로 구성 된 모든 OAuth 클라이언트 (네이티브 또는 웹 앱) 또는 리소스 (웹 api)는 응용 프로그램 그룹에 연결 해야 합니다. 응용 프로그램 그룹의 클라이언트는 동일한 그룹의 리소스에 액세스 하도록 구성할 수 있습니다. 응용 프로그램 그룹에는 여러 클라이언트 및 리소스가 포함 될 수 있습니다.  

## <a name="security-tokens"></a>보안 토큰 
 
최신 인증은 다음 토큰 유형을 사용 합니다. 
- **id_token**: 권한 부여 서버 (AD FS)에서 발급 하 고 클라이언트에서 사용 하는 JWT 토큰입니다. ID 토큰의 클레임에는 클라이언트에서 사용할 수 있도록 사용자에 대 한 정보가 포함 됩니다.  
- **access_token**: 권한 부여 서버 (AD FS)에서 발급 하 고 리소스에서 사용 하기 위한 JWT 토큰입니다. 이 토큰의 'aud' 또는 대상 그룹 클레임 리소스 또는 웹 API의 식별자를 일치 해야 합니다.  
- **refresh_token**: 클라이언트에서 id_token 및 access_token를 새로 고쳐야 할 때 사용할 수 있도록 AD FS에서 발급 한 토큰입니다. 토큰은 클라이언트에 불투명 하며 AD FS만 사용할 수 있습니다.  

## <a name="scopes"></a>영역 
 
AD FS에서 리소스를 등록 하는 동안 AD FS 특정 작업을 수행할 수 있도록 범위를 구성할 수 있습니다. 범위를 구성 하는 것 외에도 작업을 수행 하는 AD FS에 대 한 요청에 범위 값을 전송 해야 합니다. 예를 들어, 관리자는 리소스 등록 중에 openid connect로 범위를 구성 해야 하 고, 응용 프로그램 (클라이언트)이 AD FS에 대 한 인증 요청에서 범위 = openid connect를 발급 ID 토큰으로 보내야 합니다. AD FS에서 사용할 수 있는 범위에 대 한 자세한 내용은 아래에 나와 있습니다. 
 
- aza- [Broker 클라이언트에 OAuth 2.0 프로토콜 확장](https://docs.microsoft.com/openspecs/windows_protocols/ms-oapxbc/2f7d8875-0383-4058-956d-2fb216b44706) 을 사용 하는 경우 하 고 범위 매개 변수에 "aza" 범위가 포함 되어 있으면 서버가 새 주 새로 고침 토큰을 발급 하 고 응답의 refresh_token 필드에 설정 하 고, 적용 되는 경우 새 주 새로 고침 토큰의 수명으로 refresh_token_expires_in 필드를 설정 합니다. 
- openid connect-응용 프로그램에서 Openid connect Connect 권한 부여 프로토콜의 사용을 요청할 수 있습니다. 
- logon_cert-logon_cert 범위를 통해 응용 프로그램은 인증 된 사용자를 대화형으로 로그온 하는 데 사용할 수 있는 로그온 인증서를 요청할 수 있습니다. AD FS 서버는 응답에서 access_token 매개 변수를 생략 하 고 대신 b a s e 64로 인코딩된 CMS 인증서 체인 또는 CMC 전체 PKI 응답을 제공 합니다. 자세한 내용은 [여기](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-oapx/32ce8878-7d33-4c02-818b-6c9164cc731e)에 있습니다.
- user_impersonation-AD FS에서 온-의 액세스 토큰을 성공적으로 요청 하려면 user_impersonation 범위가 필요 합니다. 이 범위를 사용 하는 방법에 대 한 자세한 내용은 AD FS 2016를 사용 하 여 OAuth를 사용 하 여 [(OBO)를 사용 하는 다중 계층 응용 프로그램 빌드](ad-fs-on-behalf-of-authentication-in-windows-server.md)를 참조 하세요. 
- allatclaims – allatclaims 범위를 사용 하면 응용 프로그램에서 액세스 토큰의 클레임을 ID 토큰에 추가 하도록 요청할 수도 있습니다.   
- vpn_cert-vpn_cert 범위를 통해 응용 프로그램은 EAP-TLS 인증을 사용 하 여 VPN 연결을 설정 하는 데 사용할 수 있는 VPN 인증서를 요청할 수 있습니다. 이는 더 이상 지원 되지 않습니다. 
- 전자 메일-응용 프로그램에서 로그인 한 사용자에 대 한 전자 메일 클레임을 요청할 수 있습니다.  
- 프로필-응용 프로그램에서 로그인 사용자에 대 한 프로필 관련 클레임을 요청할 수 있습니다.  

## <a name="claims"></a>클레임 
 
AD FS에서 발급 하는 보안 토큰 (액세스 및 ID 토큰)에는 인증 된 주체에 대 한 클레임 또는 정보 어설션이 포함 됩니다. 응용 프로그램은 다음을 비롯 한 다양 한 작업에 대해 클레임을 사용할 수 있습니다. 
- 토큰의 유효성을 검사 합니다. 
- 주체의 디렉터리 테 넌 트를 식별 합니다. 
- 사용자 정보 표시 
- 주체의 권한 부여 확인 지정 된 보안 토큰에 있는 클레임은 토큰 유형, 사용자를 인증 하는 데 사용 되는 자격 증명 유형, 응용 프로그램 구성에 따라 달라 집니다.  
 
## <a name="high-level-ad-fs-authentication-flow"></a>높은 수준 AD FS 인증 흐름 

![AD FS 인증 흐름](media/adfs-modern-auth-concepts/adfsauthflow.png)


 1. AD FS 클라이언트에서 인증 요청을 받습니다.  
 
 2. AD FS는 AD FS에서 클라이언트 및 리소스 등록 중에 가져온 클라이언트 ID를 사용 하 여 인증 요청에서 클라이언트 ID의 유효성을 검사 합니다. 기밀 클라이언트를 사용 하는 경우 AD FS는 인증 요청에 제공 된 클라이언트 암호의 유효성도 검사 합니다. 클라이언트의 리디렉션 uri도 유효성을 검사 AD FS 합니다. 
 
 3. AD FS는 클라이언트가 인증 요청에 전달 된 리소스 매개 변수를 통해 액세스 하려는 리소스를 식별 합니다. MSAL 클라이언트 라이브러리를 사용 하는 경우 리소스 매개 변수가 전송 되지 않습니다. 대신 범위 *= [리소스 url]//[범위 값 (예: openid connect])* 범위 매개 변수의 일부로 리소스 url이 전송 됩니다. 

    리소스가 리소스 또는 범위 매개 변수를 사용 하 여 전달 되지 않는 경우 ADFS는 기본 리소스 urn: microsoft: policy (예: MFA, 발급 또는 권한 부여 정책)를 구성할 수 없는 기본 리소스 urn을 사용 합니다. 
 
 4. 다음 AD FS 클라이언트에 리소스에 대 한 액세스 권한이 있는지 여부를 확인 합니다. 또한 AD FS는 인증 요청에 전달 된 범위가 리소스를 등록 하는 동안 구성 된 범위와 일치 하는지를 확인 합니다. 클라이언트에 권한이 없거나 올바른 범위가 인증 요청에서 전송 되지 않으면 인증 흐름이 종료 됩니다.   
 
 5. 사용 권한과 범위의 유효성을 검사 한 후에는 AD FS 구성 된 [인증 방법을](../operations/configure-authentication-policies.md)사용 하 여 사용자를 인증 합니다.   

 6. 리소스 정책 또는 전역 인증 정책에 따라 [추가 인증 방법이](../operations/configure-additional-authentication-methods-for-ad-fs.md) 필요한 경우 AD FS는 추가 인증을 트리거합니다. 

 7. AD FS는 [AZURE mfa](../operations/configure-ad-fs-and-azure-mfa.md) 또는 타사 [MFA](../operations/additional-authentication-methods-ad-fs.md) 를 사용 하 여 인증을 수행 합니다.   
 
 8. 사용자가 인증 되 면 [클레임 규칙](../deployment/configuring-claim-rules.md) (보안 토큰의 일부로 리소스에 전송 되는 클레임을 결정) 및 [액세스 제어 정책](../operations/ad-fs-client-access-policies.md) (사용자가 리소스에 액세스 하는 데 필요한 조건을 충족 하는지 결정)을 적용 AD FS 합니다.   

 9. 그런 다음 AD FS 액세스 및 새로 고침 토큰을 생성 합니다. 

 10. 또한 AD FS는 ID 토큰을 생성 합니다. 
 
 11. 범위 = allatclaims 인증 요청에 포함 된 경우 정의 된 클레임 규칙에 따라 액세스 토큰에 클레임을 포함 하도록 [ID 토큰을 사용자 지정](custom-id-tokens-in-ad-fs.md) 합니다. 
    
 12. 필요한 토큰이 생성 되 고 사용자 지정 되 면 AD FS는 토큰을 포함 하 여 클라이언트에 응답 합니다. 인증 요청에 scope = openid connect가 포함 된 경우에만 ID 토큰이 응답에 포함 됩니다. 클라이언트는 항상 토큰 끝점을 사용 하 여 ID 토큰 사후 인증을 가져올 수 있습니다. 

## <a name="types-of-libraries"></a>라이브러리 유형 
  
AD FS에는 두 가지 유형의 라이브러리가 사용 됩니다. 
- **클라이언트 라이브러리**: 네이티브 클라이언트 및 서버 앱은 클라이언트 라이브러리를 사용 하 여 Web API와 같은 리소스를 호출 하기 위한 액세스 토큰을 가져옵니다. MSAL (Microsoft 인증 라이브러리)은 AD FS 2019를 사용할 때 사용 되는 최신 클라이언트 라이브러리입니다. Active Directory 인증 라이브러리 (ADAL) AD FS 2016에 권장 됩니다.  

- **서버 미들웨어 라이브러리**: 웹 앱은 사용자 로그인에 서버 미들웨어 라이브러리를 사용 합니다. 웹 Api는 서버 미들웨어 라이브러리를 사용 하 여 네이티브 클라이언트 또는 다른 서버에서 보낸 토큰의 유효성을 검사 합니다. OWIN (Open Web Interface for .NET)은 권장 되는 미들웨어 라이브러리입니다. 

## <a name="customize-id-token-additional-claims-in-id-token"></a>ID 토큰 사용자 지정 (ID 토큰의 추가 클레임)
 
특정 시나리오에서 웹 앱 (클라이언트)은 기능을 지원 하기 위해 ID 토큰에 추가 클레임이 필요할 수 있습니다. 다음 옵션 중 하나를 사용 하 여이를 수행할 수 있습니다. 

**옵션 1:** 공용 클라이언트를 사용 하 고 웹 앱에 액세스 하려는 리소스가 없는 경우에 사용 해야 합니다. 옵션을 사용 하려면 
1.  response_mode 설정 form_post 
2.  신뢰 당사자 식별자 (웹 API 식별자)가 클라이언트 식별자와 동일 합니다.

![AD FS 토큰 옵션 1 사용자 지정](media/adfs-modern-auth-concepts/option1.png)

**옵션 2:** 웹 앱에 액세스 하려는 리소스가 있고 ID 토큰을 통해 추가 클레임을 전달 해야 하는 경우에 사용 해야 합니다. 공용 및 기밀 클라이언트를 모두 사용할 수 있습니다. 옵션을 사용 하려면 
1.  response_mode 설정 form_post 
2.  AD FS 서버에 KB4019472이 설치 되어 있습니다. 
3.  클라이언트에 할당 된 allatclaims 범위-RP 쌍 아래 예제에 표시 된 것 처럼 ADFSApplicationPermission (이미 한 번 부여 된 경우 AdfsApplicationPermission 사용) PowerShell cmdlet을 사용 하 여 범위를 할당할 수 있습니다. 

    ``` powershell
    Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
    ```

![AD FS 토큰 옵션 2 사용자 지정](media/adfs-modern-auth-concepts/option2.png)

사용자 지정 ID 토큰을 얻기 위해 ADFS에서 웹 앱을 구성 하는 방법을 더 잘 이해 하려면 [Openid connect Connect 또는 OAuth를 AD FS 2016 이상 사용 하는 경우 id_token에서 내보낼 클레임 사용자 지정](Custom-Id-Tokens-in-AD-FS.md)을 참조 하세요.

## <a name="single-log-out"></a>단일 로그 아웃

단일 로그 아웃으로 인해 세션 id를 사용 하 여 모든 클라이언트 세션이 종료 됩니다. AD FS 2016 이상에서는 Openid connect Connect/OAuth에 대 한 단일 로그 아웃을 지원 합니다. 자세한 내용은 [Openid connect Connect에 대 한 단일 로그 아웃 AD FS](ad-fs-logout-openid-connect.md)를 참조 하세요.


## <a name="ad-fs-endpoints"></a>AD FS 끝점

|AD FS 끝점|설명|
|-----|-----|
|/authorize|AD FS는 액세스 토큰을 가져오는 데 사용할 수 있는 인증 코드를 반환 합니다.|
|/token|AD FS는 리소스 (웹 API)에 액세스 하는 데 사용할 수 있는 액세스 토큰을 반환 합니다.|
|/userinfo|AD FS는 인증 된 사용자에 대 한 클레임을 반환 합니다.|
|/devicecode|AD FS는 장치 코드 및 사용자 코드를 반환 합니다.|
|/로그 아웃|사용자를 로그 아웃 AD FS|
|/키|응답에 서명 하는 데 사용 되는 공개 키 AD FS|
|/.well-known/openid-configuration|AD FS OAuth/Openid connect Connect 메타 데이터 반환|
