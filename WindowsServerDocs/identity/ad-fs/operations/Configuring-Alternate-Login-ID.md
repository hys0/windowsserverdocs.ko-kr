---
ms.assetid: f0cbdd78-f5ae-47ff-b5d3-96faf4940f4a
title: 대체 로그인 ID 구성
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 11/14/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 220b409b2e0bcc5e5a01aeb9f244ebaa55ac0e1e
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544604"
---
# <a name="configuring-alternate-login-id"></a>대체 로그인 ID 구성


## <a name="what-is-alternate-login-id"></a>대체 로그인 ID 란?
대부분의 시나리오에서 사용자는 UPN (사용자 계정 이름)을 사용 하 여 계정에 로그인 합니다. 그러나 회사 정책 또는 온-프레미스 lob (기간 업무) 응용 프로그램 종속성으로 인해 일부 환경에서는 사용자가 다른 형태의 로그인을 사용할 수 있습니다. 

>[!NOTE]
>Microsoft의 권장 모범 사례는 UPN과 기본 SMTP 주소를 일치 시키는 것입니다. 이 문서에서는 UPN이 일치 하도록 수정할 수 없는 소수의 고객을 해결 합니다.

예를 들어 로그인에 전자 메일 id를 사용 하 고 UPN과 다를 수 있습니다. 이는 특히 UPN을 라우팅할 수 없는 시나리오에서 발생 합니다. UPN jdoe@contoso.local 및 전자 메일 주소 jdoe@contoso.com를 사용 하는 Jane Doe 사용자를 고려 합니다. Jane은 로그인에 대해 항상 전자 메일 id를 사용 하 여 UPN을 인식 하지 못할 수도 있습니다. UPN 대신 다른 로그인 방법을 사용 하면 대체 ID가 구성 됩니다. UPN을 만드는 방법에 대 한 자세한 내용은 [AZURE AD UserPrincipalName 채우기](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname)를 참조 하세요.

Active Directory Federation Services (AD FS) AD FS를 사용 하 여 페더레이션 응용 프로그램에서 대체 ID를 사용 하 여 로그인 할 수 있습니다. 이를 통해 관리자는 로그인에 사용할 기본 UPN에 대 한 대안을 지정할 수 있습니다. AD FS은 Active Directory Domain Services (AD DS)에서 허용 하는 사용자 식별자의 모든 형태를 이미 지원 합니다. 대체 ID로 구성 된 경우 사용자는 전자 메일 id를 사용 하 여 구성 된 대체 ID 값을 사용 하 여 로그인 할 수 AD FS. 대체 ID를 사용 하면 온-프레미스 Upn을 수정 하지 않고 Office 365와 같은 SaaS 공급자를 채택할 수 있습니다. 또한 소비자 구성 된 id와 업무의 서비스 응용 프로그램을 지원할 수 있습니다.

## <a name="alternate-id-in-azure-ad"></a>Azure AD의 대체 id
조직은 다음과 같은 시나리오에서 대체 ID를 사용 해야 할 수 있습니다.
1. 온-프레미스 도메인 이름은 라우팅할 수 없습니다 (예:). 예를 들어 기본 사용자 계정 이름은 라우팅할 수 없는 (jdoe@contoso.local)입니다. 로컬 응용 프로그램 종속성 또는 회사 정책으로 인해 기존 UPN을 변경할 수 없습니다. Azure AD 및 Office 365는 완전히 인터넷 라우팅할 수 있도록 Azure AD 디렉터리와 연결 된 모든 도메인 접미사를 요구 합니다. 
2. 온-프레미스 UPN은 사용자의 전자 메일 주소와 동일 하지 않으며 Office 365에 로그인 하는 경우 사용자가 메일 주소를 사용 하 고 조직 제약 조건으로 인해 UPN을 사용할 수 없습니다.
   위에서 언급 한 시나리오에서 AD FS로 대체 ID를 사용 하면 사용자가 온-프레미스 Upn을 수정 하지 않고 Azure AD에 로그인 할 수 있습니다. 

## <a name="end-user-experience-with-alternate-login-id"></a>대체 로그인 ID를 사용 하는 최종 사용자 환경
최종 사용자 환경은 대체 로그인 id에 사용 되는 인증 방법에 따라 달라 집니다.  현재 대체 로그인 id를 사용 하는 세 가지 방법이 있습니다.  구현되지 않은 것은 다음과 같습니다.

- **일반 인증 (레거시)** -기본 인증 프로토콜을 사용 합니다.
- **최신 인증** -응용 프로그램에 ACTIVE DIRECTORY 인증 라이브러리 (ADAL) 기반 로그인을 가져옵니다. 이렇게 하면 Office 클라이언트 응용 프로그램, 스마트 카드 및 인증서 기반 인증을 사용 하 여 MFA (Multi-factor Authentication), SAML 기반 타사 Id 공급자와 같은 로그인 기능을 사용할 수 있습니다.
- **하이브리드 최신 인증** -최신 인증의 모든 이점을 제공 하 고 사용자에 게 클라우드에서 얻은 권한 부여 토큰을 사용 하 여 온-프레미스 응용 프로그램에 액세스할 수 있는 기능을 제공 합니다.

>[!NOTE]
> 가능한 최상의 환경을 위해 Microsoft에서는 하이브리드 최신 인증을 적극 권장 합니다.



## <a name="configure-alternate-logon-id"></a>대체 로그온 ID 구성
Azure AD Connect 사용 하 여 사용자 환경에 대 한 대체 로그온 ID를 구성 하려면 Azure AD Connect를 사용 하는 것이 좋습니다.

- Azure AD Connect의 새 구성은 대체 ID 및 AD FS 팜을 구성 하는 방법에 대 한 자세한 지침은 Azure AD에 연결을 참조 하세요.
- 기존 Azure AD Connect 설치의 경우 로그인 방법을 변경 하는 방법에 대 한 지침은 사용자 로그인 방법 변경을 참조 하십시오 AD FS

Azure AD Connect AD FS 환경에 대 한 세부 정보를 제공 하는 경우 자동으로 AD FS에서 적절 한 KB가 있는지 확인 하 고 Azure AD 페더레이션 트러스트에 대 한 필요한 모든 올바른 클레임 규칙을 포함 하 여 대체 ID에 대 한 AD FS를 구성 합니다. 대체 ID를 구성 하는 마법사 외부에는 추가 단계가 필요 하지 않습니다.

>[!NOTE]
> Azure AD Connect를 사용 하 여 대체 로그온 ID를 구성 하는 것이 좋습니다.

### <a name="manually-configure-alternate-id"></a>대체 ID 수동 구성
대체 로그인 ID를 구성 하려면 다음 작업을 수행 해야 합니다. 대체 로그인 ID를 사용 하도록 설정 하 여 AD FS 클레임 공급자 트러스트 구성

1.  Server 2012R2가 있는 경우 모든 AD FS 서버에 KB2919355이 설치 되어 있는지 확인 합니다. 직접 다운로드 하 또는 Windows Update 서비스를 통해 얻을 수 있습니다. 

2.  팜에 페더레이션 서버 중 하나에서 다음 PowerShell cmdlet을 실행 하 여 AD FS 구성을 업데이트 (WID 팜의 경우이 명령을 실행 해야이 팜의 기본 AD FS 서버):

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID <attribute> -LookupForests <forest domain>
```

**AlternateLoginID** 로그인에 사용 하려는 특성의 LDAP 이름입니다.

**LookupForests** 포리스트의 사용자가 속하는 DNS의 목록입니다.

대체 로그인 ID 기능을 사용 하려면 null이 아닌, 유효한 값으로-AlternateLoginID와-LookupForests 매개 변수를 구성 해야 합니다.

다음 예제에서는에서 사용할 수 있도록 대체 로그인 ID 기능 contoso.com과 fabrikam.com을 포리스트의 계정 사용 하 여 사용자가 AD FS 지원 응용 프로그램을 자신의 "mail" 특성에 로그인 할 수 있도록 합니다.

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID mail -LookupForests contoso.com,fabrikam.com
```

3. 이 기능을 해제 하려면 두 매개 변수가 모두 null 일 수에 대 한 값을 설정 합니다.

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID $NULL -LookupForests $NULL
```

## <a name="hybrid-modern-authentication-with-alternate-id"></a>대체 ID를 사용 하는 하이브리드 최신 인증

>[!IMPORTANT]
>다음은 타사 id 공급자가 아닌 AD FS에 대해서만 테스트 되었습니다.

### <a name="exchange-and-skype-for-business"></a>비즈니스용 Exchange 및 Skype
Exchange 및 비즈니스용 Skype에서 대체 로그인 id를 사용 하는 경우 사용자 환경은 HMA를 사용 하는지 여부에 따라 달라 집니다.

>[!NOTE]
>최상의 최종 사용자 환경을 위해 Microsoft에서는 하이브리드 최신 인증을 사용 하는 것이 좋습니다.

자세한 내용은 [하이브리드 최신 인증 개요](https://support.office.com/en-us/article/Hybrid-Modern-Authentication-overview-and-prerequisites-for-using-it-with-on-premises-Skype-for-Business-and-Exchange-servers-ef753b32-7251-4c9e-b442-1a5aec14e58d) 를 참조 하세요.

### <a name="pre-requisites-for-exchange-and-skype-for-business"></a>Exchange 및 비즈니스용 Skype에 대 한 필수 구성 요소
다음은 대체 ID를 사용 하 여 SSO를 얻기 위한 필수 구성 요소입니다.

- Exchange Online에서 최신 인증을 설정 해야 합니다.
- 비즈니스용 Skype (SFB) Online에서 최신 인증을 설정 해야 합니다.
- Exchange 온-프레미스에서 최신 인증을 설정 해야 합니다.  모든 Exchange 서버에 exchange 2013 CU19 또는 Exchange 2016 CU18 이상이 필요 합니다. 환경에 Exchange 2010이 없습니다.
- 비즈니스용 Skype 온-프레미스에서 최신 인증을 설정 해야 합니다.
- 최신 인증을 사용 하는 Exchange 및 Skype 클라이언트를 사용 해야 합니다. 모든 서버는 SFB Server 2015 CU5를 실행 해야 합니다.
- 최신 인증을 지 원하는 비즈니스용 Skype 클라이언트
   - iOS, Android, Windows Phone
   - SFB 2016 (MA는 기본적으로 켜져 있지만 사용 하지 않도록 설정 되지 않았는지 확인 합니다.)
   - SFB 2013 (MA는 기본적으로 해제 되어 있으므로 MA가 설정 되어 있는지 확인 합니다.)
   - SFB Mac desktop
- 최신 인증을 지원 하 고 AltID regkeys을 지 원하는 Exchange 클라이언트
    - Office Pro Plus 2016만 해당





#### <a name="supported-office-version"></a>지원 되는 Office 버전

대체 id를 사용 하 여 SSO에 대 한 디렉터리를 구성 하면 이러한 추가 구성이 완료 되지 않은 경우 인증에 대 한 추가 메시지가 표시 될 수 있습니다. 대체 id로 사용자 환경에 미치는 영향에 대 한 자세한 내용은 문서를 참조 하세요.

다음과 같은 추가 구성을 사용 하 여 사용자 환경이 크게 향상 되 고 조직의 대체 id 사용자에 대 한 인증에 대해 0에 가까운 메시지를 표시할 수 있습니다.

##### <a name="step-1-update-to-required-office-version"></a>1단계. 필수 Office 버전으로 업데이트
Office 버전 1712 (빌드 없음 8827.2148) 이상에서 대체 id 시나리오를 처리 하도록 인증 논리를 업데이트 했습니다. 새 논리를 활용 하기 위해 클라이언트 컴퓨터를 Office 버전 1712 (빌드 번호 8827.2148) 이상으로 업데이트 해야 합니다.

##### <a name="step-2-update-to-required-windows-version"></a>2단계. 필수 Windows 버전으로 업데이트
Windows 버전 1709 이상에서는 대체 id 시나리오를 처리 하도록 인증 논리를 업데이트 했습니다. 새 논리를 활용 하기 위해 클라이언트 컴퓨터를 Windows 버전 1709 이상으로 업데이트 해야 합니다.

##### <a name="step-3-configure-registry-for-impacted-users-using-group-policy"></a>3단계. 그룹 정책을 사용 하 여 영향을 받는 사용자에 대 한 레지스트리 구성
Office 응용 프로그램은 디렉터리 관리자가 푸시된 정보를 사용 하 여 대체 id 환경을 식별 합니다. Office 응용 프로그램에서 추가 프롬프트를 표시 하지 않고 대체 id를 사용 하 여 사용자를 인증할 수 있도록 다음 레지스트리 키를 구성 해야 합니다.

|추가할 Regkey|Regkey 데이터 이름, 형식 및 값|Windows 7/8|Windows 10|설명|
|-----|-----|-----|-----|-----|
|HKEY_CURRENT_USER\Software\Microsoft\AuthN|DomainHint</br>REG_SZ</br>contoso.com|필수|필수|이 regkey의 값은 조직의 테 넌 트에서 확인 된 사용자 지정 도메인 이름입니다. 예를 들어 Contoso.com이 테 넌 트 Contoso.onmicrosoft.com에서 확인 된 사용자 지정 도메인 이름 중 하나인 경우 Contoso corp는이 regkey에 Contoso.com 값을 제공할 수 있습니다.|
HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\Identity|EnableAlternateIdSupport</br>REG_DWORD</br>1|Outlook 2016 ProPlus에 필요 합니다.|Outlook 2016 ProPlus에 필요 합니다.|이 regkey의 값은 1/0 일 수 있습니다 .이는 향상 된 대체 id 인증 논리에 대해 Outlook 응용 프로그램에 적용 해야 하는지 여부를 나타냅니다.|
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains\contoso.com\sts|&#42;</br>REG_DWORD</br>1|필수|필수|이 regkey는 인터넷 설정에서 STS를 신뢰할 수 있는 영역으로 설정 하는 데 사용할 수 있습니다. 표준 ADFS 배포를 통해 Internet Explorer의 로컬 인트라넷 영역에 ADFS 네임 스페이스를 추가 하는 것이 좋습니다.|

## <a name="new-authentication-flow-after-additional-configuration"></a>추가 구성 후 새 인증 흐름

![인증 흐름](media/Configure-Alternate-Login-ID/alt1a.png)

1. 은 사용자는 대체 id를 사용 하 여 Azure AD에 프로 비전 됩니다.
   </br>b 디렉터리 관리자는 영향을 받는 클라이언트 컴퓨터에 필요한 regkey 설정을 푸시합니다.
2. 사용자가 로컬 컴퓨터에서 인증 하 고 office 응용 프로그램을 엽니다.
3. Office 응용 프로그램은 로컬 세션 자격 증명을 사용 합니다.
4. Office 응용 프로그램은 관리자 및 로컬 자격 증명으로 푸시된 도메인 힌트를 사용 하 여 Azure AD에 인증 합니다.
5. Azure AD는 페더레이션 영역을 수정 하 고 토큰을 발급 하 여 사용자를 성공적으로 인증 합니다.

## <a name="applications-and-user-experience-after-the-additional-configuration"></a>추가 구성 후의 응용 프로그램 및 사용자 환경

### <a name="non-exchange-and-skype-for-business-clients"></a>비 Exchange 및 비즈니스용 Skype 클라이언트

|클라이언트|지원 문|설명|
| ----- | -----|-----|
|Microsoft Teams|지원됨|<li>Microsoft 팀은 AD FS (SAML-P, WS-급지됨, WS-TRUST 및 OAuth)와 최신 인증을 지원 합니다.</li><li> 채널, 채팅 및 파일 기능과 같은 핵심 Microsoft 팀은 대체 로그인 ID로 작동 합니다.</li><li>첫 번째 및 타사 앱은 고객이 별도로 조사 해야 합니다. 각 응용 프로그램에는 고유한 지원 가능성 인증 프로토콜이 있기 때문입니다.</li>|     
|비즈니스용 OneDrive|지원 됨-클라이언트 쪽 레지스트리 키 권장 |대체 ID를 구성 하면 확인 필드에서 온-프레미스 UPN이 미리 채워져 있는 것을 볼 수 있습니다. 이 사용 되는 대체 Id로 변경 해야 합니다. 이 문서에 나와 있는 클라이언트 쪽 레지스트리 키를 사용 하는 것이 좋습니다. Office 2013 및 Lync 2013은 정기적으로 SharePoint Online, OneDrive 및 Lync Online에 대 한 자격 증명을 묻는 메시지를 표시 합니다.|
|비즈니스 모바일 클라이언트에 대 한 OneDrive|지원됨|| 
|Office 365 Pro Plus 활성화 페이지|지원 됨-클라이언트 쪽 레지스트리 키 권장|대체 ID를 구성 하면 확인 필드에서 온-프레미스 UPN이 미리 채워져 있는 것을 볼 수 있습니다. 이 사용 되는 대체 Id로 변경 해야 합니다. 이 문서에 나와 있는 클라이언트 쪽 레지스트리 키를 사용 하는 것이 좋습니다. Office 2013 및 Lync 2013은 정기적으로 SharePoint Online, OneDrive 및 Lync Online에 대 한 자격 증명을 묻는 메시지를 표시 합니다.|

### <a name="exchange-and-skype-for-business-clients"></a>Exchange 및 비즈니스용 Skype 클라이언트

|클라이언트|지원 문-HMA 사용|지원 문-HMA 불포함|
| ----- |----- | ----- |
|Outlook|지원 됨, 추가 메시지 표시 안 함|지원됨</br></br>최신 Exchange Online **인증** 사용: 지원됨</br></br>Exchange Online에 대 한 **일반 인증** 사용: 지원 되는 주의 사항은 다음과 같습니다.</br><li>도메인에 가입 된 컴퓨터에 있어야 하며 회사 네트워크에 연결 되어 있어야 합니다. </li><li>사서함 사용자에 대 한 외부 액세스를 허용 하지 않는 환경에서 대체 ID만 사용할 수 있습니다. 즉, 사용자가 연결 되 고 회사 네트워크, VPN 또는 직접 액세스 컴퓨터를 통해 연결 되는 경우 지원 되는 방식으로 해당 사서함에 대 한 인증을 받을 수 있지만 Outlook 프로필을 구성할 때 몇 가지 추가 프롬프트가 표시 됩니다.| 
|하이브리드 공용 폴더|지원, 추가 프롬프트가 표시 되지 않습니다.|최신 Exchange Online **인증** 사용: 지원됨</br></br>Exchange Online에 대 한 **일반 인증** 사용: 지원되지 않음</br></br><li>대체 ID가 사용 되는 경우 하이브리드 공용 폴더를 확장할 수 없으므로 현재 일반 인증 방법으로 사용해 서는 안 됩니다.|
|크로스-프레미스 위임|[하이브리드 배포에서 위임 된 사서함 권한을 지원 하도록 Exchange 구성을](https://technet.microsoft.com/library/mt784505.aspx) 참조 하세요.|[하이브리드 배포에서 위임 된 사서함 권한을 지원 하도록 Exchange 구성을](https://technet.microsoft.com/library/mt784505.aspx) 참조 하세요.|
|사서함 액세스 (사서함 온-프레미스-클라우드에서 보관 파일)를 보관 합니다.|지원 됨, 추가 메시지 표시 안 함|지원 됨-사용자는 보관 파일에 액세스할 때 자격 증명에 대 한 추가 프롬프트를 받을 수 있으며, 메시지가 표시 되 면 해당 대체 ID를 제공 해야 합니다.| 
|Outlook Web Access|지원됨|지원됨|
|Android, IOS 및 Windows Phone 용 outlook 모바일 앱|지원됨|지원됨|
|비즈니스용 Skype/Lync|추가 프롬프트 없이 지원 됨|지원 됨 (언급 된 경우 제외), 사용자 혼동 가능성이 있습니다.</br></br>모바일 클라이언트에서 대체 Id는 SIP 주소 = 전자 메일 주소 = 대체 ID 인 경우에만 지원 됩니다.</br></br> 사용자는 먼저 온-프레미스 UPN을 사용 하 고 대체 ID를 사용 하 여 비즈니스용 Skype 데스크톱 클라이언트에 두 번 로그인 해야 할 수 있습니다. "로그인 주소"는 실제로 "사용자 이름"과 같지 않을 수 있는 SIP 주소입니다 (종종). 사용자 이름을 입력 하 라는 메시지가 처음 표시 되 면 사용자는 UPN을 입력 해야 합니다 .이는 대체 ID 또는 SIP 주소로 잘못 미리 채워져 있는 경우에도 마찬가지입니다. 사용자가 UPN을 사용 하 여 로그인을 클릭 하면 사용자 이름 프롬프트가 다시 표시 됩니다 .이 시간은 UPN으로 미리 채워져 있습니다. 이번에는 사용자가이를 대체 ID로 바꾸어야 하 고 로그인을 클릭 하 여 로그인 프로세스를 완료 해야 합니다. 모바일 클라이언트에서 사용자는 UPN 형식이 아닌 SAM 스타일 형식 (domain\username)을 사용 하 여 고급 페이지에서 온-프레미스 사용자 ID를 입력 해야 합니다.</br></br>성공적으로 로그인 한 후 비즈니스용 Skype 또는 Lync가 "Exchange에 자격 증명이 필요 합니다." 라고 표시 되 면 사서함이 있는 위치에 대해 유효한 자격 증명을 제공 해야 합니다. 사서함이 클라우드에 있는 경우 대체 ID를 제공 해야 합니다. 사서함이 온-프레미스 인 경우 온-프레미스 UPN을 제공 해야 합니다.| 

## <a name="additional-details--considerations"></a>추가 세부 정보 및 고려 사항

-   대체 로그인 ID 기능은 AD FS 배포 된 페더레이션 환경에 사용할 수 있습니다.  다음 시나리오에서는 지원 되지 않습니다.
    -   Azure AD에서 확인할 수 없는 라우팅할 수 없는 도메인 (예: Contoso.com)입니다.
    -   AD FS 배포 되지 않은 관리 되는 환경


-   사용 하도록 설정 하는 경우는 대체 로그인 ID만 기능을 사용자 이름/암호 인증에 사용할 수 있는 AD FS에서 지 원하는 하는 모든 사용자 이름/암호 인증 프로토콜에서 (Saml-p, Ws-fed, Ws-trust 및 OAuth).


-   WIA (Windows 통합 인증)가 수행 되는 경우 (예: 사용자가 인트라넷에서 도메인에 가입 된 컴퓨터의 회사 응용 프로그램에 액세스 하려고 하 고 AD FS 관리자가 인트라넷에 대해 WIA를 사용 하도록 인증 정책을 구성 하는 경우), UPN isused 인증의 경우. 대체 로그인 ID 기능에 대 한 신뢰 당사자에 대 한 모든 클레임 규칙을 구성한 경우 해당 규칙 WIA 경우에서 여전히 유효한 지 확인 해야 합니다.

-   사용 하도록 설정 하는 경우 대체 로그인 ID 기능은 AD FS에서 지 원하는 각 사용자 계정 포리스트의 AD FS 서버에서 연결할 수 글로벌 카탈로그 서버를 하나 이상 필요 합니다. 사용자 계정 포리스트의 글로벌 카탈로그 서버에 연결 하지 못하면 AD FS UPN을 사용 하는 것으로 대체 됩니다. 기본적으로 모든 도메인 컨트롤러는 글로벌 카탈로그 서버입니다.

-   사용 하도록 설정 하면 AD FS 서버에서 구성 된 모든 사용자 계정 포리스트에 대해 지정 된 대체 로그인 ID 값을 사용 하 여 둘 이상의 사용자 개체를 찾으면 로그인에 실패 합니다.

-   대체 로그인 ID 기능을 사용 하도록 설정 하면 AD FS는 먼저 대체 로그인 ID를 사용 하 여 최종 사용자를 인증 한 다음 대체 로그인 ID로 식별할 수 있는 계정을 찾을 수 없는 경우 UPN을 사용 하도록 대체 합니다. 여전히 UPN 로그인을 지원 하려는 경우 대체 로그인 ID와 UPN 간의 충돌 로부터 하지는 않도록 해야 합니다. 예를 들어, 한 사람의 메일 특성을 다른의 UPN으로 설정 하면 다른 사용자가 UPN으로 로그인 하지 못하도록 차단 됩니다.

-   관리자가 구성한 포리스트 중 하나가 다운 된 경우 AD FS는 구성 된 다른 포리스트에서 대체 로그인 ID를 사용 하 여 사용자 계정을 계속 조회 합니다. AD FS 서버에서 검색 한 포리스트에서 고유한 사용자 개체를 찾으면 사용자가 성공적으로 로그인 합니다.

-   일부 힌트가 대체 로그인 ID에 대 한 최종 사용자에 게 AD FS 로그인 페이지 사용자 지정 또한 하려는 경우 사용자 지정된 로그인 페이지 설명을 추가 하거나 수행할 수 있습니다 (자세한 내용은 참조 [AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx) 또는 사용자 이름 필드 위 "조직 계정으로 로그인" 문자열을 사용자 지정 (자세한 내용은 참조 [AD FS 로그인 페이지의 고급 사용자 지정](https://technet.microsoft.com/library/dn636121.aspx)합니다.

-   대체 로그인 ID 값을 포함 하는 새 클레임 형식은 **http:schemas.microsoft.com/ws/2013/11/alternateloginid**

## <a name="events-and-performance-counters"></a>이벤트 및 성능 카운터
대체 로그인 ID가 설정 된 경우 AD FS 서버 성능을 측정 하는 다음 성능 카운터가 추가 되었습니다.

-   대체 로그인 ID를 사용 하 여 수행 하는 인증 수 대체 로그인 Id 인증:

-   초당 대체 로그인 ID를 사용 하 여 수행 하는 인증 수 대체 로그인 Id 인증/Sec:

-   대체 로그인 ID에 대 한 평균 검색 대기 시간: 대체 로그인 ID에 대 한 관리자가 구성 하는 포리스트 간 평균 검색 대기 시간

다음은 다양 한 오류 사례와 AD FS에서 기록 된 이벤트와 사용자의 로그인 환경에 해당 영향입니다.



|                       **오류 사례**                        | **로그인 환경에 미치는 영향** |                                                              **이벤트**                                                              |
|--------------------------------------------------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| SAMAccountName에 대 한 사용자 개체에 대 한 값을 가져올 수 없습니다. |          로그인 실패           |                  예외 메시지 MSIS8012를 사용 하는 이벤트 ID 364: 사용자 '{0}'에 대 한 samAccountName을 찾을 수 없습니다.                   |
|        CanonicalName 특성에 액세스할 수 없습니다         |          로그인 실패           |               예외 메시지 MSIS8013를 사용 하는 이벤트 ID 364: CanonicalName: '{0}' 사용자{1}의 ' ' 형식이 잘못 되었습니다.                |
|        여러 사용자 개체가 하나의 포리스트에 있습니다.        |          로그인 실패           | 예외 메시지 MSIS8015를 사용 하는 이벤트 ID 364: Id가 인 ' '{0}{1}포리스트에서 id가 ' ' 인 여러 사용자 계정을 찾았습니다.{2} |
|   여러 포리스트에 걸친 여러 사용자 개체가 있습니다.    |          로그인 실패           |           예외 메시지 MSIS8014를 사용 하는 이벤트 ID 364: 포리스트에서 id가 '{0}' 인 여러 사용자 계정을 찾았습니다.{1}            |

## <a name="see-also"></a>관련 항목
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)


