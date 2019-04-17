---
ms.assetid: b734cbcb-342c-4a28-8ab5-b9cd990bb1c2
title: "승인 클레임 규칙을 사용 하는 경우"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 144e382692e8f2a6732f8c7c5b8a1dd6049192cb
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="when-to-use-an-authorization-claim-rule"></a>승인 클레임 규칙을 사용 하는 경우
이 규칙 수신 클레임 유형 촬영 한 다음 사용자를 허용 또는 규칙에 지정 된 값에 따라 액세스 거부는 지 여부를 결정 하는 작업을 적용 해야 할 때 Active Directory Federation Services \(AD FS\)에서 사용할 수 있습니다. 이 규칙을 사용 하면 통과 또는 변환 클레임 규칙에서 구성 옵션 중 하나에 따라 다음 규칙 논리 일치 하는 다음과 같습니다.  
  
|규칙 옵션|규칙 논리|  
|---------------|--------------|  
|모든 사용자가 허용|수신 클레임 유형 같으면 *유형 청구* 같음 가치 및 *값*, 문제 값 같음와 주장 다음 *허용*|  
|이 들어오는 클레임 있는 사용자에 게 액세스 권한을|수신 클레임 유형 같으면 *클레임 유형 지정* 같음 값 및 *클레임 값 지정 된*, 문제 값 같음와 주장 다음 *허용*|  
|액세스를 사용자에 게가 들어오는 클레임 거부|수신 클레임 유형 같으면 *클레임 유형 지정* 같음 값 및 *클레임 값 지정 된*, 문제 값 같음와 주장 다음 *거부*|  
  
다음 섹션에서는 소개 규칙와이 규칙을 사용 하는 경우에 대 한 추가 세부 정보를 제공 합니다.  
  
## <a name="about-claim-rules"></a>클레임은 규칙에 대 한  
클레임은 규칙 비즈니스 논리를 수신 클레임, 조건이 적용 됩니다 인스턴스를 나타냅니다 \ (경우 다음 y\ x) 조건에 따라 보내는 클레임은 생성 하 고 있습니다. 다음 목록에 대해 알아야 하는 팁 더 읽기 전에 규칙 주장 중요 한 개요가이 항목에서:  
  
-   Snap\에서 광고 FS 관리에 클레임 규칙 만들 수만 클레임 규칙 템플릿을 사용 하 여  
  
-   클레임 규칙 프로세스 들어오는 주장 클레임 공급자에서 직접 \ (Active Directory Federation Service\ 다른 등) 또는 수용 출력에서 변형 클레임 공급자 보안에 대 한 규칙 합니다.  
  
-   클레임은 규칙 해당된 규칙 설정 내에서 시간 순서로 클레임 발급 엔진에서 처리 됩니다. 규칙의 우선 순위를 설정 하 여 조정 해가면서 하거나 이전 규칙 해당된 규칙 설정 내에서 생성 되는 클레임 필터링 더 있습니다.  
  
-   청구 규칙 템플릿 항상 해야 하는 수신 클레임 종류를 지정할 수 있습니다. 그러나 규칙 하나를 사용 하 여 동일한 클레임 종류 여러 클레임 값을 처리할 수 있습니다.  
  
자세한 청구 규칙 및 청구 규칙 집합에 대 한 정보를 참조 [주장 규칙의 역할은](The-Role-of-Claim-Rules.md)합니다. 규칙은 처리 하는 방법에 대 한 자세한 내용은 참조 [클레임 엔진 The 역할](The-Role-of-the-Claims-Engine.md)합니다. 자세한 내용은 클레임 규칙 집합 처리 하는 방법을 참조 하세요. [클레임 파이프라인 The 역할](The-Role-of-the-Claims-Pipeline.md)합니다.  
  
## <a name="permit-all-users"></a>모든 사용자가 허용  
모든 사용자가 허용 규칙 서식 파일을 사용 하는 경우 모든 사용자에 게 당사자에 액세스할을 수 있습니다. 그러나 액세스를 제한 하려면 추가 인증 규칙을 사용할 수 있습니다. 한 규칙은 사용자 당사자, 액세스를 허용 하는 경우 다른 규칙 당사자에 대 한 사용자 액세스 거부 거부 결과 재정의 허용 결과 하 고 사용자는 액세스할 수 있습니다.  
  
Federation 서비스에서 당사자에 액세스할 수 있는 사용자를 계속 거부 될 수 있습니다 서비스 당사자가 있습니다.  
  
## <a name="permit-access-to-users-with-this-incoming-claim"></a>이 들어오는 클레임 있는 사용자에 게 액세스 권한을  
를 사용 하면 허용 하거나 사용자가 기반 거부 들어오는 주장 규칙 템플릿을 규칙을 만들고을 허용 조건을 설정 유형과 수신 클레임 값에 따라 당사자에 특정 사용자의 액세스를 허용할 수 있습니다. 예를 들어이 규칙 템플릿을 도메인 관리자 값 주장 그룹 수 있는 사용자만 수 있도록 규칙을 만드는 사용할 수 있습니다. 한 규칙은 사용자 당사자, 액세스를 허용 하는 경우 다른 규칙 당사자에 대 한 사용자 액세스 거부 거부 결과 재정의 허용 결과 하 고 사용자는 액세스할 수 있습니다.  
  
당사자 Federation 서비스에서 액세스할 수 있는 사용자를 계속 거부 될 수 있습니다 서비스 당사자가 있습니다. 당사자에 액세스 하도록 허용 하는 경우 모든 사용자가 허용 규칙 템플릿을 사용 합니다.  
  
## <a name="deny-access-to-users-with-this-incoming-claim"></a>액세스를 사용자에 게가 들어오는 클레임 거부  
를 사용 하면 허용 하거나 사용자가 기반 거부 들어오는 주장 규칙 템플릿을 규칙을 만들고 조건을 거부 하려면 설정에 유형과 수신 클레임 값에 따라 당사자에 대 한 사용자의 액세스를 거부할 수 있습니다. 예를 들어이 규칙 템플릿을 규칙을 거부할 도메인 사용자의 값이 그룹에 있는 모든 사용자에 게 주장 하는 사용할 수 있습니다.  
  
거부 조건을 사용 하면서도 특정 사용자에 대해 당사자에 액세스할 수 있도록 하려면 해당 사용자가 당사자에 액세스할 수 있도록 허용 조건으로 인증 규칙 명시적으로 나중에 추가 해야 합니다.  
  
사용자는 액세스할 클레임 발급 엔진 규칙 설정에서 처리 하는 경우, 처리 추가 규칙 종료 하 고 ADFS 사용자의 요청에 "액세스 거부" 오류를 반환 합니다.  
  
## <a name="authorizing-users"></a>사용자가 허가  
Adfs, 인증 규칙 하는 데 사용을 허용 또는의 사용자 그룹 또는 사용자 있는지 여부를 결정 하는 클레임 거부 \ (에 따라 클레임 종류 used\) 할 수 있는 여부에 지정 된 당사자 Web\ 기반 리소스에 액세스 합니다. 승인 규칙 신뢰 파티 신뢰 에서만 설정 가능 합니다.  
  
### <a name="authorization-rule-sets"></a>인증 규칙 설정  
다른 인증 규칙 집합 허용 유형에 따라 없거나 구성 해야 할 작업을 거부 합니다. 이 규칙 세트 다음과 같습니다.  
  
-   **발급 승인 규칙**:이 규칙 있는지 확인 하는 사용자 수를 당사자에 대 한 주장 받을, 따라서 당사자에 대 한 액세스 합니다.  
  
-   **위임 인증 규칙**: 이러한 규칙 사용자 당사자에 다른 사용자도 사용할 수 있는지 여부를 결정 합니다. 사용자를 다른 사용자와 작동 하는 경우 청구 요청 하는 사용자에 대해 계속 토큰에 배치 됩니다.  
  
-   **가장 인증 규칙**: 이러한 규칙 사용자 당사자에 다른 사용자를 완전히 가장 수 있는지 여부를 결정 합니다. 다른 사용자 가장 당사자는 사용자가 가장 알지 강력한 기능을입니다.  
  
클레임 발급 파이프라인으로 인증 규칙 프로세스 적용 하는 방법에 대 한 자세한 내용은 클레임 발급 엔진 The 역할을 참조 하세요.  
  
### <a name="supported-claim-types"></a>지원 되는 클레임 유형  
광고 FSdefines 두 클레임 사용자가 허용 여부를 결정 하는 데 사용 하는 형식 있습니다. 이러한 클레임 유형 Uniform 리소스 식별자 \(URIs\) 사항은 다음과 같습니다.  
  
1.  **허용**: http:///\/schemas.microsoft.com\/authorization\/claims\/permit  
  
2.  **거부**: http:///\/schemas.microsoft.com\/authorization\/claims\/deny  
  
## <a name="how-to-create-this-rule"></a>이 규칙 만드는 방법  
또는 클레임 규칙 언어를 사용 하 여 두 인증 규칙을 만들 수는 **모든 사용자가 허용** 규칙 템플릿 또는 **허용 또는 거부 들어오는 요구에 따라 사용자** snap\에서 광고 FS 관리에서 템플릿 규칙 합니다. 모든 사용자가 허용 규칙 서식 구성 옵션을 제공 하지 않습니다. 그러나 거부 들어오는 클레임 규칙 템플릿을에 따라 사용자가 허용 또는 다음과 같은 구성 옵션을 제공합니다.  
  
-   클레임은 규칙 이름을 지정합니다  
  
-   수신 청구 유형  
  
-   수신 청구 값을 입력  
  
-   이 들어오는 클레임 있는 사용자에 게 액세스 권한을  
  
-   액세스를 사용자에 게가 들어오는 클레임 거부  
  
이 서식 만드는 방법에 추가 지침을 참조 [모든 사용자가 허용 하는 규칙 만들](https://technet.microsoft.com/library/ee913577.aspx) 또는 [수신 클레임에 규칙을 허용 하거나 사용자가 기반 거부 만듭니다](https://technet.microsoft.com/library/ee913594.aspx) AD FS 배포 가이드에 합니다.  
  
## <a name="using-the-claim-rule-language"></a>클레임은 규칙 언어를 사용 하 여  
클레임 클레임 값 사용자 지정 패턴와 일치 하는 경우에를 보낼 사용자 지정 규칙을 사용 해야 합니다. 자세한 내용은 참조 [사용자 지정 클레임 규칙을 사용 하는 경우](When-to-Use-a-Custom-Claim-Rule.md)합니다.  
  
### <a name="example-of-how-to-create-an-authorization-rule-based-on-multiple-claims"></a>여러 클레임에 따라 인증 규칙을 작성 하는 방법  
클레임 규칙 언어 구문을 승인할 청구를 사용할 때 클레임도 실행할 수의 사용자의 원래 클레임에 여러 클레임 있는지 여부에 따라 합니다. 다음 규칙의 사용자 그룹 편집기의 회원 이며 Windows 인증 인증 된 경우에 승인 클레임 문제:  
  
```  
[type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod",   
value == "urn:federation:authentication:windows" ]  
&& [type == "http://schemas.xmlsoap.org/claims/Group ", value == “editors”]   
=> issue(type = "http://schemas.xmlsoap.org/claims/authZ", value = "Granted");  
```  
  
### <a name="example-of-how-to-create-authorization-rules-that-will-delegate-who-can-create-or-remove-federation-server-proxy-trusts"></a>만들기 승인 하는 방법 규칙 만들거나 federation 서버 프록시 신뢰를 제거할 수 있는 위임은 하  
Federation 서비스를 사용 하려면 먼저 federation 프록시 서버를 리디렉션하여 클라이언트 요청 신뢰를 먼저 Federation 서비스와 해당 federation 서버 프록시 컴퓨터 간에 설정 해야 합니다. 프록시 신뢰 기본적으로 설정 된 경우 다음과 같은 자격 증명 중 하나에서 제공 되는 성공적으로 AD FS Federation 서버 프록시 구성을 마법사:  
  
-   프록시 보호 하는 Federation 서비스를 사용 하 여 서비스 계정,  
  
-   해당 federation 서버 농장의 모든 federation 서버에서 로컬 관리자가 그룹의 회원 하는 Active Directory 도메인 계정  
  
사용자 또는 사용자가 해당된 Federation 서비스에 대 한 프록시 신뢰를 만들 수 있는 지정 하려는 경우 다음 위임 방법 중 하나를 사용할 수 있습니다. 방법을이 목록은 위임 하는 가장 안전 및 가장 문제가 있는 방법의 ADFS 제품 팀 추천에 따라 우선 순위를입니다. 조직의 요구에 따라 이러한 방법 중 하나를 사용 해야 하는 다음과 같습니다.  
  
1.  Active Directory에 도메인 보안 그룹을 만들고 \ 각는 농장의 federation 서버에 로컬 관리자가 그룹 (예: FSProxyTrustCreators\)이이 그룹에 추가 하 고 다음이 권한을 새 그룹에 위임를 원하는 사용자 계정 추가 합니다. 이 것이 좋습니다.  
  
2.  관리자가 그룹 각 그룹에 federation 서버에 사용자의 도메인 계정을 추가 합니다.  
  
3.  몇 가지 이유로 이러한 방법 중 하나를 사용할 수 없는 경우이 위해 인증 규칙도 만들 수 있습니다. 있지만 권장 하지 않습니다 등이 규칙은 올바르게 작성 되지 경우 발생할 수 있는 문제가 없음을 때문-도메인 사용자 계정을 만들 수도 하거나 더 해당된 Federation 서비스와 관련 된 모든 federation 서버 프록시 사이의 신뢰를 제거할 수 있는 Active Directory 위임 하는 사용자 지정 인증 규칙을 사용할 수 있습니다.  
  
    방법 3을 선택 하면를 사용자 지정된 수 있도록 승인 클레임 발급 다음 규칙 구문을 사용할 수 있습니다 \ (이 경우 contoso\\frankm\)에서 하나 이상의 federation는 Federation 서비스에 프록시 서버 만들 수 있습니다. 이 규칙 Windows PowerShell 명령을 사용 하 여 적용 해야 **Set\ ADFSProperties AddProxyAuthorizationRules**합니다.  
  
    ```  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", issuer=~"^AD AUTHORITY$" value == "contoso\frankm" ] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true")  
  
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])   
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );  
    ```  
  
    나중에 사용자 프록시 신뢰를 만들 수 없으므로 되도록 사용자를 제거 하려는 경우 기본 프록시 신뢰 승인 규칙 Federation 서비스에 대 한 프록시 신뢰를 만들 수 있는 사용자에 대 한 바로 제거에 되돌릴 수 없습니다. 이 규칙 Windows PowerShell 명령을 사용 하 여 적용 해야 **Set\ ADFSProperties AddProxyAuthorizationRules**합니다.  
  
    ```  
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])   
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );  
    ```  
  
클레임은 규칙 언어를 사용 하는 방법에 대 한 자세한 내용은 참조 [주장 규칙 언어의 The 역할](The-Role-of-the-Claim-Rule-Language.md)합니다.  
  

