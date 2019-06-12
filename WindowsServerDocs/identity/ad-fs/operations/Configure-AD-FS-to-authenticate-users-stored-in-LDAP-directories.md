---
ms.assetid: e863ab80-4e4c-48d3-bdaa-31815ef36bae
title: LDAP 디렉터리에 저장된 사용자를 인증하도록 AD FS 구성
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2053f0a93f33cdfdd85eec8cdbb6eca4ebad1ff0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444921"
---
# <a name="configure-ad-fs-to-authenticate-users-stored-in-ldap-directories"></a>LDAP 디렉터리에 저장된 사용자를 인증하도록 AD FS 구성

다음 항목에서는 id 액세스 프로토콜 LDAP (Lightweight Directory) v3 호환 디렉터리에 저장 된 사용자를 인증 하도록 AD FS 인프라를 사용 하도록 설정 하는 데 필요한 구성을 설명 합니다.

많은 조직에서 id 관리 솔루션 Active Directory, AD LDS 또는 타사 LDAP 디렉터리의 조합으로 구성 됩니다. LDAP v3 호환 디렉터리에 저장 된 사용자를 인증 하는 것에 대 한 AD FS 지원 추가 사용 하 여 얻을 수 있습니다 전체 엔터프라이즈 수준에서 AD FS 기능 사용자 id에 저장 되는 위치에 관계 없이 집합입니다. AD FS 모든 LDAP v3 호환 디렉터리를 지원합니다.

> [!NOTE]
> AD FS 기능 중 일부에서 single sign-on (SSO), 장치 인증을 유연한 조건부 액세스 정책을 포함, 지원에서-어디서 나 작업 가능한 웹 응용 프로그램 프록시를 사용 하 여 통합을 통해 원활 하 게는 Azure AD와 페더레이션 있습니다 및 사용자가 Office 365 및 기타 SaaS 응용 프로그램을 포함 하 여 클라우드를 활용할 수 있습니다.  자세한 내용은 [Active Directory Federation Services 개요](../../ad-fs/AD-FS-2016-Overview.md)합니다.

LDAP 디렉터리에서 사용자를 인증 하도록 AD FS에 대 한 순서로 연결 해야이 LDAP 디렉터리에 AD FS 팜에 만들어를 **로컬 클레임 공급자 트러스트**합니다.  로컬 클레임 공급자 트러스트에는 AD FS 팜의 LDAP 디렉터리를 나타내는 트러스트 개체입니다. 로컬 클레임 공급자 트러스트 개체는 다양 한 식별자, 이름 및 로컬 페더레이션 서비스에이 LDAP 디렉터리를 식별 하는 규칙으로 구성 됩니다.

여러 추가 하 여 동일한 AD FS 팜에서 자체 구성을 사용 하 여 각 여러 LDAP 디렉터리를 지원할 수 있습니다 **로컬 클레임 공급자 트러스트**합니다. 또한에 거주 하 고 AD FS 된 포리스트에서 신뢰 하지 않는 AD DS 포리스트 로컬 클레임 공급자 트러스트로 모델링할 수도 있습니다. Windows PowerShell을 사용 하 여 로컬 클레임 공급자 트러스트를 만들 수 있습니다.

동일한 AD FS 팜 내에서 동일한 AD FS 서버에서 AD 디렉터리 (클레임 공급자 트러스트)를 사용 하 여 LDAP 디렉터리 (로컬 클레임 공급자 트러스트) 공존할 수 있습니다, 그리고 따라서 AD FS의 단일 인스턴스는 지원 되는 사용자에 대 한 액세스 권한 부여 및 인증 두 AD에 저장 하 고 비 AD 디렉터리입니다.

LDAP 디렉터리에서 사용자를 인증 양식 기반 인증만 사용할 수 있습니다. LDAP 디렉터리에 사용자를 인증 하는 것에 대 한 인증서 기반 인증 및 통합 Windows 인증을 사용할 수 없습니다.

모든 수동 권한 부여 프로토콜 SAML, Ws-federation을 포함 하 여 AD FS에서 지원 되는 및 LDAP 디렉터리에 저장 되는 id에 대 한 OAuth 지원 됩니다.

LDAP 디렉터리에 저장 되는 id에 대 한 Ws-trust 활성 인증 프로토콜도 지원 됩니다.

## <a name="configure-ad-fs-to-authenticate-users-stored-in-an-ldap-directory"></a>LDAP 디렉터리에 저장 된 사용자를 인증 하도록 AD FS를 구성 합니다.
LDAP 디렉터리에서 사용자를 인증 하도록 AD FS 팜을 구성 하려면 다음 단계를 완료할 수 있습니다.

1. 먼저, 사용 하 여 LDAP 디렉터리에 대 한 연결을 구성 합니다 **새로 만들기-AdfsLdapServerConnection** cmdlet:

   ```
   $DirectoryCred = Get-Credential
   $vendorDirectory = New-AdfsLdapServerConnection -HostName dirserver -Port 50000 -SslMode None -AuthenticationMethod Basic -Credential $DirectoryCred
   ```

   > [!NOTE]
   > 에 연결 하려는 각 LDAP 서버에 대 한 새 연결 개체를 만드는 것이 좋습니다. AD FS는 여러 복제본 LDAP 서버에 연결 하 고 자동으로 장애 조치 특정 LDAP 서버가 다운 된 경우 수 있습니다. 이러한 경우에 대 한 각 복제본 LDAP 서버에 대 한 하나의 AdfsLdapServerConnection 만들기 추가 하는 다음 사용 하 여 연결 개체의 배열-**LdapServerConnection** 의 매개 변수는  **추가 AdfsLocalClaimsProviderTrust** cmdlet.

   **참고:** LDAP 인스턴스에 바인딩하는 데 사용 될 Get-credential 및 형식에 DN 및 암호를 사용 하려고 하기 때문에 오류가 발생할 수 있습니다는 특정 입력된 형식, 예를 들어 도메인 \ 사용자 이름에 대 한 사용자 인터페이스 요구 사항 또는 user@domain.tld합니다. 대신 사용할 수 있습니다 Convertto-securestring cmdlet은 다음과 같습니다 (아래 예제에서는 가정 uid 관리, ou = LDAP 인스턴스에 바인딩하는 데 사용 될 자격 증명의 dn = 시스템):

   ```
   $ldapuser = ConvertTo-SecureString -string "uid=admin,ou=system" -asplaintext -force
   $DirectoryCred = Get-Credential -username $ldapuser -Message "Enter the credentials to bind to the LDAP instance:"
   ```

   Uid에 대 한 암호를 입력 한 다음 = admin 및 나머지 단계를 완료 합니다.

2. LDAP 특성을 사용 하 여 기존 AD FS 클레임 매핑의 선택적 단계를 수행 하는 다음에 **새로 만들기-AdfsLdapAttributeToClaimMapping** cmdlet. 아래 예에서 givenName, 성 매핑하고 CommonName LDAP 특성을 클레임으로 AD FS:

   ```
   #Map given name claim
   $GivenName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute givenName -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname"
   # Map surname claim
   $Surname = New-AdfsLdapAttributeToClaimMapping -LdapAttribute sn -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname"
   # Map common name claim
   $CommonName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute cn -ClaimType "http://schemas.xmlsoap.org/claims/CommonName"
   ```

   이 매핑은 특성 LDAP 저장소에서 사용할 수 있도록 AD FS의 조건부 액세스 제어 규칙을 만들기 위해 AD FS에서 클레임으로 수행 됩니다. 또한 AD FS를 클레임으로 LDAP 특성을 매핑할 수 있는 간단한 방법을 제공 하 여 LDAP 저장소에서 사용자 지정 스키마를 작업할 수 있습니다.

3. 마지막으로 등록 해야 LDAP 저장소 AD FS를 사용 하 여 로컬 클레임 공급자 트러스트를 사용 하 여 **추가 AdfsLocalClaimsProviderTrust** cmdlet:

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

   위의 예에서 "공급 업체" 라는 로컬 클레임 공급자 트러스트를 만듭니다. 이 로컬 클레임 공급자 트러스트를 할당 하 여 나타내는 LDAP 디렉터리에 연결 하려면 AD FS에 대 한 연결 정보를 지정할 `$vendorDirectory` 에 `-LdapServerConnection` 매개 변수입니다. 1 단계에서 하 한이 할당 `$vendorDirectory` 특정 LDAP 디렉터리에 연결할 때 사용할 연결 문자열입니다. 마지막으로 지정 하는 하는 `$GivenName`, `$Surname`, 및 `$CommonName` multi-factor authentication 및 발급을 포함 하 여 조건부 액세스 제어를 사용 해야 하는 LDAP 특성 (AD FS 클레임을 매핑한) 권한 부여와 AD FS에서 발급 한 보안 토큰의 클레임을 통해 발급도 규칙입니다. AD FS를 사용 하 여 Ws-trust 같은 활성 프로토콜을 사용 하려면 현재 권한 부여 요청을 서비스 하는 경우 로컬 클레임 공급자 트러스트를 구분 하도록 AD FS를 사용 하도록 설정 하는 OrganizationalAccountSuffix 매개 변수를 지정 해야 합니다.

## <a name="see-also"></a>관련 항목
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)


