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
ms.openlocfilehash: 615faf4153949aa4ad989f017068d1809fca26b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820874"
---
# <a name="configuring-alternate-login-id"></a>대체 로그인 ID 구성

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

## <a name="what-is-alternate-login-id"></a>대체 로그인 ID 란?
대부분의 시나리오에서 사용자는 해당 계정에 로그인 하는 UPN (사용자 계정 이름)을 사용합니다. 그러나 회사 정책 또는 온-프레미스 기간 업무 응용 프로그램 종속성으로 인해 일부 환경에서는 사용자가 사용할 수 있습니다 다른 형태의 로그인. 

>[!NOTE]
>Microsoft의 모범 사례는 기본 SMTP 주소를 UPN과 일치 하는 것이 좋습니다. 이 문서에서는 일치 하도록 UPN을 수정할 수 없습니다. 고객의 작은 비율의입니다.

예를 들어, 이러한 수 해당 전자 메일 id에 사용할 로그인 및는 해당 UPN에서 다를 수 있습니다. 이 특히 해당 UPN이 라우팅할 수 없는 시나리오에서 자주 발생 합니다. 사용자 UPN 사용 하 여 Jane Doe는 것이 좋습니다 jdoe@contoso.local 전자 메일 주소 및 jdoe@contoso.com합니다. Jane은 로그인에 대 한 자신의 전자 메일 id를 항상 사용에 자신이 UPN의도 인식 하지 못할 수 있습니다. 메서드의 다른 로그인 UPN 대신 사용 하 여 대체 ID를 구성합니다. UPN 하는 방법에 자세한 내용은 만듭니다에 대 한 [Azure AD UserPrincipalName 채우기](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname)합니다.

Active Directory Federation Services (ADFS) 사용 하도록 설정 페더레이션된 응용 프로그램 대체를 사용 하 여 로그인을 AD FS를 사용 하 여 id입니다. 따라서 관리자가 기본 로그인에 사용 되는 UPN 대신 지정할 수 있습니다. AD FS는 Active Directory Domain Services (AD DS)에서 허용 되는 사용자 식별자의 모든 형태를 사용 하 여 이미 지원 합니다. 대체 ID를 구성 하는 경우 AD FS 구성 된 대체 ID 값을 사용 하 여 로그인, 전자 메일 id를 말할 수가 있습니다. 대체 ID를 사용 하 여 온-프레미스 Upn을 수정 하지 않고 Office 365와 같은 SaaS 공급자를 채택할 수 있습니다. 또한 소비자 구성 된 id와 업무의 서비스 응용 프로그램을 지원할 수 있습니다.

## <a name="alternate-id-in-azure-ad"></a>Azure AD에서 대체 id
조직은 다음과 같은 시나리오에서 대체 ID를 사용 해야 할 수 있습니다.
1.  온-프레미스 도메인 이름은 라우팅할 수 없는, 예입니다. Contoso.local 이며 결과적으로 기본 사용자 계정 이름 라우팅할 수 없는 (jdoe@contoso.local). 회사 정책 또는 로컬 응용 프로그램 종속성으로 인해 기존 UPN은 변경할 수 없습니다. Azure AD 및 Office 365 Azure AD directory 완벽 하 게 라우팅할 수 있는 인터넷에 연결 하는 모든 도메인 접미사 필요 합니다. 
2.  온-프레미스 UPN 사용자의 전자 메일 주소와 동일 하지 않습니다. 로그인에 Office 365에 사용자 전자 메일 주소를 사용 하 고 조직 제약 조건으로 인해 UPN을 사용할 수 없습니다.
위에서 언급 한 시나리오에서 AD FS 사용 하 여 대체 ID를 사용 하면 로그인에 Azure AD에 온-프레미스 Upn을 수정 하지 않고 있습니다. 

## <a name="end-user-experience-with-alternate-login-id"></a>대체 로그인 ID 사용 하 여 최종 사용자 환경
최종 사용자 환경을 대체 로그인 id를 사용 하 여 사용 된 인증 방법에 따라 달라 집니다.  현재 여기 세 가지 방법으로 대체 로그인 id를 사용 하 여 수행할 수 있습니다.  다음 창이 여기에 포함됩니다.

- **일반 인증 (레거시)**-기본 인증 프로토콜을 사용 합니다.
- **최신 인증** -응용 프로그램에 Active Directory 인증 라이브러리 ADAL 기반 로그인을 제공 합니다. 이 통해 로그인 기능와 같은 다단계 인증 (MFA), SAML 기반 타사 Id 공급자 Office 클라이언트 응용 프로그램, 스마트 카드 및 인증서 기반 인증을 사용 하 여.
- **하이브리드 최신 인증** -최신 인증의 장점을 모두 제공 하 고 클라우드 로부터 얻은 권한 부여 토큰을 사용 하 여 온-프레미스 응용 프로그램에 액세스할 수 있도록 사용자를 제공 합니다.

>[!NOTE]
> 가능한 최상의 환경에 대 한 Microsoft 하이브리드 최신 인증 높은 것이 좋습니다.



## <a name="configure-alternate-logon-id"></a>대체 로그인 ID 구성
Azure AD Connect에서는 사용 하 여 Azure AD를 사용 하는 것이 좋습니다. 사용자 환경에 대 한 대체 로그온 ID를 구성 하는 연결 합니다.

- Azure AD Connect의 새 구성에 대 한 대체 ID 및 AD FS 팜을 구성 하는 방법에 대 한 자세한 지침은 Azure ad Connect를 참조 하세요.
- 기존 Azure AD Connect 설치의 경우 AD fs 로그인 방법 변경에 대 한 지침에 대 한 사용자 로그인 방법 변경를 참조합니다

Azure AD Connect가 AD FS 환경에 대 한 세부 정보를 제공 하는 경우 자동으로 AD FS에서 오른쪽 KB가 있는지 확인 하 고 Azure AD 페더레이션 트러스트에 대 한 모든 필요한 올바른 클레임 규칙을 포함 하 여 대체 ID에 대 한 AD FS를 구성 합니다. 없는 추가 단계가 필요한 외부 마법사가 대체 ID를 구성 하려면

>[!NOTE]
> Azure AD Connect를 사용 하 여 대체 로그온 id입니다. 구성 하는 것이 좋습니다.

### <a name="manually-configure-alternate-id"></a>대체 ID를 수동으로 구성
대체 로그인 ID를 구성 하려면 다음 작업을 수행 해야 합니다. 대체 로그인 ID를 사용 하도록 설정 하 여 AD FS 클레임 공급자 트러스트 구성

1.  Server 2012 r2에 있는 경우 KB2919355 모든 AD FS 서버에 설치 해야 확인 합니다. 직접 다운로드 하 또는 Windows Update 서비스를 통해 얻을 수 있습니다. 

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

3.  이 기능을 해제 하려면 두 매개 변수가 모두 null 일 수에 대 한 값을 설정 합니다.

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID $NULL -LookupForests $NULL
```

## <a name="hybrid-modern-authentication-with-alternate-id"></a>대체 ID를 사용 하 여 하이브리드 최신 인증

>[!IMPORTANT]
>다음에 대해서만 테스트 되었으므로 AD FS와 하지 타사 타사 id 공급자입니다.

### <a name="exchange-and-skype-for-business"></a>Exchange 및 비즈니스용 Skype
대체 로그인 id Exchange 및 Skype for Business를 사용할 경우 사용자 환경을 HMA를 사용 하는 여부에 따라 달라 집니다.

>[!NOTE]
>최종 사용자 환경을 최적화에 대 한 하이브리드 최신 인증을 사용 하는 것이 좋습니다.

자세한 내용은 또는 [하이브리드 최신 인증 개요](https://support.office.com/en-us/article/Hybrid-Modern-Authentication-overview-and-prerequisites-for-using-it-with-on-premises-Skype-for-Business-and-Exchange-servers-ef753b32-7251-4c9e-b442-1a5aec14e58d)

### <a name="pre-requisites-for-exchange-and-skype-for-business"></a>Exchange 및 비즈니스용 Skype에 대 한 필수 조건
다음은 대체 ID 사용 하 여 SSO를 달성 하기 위한 필수 조건

- Exchange Online 보다 최신 인증을 ON으로 설정 해야 합니다.
- 비즈니스 (SFB) Online에 대 한 Skype를 ON으로 설정 하는 최신 인증 해야 합니다.
- Exchange 온-프레미스 최신 인증 변해야 ON입니다.  Exchange 2013 CU19 또는 Exchange 2016 CU18 및 모든 Exchange 서버에 최대가 필요 합니다. 환경에서 Exchange 2010 없습니다.
- 비즈니스용 Skype 온-프레미스 최신 인증 변해야 ON.
- 최신 인증을 사용 하는 Exchange 및 Skype 클라이언트를 사용 해야 합니다. 모든 서버 SFB 서버 2015 CU5 실행 되어야 합니다.
- 최신 인증 지원 되는 비즈니스 클라이언트에 대 한 Skype
   - iOS, Android, Windows Phone
   - SFB 2016 (MA 기본적으로 켜져 있지만 사용할 수 있는지 확인.)
   - SFB 2013 (MA 기본적으로 꺼져, 있도록 MA 켜 졌습니다.)
   - SFB Mac 데스크톱
- 최신 인증을 지원 하 고 않으므로 AltID regkeys를 지 원하는 Exchange 클라이언트
    - Office Pro Plus 2016만





#### <a name="supported-office-version"></a>지원 되는 Office 버전

대체 id를 사용 하 여 대체 id를 사용 하 여 SSO에 대 한 디렉터리를 구성 하면 이러한 추가 구성을 완료 하지 않으면 인증에 대 한 추가 프롬프트 발생할 수 있습니다. 대체 id를 사용 하 여 사용자 경험에 미치는 영향에 대 한 문서를 참조 하십시오.

다음 추가 구성으로 사용자 환경을 크게 향상 됩니다 하 고 조직에서 대체 id 사용자에 대 한 인증에 대 한 0 프롬프트 거의 얻을 수 있습니다.

##### <a name="step-1-update-to-required-office-version"></a>1단계. 필요한 office 버전으로 업데이트
Office 버전 1712 (없습니다 8827.2148 빌드) 위의 대체 id 시나리오를 처리 하는 인증 논리를 업데이트 합니다. 새 논리를 활용 하기 위해 클라이언트 컴퓨터 위에 office 버전 1712 (없습니다 8827.2148 빌드)를 업데이트 해야 합니다.

##### <a name="step-2-configure-registry-for-impacted-users-using-group-policy"></a>2단계. 그룹 정책을 사용 하 여 영향을 받는 사용자에 대 한 레지스트리 구성
Office 응용 프로그램 디렉터리 관리자가 대체 id 환경을 식별할 푸시 정보를 사용 합니다. 다음 레지스트리 키 추가 프롬프트를 표시 하지 않고 대체 id를 사용 하 여 사용자를 인증 하는 office 응용 프로그램을 구성 해야 합니다.

|레지스트리 키 추가|레지스트리 키 데이터 이름, 형식 및 값|Windows 7/8|Windows 10|설명|
|-----|-----|-----|-----|-----|
|HKEY_CURRENT_USER\Software\Microsoft\AuthN|DomainHint</br>REG_SZ</br>contoso.com|필수|필수|이 레지스트리 키의 값에는 조직의 테 넌 트에서 확인 된 사용자 지정 도메인 이름입니다. 예를 들어, Contoso corp Contoso.com을 사용 하면 Contoso.onmicrosoft.com 테 넌 트에서 확인 된 사용자 지정 도메인 이름 중 하나인 경우 Contoso.com이 레지스트리이 키의 값을 제공할 수 있습니다.|
HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\Identity|EnableAlternateIdSupport</br>REG_DWORD</br>1|Outlook 2016 ProPlus에 대 한 필요|Outlook 2016 ProPlus에 대 한 필요|이 레지스트리 키의 값 1은 0 / Outlook 응용 프로그램에 게 향상 된 대체 id 인증 논리를 활용 해야 하는지 여부를 나타내기 위해.|
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Common\Identity|DisableADALatopWAMOverride</br>REG_DWORD</br>1|해당 사항 없음|필수.|이렇게 하면 Office에서 사용 하지 않음을 WAM alt id WAM에서 지원 되지 않습니다.|
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Common\Identity|DisableAADWAM</br>REG_DWORD</br>1|해당 사항 없음|필수.|이렇게 하면 Office에서 사용 하지 않음을 WAM alt id WAM에서 지원 되지 않습니다.|
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains\contoso.com\sts|&#42;</br>REG_DWORD</br>1|필수|필수|인터넷 설정에 신뢰할 수 있는 영역으로 STS를 설정 하려면이 레지스트리 키를 사용할 수 있습니다. 표준 ADFS 배포 Internet explorer 로컬 인트라넷 영역에 ADFS 네임 스페이스를 추가 하는 것이 좋습니다.|

## <a name="new-authentication-flow-after-additional-configuration"></a>추가 구성 후 새 인증 흐름

![인증 흐름](media/Configure-Alternate-Login-ID/alt1a.png)

1. a: 대체 id를 사용 하 여 Azure AD에서 사용자가 프로 비전
   </br>b: 디렉터리 관리자에 게 영향을 받는 클라이언트 컴퓨터에 필요한 레지스트리 키 설정을 푸시합니다
2. 사용자는 로컬 컴퓨터에 인증 하 고 office 응용 프로그램을 엽니다.
3. Office 응용 프로그램은 로컬 세션 자격 증명
4. Office 응용 프로그램 관리자 및 로컬 자격 증명으로 밀어 넣는 도메인 힌트를 사용 하 여 Azure AD에 인증
5. Azure AD 페더레이션 영역을 수정 하는 토큰을 발급 하 여 사용자를 성공적으로 인증

## <a name="applications-and-user-experience-after-the-additional-configuration"></a>추가 구성 후 응용 프로그램 및 사용자 환경

### <a name="non-exchange-and-skype-for-business-clients"></a>교환과 비즈니스 클라이언트에 대 한 Skype
|클라이언트|지원 문의|설명|
| ----- | -----|-----|
|Microsoft Teams|지원됨|<li>Microsoft Teams AD FS 지원 (Saml-p, Ws-fed, Ws-trust 및 OAuth) 및 최신 인증 합니다.</li><li> 핵심 Microsoft Teams 채널, 채팅 및 파일 기능 같은 대체 로그인 ID와 함께 작동 합니다.</li><li>첫 번째 및 세 번째 파티 앱 고객이 개별적으로 조사 해야 합니다. 각 응용 프로그램에 고유한 지원 인증 프로토콜 때문입니다.</li>|     
|비즈니스용 OneDrive|지원-권장 되는 클라이언트 쪽 레지스트리 키 |구성 된 대체 ID를 사용 하 여 온-프레미스 UPN 미리 채워집니다 확인 필드는 것이 표시 됩니다. 이 사용 되는 대체 Id로 변경 해야 합니다. 이 문서에 명시 된 클라이언트 쪽 레지스트리 키를 사용 하는 것이 좋습니다. Office 2013 및 Lync 2013 정기적으로 SharePoint Online, OneDrive 및 Lync Online 자격 증명을 묻는 합니다.|
|비즈니스 모바일 클라이언트에 대 한 OneDrive|지원됨|| 
|Office 365 Pro Plus 활성화 페이지|지원-권장 되는 클라이언트 쪽 레지스트리 키|구성 된 대체 ID를 사용 하 여 온-프레미스 UPN 미리 채워집니다 확인 필드는 것이 표시 됩니다. 이 사용 되는 대체 Id로 변경 해야 합니다. 이 문서에 명시 된 클라이언트 쪽 레지스트리 키를 사용 하는 것이 좋습니다. Office 2013 및 Lync 2013 정기적으로 SharePoint Online, OneDrive 및 Lync Online 자격 증명을 묻는 합니다.|

### <a name="exchange-and-skype-for-business-clients"></a>Exchange 및 Skype for Business 클라이언트

|클라이언트|지원 문의-HMA 사용 하 여|지원 문의-HMA 없이|
| ----- |----- | ----- |
|Outlook|지원 되는, 더 추가 프롬프트|지원됨</br></br>사용 하 여 **최신 인증** Exchange Online에 대 한 합니다. 지원됨</br></br>사용 하 여 **일반 인증** Exchange Online에 대 한 합니다. 다음 방법으로 지원 합니다.</br><li>도메인 가입된 컴퓨터에 있어야 하 고 회사 네트워크에 연결 </li><li>사서함 사용자에 대 한 외부 액세스를 허용 하지 않는 환경에서 대체 ID만 사용할 수 있습니다. 이 사용자만 인증할 수 해당 사서함에 지원 되는 방식으로 Outlook 프로필을 구성할 때 몇 가지 추가 프롬프트가 표시 되지만 연결 및 vpn을 회사 네트워크에 가입 되거나 컴퓨터에 직접 액세스를 통해 연결 될 것을 의미 합니다.| 
|하이브리드 공용 폴더|지원 되는, 더 추가 메시지 표시 합니다.|사용 하 여 **최신 인증** Exchange Online에 대 한 합니다. 지원됨</br></br>사용 하 여 **일반 인증** Exchange Online에 대 한 합니다. 지원되지 않음</br></br><li>하이브리드 공용 폴더 대체 ID를 사용 하 고 따라서 해서는 안 오늘날 일반 인증 메서드를 사용 하 여 확장 하지 못합니다.|
|크로스-프레미스 위임|참조 [하이브리드 배포에서 위임 된 사서함 권한을 지원 하기 위한 Exchange 구성](https://technet.microsoft.com/library/mt784505.aspx)|참조 [하이브리드 배포에서 위임 된 사서함 권한을 지원 하기 위한 Exchange 구성](https://technet.microsoft.com/library/mt784505.aspx)|
|사서함 액세스 (사서함 온-프레미스-클라우드에서 보관 파일)를 보관 합니다.|지원 되는, 더 추가 프롬프트|지원-사용자가 보관 파일에 액세스할 때 자격 증명에 대 한 프롬프트를 추가로 가져올, 메시지가 표시 되 면 자신의 대체 ID를 제공 해야 합니다.| 
|Outlook Web Access|지원됨|지원됨|
|Android, IOS 및 Windows Phone 용 outlook 모바일 앱|지원됨|지원됨|
|비즈니스용 Skype / Lync|추가 프롬프트 없이 지원|지원 (설명 했 듯이 제외) 사용자의 혼동 가능성이 있지만.</br></br>모바일 클라이언트에서 대체 Id는 지원 되는 경우에 SIP 주소 = 전자 메일 주소 = 대체 id입니다.</br></br> 사용자는 로그인에 Skype를 두 번 비즈니스 데스크톱 클라이언트를 먼저 온-프레미스 UPN을 사용 하 고 대체 id입니다. 사용 하 여 해야 합니다. ("로그인 주소" 하지 않을 수 있는 "사용자 이름"으로 동일 하지만 자주 SIP 주소 실제로입니다). 먼저 사용자 이름에 대 한 메시지가 표시 되 면이 올바르게 미리 채워져 있지 대체 ID 또는 SIP 주소를 하는 경우에 사용자 UPN을 입력 해야 합니다. 사용자가 로그인 된 UPN, 이름 프롬프트가 다시 표시 하는 사용자,이 이번에는 UPN 미리 채워집니다. 이 현재 사용자의 대체 ID를 사용 하 여이 대체 하며 클릭 로그인 프로세스를 완료 하려면 로그인 합니다. 모바일 클라이언트에서 사용자는 온-프레미스 사용자 ID를 입력 고급 페이지에서 UPN 형식이 아니라 SAM 스타일 형식 (도메인 \ 사용자 이름)을 사용 하 여 합니다.</br></br>성공적인 로그인 후 비즈니스 또는 Lync Skype "교환에는 자격 증명 필요", 표시 되 면 필요한 사서함이에 대 한 유효한 자격 증명을 제공 합니다. 대체 ID를 제공 해야 하는 클라우드에서 사서함이 있는 경우 사서함이 온-프레미스는 온-프레미스 UPN을 제공 해야 합니다.| 
 
## <a name="additional-details--considerations"></a>추가 세부 정보 및 고려 사항

-   대체 로그인 ID 기능은 배포 된 AD FS를 사용 하 여 페더레이션된 환경에서 사용할 수 있습니다.  다음 시나리오에서 지원 되지 않습니다.
    -   라우팅할 수 없는 도메인 (예: Contoso.local) Azure AD에서 확인할 수 없습니다.
    -   AD FS 배포 되지 않은 환경을 관리 합니다.


-   사용 하도록 설정 하는 경우는 대체 로그인 ID만 기능을 사용자 이름/암호 인증에 사용할 수 있는 AD FS에서 지 원하는 하는 모든 사용자 이름/암호 인증 프로토콜에서 (Saml-p, Ws-fed, Ws-trust 및 OAuth).


-   Windows 통합 인증 WIA () 수행 될 때 (예를 들어 사용자가 인트라넷에서 도메인에 가입 된 컴퓨터에서 회사 응용 프로그램에 액세스 하려고 합니다. AD FS 관리자가 구성 된 경우 인트라넷에 대 한 WIA를 사용 하 여 인증 정책) UPN isused 인증 합니다. 대체 로그인 ID 기능에 대 한 신뢰 당사자에 대 한 모든 클레임 규칙을 구성한 경우 해당 규칙 WIA 경우에서 여전히 유효한 지 확인 해야 합니다.

-   사용 하도록 설정 하는 경우 대체 로그인 ID 기능은 AD FS에서 지 원하는 각 사용자 계정 포리스트의 AD FS 서버에서 연결할 수 글로벌 카탈로그 서버를 하나 이상 필요 합니다. 사용자 계정 포리스트의 글로벌 카탈로그 서버에 도달 하지 못하면 UPN을 사용 하도록 대체 하는 AD FS에서. 기본적으로 모든 도메인 컨트롤러는 글로벌 카탈로그 서버입니다.

-   사용 하도록 설정 하면 AD FS 서버에서 지정한 모든 구성 된 사용자 계정 포리스트에서 동일한 대체 로그인 ID 값을 사용 하 여 둘 이상의 사용자 개체를 발견 한 경우, 로그인을 실패 합니다.

-   대체 로그인 ID 기능을 사용 하는 경우 AD FS 하려고 먼저 대체 로그인 ID 사용 하 여 최종 사용자를 인증 하 고 대체 로그인 ID로 식별 될 수 있는 계정을 찾을 수 없으면 UPN을 사용 하 여 다음 대체 여전히 UPN 로그인을 지원 하려는 경우 대체 로그인 ID와 UPN 간의 충돌 로부터 하지는 않도록 해야 합니다. UPN에 다른 사용자가 UPN을 로그인에서 차단 되는 예를 들어, 서로의 사용 하 여 1의 메일 특성을 설정 합니다.

-   관리자가 구성 된 포리스트 중 하나가 다운 된 경우 AD FS 구성 된 다른 포리스트의 대체 로그인 ID 사용 하 여 사용자 계정을 조회를 계속 합니다. AD FS 서버 고유한 사용자 개체를 검색 하는 포리스트 간 찾습니다, 하는 경우 사용자가 로그인 했습니다.

-   일부 힌트가 대체 로그인 ID에 대 한 최종 사용자에 게 AD FS 로그인 페이지 사용자 지정 또한 하려는 경우 사용자 지정된 로그인 페이지 설명을 추가 하거나 수행할 수 있습니다 (자세한 내용은 참조 [AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx) 또는 사용자 이름 필드 위 "조직 계정으로 로그인" 문자열을 사용자 지정 (자세한 내용은 참조 [AD FS 로그인 페이지의 고급 사용자 지정](https://technet.microsoft.com/library/dn636121.aspx)합니다.

-   대체 로그인 ID 값을 포함 하는 새 클레임 형식은 **http:schemas.microsoft.com/ws/2013/11/alternateloginid**

## <a name="events-and-performance-counters"></a>이벤트 및 성능 카운터
대체 로그인 ID가 설정 된 경우 AD FS 서버 성능을 측정 하는 다음 성능 카운터가 추가 되었습니다.

-   대체 로그인 ID를 사용 하 여 수행 하는 인증 수 대체 로그인 Id 인증:

-   초당 대체 로그인 ID를 사용 하 여 수행 하는 인증 수 대체 로그인 Id 인증/Sec:

-   대체 로그인 ID에 대 한 평균 검색 대기 시간: 대체 로그인 ID에 대 한 관리자가 구성 하는 포리스트 간 평균 검색 대기 시간

다음은 다양 한 오류 사례와 AD FS에서 기록 된 이벤트와 사용자의 로그인 환경에 해당 영향입니다.



**오류 사례**|**로그인 경험에 미치는 영향**|**이벤트**|
---------|---------|---------
SAMAccountName에 대 한 사용자 개체에 대 한 값을 가져올 수 없습니다.|로그인 실패|이벤트 ID 364 된 예외 메시지 MSIS8012: 사용자에 대 한 samAccountName을 찾을 수 없습니다. '{0}'.|
CanonicalName 특성에 액세스할 수 없습니다|로그인 실패|MSIS8013 예외 메시지와 이벤트 ID 364: CanonicalName: '{0}' 사용자의:'{1}'에 잘못 된 형식입니다.|
여러 사용자 개체가 하나의 포리스트에 있습니다.|로그인 실패|이벤트 ID 364 된 예외 메시지 MSIS8015: Id 가진 여러 사용자 계정이 '{0}'포리스트에'{1}' id: {2}|
여러 포리스트에 걸친 여러 사용자 개체가 있습니다.|로그인 실패|이벤트 ID 364 된 예외 메시지 MSIS8014: Id 가진 여러 사용자 계정이 '{0}' 포리스트에: {1}|

## <a name="see-also"></a>관련 항목
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)


