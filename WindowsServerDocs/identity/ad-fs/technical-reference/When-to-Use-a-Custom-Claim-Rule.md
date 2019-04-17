---
ms.assetid: 20d183f0-ef94-44bb-9dfc-ed93799dd1a6
title: "사용자 지정 클레임 규칙을 사용 하는 경우"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f5398f0b10d9e62548145fdde0354a3d047eb0ae
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="when-to-use-a-custom-claim-rule"></a>사용자 지정 클레임 규칙을 사용 하는 경우
사용자 지정 클레임 규칙 Active Directory Federation Services \(AD FS\) 클레임 발급 엔진 프로그래밍 방식으로, 변환를 생성 통과 하는 데 사용 된 프레임 워크 클레임 규칙 언어를 사용 하 여 작성 및 클레임 필터링 합니다. 사용자 지정 규칙을 사용 하 여 규칙 표준 규칙 템플릿 보다 더 복잡 한 논리를 만들 수 있습니다. 하려는 경우 사용자 지정 규칙을 사용 하는 것이 좋습니다.  
  
-   클레임 구조적 쿼리 언어 \(SQL\) 특성 스토어에서 추출 된 값에 따라 전송 합니다.  
  
-   사용자 지정 LDAP 필터를 사용 하 여 간단 디렉터리 Access Protocol \(LDAP\) 특성 스토어에서 추출 된 값에 따라 클레임 전송 합니다.  
  
-   사용자 지정 된 특성 스토어에서 추출 된 값에 따라 클레임 전송 합니다.  
  
-   클레임 수신 클레임 두 개 이상 있는 경우에 전송 됩니다.  
  
-   클레임 들어오는 맞는 값 복잡 한 패턴 주장 하는 경우에 전송 됩니다.  
  
-   클레임 값을 복잡 한 변경 내용으로 클레임 들어오는에 전송 합니다.  
  
-   실제로 클레임을 보내지 않고 이후 규칙에만 사용에 대 한 주장을 만듭니다.  
  
-   둘 이상의 들어오는 클레임 콘텐츠에서 보내는 클레임을 생성 합니다.  
  
또한 보내는 클레임 클레임 값 들어오는 클레임 값 기반으로 해야 하지만 추가 콘텐츠도 포함 되어 있어야 하는 경우 사용자 지정 규칙을 사용할 수 있습니다.  
  
클레임 규칙 언어 규칙 기반입니다. 가 조건 부분과 실행 부분을 차지 합니다. 클레임 규칙 언어 구문을 열거할 추가, 삭제, 사용 하거나 조직에서 요구 하는 클레임 수정할 수 있습니다. 작동 이러한의 각 부분 방법에 대 한 자세한 내용은 참조 [클레임 규칙 언어의 The 역할](The-Role-of-the-Claim-Rule-Language.md)합니다.  
  
다음 섹션에서는 주장 규칙에 대 한 기본 소개 합니다. 또한 사용자 지정 클레임 규칙을 사용 하는 경우에 대 한 세부 정보 제공 합니다.  
  
## <a name="about-claim-rules"></a>클레임은 규칙에 대 한  
클레임은 규칙 수신 클레임을 사용 하는 비즈니스 논리 인스턴스를 나타냅니다, 조건이 적용 \ (경우 다음 y\ x) 조건에 따라 보내는 클레임은 생성 하 고 있습니다.  
  
> [!IMPORTANT]  
> -   청구 규칙 템플릿만 사용 규칙에 만들 수 주장 snap\에서 광고 FS 관리  
> -   클레임 규칙 프로세스 들어오는 주장 클레임 공급자에서 직접 \ (Active Directory Federation Service\ 다른 등) 또는 수용 출력에서 변형 클레임 공급자 보안에 대 한 규칙 합니다.  
> -   클레임은 규칙 해당된 규칙 설정 내에서 시간 순서로 클레임 발급 엔진에서 처리 됩니다. 규칙에 우선 순위를 설정 하 여 조정 해가면서 하거나 이전 규칙 해당된 규칙 설정 내에서 생성 되는 클레임 필터링 더 있습니다.  
> -   청구 규칙 템플릿 반드시 수신 클레임 유형 지정할 수 있습니다. 그러나 단일 규칙을 사용 하 여 동일한 클레임 종류 여러 클레임 값을 처리할 수 있습니다.  
  
자세한 청구 규칙 및 청구 규칙 집합에 대 한 정보를 참조 [주장 규칙의 역할은](The-Role-of-Claim-Rules.md)합니다. 규칙은 처리 하는 방법에 대 한 자세한 내용은 참조 [클레임 엔진 The 역할](The-Role-of-the-Claims-Engine.md)합니다. 자세한 내용은 클레임 규칙 집합 처리 하는 방법을 참조 하세요. [클레임 파이프라인 The 역할](The-Role-of-the-Claims-Pipeline.md)합니다.  
  
## <a name="how-to-create-this-rule"></a>이 규칙 만드는 방법  
첫 번째는 클레임 규칙 언어를 사용 하 여 작업을 위해 필요한 다음 신뢰 클레임 사용 속성 클레임 공급자의 사용자 지정 규칙 서식 보내기에서 제공 되는 텍스트 상자에 결과 붙여넣어 하거나 snap\에서 광고 FS 관리에서 당사자를 신뢰 하는 구문을 작성 하 여이 규칙을 만듭니다.  
  
이 규칙 템플릿을 다음과 같은 옵션을 제공합니다.  
  
-   클레임은 규칙 이름을 지정합니다  
  
-   암호를 입력 하거나 더 선택적 조건 및 사용 하 여 Adfs에서 발급 문을 주장 규칙 언어  
  
만들기 사용자 지정이 템플릿을 사용 규칙에 대 한 자세한 내용은 참조 [보내기 클레임 사용 규칙을 사용자 지정 규칙 만들](https://technet.microsoft.com/library/dd807049.aspx) AD FS 배포 가이드에 있습니다.  
  
더 잘 이해 클레임 규칙 언어의 작동 방식을,에 대 한 이미 있는 다른 규칙 클레임 규칙 언어 구문을 snap\ 기능에서 클릭 하 여 보려면는 **보기 규칙 언어** 속성 해당 규칙을 탭 합니다. 이 탭이 섹션의 정보와 구문 정보를 사용 하 여 사용자 지정 규칙 생성 하는 방법에 대 한 의견을 제공할 수 있습니다.  
  
클레임은 규칙 언어를 사용 하는 방법에 대 한 자세한 내용은 참조 [주장 규칙 언어의 The 역할](The-Role-of-the-Claim-Rule-Language.md)합니다.  
  
## <a name="using-the-claim-rule-language"></a>클레임은 규칙 언어를 사용 하 여  
  
### <a name="example-how-to-combine-first-and-last-names-based-on-a-users-name-attribute-values"></a>예: 사용자의 이름 특성 값에 따라 성과 이름 결합 하는 방법  
다음 규칙 구문을 성과 이름 지정 된 특성 스토어의 특성 값에서 결합 되어 있습니다. 정책 엔진 카티션 제품에 대 한 각 조건 일치 항목을 구성합니다. 예를 들어 이름 {"프랭크", "앨런"} 및 성을 {"Miller", "사람"}에 대 한 출력 {"프랭크 Miller", "프랭크 사람", "앨런 Miller", "앨런 사람"}는 다음과 같습니다.  
  
```  
c1:[type == "http://exampleschema/firstname" ]  
&&  c2:[type == "http://exampleschema/lastname",]   
=> issue(type = "http://exampleschema/name", value = c1.value + “  “ + c2.value);  
```  
  
### <a name="example-how-to-issue-a-manager-claim-based-on-whether-users-have-direct-reports"></a>예: 사용자가 직접 보고서 있는지 여부에 따라 관리자 클레임 실행 하는 방법  
다음 규칙 경우에 사용자가 직접 보고서 관리자 클레임 문제:  
  
```  
c:[type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name"] => add(store = "SQL Store", types = ("http://schemas.xmlsoap.org/claims/Reports"), query = "SELECT Reports FROM dbo.DirectReports WHERE UserName = {0}", param = c.value );  
count([type == “http://schemas.xmlsoap.org/claims/Reports“] ) > 0 => issue(= "http://schemas.xmlsoap.org/claims/ismanager", value = "true");  
```  
  
### <a name="example-how-to-issue-a-ppid-claim-based-on-an-ldap-attribute"></a>예: 기반 LDAP 특성으로 PPID 클레임 실행 하는 방법  
다음 규칙의 경우에 따라 개인 개인 식별자 \(PPID\) 클레임 문제는 **windowsaccountname** 및 **originalissuer** LDAP 특성 스토어에서 사용자의 특성 다음과 같습니다.  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
 => issue(store = "_OpaqueIdStore", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier"), query = "{0};{1};{2}", param = "ppid", param = c.Value, param = c.OriginalIssuer);  
```  
  
사용자에 게이 쿼리 고유 하 게 식별 하는 데 사용 될 수 있는 일반 특성은 다음과 같습니다.  
  
-   **사용자 SID**  
  
-   **windowsaccountname**  
  
-   **samaccountname**  
  

