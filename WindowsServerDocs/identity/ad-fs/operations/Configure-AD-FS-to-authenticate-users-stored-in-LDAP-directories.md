---
ms.assetid: e863ab80-4e4c-48d3-bdaa-31815ef36bae
title: "사용자가 LDAP 디렉터리에 저장 된 인증 ADFS 구성"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 05f8b8991e664a84c3f2b3200de4068af8d1476a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="configure-ad-fs-to-authenticate-users-stored-in-ldap-directories"></a>사용자가 LDAP 디렉터리에 저장 된 인증 ADFS 구성

>Windows Server 2016 적용 됩니다.

다음 항목 ADFS 인프라 사용자 id LDAP(Lightweight Directory Access Protocol) (LDAP) v3 호환 디렉터리에 저장 된 인증을 사용 하는 데 필요한 구성에 설명 합니다.

Id 관리 솔루션 많은 조직에서 Active Directory, 광고 LDS 또는 제 3 자 LDAP 디렉터리의 조합으로 구성 됩니다. 이점을 활용할 수 있는 사용자 LDAP v3 호환 디렉터리에 저장 된 인증에 대 한 ADFS 지원 추가 하 여 전체 엔터프라이즈급에서 ADFS 기능 집합에 관계 없이 사용자 id 저장 됩니다. Adfs는 LDAP v3 호환 디렉터리를 지원 합니다.

> [!NOTE]
> ADFS 기능 중 일부를 단일 로그온 (SSO), 장치 인증, 유연한 조건부 액세스 정책, 사용자와 사용자가 Office 365 및 기타 SaaS 응용 프로그램을 포함 하 여 클라우드를 이용 하 작업-에서-아무 곳 이나 웹 응용 프로그램 프록시와 통합 및 설정에 Azure AD로 원활 하 게 federation를 통해 사용에 대 한 지원은 있습니다.  자세한 내용은 참조 [Active Directory Federation Services 개요](../../ad-fs/AD-FS-2016-Overview.md)합니다.

ADFS LDAP 디렉터리에서 사용자를 인증에 대 한 순서를 연결 해야이 LDAP 디렉터리 ADFS 농장 만들어는 **로컬 클레임 공급자 신뢰**합니다.  로컬 클레임 공급자 신뢰 ADFS 농장의 LDAP 디렉터리 나타내는 신뢰 개체를입니다. 로컬 주장 공급자 신뢰 개체 식별자, 이름과이 LDAP 디렉터리 로컬 federation 서비스를 식별 하는 규칙의 다양 한 구성 됩니다.

각각 고유한 구성 여러를 추가 하 여 동일한 ADFS 농장 내에서 여러 LDAP 디렉터리를 지원할 수 있는 **로컬 클레임 제공자 신뢰**합니다. 또한에 거주 하 고 ADFS 숲에서 신뢰할 수 없는 AD DS 숲 로컬 클레임 제공자 신뢰도 모델링도 수 있습니다. Windows PowerShell를 사용 하 여 로컬 클레임 제공자 신뢰를 만들 수 있습니다.

동일한 ADFS 농장 내 같은 ADFS 서버의 광고 디렉터리 (청구 제공자 신뢰) 함께 LDAP 디렉터리 (로컬 클레임 제공자 신뢰) 존재할 수 있습니다, 따라서 Adfs의 단일 인스턴스는 인증과 둘 다에 저장 되어 있는 사용자에 대 한 액세스 권한을 부여할 수 있는 광고 및 비 광고 디렉터리 합니다.

LDAP에서 사용자가 인증 폼 기반 인증만 지원 됩니다. Windows 인증 인증서 기반와 통합 LDAP 디렉터리에 사용자를 인증에 대 한 지원 되지 않습니다.

모든 수동 인증 프로토콜 WS Federation SAML를 포함 한 Adfs에서 지 원하는 및 id LDAP 디렉터리에 저장 된에 대 한 OAuth도 지원 됩니다.

LDAP 디렉터리에 저장 된 id Ws-trust 활성 인증 프로토콜도 지원 됩니다.

## <a name="configure-ad-fs-to-authenticate-users-stored-in-an-ldap-directory"></a>사용자가 LDAP 디렉터리에 저장 된 인증 ADFS 구성
LDAP 디렉터리에서 사용자를 인증 하면 ADFS 농장을 구성 하려면 다음 단계를 수행할 수 있습니다.

1.  먼저 사용 하 여 LDAP 디렉터리에 대 한 연결 구성는 **새로 AdfsLdapServerConnection** cmdlet:

    ```
    $DirectoryCred = Get-Credential
    $vendorDirectory = New-AdfsLdapServerConnection -HostName dirserver -Port 50000 -SslMode None -AuthenticationMethod Basic -Credential $DirectoryCred
    ```

    > [!NOTE]
    > 연결 하려는 각 LDAP 서버에 대 한 새 연결 개체 만드는 것이 좋습니다. ADFS 여러 복제 LDAP 서버에 연결할 수 있고 자동으로 장애 조치 경우 특정 LDAP 서버 내려간 금액입니다. 이 경우에 대 한 각 복제본 LDAP 서버에 대 한 AdfsLdapServerConnection 만들 추가 하는 다음 사용 하 여 연결 개체 배열-**LdapServerConnection** 매개는 **추가 AdfsLocalClaimsProviderTrust** cmdlet 합니다.

    **참고:** DN 및 암호를 입력 하 고 Get-Credential LDAP 인스턴스를 연결 하는 데 사용할 사용 하려고 하면 오류가 발생 하기 때문에 될 수 있는 특정 입력된 형식 도메인 예를 들어, \ 사용자 이름에 대 한 사용자 인터페이스 요구 사항 또는 user@domain.tld합니다. 대신 사용할 수 있습니다 ConvertTo-SecureString cmdlet 다음과 같은 (아래 예로 가정 uid ou 관리자 = LDAP 인스턴스를 연결 하는 데 사용할 DN 자격 증명으로 = system):

    ```
    $ldapuser = ConvertTo-SecureString -string "uid=admin,ou=system" -asplaintext -force
    $DirectoryCred = Get-Credential -username $ldapuser -Message "Enter the credentials to bind to the LDAP instance:"
    ```

    Uid에 대 한 암호를 입력 한 다음 관리자 = 및 나머지 단계를 완료 합니다.

2.  그런 다음에 사용 하 여 기존 ADFS 클레임 LDAP 특성 매핑의 옵션 단계를 수행할 수 있습니다는 **새로 AdfsLdapAttributeToClaimMapping** cmdlet 합니다. 아래의 예제 givenName, 성, 지도 CommonName LDAP 특성 ADFS 클레임을:

    ```
    #Map given name claim
    $GivenName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute givenName -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname"
    # Map surname claim
    $Surname = New-AdfsLdapAttributeToClaimMapping -LdapAttribute sn -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname"
    # Map common name claim
    $CommonName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute cn -ClaimType "http://schemas.xmlsoap.org/claims/CommonName"
    ```

    이 매핑이 특성 LDAP 스토어에서 사용할 수 있도록 adfs에서 조건부 액세스 제어 규칙을 만들기 위해 Adfs의 클레임으로 수행 됩니다. 또한 Adfs를 쉽게 클레임 LDAP 특성 매핑될 수 있는 방법을 제공 하 여 사용자 지정 스키마 LDAP 스토어에서 작업할 수 있습니다.

3.  마지막으로,에 등록 해야 LDAP 스토어 Adfs로 사용 하 여 공급자 신뢰 하는 로컬 클레임은 **추가 AdfsLocalClaimsProviderTrust** cmdlet:

    ```
    Add-AdfsLocalClaimsProviderTrust -Name "Vendors" -Identifier "urn:vendors" -Type Ldap

    # Connection info
    -LdapServerConnection $vendorDirectory 

    # How to locate user objects in directory
    -UserObjectClass inetOrgPerson -UserContainer "CN=VendorsContainer,CN=VendorsPartition" -LdapAuthenticationMethod Basic 

    # Claims for authenticated users
    -AnchorClaimLdapAttribute mail -AnchorClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" -LdapAttributeToClaimMapping @($GivenName, $Surname, $CommonName) 

    # General claims provider properties
    -AcceptanceTransformRules "c:[Type != ''] => issue(claim=c);" -Enabled $true 

    # Optional - supply user name suffix if you want to use Ws-Trust
    -OrganizationalAccountSuffix "vendors.contoso.com"

    ```

    위 예제에서는 "공급 업체" 라고 로컬 클레임 공급자 신뢰를 만들고 있습니다. 지정 하 여 로컬 클레임 공급자 신뢰가 나와 LDAP 디렉터리에 연결 하려면 adfs 연결 정보를 지정 하는 `$vendorDirectory`하 고 `-LdapServerConnection`매개 합니다. 1 단계에서 사용자가 할당 `$vendorDirectory`연결 문자열 특정 LDAP 디렉터리에 연결할 때 사용할 수 있습니다. 마지막으로 지정 하는 하 고 `$GivenName`, `$Surname`, 및 `$CommonName`LDAP 특성 (ADFS 클레임에 매핑됩니다) 보안 FS 발급 토큰과 광고에에서 클레임 통해 발급 뿐만 아니라 다단계 인증 정책 및 발급 인증 규칙을 포함 하 여 조건부 액세스 제어를 사용 하려는 합니다. Adfs와 같은 Ws-trust 프로토콜 활성화를 사용 하기 위해이 통해 ADFS 사용 권한 요청을 처리 하는 경우 현지 클레임 제공자 신뢰 구분할 OrganizationalAccountSuffix 매개를 지정 해야 합니다.

## <a name="see-also"></a>참조 하십시오
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)


