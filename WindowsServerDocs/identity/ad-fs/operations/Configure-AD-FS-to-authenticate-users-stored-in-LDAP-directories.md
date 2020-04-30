---
ms.assetid: e863ab80-4e4c-48d3-bdaa-31815ef36bae
title: LDAP 디렉터리에 저장된 사용자를 인증하도록 AD FS 구성
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a3e429d43fd644cd2b8ba3a5b123deecc2696f24
ms.sourcegitcommit: 912a5a402ecc6b39c1584338ea635a2ac11a4eb9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82219287"
---
# <a name="configure-ad-fs-to-authenticate-users-stored-in-ldap-directories-in-windows-server-2016-or-later"></a>Windows Server 2016 이상에서 LDAP 디렉터리에 저장 된 사용자를 인증 하도록 AD FS 구성

다음 항목에서는 LDAP (Lightweight Directory Access Protocol) v3 규격 디렉터리에 id가 저장 된 사용자를 인증 하도록 AD FS 인프라를 설정 하는 데 필요한 구성을 설명 합니다.

많은 조직에서 id 관리 솔루션은 Active Directory, AD LDS 또는 타사 LDAP 디렉터리의 조합으로 구성 됩니다. LDAP v3 규격 디렉터리에 저장 된 사용자를 인증 하는 AD FS 지원 추가를 통해 사용자 id의 저장 위치에 관계 없이 전체 엔터프라이즈급 AD FS 기능 집합을 활용할 수 있습니다. AD FS LDAP v3 호환 디렉터리를 지원 합니다.

> [!NOTE]
> AD FS 기능 중 일부에는 SSO (Single Sign-On), 장치 인증, 유연한 조건부 액세스 정책, 웹 응용 프로그램 프록시와의 통합을 통해 어디에서 나 작업 지원, Azure AD와의 원활한 페더레이션 등이 있습니다. 그러면 사용자와 사용자가 Office 365 및 기타 SaaS 응용 프로그램을 포함 하 여 클라우드를 활용할 수 있습니다.  자세한 내용은 [Active Directory Federation Services 개요](../../ad-fs/AD-FS-2016-Overview.md)를 참조 하세요.

AD FS가 LDAP 디렉터리에서 사용자를 인증 하도록 하려면 **로컬 클레임 공급자 트러스트**를 만들어이 ldap 디렉터리를 AD FS 팜에 연결 해야 합니다.  로컬 클레임 공급자 트러스트는 AD FS 팜의 LDAP 디렉터리를 나타내는 트러스트 개체입니다. 로컬 클레임 공급자 트러스트 개체는 로컬 페더레이션 서비스에이 LDAP 디렉터리를 식별 하는 다양 한 식별자, 이름 및 규칙으로 구성 됩니다.

여러 **로컬 클레임 공급자 트러스트**를 추가 하 여 동일한 AD FS 팜 내에서 각각 고유한 구성을 사용 하는 여러 LDAP 디렉터리를 지원할 수 있습니다. 또한 AD FS 있는 포리스트에서 신뢰 하지 않는 AD DS 포리스트는 로컬 클레임 공급자 트러스트로도 모델링할 수 있습니다. Windows PowerShell을 사용 하 여 로컬 클레임 공급자 트러스트를 만들 수 있습니다.

LDAP 디렉터리 (로컬 클레임 공급자 트러스트)는 동일한 AD FS 팜 내에서 동일한 AD FS 서버에 AD 디렉터리 (클레임 공급자 트러스트)와 공존할 수 있습니다. 따라서 AD FS의 단일 인스턴스는 AD 및 비-AD 디렉터리에 저장 된 사용자에 대 한 액세스를 인증 하 고 권한을 부여할 수 있습니다.

LDAP 디렉터리에서 사용자를 인증 하는 데는 폼 기반 인증만 지원 됩니다. LDAP 디렉터리에서 사용자를 인증 하는 데는 인증서 기반 및 Windows 통합 인증이 지원 되지 않습니다.

SAML, WS-FEDERATION 및 OAuth를 비롯 하 여 AD FS에서 지 원하는 모든 수동 권한 부여 프로토콜은 LDAP 디렉터리에 저장 된 id에 대해서도 지원 됩니다.

WS-TRUST 활성 권한 부여 프로토콜은 LDAP 디렉터리에 저장 된 id에 대해서도 지원 됩니다.

## <a name="configure-ad-fs-to-authenticate-users-stored-in-an-ldap-directory"></a>LDAP 디렉터리에 저장 된 사용자를 인증 하도록 AD FS 구성
LDAP 디렉터리에서 사용자를 인증 하도록 AD FS 팜을 구성 하려면 다음 단계를 완료할 수 있습니다.

1. 먼저 **AdfsLdapServerConnection** cmdlet을 사용 하 여 LDAP 디렉터리에 대 한 연결을 구성 합니다.

   ```
   $DirectoryCred = Get-Credential
   $vendorDirectory = New-AdfsLdapServerConnection -HostName dirserver -Port 50000 -SslMode None -AuthenticationMethod Basic -Credential $DirectoryCred
   ```

   > [!NOTE]
   > 연결 하려는 각 LDAP 서버에 대 한 새 연결 개체를 만드는 것이 좋습니다. AD FS는 여러 복제본 LDAP 서버에 연결할 수 있으며 특정 LDAP 서버가 다운 되는 경우 자동으로 장애 조치 (failover) 됩니다. 이러한 경우에는 이러한 각 복제본 LDAP 서버에 대해 하나의 AdfsLdapServerConnection을 만든 다음 **AdfsLocalClaimsProviderTrust** cmdlet의-**LdapServerConnection** 매개 변수를 사용 하 여 연결 개체의 배열을 추가할 수 있습니다.

   **참고:** LDAP 인스턴스에 바인딩하는 데 사용할 DN 및 암호에 Get 자격 증명과 유형을 사용 하려고 하면 특정 입력 형식에 대 한 사용자 인터페이스 요구 사항 (예: domain\username 또는 user@domain.tld) 때문에 오류가 발생할 수 있습니다. 대신 다음과 같이 Convertto-html cmdlet을 사용할 수 있습니다. 아래 예제에서는 uid = admin, ou = system을 LDAP 인스턴스에 바인딩하는 데 사용할 자격 증명의 DN으로 가정 합니다.

   ```
   $ldapuser = ConvertTo-SecureString -string "uid=admin,ou=system" -asplaintext -force
   $DirectoryCred = Get-Credential -username $ldapuser -Message "Enter the credentials to bind to the LDAP instance:"
   ```

   그런 다음 uid = admin에 대 한 암호를 입력 하 고 나머지 단계를 완료 합니다.

2. 그런 다음, **새-AdfsLdapAttributeToClaimMapping** cmdlet을 사용 하 여 기존 AD FS 클레임에 대 한 LDAP 특성 매핑을 위한 선택적 단계를 수행할 수 있습니다. 아래 예제에서는 givenName, 성 및 CommonName LDAP 특성을 AD FS 클레임에 매핑합니다.

   ```
   #Map given name claim
   $GivenName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute givenName -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname"
   # Map surname claim
   $Surname = New-AdfsLdapAttributeToClaimMapping -LdapAttribute sn -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname"
   # Map common name claim
   $CommonName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute cn -ClaimType "http://schemas.xmlsoap.org/claims/CommonName"
   ```

   이 매핑은 AD FS에서 조건부 액세스 제어 규칙을 만들기 위해 AD FS에서 클레임으로 사용할 수 있는 LDAP 저장소의 특성을 설정 하기 위해 수행 됩니다. 또한 ldap 특성을 클레임에 쉽게 매핑할 수 있는 방법을 제공 하 여 AD FS LDAP 저장소에서 사용자 지정 스키마를 사용할 수 있습니다.

3. 마지막으로 **AdfsLocalClaimsProviderTrust** cmdlet을 사용 하 여 AD FS에 LDAP 저장소를 로컬 클레임 공급자 트러스트로 등록 해야 합니다.

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

   위의 예제에서는 "공급 업체" 라는 로컬 클레임 공급자 트러스트를 만듭니다. AD FS에 대 한 연결 정보를 지정 하 여 `$vendorDirectory` `-LdapServerConnection` 이 로컬 클레임 공급자 트러스트가 나타내는 LDAP 디렉터리에 연결 합니다. 1 단계에서는 특정 LDAP 디렉터리에 연결할 때 `$vendorDirectory` 사용할 연결 문자열을 할당 했습니다. 마지막으로 `$GivenName`, `$Surname`, 및 `$CommonName` LDAP 특성 (AD FS 클레임에 매핑)이 multi-factor authentication 정책 및 발급 권한 부여 규칙을 비롯 한 조건부 액세스 제어에 사용 되 고 AD FS 발급 된 보안 토큰에서 클레임을 통해 발급 하도록 지정 합니다. AD FS에서 Ws-trust와 같은 활성 프로토콜을 사용 하려면 활성 권한 부여 요청을 처리할 때 로컬 클레임 공급자 트러스트를 구분할 수 AD FS 있도록 하는 OrganizationalAccountSuffix 매개 변수를 지정 해야 합니다.

## <a name="see-also"></a>참고 항목
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)

