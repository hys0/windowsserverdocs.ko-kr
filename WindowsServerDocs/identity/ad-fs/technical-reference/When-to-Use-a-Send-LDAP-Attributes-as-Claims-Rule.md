---
ms.assetid: 606f4196-b579-4806-a462-3abd4d93e87c
title: LDAP 특성을 클레임으로 보내기 규칙을 사용하는 경우
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 05a2dd88057b64675bbc3bd30724d1eda0880c44
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860664"
---
>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="when-to-use-a-send-ldap-attributes-as-claims-rule"></a>LDAP 특성을 클레임으로 보내기 규칙을 사용하는 경우
Active Directory Federation Services에서이 규칙을 사용할 수 있습니다 \(AD FS\) 실제 Lightweight Directory Access Protocol을 포함 하는 나가는 클레임을 발급 하려는 경우 \(LDAP\) 특성에 있는 값 특성 저장 하 고 클레임 유형을 각 LDAP 특성을 사용 하 여 연결 합니다. 특성 저장소에 대 한 자세한 내용은 참조 하세요. [The 특성 저장소의 역할](The-Role-of-Attribute-Stores.md)입니다.  
  
이 규칙을 사용하는 경우 다음 표에 설명된 대로 지정하는 각 LDAP 특성에 대해 규칙 논리와 일치하는 클레임을 발급합니다.  
  
|규칙 옵션|규칙 논리|  
|---------------|--------------|  
|LDAP 특성을 나가는 클레임 유형에 매핑|특성 저장소가 *지정한 특성 저장소*와 같고 LDAP 특성이 *지정한 값*과 같은 경우 LDAP 특성 값을 *지정한 나가는 클레임* 유형에 매핑하고 클레임을 발급합니다.|  
  
다음 섹션에서는 클레임 규칙에 대한 기본 사항을 소개합니다. 또한 LDAP 특성을 클레임으로 보내기 규칙을 사용하는 경우에 대해 자세하게 설명합니다.  
  
## <a name="about-claim-rules"></a>클레임 규칙 정보  
클레임 규칙은 들어오는 클레임에 조건을 적용 하는 비즈니스 논리의 인스턴스를 나타냅니다 \(다음 y x if\) 조건 매개 변수를 기반으로 하는 나가는 클레임을 생성 합니다. 다음 목록은 이 항목을 더 읽기 전에 클레임 규칙에 대해 알아야 하는 중요한 팁을 간략하게 설명합니다.  
  
-   AD FS 관리 스냅인에서\-클레임 규칙을 다시 만든 클레임 규칙 템플릿을 사용 하 여  
  
-   클레임 규칙 프로세스 들어오는 클레임을 클레임 공급자에서 직접 \(Active Directory 또는 다른 페더레이션 서비스와 같은\) 또는 수용의 출력에서 클레임 공급자 트러스트에 대 한 규칙을 변환 합니다.  
  
-   클레임 규칙은 지정된 규칙 집합 내의 시간 순서대로 클레임 발급 엔진에 의해 처리됩니다. 규칙에 우선 순위를 설정하여 지정된 규칙 집합 내의 이전 규칙에 의해 생성된 클레임을 더욱 구체화하거나 필터링할 수 있습니다.  
  
-   클레임 규칙 템플릿에서는 항상 들어오는 클레임 유형을 지정해야 합니다. 그러나 단일 규칙을 사용하여 동일한 클레임 유형 내의 여러 클레임 값을 처리할 수 있습니다.  
  
클레임 규칙 및 클레임 규칙 집합에 대 한 정보를 자세한 참조 [규칙의 역할 클레임](The-Role-of-Claim-Rules.md)합니다. 규칙은 처리 하는 방법에 대 한 자세한 내용은 참조 [클레임 엔진의 역할](The-Role-of-the-Claims-Engine.md)합니다. 자세한 내용은 클레임 규칙 집합을 처리 하는 방법을 참조 하십시오 [클레임 파이프라인의 역할](The-Role-of-the-Claims-Pipeline.md)합니다.  
  
## <a name="mapping-of-ldap-attributes-to-outgoing-claim-types"></a>LDAP 특성을 나가는 클레임 유형에 매핑  
클레임 규칙 템플릿으로 보내기 LDAP 특성을 사용 하는 경우 Active Directory 또는 Active Directory Domain Services와 같은 LDAP 특성 저장소에서 특성을 선택할 수 있습니다 \(AD DS\) 해당 값을 신뢰 당사자에 대 한 클레임으로 보낼 . 그러면 정의하는 특정 저장소의 특정 LDAP 특성을 권한 부여에 대해 사용할 수 있는 나가는 클레임 집합에 기본적으로 매핑합니다.  
  
이 템플릿을 사용하면 단일 규칙에서 여러 클레임으로 보내는 여러 특성을 추가할 수 있습니다. 예를 들어 이 규칙 템플릿을 사용하여 **company** 및 **department** Active Directory 특성에서 인증된 사용자에 대한 특성 값을 조회하는 규칙을 만든 다음 두 개의 서로 다른 나가는 클레임으로 이 규칙을 보냅니다.  
  
또한 이 규칙을 사용하여 모든 사용자 그룹의 구성원을 보낼 수도 있습니다. 개별 그룹 구성원만 보내려는 경우 그룹 구성원을 클레임으로 보내기 규칙 템플릿을 사용합니다. 자세한 내용은 [When to Use a Send Group Membership as a Claim Rule](When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)를 참조하세요.  
  
## <a name="how-to-create-this-rule"></a>이 규칙을 만드는 방법  
클레임 규칙 언어 중 하나를 사용 하 여이 규칙을 만들 수도 있고 AD FS 관리에서 클레임 규칙 템플릿으로 보내기 LDAP 특성을 사용 하 여 맞춤\-에서 합니다. 이 규칙 템플릿은 다음과 같은 구성 옵션을 제공합니다.  
  
-   클레임 규칙 이름 지정  
  
-   LDAP 특성을 추출할 특성 저장소를 선택합니다.  
  
-   LDAP 특성을 나가는 클레임 유형에 매핑  
  
이 규칙을 만드는 방법에 대 한 자세한 내용은 참조 하세요. [LDAP 특성을 클레임으로 보내기 규칙을 만들어](https://technet.microsoft.com/library/dd807115.aspx)합니다.  
  
## <a name="using-the-claim-rule-language"></a>클레임 규칙 언어 사용  
하는 경우 Active Directory, AD DS 또는 Active Directory Lightweight Directory Services 쿼리 \(AD LDS\) 이외의 LDAP 특성에 대해 비교 해야 **samAccountname**, 사용자 지정 규칙을 대신 사용 해야 합니다. 입력 집합에 Windows 계정 이름 클레임이 없는 경우 사용자 지정 규칙을 사용하여 AD DS 또는 AD LDS를 쿼리하기 위해 사용할 클레임을 지정해야 합니다.  
  
다음 예를 통해 클레임 규칙 언어를 통해 사용자 지정 규칙을 구성하여 특성 저장소에서 데이터를 쿼리하고 추출할 수 있는 다양한 방식 중 몇 가지를 이해할 수 있습니다.  
  
### <a name="example-how-to-query-an-adlds-attribute-store-and-return-a-specified-value"></a>예: AD LDS 특성 저장소를 쿼리하고 지정한 값을 반환하는 방법  
매개 변수는 세미콜론으로 구분되어야 합니다. 첫 번째 매개 변수는 LDAP 필터입니다. 후속 매개 변수는 일치하는 개체에서 반환할 특성입니다.  
  
다음 예제에서는 사용 하 여 사용자를 조회 하는 방법을 보여 줍니다 합니다 **sAMAccountName** 특성 및 e 발급\-메일 주소 클레임을 사용자의 메일 특성의 값을 사용 하 여:  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"));  
  
```  
  
다음 예는 **mail** 특성으로 사용자를 조회하고 사용자의 **title** 및 **displayname** 특성 값을 사용하여 제목 및 표시 이름 클레임을 발급하는 방법을 보여 줍니다.  
  
```  
c:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress ", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "mail={0};title;displayname", param = c.Value);  
```  
  
다음 예는 메일 및 제목으로 사용자를 조회하고 사용자의 **displayname** 특성을 사용하여 표시 이름 클레임을 발급하는 방법을 보여 줍니다.  
  
```  
c1:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"] && c2:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "(&(mail={0})(title={1}));displayname", param = c1.Value, param = c2.Value);  
```  
  
### <a name="example-how-to-query-an-activedirectory-attribute-store-and-return-a-specified-value"></a>예: Active Directory 특성 저장소를 쿼리하고 지정한 값을 반환하는 방법  
Active Directory 쿼리를 사용자의 이름을 포함 해야 합니다 \(도메인 이름의\) 쿼리로 마지막 매개 변수는 Active Directory 특성을 저장할 수 올바른 도메인입니다. 그렇지 않은 경우 동일한 구문이 지원됩니다.  
  
다음 예는 도메인에서 **sAMAccountName** 특성으로 사용자를 조회한 다음 **mail** 특성을 반환하는 방법을 보여 줍니다.  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail;{1}", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"), param = c.Value);  
```  
  
### <a name="example-how-to-query-an-activedirectory-attribute-store-based-on-the-value-of-an-incoming-claim"></a>예: 들어오는 클레임 값에 따라 Active Directory 특성 저장소를 쿼리하는 방법  
  
```  
c:[Type == "http://test/name"]  
  
   => issue(store = "Enterprise AD Attribute Store",  
  
         types = ("http://test/email"),  
  
         query = ";mail;{0}",  
  
         param = c.Value)  
  
```  
  
앞의 쿼리는 다음 세 부분으로 구성됩니다.  
  
-   LDAP 필터 - 쿼리의 이 부분을 지정하여 특성을 쿼리하려는 개체를 검색합니다. 유효한 LDAP 쿼리에 대한 일반 정보는 RFC 2254를 참조하세요. Active Directory 특성 저장소를 쿼리 하는 samAccountName LDAP 필터를 지정 하지 않으면 시점과\= {0} 쿼리가 가정 되 고 Active Directory 특성 저장소 에대한값을제공할수있는매개변수가필요{0}. 그렇지 않은 경우 쿼리에서 오류가 발생합니다. Active Directory 이외의 LDAP 특성 저장소의 경우 쿼리의 LDAP 필터 부분을 생략할 수 없습니다. 그렇지 않으면 쿼리에서 오류가 발생합니다.  
  
-   특성 사양-쿼리의이 두 번째 부분에서 특성을 지정 하면 \(는 쉼표\-구분 된 여러 특성 값을 사용 하는 경우\) 필터링된 된 개체에서 원하는 합니다. 지정하는 특성 수는 쿼리에서 정의하는 클레임 유형 수와 일치해야 합니다.  
  
-   Active Directory 도메인 - 특성 저장소가 Active Directory인 경우에만 쿼리의 마지막 부분을 지정합니다(다른  \(특성 저장소를 쿼리할 경우 필요 하지 않습니다.\) 쿼리의이 부분은 양식 도메인 사용자 계정을 지정 하는\\이름입니다. Active Directory 특성 저장소는 도메인 부분을 사용하여 적절한 도메인 컨트롤러를 결정하고 쿼리를 연결하고 실행하며 특성을 요청합니다.  
  
### <a name="example-how-to-use-two-custom-rules-to-extract-the-manager-e-mail-from-an-attribute-in-activedirectory"></a>예: 두 개의 사용자 지정 규칙을 사용 하 여 e 관리자를 추출 하는 방법을\-Active Directory의 특성에서 메일  
다음 두 가지 사용자 지정 규칙은 아래에 나와 있는 순서 대로 함께 사용 하는 경우에 대 한 Active Directory를 쿼리 합니다 **manager** 사용자 계정의 특성 \(Rule 1\) 다음 해당 특성을 사용 하 여 사용자를 쿼리하려면 에 대 한 관리자의 계정 합니다 **메일** 특성 \(Rule 2\)합니다. 마지막으로 **mail** 특성이 "ManagerEmail" 클레임으로 발급됩니다. 요약 하면 규칙 1을 Active Directory 쿼리 및 다음 e 관리자를 추출 하는 규칙 2에 쿼리의 결과 전달\-메일 값입니다.  
  
예를 들어, 이러한 규칙 실행이 완료 되 면 클레임이 발급 됩니다 관리자의 전자를 포함 하는\-메일 corp.fabrikam.com 도메인의 사용자에 대 한 주소입니다.  
  
**규칙 1**  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
=> add(store = "Active Directory", types = ("http://schemas.xmlsoap.org/claims/ManagerDistinguishedName"), query = "sAMAccountName=  
{0};mail,userPrincipalName,extensionAttribute5,manager,department,extensionAttribute2,cn;{1}", param = regexreplace(c.Value, "(?  
<domain>[^\\]+)\\(?<user>.+)", "${user}"), param = c.Value);  
```  
  
**규칙 2**  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
&& c1:[Type == "http://schemas.xmlsoap.org/claims/ManagerDistinguishedName"]  
=> issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/claims/ManagerEmail"), query = "distinguishedName={0};mail;{1}", param = c1.Value,   
param = regexreplace(c1.Value, ".*DC=(?<domain>.+),DC=corp,DC=fabrikam,DC=com", "${domain}\username"));  
```  
  
> [!NOTE]  
> 이러한 규칙은 사용자의 관리자가 사용자와 동일한 도메인 하는 경우에 작동 \(이 예에서는 corp.fabrikam.com\)합니다.  
  
## <a name="additional-references"></a>추가 참조  
[클레임으로 LDAP 특성을 보내도록 규칙 만들기](https://technet.microsoft.com/library/dd807115.aspx)  
  

