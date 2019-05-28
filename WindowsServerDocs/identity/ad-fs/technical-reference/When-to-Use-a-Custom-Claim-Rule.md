---
ms.assetid: 20d183f0-ef94-44bb-9dfc-ed93799dd1a6
title: 사용자 지정 클레임 규칙을 사용하는 경우
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e566de4df2895dfa2ed1104f85c1429881ff5bbf
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188292"
---
# <a name="when-to-use-a-custom-claim-rule"></a>사용자 지정 클레임 규칙을 사용하는 경우
Active Directory Federation Services에서 사용자 지정 클레임 규칙을 작성할 \(AD FS\) 클레임 발급 엔진이 프로그래밍 방식으로 생성 하는 데 사용 하는 프레임 워크인 클레임 규칙 언어를 사용 하 여 변환, 통과 및 필터링 클레임입니다. 사용자 지정 규칙을 사용하여 표준 규칙 템플릿보다 더 복잡한 논리를 포함하는 규칙을 만들 수 있습니다. 다음을 수행하려는 경우 사용자 지정 규칙을 사용하는 것이 좋습니다.  
  
-   구조적 쿼리 언어에서 추출 된 값을 기반으로 하는 클레임을 보내도록 \(SQL\) 특성 저장소입니다.  
  
-   Lightweight Directory Access Protocol에서 추출 된 값을 기반으로 하는 클레임을 보내도록 \(LDAP\) 사용자 지정 LDAP 필터를 사용 하 여 특성 저장소입니다.  
  
-   사용자 지정 특성 저장소에서 추출된 값을 기준으로 클레임을 보내려는 경우  
  
-   들어오는 클레임이 두 개 이상 있는 경우에만 클레임을 보내려는 경우  
  
-   들어오는 클레임 값이 복잡한 패턴과 일치하는 경우에만 클레임을 보내려는 경우  
  
-   들어오는 클레임 값을 복잡하게 변경하여 클레임을 보내려는 경우  
  
-   실제로 클레임을 보내지 않고 이후 규칙에서만 사용하기 위해 클레임을 만들려는 경우  
  
-   둘 이상의 들어오는 클레임 내용에서 나가는 클레임을 생성하려는 경우  
  
나가는 클레임의 클레임 값이 들어오는 클레임 값을 기반으로 해야 하지만 추가 콘텐츠도 포함해야 하는 경우에 사용자 지정 규칙을 사용할 수도 있습니다.  
  
클레임 규칙 언어는 규칙 기반입니다. 조건 부분과 실행 부분이 있습니다. 클레임 규칙 언어 구문을 사용하여 조직의 요구에 맞게 클레임을 열거, 추가, 삭제 또는 수정할 수 있습니다. 이러한 각 부분의 작동 하는 방법에 대 한 자세한 내용은 참조 하세요. [클레임 규칙 언어의 역할](The-Role-of-the-Claim-Rule-Language.md)입니다.  
  
다음 섹션에서는 클레임 규칙에 대한 기본 사항을 소개합니다. 또한 사용자 지정 클레임 규칙을 사용하는 경우에 대한 세부 정보를 제공합니다.  
  
## <a name="about-claim-rules"></a>클레임 규칙 정보  
클레임 규칙 들어오는 클레임을 사용 하는 비즈니스 논리의 인스턴스를 나타내며, 조건을 적용할 \(그런 다음 y x if\) 조건 매개 변수에 따라 나가는 클레임을 생성 하 고 있습니다.  
  
> [!IMPORTANT]  
> -   AD FS 관리 스냅인에서\-, 클레임만 클레임 규칙 템플릿을 사용 하 여 규칙을 만들 수 있습니다  
> -   클레임 규칙 프로세스 들어오는 클레임을 클레임 공급자에서 직접 들어오거나 \(Active Directory 또는 다른 페더레이션 서비스와 같은\) 또는 수용의 출력에서 클레임 공급자 트러스트에 대 한 규칙을 변환 합니다.  
> -   클레임 규칙은 지정된 규칙 집합 내의 시간 순서대로 클레임 발급 엔진에 의해 처리됩니다. 규칙에 우선 순위를 설정하여 지정된 규칙 집합 내의 이전 규칙에 의해 생성된 클레임을 더욱 구체화하거나 필터링할 수 있습니다.  
> -   클레임 규칙 템플릿에서는 항상 들어오는 클레임 유형을 지정해야 합니다. 그러나 단일 규칙을 사용하여 동일한 클레임 유형 내의 여러 클레임 값을 처리할 수 있습니다.  
  
클레임 규칙 및 클레임 규칙 집합에 대 한 정보를 자세한 참조 [규칙의 역할 클레임](The-Role-of-Claim-Rules.md)합니다. 규칙은 처리 하는 방법에 대 한 자세한 내용은 참조 [클레임 엔진의 역할](The-Role-of-the-Claims-Engine.md)합니다. 자세한 내용은 클레임 규칙 집합을 처리 하는 방법을 참조 하십시오 [클레임 파이프라인의 역할](The-Role-of-the-Claims-Pipeline.md)합니다.  
  
## <a name="how-to-create-this-rule"></a>이 규칙을 만드는 방법  
이 규칙 구문을 사용 하 여 클레임 보내기에서 작업 결과를 텍스트 상자는 클레임 규칙 언어 및 그런 다음 붙여넣기를 사용 하 여 제공 해야 하는 첫 번째 작성 하 여 사용자 지정 규칙 템플릿을 만든 클레임 공급자의 속성에 대해 tr AD FS 관리 스냅인에서 신뢰 하는 ust 또는 신뢰 당사자\-에서 합니다.  
  
이 규칙 템플릿에서는 다음 옵션을 제공합니다.  
  
-   클레임 규칙 이름 지정  
  
-   하나를 입력 하거나 이상의 선택 조건과 발급 문을 AD FS를 사용 하 여 클레임 규칙 언어  
  
이 템플릿을 사용 하 여 사용자 지정 규칙을 만들기 위한 자세한 지침을 참조 하세요 [클레임으로 보내기 규칙을 사용자 지정 규칙을 만들어](https://technet.microsoft.com/library/dd807049.aspx) AD FS 배포 가이드에서.  
  
이해를 돕기 위해 클레임 규칙 언어의 작동 방식, 이미 존재 하는 다른 규칙의 클레임 규칙 언어 구문을 스냅인에서 볼\-에서 클릭 하 여는 **규칙 언어 보기** 해당 규칙에 대 한 속성에서 탭 합니다. 이 섹션의 정보와 이 탭의 구문 정보를 사용하여 고유한 사용자 지정 규칙을 생성하는 방법을 파악할 수 있습니다.  
  
클레임 규칙 언어를 사용 하는 방법에 대 한 자세한 내용은 참조 [클레임 규칙 언어의 역할](The-Role-of-the-Claim-Rule-Language.md)합니다.  
  
## <a name="using-the-claim-rule-language"></a>클레임 규칙 언어 사용  
  
### <a name="example-how-to-combine-first-and-last-names-based-on-a-users-name-attribute-values"></a>예: 사용자의 이름 특성 값을 기반으로 하여 성과 이름을 결합하는 방법  
다음 규칙 구문은 지정된 특성 저장소에 있는 특성 값의 이름과 성을 결합합니다. 정책 엔진은 각 조건에 대한 일치 항목의 카티전 곱을 형성합니다. 예를 들어 이름 {"Frank", "Alan"}과 성 {"Miller", "Shen"}의 출력은 {"Frank Miller", "Frank Shen", "Alan Miller", "Alan Shen"입니다.  
  
```  
c1:[type == "http://exampleschema/firstname" ]  
&&  c2:[type == "http://exampleschema/lastname",]   
=> issue(type = "http://exampleschema/name", value = c1.value + “  “ + c2.value);  
```  
  
### <a name="example-how-to-issue-a-manager-claim-based-on-whether-users-have-direct-reports"></a>예: 사용자에게 부하 직원이 있는지 여부에 따라 관리자 클레임을 발급하는 방법  
다음 규칙은 사용자에게 부하 직원이 있는 경우에만 관리자 클레임을 발급합니다.  
  
```  
c:[type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name"] => add(store = "SQL Store", types = ("http://schemas.xmlsoap.org/claims/Reports"), query = "SELECT Reports FROM dbo.DirectReports WHERE UserName = {0}", param = c.value );  
count([type == “http://schemas.xmlsoap.org/claims/Reports“] ) > 0 => issue(= "http://schemas.xmlsoap.org/claims/ismanager", value = "true");  
```  
  
### <a name="example-how-to-issue-a-ppid-claim-based-on-an-ldap-attribute"></a>예: LDAP 특성을 기준으로 PPID 클레임을 발급하는 방법  
다음 규칙은 발급 Private Personal Identifier \(PPID\) 클레임 기반을 **windowsaccountname** 하 고 **originalissuer** LDAP 특성의 사용자 특성 저장소:  
  
```  
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
 => issue(store = "_OpaqueIdStore", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier"), query = "{0};{1};{2}", param = "ppid", param = c.Value, param = c.OriginalIssuer);  
```  
  
이 쿼리에 대한 사용자를 고유하게 식별하는 데 사용할 수 있는 공통 특성은 다음과 같습니다.  
  
-   **user SID**  
  
-   **windowsaccountname**  
  
-   **samaccountname**  
  

