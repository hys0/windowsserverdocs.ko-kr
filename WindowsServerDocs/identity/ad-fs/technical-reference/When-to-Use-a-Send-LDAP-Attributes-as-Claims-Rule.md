---
ms.assetid: 606f4196-b579-4806-a462-3abd4d93e87c
title: "보내기 LDAP 특성 클레임 일반적으로 사용 하는 경우"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 05a2dd88057b64675bbc3bd30724d1eda0880c44
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="when-to-use-a-send-ldap-attributes-as-claims-rule"></a>보내기 LDAP 특성 클레임 일반적으로 사용 하는 경우
실제 경량 디렉터리 Access Protocol \(LDAP\) 특성 값 특성 저장소에 다음 청구 형식을 각 LDAP 특성와 연결을 포함 하는 보내는 클레임 실행 하려는 경우이 규칙 Active Directory Federation Services \(AD FS\)에서 사용할 수 있습니다. 특성 스토어에 대 한 자세한 내용은 참조 [The 역할의 특성을 저장](The-Role-of-Attribute-Stores.md)합니다.  
  
이 규칙을 사용 하는 경우 각 LDAP 특성 클레임 지정 하는 발생 하 고 다음 표에 설명 된 대로 규칙 논리 일치 하는 합니다.  
  
|규칙 옵션|규칙 논리|  
|---------------|--------------|  
|LDAP 특성을 보내는 클레임 유형 매핑|특성 스토어가 인 경우 *지정 된 특성 스토어* LDAP 특성 고 *값을 지정*, LDAP 특성 값을 다음 지도 *지정된 보내는 클레임* 입력 한 청구 발생 합니다.|  
  
다음 섹션에서는 주장 규칙에 대 한 기본 소개 합니다. 또한 보내기 LDAP 특성 클레임 일반적으로 사용 하는 경우에 대 한 세부 정보 제공 합니다.  
  
## <a name="about-claim-rules"></a>클레임은 규칙에 대 한  
클레임은 규칙 비즈니스 논리를 수신 클레임, 조건이 적용 됩니다 인스턴스를 나타냅니다 \ (경우 다음 y\ x) 조건에 따라 보내는 클레임은 생성 하 고 있습니다. 다음 목록에 대해 알아야 하는 팁 더 읽기 전에 규칙 주장 중요 한 개요가이 항목에서:  
  
-   Snap\에서 광고 FS 관리에 클레임 규칙 만들 수만 클레임 규칙 템플릿을 사용 하 여  
  
-   클레임 규칙 프로세스 들어오는 주장 클레임 공급자에서 직접 \ (Active Directory Federation Service\ 다른 등) 또는 수용 출력에서 변형 클레임 공급자 보안에 대 한 규칙 합니다.  
  
-   클레임은 규칙 해당된 규칙 설정 내에서 시간 순서로 클레임 발급 엔진에서 처리 됩니다. 규칙의 우선 순위를 설정 하 여 조정 해가면서 하거나 이전 규칙 해당된 규칙 설정 내에서 생성 되는 클레임 필터링 더 있습니다.  
  
-   청구 규칙 템플릿 항상 해야 하는 수신 클레임 종류를 지정할 수 있습니다. 그러나 규칙 하나를 사용 하 여 동일한 클레임 종류 여러 클레임 값을 처리할 수 있습니다.  
  
자세한 청구 규칙 및 청구 규칙 집합에 대 한 정보를 참조 [주장 규칙의 역할은](The-Role-of-Claim-Rules.md)합니다. 규칙은 처리 하는 방법에 대 한 자세한 내용은 참조 [클레임 엔진 The 역할](The-Role-of-the-Claims-Engine.md)합니다. 자세한 내용은 클레임 규칙 집합 처리 하는 방법을 참조 하세요. [클레임 파이프라인 The 역할](The-Role-of-the-Claims-Pipeline.md)합니다.  
  
## <a name="mapping-of-ldap-attributes-to-outgoing-claim-types"></a>LDAP 특성을 보내는 클레임 유형 매핑  
LDAP 보내기 특성 클레임 규칙 템플릿으로 사용 하면 해당 값 클레임 당사자에 파일로 보낼 Active Directory 또는 Active Directory 도메인 서비스 \(AD DS\) 등 LDAP 특성 스토어에서 특성을 선택할 수 있습니다. 이 기본적으로 지도 인증을 위해 사용할 수 있는 보내는 클레임 집합으로 정의 하는 특성 스토어에서 특정 LDAP 특성 합니다.  
  
이 서식 파일을 사용 하 여 여러 클레임으로 보낼, 여러 특성을 하나의 규칙에서 추가할 수 있습니다. 이 규칙 템플릿을 사용 하 여 규칙은 사용자가 인증된에 대 한 값 특성을 우러러 보세요을 만들 수 예를 들어 있는 **회사** 및 **부서** Active Directory 특성을 다음 두 가지 보내는 클레임으로 이러한 값을 보냅니다.  
  
또한이 규칙 모든 사용자의 그룹 구성원 보내려면 사용할 수 있습니다. 개별 그룹 구성원만 보내려는 경우 클레임 규칙 템플릿으로 보내기 그룹 구성원을 사용 합니다. 자세한 내용은 참조 [보내기 그룹 구성원 클레임 일반적으로 사용 하는 경우](When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)합니다.  
  
## <a name="how-to-create-this-rule"></a>이 규칙 만드는 방법  
이 규칙을 클레임 규칙 언어 중 하나를 사용 하 여 만들 하거나 규칙 snap\에서 광고 FS 관리에서 템플릿 클레임으로 보내기 LDAP 특성을 사용 하 여 수 있습니다. 이 규칙 템플릿을 다음과 같은 구성 옵션을 제공합니다.  
  
-   클레임은 규칙 이름을 지정합니다  
  
-   LDAP 특성 압축을 특성 스토어를 선택 합니다.  
  
-   LDAP 특성을 보내는 클레임 유형 매핑  
  
이 규칙 만드는 방법에 대 한 자세한 내용은 참조 [규칙 클레임으로 전송 LDAP 특성을 만들어](https://technet.microsoft.com/library/dd807115.aspx)합니다.  
  
## <a name="using-the-claim-rule-language"></a>클레임은 규칙 언어를 사용 하 여  
쿼리 \(AD LDS\) Active Directory, 광고 DS 또는 Active Directory 경량 디렉터리 서비스를 이외의 LDAP 특성와 비교 해야 하는 경우 **samAccountname**를 사용자 지정 규칙을 대신 사용 해야 합니다. 입력된 설정에 없는 계정 이름 Windows 클레임 경우 광고 DS 또는 광고 LDS 쿼리를 사용 하 여 클레임 지정 하려면 사용자 지정 규칙을도 사용 해야 합니다.  
  
다음은 일부의 특성 스토어에서 압축 풀기 및 쿼리 데이터를 클레임 규칙 언어를 사용 하 여 사용자 지정 규칙 생성할 수 다양 한 방법을 이해를 돕는 제공 됩니다.  
  
### <a name="example-how-to-query-an-ad-lds-attribute-store-and-return-a-specified-value"></a>예: AD LDS 특성 저장소 쿼리 고 지정된 값을 반환 하는 방법  
매개는 세미콜론 하 여 구분 합니다. 첫 번째 LDAP 필터입니다. 후속 매개 특성 일치 하는 모든 개체를 반환 하는 합니다.  
  
다음 예제으로 사용자를 검색 하는 방법을 고 **sAMAccountName** 특성 하 고 사용 하 여 사용자의 메일 특성 값 전자 e\ 메일 주소 클레임 발급:  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"));  
  
```  
  
다음 예제으로 사용자를 검색 하는 방법을 고 **메일** 특성 하 고 사용 하 여 사용자의 값 제목 및 표시 이름을 클레임 발급 **제목** 및 **표시 이름** 특성:  
  
```  
c:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress ", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "mail={0};title;displayname", param = c.Value);  
```  
  
제목 및 메일에서 사용자를 검색 한 다음 사용 하 여 사용자의 표시 이름을 클레임 발행 하는 방법을 보여 주는 다음 예제 **표시 이름** 특성:  
  
```  
c1:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"] && c2:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "(&(mail={0})(title={1}));displayname", param = c1.Value, param = c2.Value);  
```  
  
### <a name="example-how-to-query-an-active-directory-attribute-store-and-return-a-specified-value"></a>예: 된 Active Directory 특성 저장소 쿼리 고 지정된 값을 반환 하는 방법  
Active Directory 쿼리 사용자의 이름을 포함 해야 \ (와 도메인 name\)을 최종 매개 Active Directory 특성 저장할 수 있도록 수 쿼리 올바른 도메인. 그렇지 않은 경우 동일한 구문을 지원 됩니다.  
  
다음 예제으로 사용자를 검색 하는 방법을 고 **sAMAccountName** 자신의 도메인에 있는 특성 있다가 **메일** 특성:  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail;{1}", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"), param = c.Value);  
```  
  
### <a name="example-how-to-query-an-active-directory-attribute-store-based-on-the-value-of-an-incoming-claim"></a>예: 된 Active Directory 특성 저장소 수신 클레임 값에 따라 쿼리 하는 방법  
  
```  
c:[Type == "http://test/name"]  
  
   => issue(store = "Enterprise AD Attribute Store",  
  
         types = ("http://test/email"),  
  
         query = ";mail;{0}",  
  
         param = c.Value)  
  
```  
  
이전 쿼리 다음 세 가지 부분으로 구성 됩니다.  
  
-   LDAP 필터-특성을 쿼리 하려는 개체를 검색할 쿼리의이 부분을 지정 합니다. 유효한 LDAP 쿼리에 대 한 일반 정보 RFC 2254 참조 합니다. Active Directory 특성 스토어 쿼리 하는 시간과 samAccountName\ LDAP 필터를 지정 하지 않으면 {0} = 쿼리 간주 되 고 Active Directory 특성 스토어 매개 {0}에 대 한 값 피드 수 있는 것으로 예상 합니다. 그렇지 않으면 쿼리 오류가 발생 합니다. Active Directory 이외의 LDAP 특성 스토어에 대 한 쿼리 LDAP 필터 일부 생략 수 없는 또는 쿼리 오류가 발생 합니다.  
  
-   특성 사양-특성 뒷부분 쿼리에서에서 지정 \ (되는 comma\ 구분 여러 특성 values\ 사용 하는 경우) 필터링된 개체 아웃 원하는 합니다. 사용자가 지정 된 특성 수가 쿼리에 정의 클레임 형식의 수를 일치 해야 합니다.  
  
-   Active Directory 도메인-있을 때만 특성 스토어 Active Directory 쿼리의 마지막 부분을 지정 합니다. \ (쿼리 다른 특성 저장소. 경우 필요 하지 않습니다 \) 쿼리의이 부분을 사용 하 여 양식 domain\\name의 사용자 계정을 지정할 수 있습니다. Active Directory 특성 스토어 도메인 일부를 사용 하 여 해당 도메인 컨트롤러에 연결 하 여 쿼리를 실행할 특성 요청 결정 합니다.  
  
### <a name="example-how-to-use-two-custom-rules-to-extract-the-manager-e-mail-from-an-attribute-in-active-directory"></a>예: 특성 Active Directory에에서 관리자 e\ 메일을 추출 하 사용자 지정 규칙 두 개를 사용 하는 방법  
다음 두 가지 지정 규칙을 아래 나와 있는 순서 대로 함께 사용 하면에 대 한 Active Directory 쿼리는 **관리자** 사용자의 계정 \(Rule 1\) 특성과를 사용 하 여 해당 특성 쿼리 관리자의 사용자 계정에서 **메일** \(Rule 2\) 특성 합니다. 마지막으로,는 **메일** 특성 "ManagerEmail" 주장으로 실행 됩니다. 즉,에서 규칙 1 Active Directory 쿼리을 다음 관리자를 추출 하 규칙 2 e\ 메일 값 결과를 전달 합니다.  
  
예를 들어,을 실행 중이이 규칙 마치면 클레임은 corp.fabrikam.com 도메인에 있는 사용자에 대해 관리자의 e\ 메일 주소를 포함 하는 발급 됩니다.  
  
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
> 이 규칙은 사용자의 관리자가 사용자와 같은 도메인에 있는 경우에 작동 \ (이 example\에 corp.fabrikam.com).  
  
## <a name="additional-references"></a>추가 참조  
[LDAP 특성 클레임 파일로 보낼 규칙 만들기](https://technet.microsoft.com/library/dd807115.aspx)  
  

