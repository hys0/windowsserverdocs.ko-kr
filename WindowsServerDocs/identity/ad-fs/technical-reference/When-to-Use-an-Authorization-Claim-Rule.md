---
ms.assetid: b734cbcb-342c-4a28-8ab5-b9cd990bb1c2
title: 권한 부여 클레임 규칙을 사용하는 경우
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 49246d9df294b966f0ba38b1d3c1f361ce5f1d5f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407268"
---
# <a name="when-to-use-an-authorization-claim-rule"></a>권한 부여 클레임 규칙을 사용하는 경우
들어오는 클레임 유형을 사용 해야 하는 \(경우\) Active Directory Federation Services AD FS에서이 규칙을 사용할 수 있습니다. 그런 다음 사용자가 선택한 값에 따라 사용자가 액세스를 허용할지 또는 거부할지를 결정 하는 작업을 적용 합니다. 규칙에를 지정 합니다. 이 규칙을 사용하는 경우 규칙에서 구성하는 옵션 중 하나에 따라 다음 규칙 논리와 일치하는 클레임을 통과 또는 변환합니다.  
  
|규칙 옵션|규칙 논리|  
|---------------|--------------|  
|모든 사용자 허용|들어오는 클레임 유형이 *임의의 클레임 유형* 이고 값이 *임의의 값*이면 값이 있는 클레임 발급이 *허용*됩니다.|  
|이 들어오는 클레임의 사용자에 대한 액세스 허용|들어오는 클레임 유형이 *지정된 클레임 유형* 이고 값이 *지정된 값*이면 값이 있는 클레임 발급이 *허용*됩니다.|  
|이 들어오는 클레임의 사용자에 대한 액세스 거부|들어오는 클레임 유형이 *지정된 클레임 유형* 이고 값이 *지정된 값*이면 값이 있는 클레임 발급이 *거부*됩니다.|  
  
다음 섹션에서는 클레임 규칙의 기본 사항을 소개하고 이 규칙을 사용하는 경우에 대한 추가 정보를 제공합니다.  
  
## <a name="about-claim-rules"></a>클레임 규칙 정보  
클레임 규칙은 들어오는 클레임에 조건을 적용 하는 비즈니스 논리의 인스턴스를 나타냅니다 \(다음 y x if\) 조건 매개 변수를 기반으로 하는 나가는 클레임을 생성 합니다. 다음 목록은 이 항목을 더 읽기 전에 클레임 규칙에 대해 알아야 하는 중요한 팁을 간략하게 설명합니다.  
  
-   AD FS 관리 스냅인에서\-클레임 규칙을 다시 만든 클레임 규칙 템플릿을 사용 하 여  
  
-   클레임 규칙 프로세스 들어오는 클레임을 클레임 공급자에서 직접 \(Active Directory 또는 다른 페더레이션 서비스와 같은\) 또는 수용의 출력에서 클레임 공급자 트러스트에 대 한 규칙을 변환 합니다.  
  
-   클레임 규칙은 지정된 규칙 집합 내의 시간 순서대로 클레임 발급 엔진에 의해 처리됩니다. 규칙에 우선 순위를 설정하여 지정된 규칙 집합 내의 이전 규칙에 의해 생성된 클레임을 더욱 구체화하거나 필터링할 수 있습니다.  
  
-   클레임 규칙 템플릿에서는 항상 들어오는 클레임 유형을 지정해야 합니다. 그러나 단일 규칙을 사용하여 동일한 클레임 유형 내의 여러 클레임 값을 처리할 수 있습니다.  
  
클레임 규칙 및 클레임 규칙 집합에 대 한 정보를 자세한 참조 [규칙의 역할 클레임](The-Role-of-Claim-Rules.md)합니다. 규칙은 처리 하는 방법에 대 한 자세한 내용은 참조 [클레임 엔진의 역할](The-Role-of-the-Claims-Engine.md)합니다. 자세한 내용은 클레임 규칙 집합을 처리 하는 방법을 참조 하십시오 [클레임 파이프라인의 역할](The-Role-of-the-Claims-Pipeline.md)합니다.  
  
## <a name="permit-all-users"></a>모든 사용자 허용  
모든 사용자 허용 규칙 템플릿을 사용하는 경우 모든 사용자가 신뢰 당사자에 액세스할 수 있습니다. 그러나 추가 권한 부여 규칙을 사용하여 액세스를 더욱 제한할 수 있습니다. 한 규칙은 사용자가 신뢰 당사자에 액세스할 수 있도록 허용하고 다른 규칙은 신뢰 당사자에 대한 사용자 액세스를 거부하는 경우 거부 결과가 허용 결과를 재정의하며 사용자 액세스가 거부됩니다.  
  
페더레이션 서비스에서 신뢰 당사자에 대한 액세스가 허용된 사용자도 신뢰 당사자에 의해 서비스가 거부될 수 있습니다.  
  
## <a name="permit-access-to-users-with-this-incoming-claim"></a>이 들어오는 클레임의 사용자에 대한 액세스 허용  
들어오는 클레임에 따라 사용자 허용 또는 거부 규칙 템플릿을 사용 하 여 규칙을 만들고 허용 조건을 설정 하는 경우 들어오는 클레임의 유형 및 값에 따라 신뢰 당사자에 대 한 특정 사용자의 액세스를 허용할 수 있습니다. 예를 들어 이 규칙 템플릿을 사용하여 값이 Domain Admins인 그룹 클레임이 있는 사용자만 허용하는 규칙을 만들 수 있습니다. 한 규칙은 사용자가 신뢰 당사자에 액세스할 수 있도록 허용하고 다른 규칙은 신뢰 당사자에 대한 사용자 액세스를 거부하는 경우 거부 결과가 허용 결과를 재정의하며 사용자 액세스가 거부됩니다.  
  
페더레이션 서비스에서 신뢰 당사자에 대한 액세스가 허용된 사용자도 신뢰 당사자에 의해 서비스가 거부될 수 있습니다. 모든 사용자가 신뢰 당사자에 액세스할 수 있도록 허용하려면 모든 사용자 허용 규칙 템플릿을 사용합니다.  
  
## <a name="deny-access-to-users-with-this-incoming-claim"></a>이 들어오는 클레임의 사용자에 대한 액세스 거부  
들어오는 클레임에 따라 사용자 허용 또는 거부 규칙 템플릿을 사용 하 여 규칙을 만들고 조건을 거부로 설정 하는 경우 들어오는 클레임의 유형 및 값에 따라 신뢰 당사자에 대 한 사용자의 액세스를 거부할 수 있습니다. 예를 들어 이 규칙 템플릿을 사용하여 값이 Domain Users인 그룹 클레임이 있는 사용자를 모두 거부하는 규칙을 만들 수 있습니다.  
  
거부 조건을 사용하면서도 특정 사용자가 신뢰 당사자에 액세스할 수 있게 하려는 경우 신뢰 당사자에 대한 해당 사용자의 액세스를 허용하는 허용 조건이 포함된 권한 부여 규칙을 나중에 명시적으로 추가해야 합니다.  
  
클레임 발급 엔진이 규칙 집합을 처리할 때 사용자 액세스가 거부 된 경우 추가 규칙 처리가 종료 되 고 AD FS 사용자의 요청에 "액세스 거부" 오류가 반환 됩니다.  
  
## <a name="authorizing-users"></a>사용자 권한 부여  
AD FS에서 권한 부여 규칙은 사용 \(\) 된 클레임 유형에 따라 사용자 또는 사용자 그룹이 지정 된 신뢰 당사자의 웹\-기반 리소스에 액세스할 수 있는지 여부를 결정 하는 허용 또는 거부 클레임을 발급 하는 데 사용 됩니다. 파티. 권한 부여 규칙은 신뢰 당사자 트러스트에만 설정할 수 있습니다.  
  
### <a name="authorization-rule-sets"></a>권한 부여 규칙 집합  
구성해야 하는 허용 또는 거부 작업의 유형에 따라 다양한 권한 부여 규칙 집합이 존재합니다. 이러한 규칙 집합은 다음과 같습니다.  
  
-   **발급 권한 부여 규칙**: 이러한 규칙은 사용자가 신뢰 당사자에 대한 클레임을 수신하여 신뢰 당사자에 액세스할 수 있는지 여부를 결정합니다.  
  
-   **위임 권한 부여 규칙**: 이러한 규칙은 사용자가 신뢰 당사자에게 다른 사용자로 작업할 수 있는지 여부를 결정합니다. 사용자가 다른 사용자로 작업하는 경우에도 요청하는 사용자에 대한 클레임이 토큰에 배치됩니다.  
  
-   **가장 권한 부여 규칙**: 이러한 규칙은 사용자가 신뢰 당사자에게 다른 사용자를 완전히 가장할 수 있는지 여부를 결정합니다. 다른 사용자를 가장하면 신뢰 당사자가 사용자의 가장 여부를 확인할 수 없으므로 매우 강력한 기능입니다.  
  
권한 부여 규칙 프로세스가 클레임 발급 파이프라인에 얼마나 적합한지에 대한 자세한 내용은 클레임 발급 엔진의 역할을 참조하세요.  
  
### <a name="supported-claim-types"></a>지원되는 클레임 유형  
AD FS은 사용자의 허용 또는 거부 여부를 결정 하는 데 사용 되는 두 클레임 유형을 정의 합니다. 이러한 클레임 유형 Uniform resource identifier \(uri\) 는 다음과 같습니다.  
  
1.  **허용**: http:\/\/schemas.microsoft.com\/authorization\/클레임허용\/  
  
2.  **거부**: http:\/\/schemas.microsoft.com\/권한부여\/클레임거부\/  
  
## <a name="how-to-create-this-rule"></a>이 규칙을 만드는 방법  
클레임 규칙 언어를 사용 하거나 **모든 사용자 허용** 규칙 템플릿을 사용 하거나 AD FS 관리 스냅인\-의 **들어오는 클레임에 따라 사용자 허용 또는 거부** 규칙 템플릿을 사용 하 여 권한 부여 규칙을 모두 만들 수 있습니다. 모든 사용자 허용 규칙 템플릿은 구성 옵션을 제공하지 않습니다. 그러나 들어오는 클레임에 따라 사용자 허용 또는 거부 규칙 템플릿은 다음과 같은 구성 옵션을 제공합니다.  
  
-   클레임 규칙 이름 지정  
  
-   들어오는 클레임 유형 지정  
  
-   들어오는 클레임 값 입력  
  
-   이 들어오는 클레임의 사용자에 대한 액세스 허용  
  
-   이 들어오는 클레임의 사용자에 대한 액세스 거부  
  
이 템플릿을 만드는 방법에 대 한 자세한 내용은 [모든 사용자를 허용 하는 규칙 만들기](https://technet.microsoft.com/library/ee913577.aspx) 또는 AD FS 배포 가이드에서 [들어오는 클레임에 따라 사용자를 허용 하거나 거부 하는 규칙](https://technet.microsoft.com/library/ee913594.aspx) 만들기를 참조 하세요.  
  
## <a name="using-the-claim-rule-language"></a>클레임 규칙 언어 사용  
클레임 값이 사용자 지정 패턴과 일치하는 경우에만 클레임을 보내야 하는 경우 사용자 지정 규칙을 사용해야 합니다. 자세한 내용은 [사용자 지정 클레임 규칙을 사용 하는 경우](When-to-Use-a-Custom-Claim-Rule.md)합니다.  
  
### <a name="example-of-how-to-create-an-authorization-rule-based-on-multiple-claims"></a>여러 클레임을 기반으로 하여 권한 부여 규칙을 만드는 방법의 예  
클레임 규칙 언어 구문을 사용 하 여 클레임에 권한을 부여 하는 경우 사용자의 원래 클레임에 여러 클레임이 있는지 여부에 따라 클레임을 발급할 수도 있습니다. 다음 규칙은 사용자가 Editors 그룹의 구성원이고 Windows 인증을 사용하여 인증하는 경우에만 권한 부여 클레임을 발급합니다.  
  
```  
[type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod",   
value == "urn:federation:authentication:windows" ]  
&& [type == "http://schemas.xmlsoap.org/claims/Group ", value == “editors”]   
=> issue(type = "http://schemas.xmlsoap.org/claims/authZ", value = "Granted");  
```  
  
### <a name="example-of-how-to-create-authorization-rules-that-will-delegate-who-can-create-or-remove-federation-server-proxy-trusts"></a>페더레이션 서버 프록시 트러스트를 만들거나 제거할 수 있는 사람을 위임하는 권한 부여 규칙을 만드는 방법의 예  
페더레이션 서비스가 페더레이션 서버 프록시를 사용하여 클라이언트 요청을 리디렉션하려면 먼저 페더레이션 서비스와 페더레이션 서버 프록시 컴퓨터 간에 트러스트를 설정해야 합니다. 기본적으로 AD FS 페더레이션 서버 프록시 구성 마법사에서 다음 자격 증명 중 하나를 성공적으로 제공하면 프록시 트러스트가 설정됩니다.  
  
-   프록시가 보호하는, 페더레이션 서비스에서 사용되는 서비스 계정  
  
-   페더레이션 서버 팜의 모든 페더레이션 서버에서 로컬 Administrators 그룹의 구성원인 Active Directory 도메인 계정  
  
지정된 페더레이션 서비스에 대한 프록시 트러스트를 만들 수 있는 사용자를 지정하려는 경우 다음 위임 방법 중 하나를 사용할 수 있습니다. 이 방법 목록은 가장 안전 하 고 문제가 적은 위임 방법에 대 한 AD FS 제품 팀의 권장 사항에 따라 우선 순위를 갖습니다. 조직의 요구에 따라 이러한 방법 중 하나만 사용해야 합니다.  
  
1.  Active Directory \(에서 도메인 보안 그룹을 만듭니다. 예를 들어, fsproxytrustcreators\)는 팜의 각 페더레이션 서버에서 로컬 관리자 그룹에이 그룹을 추가 하 고 원하는 사용자 계정만 추가 합니다. 새 그룹에이 권한을 위임 하려면입니다. 이것은 기본적으로 사용되는 방법입니다.  
  
2.  팜의 각 페더레이션 서버에서 관리자 그룹에 사용자의 도메인 계정을 추가 합니다.  
  
3.  어떤 이유로든 이러한 방법 중 하나를 사용할 수 없는 경우 이 용도로 권한 부여 규칙을 만들 수도 있습니다. 이 규칙을 제대로 작성하지 않을 경우 발생할 수 있는 가능한 복잡성으로 인해 권장되지는 않지만 사용자 지정 권한 부여 규칙을 사용하여 지정된 페더레이션 서비스와 연결된 모든 페더레이션 서버 프록시 간에 트러스트를 만들거나 제거할 수 있는 Active Directory 도메인 사용자 계정을 위임할 수 있습니다.  
  
    방법 3을 선택 하는 경우 다음 규칙 구문을 사용 하 여 지정 된 사용자 \(가 허용 하는 권한 부여 클레임을 발급할 수 있습니다 .이 경우 contoso\\frankm\) 는 하나 이상의 페더레이션 서버 프록시에 대 한 트러스트를 만들 수 있습니다. 페더레이션 서비스. Windows PowerShell 명령 **Set\-set-adfsproperties addproxyauthorizationrules**를 사용 하 여이 규칙을 적용 해야 합니다.  
  
    ```  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", issuer=~"^AD AUTHORITY$" value == "contoso\frankm" ] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true")  
  
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])   
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );  
    ```  
  
    나중에 사용자가 더 이상 프록시 트러스트를 만들 수 없도록 사용자를 제거하려는 경우 기본 프록시 트러스트 권한 부여 규칙으로 되돌려 페더레이션 서비스에 대한 프록시 트러스트를 만들 수 있는 사용자 권한을 제거할 수 있습니다. 또한 Windows PowerShell 명령 **Set\-set-adfsproperties addproxyauthorizationrules**를 사용 하 여이 규칙을 적용 해야 합니다.  
  
    ```  
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])   
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );  
    ```  
  
클레임 규칙 언어를 사용 하는 방법에 대 한 자세한 내용은 참조 [클레임 규칙 언어의 역할](The-Role-of-the-Claim-Rule-Language.md)합니다.  
  

