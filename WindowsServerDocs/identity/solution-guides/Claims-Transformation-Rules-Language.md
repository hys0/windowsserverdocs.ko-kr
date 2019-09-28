---
ms.assetid: e831f781-3c45-4d44-b411-160d121d1324
title: 클레임 변환 규칙 언어
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 200d592bc68562856bbdee623e70d73d41457c15
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357585"
---
# <a name="claims-transformation-rules-language"></a>클레임 변환 규칙 언어

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포리스트 간 클레임 변환 기능을 사용 하면 포리스트 간 트러스트에서 클레임 변환 정책을 설정 하 여 동적 Access Control에 대 한 클레임을 포리스트 경계에서 브리지로 연결할 수 있습니다. 모든 정책의 기본 구성 요소는 클레임 변환 규칙 언어로 작성 된 규칙입니다. 이 항목에서는이 언어에 대해 자세히 설명 하 고 클레임 변환 규칙 작성에 대 한 지침을 제공 합니다.  
  
포리스트 간 트러스트의 변환 정책에 대 한 Windows PowerShell cmdlet에는 일반적인 시나리오에 필요한 간단한 정책을 설정 하는 옵션이 있습니다. 이러한 cmdlet은 사용자 입력을 클레임 변환 규칙 언어의 정책 및 규칙으로 변환한 다음 지정 된 형식으로 Active Directory에 저장 합니다. 클레임 변환에 대 한 cmdlet에 대 한 자세한 내용은 [AD DS cmdlet For Dynamic Access Control](https://go.microsoft.com/fwlink/?LinkId=243150)을 참조 하세요.  
  
Active Directory 포리스트에 있는 포리스트 간 트러스트에 적용 되는 요구 사항 및 클레임 구성에 따라 클레임 변환 정책은 Windows PowerShell cmdlet이 활성화 된 정책 보다 더 복잡 해야 할 수 있습니다. 디렉터리나. 이러한 정책을 효과적으로 작성 하려면 클레임 변환 규칙 언어 구문 및 의미 체계를 이해 하는 것이 중요 합니다. Active Directory의이 클레임 변환 규칙 언어 ("언어")는 비슷한 목적을 위해 [Active Directory Federation Services](https://go.microsoft.com/fwlink/?LinkId=243982) 에서 사용 하는 언어의 하위 집합이 며 구문과 의미 체계가 매우 유사 합니다. 그러나 허용 되는 작업이 적고 언어의 Active Directory 버전에 추가 구문 제한이 적용 됩니다.  
  
이 항목에서는 Active Directory에서 클레임 변환 규칙 언어의 구문 및 의미 체계와 정책을 제작할 때 수행할 사항을 간략하게 설명 합니다. 이 클래스는 사용자가 시작 하는 데 사용할 수 있는 몇 가지 예제 규칙 집합을 제공 하 고, 잘못 된 구문과 생성 되는 메시지의 예를 제공 하 여 규칙을 작성할 때 오류 메시지를 쉽게 해독할 수 있도록 합니다.  
  
## <a name="tools-for-authoring-claims-transformation-policies"></a>클레임 변환 정책을 작성 하기 위한 도구  
**Active Directory에 대 한 Windows PowerShell cmdlet**: 클레임 변환 정책을 작성 하 고 설정 하는 데 권장 되는 방법입니다. 이러한 cmdlet은 간단한 정책에 대 한 스위치를 제공 하 고 더 복잡 한 정책에 대해 설정 된 규칙을 확인 합니다.  
  
**LDAP**: 클레임 변환 정책은 LDAP (Lightweight Directory Access Protocol)를 통해 Active Directory에서 편집할 수 있습니다. 그러나 정책에 복잡 한 구성 요소가 여러 개 있으므로 사용 하는 도구에서 Active Directory 정책의 유효성을 검사 하지 못할 수 있습니다. 이후에 문제를 진단 하는 데 상당한 시간이 걸릴 수 있습니다.  
  
## <a name="active-directory-claims-transformation-rules-language"></a>Active Directory 클레임 변환 규칙 언어  
  
### <a name="syntax-overview"></a>구문 개요  
다음은 해당 언어의 구문 및 의미에 대 한 간략 한 개요입니다.  
  
-   클레임 변환 규칙 집합은 0 개 이상의 규칙으로 구성 됩니다. 각 규칙에는 두 가지 활성 부분이 있습니다. **조건 목록** 및 **규칙 동작**을 선택 합니다. **조건 선택 목록이** TRUE로 평가 되 면 해당 규칙 동작이 실행 됩니다.  
  
-   **조건 목록** 에서 **select 조건이**0 개 이상 있습니다. Select **조건 목록을** true로 평가 하려면 모든 **select 조건이** true로 평가 되어야 합니다.  
  
-   각 **Select 조건** 에는 0 개 이상의 **일치 조건**집합이 있습니다. Select 조건을 TRUE로 평가 하려면 일치 하는 모든 **조건이** true로 평가 되어야 합니다. 이러한 모든 조건은 단일 클레임에 대해 평가 됩니다. **선택 조건과** 일치 하는 클레임은 **식별자** 로 태그를 지정 하 고 **규칙 동작**에서 참조할 수 있습니다.  
  
-   각 **일치 조건은** 다른 **조건 연산자** 및 **문자열 리터럴을**사용 하 여 클레임의 **형식** 또는 **값** 또는 **ValueType** 과 일치 하는 조건을 지정 합니다.  
  
    -   **값**에 **일치 조건을** 지정 하는 경우 특정 **ValueType** 에 대해 일치 하는 **조건만** 지정 해야 하며 그 반대의 경우도 마찬가지입니다. 이러한 조건은 구문에서 서로 옆에 있어야 합니다.  
  
    -   **Valuetype** 일치 조건은 특정 **valuetype** 리터럴을 사용 해야 합니다.  
  
-   **규칙 작업** 은 **식별자** 로 태그가 지정 된 클레임 하나를 복사 하거나 식별자 및/또는 지정 된 문자열 리터럴로 태그가 지정 된 클레임을 기반으로 한 클레임을 발급할 수 있습니다.  
  
**예제 규칙**  
  
이 예에서는 두 포리스트 간에 클레임 유형을 변환 하는 데 사용할 수 있는 규칙을 보여 줍니다. 동일한 클레임 ValueTypes을 사용 하 고이 유형의 클레임 값에 대해 동일한 해석을 사용 합니다. 규칙에는 문자열 리터럴과 일치 하는 클레임 참조를 사용 하는 하나의 일치 조건 및 Issue 문이 있습니다.  
  
```  
C1: [TYPE=="EmployeeType"]    
                 => ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE);  
[TYPE=="EmployeeType"] == Select Condition List with one Matching Condition for claims Type.  
ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE) == Rule Action that issues a claims using string literal and matching claim referred with the Identifier.  
  
```  
  
### <a name="runtime-operation"></a>런타임 작업  
규칙을 효과적으로 작성 하려면 클레임 변환의 런타임 작업을 이해 하는 것이 중요 합니다. 런타임 작업은 다음과 같은 세 가지 클레임 집합을 사용 합니다.  
  
1.  **입력 클레임 집합**: 클레임 변환 작업에 지정 된 클레임의 입력 집합입니다.  
  
2.  **작업 클레임 집합**: 클레임 변환 중에 읽고 쓰는 중간 클레임입니다.  
  
3.  **출력 클레임 집합**: 클레임 변환 작업의 출력입니다.  
  
다음은 런타임 클레임 변환 작업에 대 한 간략 한 개요입니다.  
  
1.  클레임 변환에 대 한 입력 클레임은 작업 클레임 집합을 초기화 하는 데 사용 됩니다.  
  
    1.  각 규칙을 처리할 때 작업 클레임 집합이 입력 클레임에 사용 됩니다.  
  
    2.  규칙의 선택 조건 목록은 작업 클레임 집합에서 가능한 모든 클레임 집합에 대해 일치 됩니다.  
  
    3.  일치 하는 각 클레임 집합은 해당 규칙에서 작업을 실행 하는 데 사용 됩니다.  
  
    4.  규칙 작업을 실행 하면 하나의 클레임이 생성 되 고,이는 출력 클레임 집합 및 작업 클레임 집합에 추가 됩니다. 따라서 규칙의 출력은 규칙 집합의 후속 규칙에 대 한 입력으로 사용 됩니다.  
  
2.  규칙 집합의 규칙은 첫 번째 규칙부터 시작 하 여 순차적 순서로 처리 됩니다.  
  
3.  전체 규칙 집합이 처리 되 면 중복 된 클레임을 제거 하 고 다른 보안 문제에 대해 출력 클레임 집합이 처리 됩니다. 결과 클레임은 클레임 변환 프로세스의 출력입니다.  
  
이전 런타임 동작을 기반으로 복잡 한 클레임 변환을 작성할 수 있습니다.  
  
**예제: 런타임 작업 @ no__t-0  
  
이 예제에서는 두 개의 규칙을 사용 하는 클레임 변환의 런타임 작업을 보여 줍니다.  
  
```  
  
     C1:[Type=="EmpType", Value=="FullTime",ValueType=="string"] =>  
                Issue(Type=="EmployeeType", Value=="FullTime",ValueType=="string");  
     [Type=="EmployeeType"] =>   
               Issue(Type=="AccessType", Value=="Privileged", ValueType=="string");  
Input claims and Initial Evaluation Context:  
  {(Type= "EmpType"),(Value="FullTime"),(ValueType="String")}  
{(Type= "Organization"),(Value="Marketing"),(ValueType="String")}  
After Processing Rule 1:  
 Evaluation Context:  
  {(Type= "EmpType"),(Value="FullTime"),(ValueType="String")}  
{(Type= "Organization"), (Value="Marketing"),(ValueType="String")}  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
Output Context:  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
  
After Processing Rule 2:  
Evaluation Context:  
  {(Type= "EmpType"),(Value="FullTime"),(ValueType="String")}  
{(Type= "Organization"),(Value="Marketing"),(ValueType="String")}  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
  {(Type= "AccessType"),(Value="Privileged"),(ValueType="String")}  
Output Context:  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
  {(Type= "AccessType"),(Value="Privileged"),(ValueType="String")}  
  
Final Output:  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
  {(Type= "AccessType"),(Value="Privileged"),(ValueType="String")}  
  
```  
  
### <a name="special-rules-semantics"></a>특수 규칙 의미 체계  
규칙에 대 한 특수 구문은 다음과 같습니다.  
  
1.  빈 규칙 집합 = = 출력 클레임 없음  
  
2.  Empty Select Condition List = = 모든 클레임이 조건 선택 목록과 일치  
  
    **예제: 빈 Select 조건 목록 @ no__t-0  
  
    다음 규칙은 작업 집합의 모든 클레임과 일치 합니다.  
  
    ```  
    => Issue (Type = "UserType", Value = "External", ValueType = "string")  
    ```  
  
3.  빈 Select 일치 목록 = = 모든 클레임이 조건 선택 목록과 일치  
  
    **예제: 빈 일치 조건 @ no__t-0  
  
    다음 규칙은 작업 집합의 모든 클레임과 일치 합니다. 단독으로 사용 되는 경우 기본 "허용-모든" 규칙입니다.  
  
    ```  
    C1:[] => Issule (claim = C1);  
    ```  
  
## <a name="security-considerations"></a>보안 고려 사항  
**포리스트를 입력 하는 클레임**  
  
포리스트에 들어오는 보안 주체가 제공 하는 클레임을 철저 하 게 검사 하 여 올바른 클레임만 허용 하거나 발급할 수 있도록 해야 합니다. 부적절 한 클레임은 포리스트 보안을 손상 시킬 수 있으며,이는 포리스트를 시작 하는 클레임에 대 한 변환 정책을 제작할 때 가장 중요 한 고려 사항입니다.  
  
Active Directory에는 포리스트를 입력 하는 클레임의 잘못 된 구성을 방지 하기 위해 다음과 같은 기능이 있습니다.  
  
-   포리스트 트러스트에 포리스트를 입력 하는 클레임에 대 한 클레임 변환 정책이 설정 되지 않은 경우에는 보안을 위해 포리스트에 입력 하는 모든 주요 클레임을 Active Directory 삭제 합니다.  
  
-   포리스트를 입력 하는 클레임에 대 한 규칙 집합을 실행 하면 포리스트에 정의 되지 않은 클레임이 생성 되 고, 정의 되지 않은 클레임이 출력 클레임에서 삭제 됩니다.  
  
**포리스트를 종료 하는 클레임**  
  
포리스트를 종료 하는 클레임은 포리스트에 입력 하는 클레임 보다 포리스트의 보안 문제를 덜 일으킬 것입니다. 클레임은 적절 한 클레임 변환 정책이 없는 경우에도 포리스트를 그대로 둘 수 있습니다. 포리스트에 유지 되는 클레임을 변환 하는 과정에서 포리스트에 정의 되지 않은 클레임을 발급 하는 것도 가능 합니다. 이는 클레임을 사용 하 여 포리스트 간 트러스트를 쉽게 설정 하는 것입니다. 관리자는 포리스트를 입력 하는 클레임을 변환 해야 하는지 여부를 확인 하 고 적절 한 정책을 설정할 수 있습니다. 예를 들어 관리자는 클레임을 숨겨 정보 공개를 방지 해야 하는 경우 정책을 설정할 수 있습니다.  
  
**클레임 변환 규칙의 구문 오류**  
  
지정 된 클레임 변환 정책에 구문상 잘못 된 규칙 집합이 있거나 다른 구문 또는 저장소 문제가 있는 경우 정책이 잘못 된 것으로 간주 됩니다. 이는 앞에서 언급 한 기본 조건과 다르게 처리 됩니다.  
  
이 경우 의도를 확인할 수 없으며, 유사 시 대기 모드로 전환 될 수 없습니다 .이 경우에는 해당 신뢰 수준 + 순회 방향에 대해 출력 클레임이 생성 되지 않습니다. Active Directory 문제를 해결 하려면 관리자 개입이 필요 합니다. 이는 LDAP를 사용 하 여 클레임 변환 정책을 편집 하는 경우에 발생할 수 있습니다. Active Directory에 대 한 Windows PowerShell cmdlet은 구문 문제가 있는 정책 작성을 방지 하기 위해 유효성 검사를 수행 합니다.  
  
## <a name="other-language-considerations"></a>기타 언어 고려 사항  
  
1.  이 언어에서 특수 한 몇 가지 주요 단어나 문자 (터미널 이라고 함)가 있습니다. 이러한 항목은이 항목의 뒷부분에 나오는 [언어 터미널](Claims-Transformation-Rules-Language.md#BKMK_LT) 표에 나와 있습니다. 오류 메시지는 이러한 터미널의 명확성을 위해 태그를 사용 합니다.  
  
2.  경우에 따라 터미널을 문자열 리터럴로 사용할 수 있습니다. 그러나 이러한 사용은 언어 정의와 충돌 하거나 의도 하지 않은 결과가 발생할 수 있습니다. 이러한 종류의 사용은 권장 되지 않습니다.  
  
3.  규칙 작업은 클레임 값에 대 한 형식 변환을 수행할 수 없으며 이러한 규칙 동작을 포함 하는 규칙 집합은 잘못 된 것으로 간주 됩니다. 이로 인해 런타임 오류가 발생 하 고 출력 클레임이 생성 되지 않습니다.  
  
4.  규칙 동작이 규칙의 Select Condition 목록 부분에서 사용 되지 않은 식별자를 참조 하는 경우에는 잘못 된 사용입니다. 이 경우 구문 오류가 발생 합니다.  
  
    **예제: 식별자 참조가 잘못 되었습니다. @ no__t-0  
    다음 규칙은 규칙 동작에 사용 된 잘못 된 식별자를 보여 줍니다.  
  
    ```  
    C1:[] => Issue (claim = C2);  
    ```  
  
## <a name="sample-transformation-rules"></a>샘플 변환 규칙  
  
-   **특정 형식의 모든 클레임 허용**  
  
    정확한 형식  
  
    ```  
    C1:[type=="XYZ"] => Issue (claim = C1);  
    ```  
  
    Regex 사용  
  
    ```  
    C1: [type =~ "XYZ*"] => Issue (claim = C1);  
    ```  
  
-   **특정 클레임 유형 허용 안 함**  
    정확한 형식  
  
    ```  
    C1:[type != "XYZ"] => Issue (claim=C1);  
    ```  
  
    Regex 사용  
  
    ```  
    C1:[Type !~ "XYZ?"] => Issue (claim=C1);  
    ```  
  
## <a name="examples-of-rules-parser-errors"></a>규칙 파서 오류의 예  
클레임 변환 규칙은 사용자 지정 파서에서 구문 오류를 확인 하기 위해 구문 분석 됩니다. 이 파서는 Active Directory에 규칙을 저장 하기 전에 관련 Windows PowerShell cmdlet에 의해 실행 됩니다. 구문 오류를 포함 하 여 규칙을 구문 분석 하는 동안 발생 하는 모든 오류는 콘솔에 출력 됩니다. 또한 도메인 컨트롤러는 클레임 변환 규칙을 사용 하기 전에 파서를 실행 하 고 이벤트 로그에 오류를 기록 합니다 (이벤트 로그 번호 추가).  
  
이 섹션에서는 잘못 된 구문과 파서에서 생성 되는 해당 구문 오류를 사용 하 여 작성 된 규칙의 몇 가지 예를 보여 줍니다.  
  
1. 예:  
  
   ```  
   c1;[]=>Issue(claim=c1);  
   ```  
  
   이 예제에는 콜론 대신 잘못 사용 된 세미콜론이 있습니다.   
   **오류 메시지:**  
   *POLICY0002: 정책 데이터를 구문 분석할 수 없습니다.*  
   *줄 번호: 1, 열 번호: 2, 오류 토큰:;. 줄: ' c1; [] = > Issue (클레임 = c1); '.*  
   *Parser 오류: 'POLICY0030: 구문 오류, 예기치 않은 '; ', ': ' 중 하나가 필요 합니다. '*  
  
2. 예:  
  
   ```  
   c1:[]=>Issue(claim=c2);  
   ```  
  
   이 예에서 copy 발급 문의 식별자 태그는 정의 되지 않습니다.   
   **오류 메시지**:   
   *POLICY0011: 클레임 규칙의 조건이 CopyIssuanceStatement에 지정 된 조건 태그와 일치 하지 않습니다. ' c2 '.*  
  
3. 예:  
  
   ```  
   c1:[type=="x1", value=="1", valuetype=="bool"]=>Issue(claim=c1)  
   ```  
  
   "bool"은 언어의 터미널이 아니고 유효한 ValueType이 아닙니다. 유효한 터미널은 다음 오류 메시지에 나열 됩니다.   
   **오류 메시지:**  
   *POLICY0002: 정책 데이터를 구문 분석할 수 없습니다.*  
   줄 번호: 1, 열 번호: 39, 오류 토큰: "bool". 줄: ' c1: [type = = "x1", 값 = = "1", valuetype = = "bool"] = > Issue (클레임 = c1); '.   
   *Parser 오류: 'POLICY0030: 구문 오류, 예기치 않은 ' STRING ', 다음 중 하나가 필요 합니다. ' INT64_TYPE ' ' UINT64_TYPE ' ' STRING_TYPE ' ' BOOLEAN_TYPE ' ' IDENTIFIER '*  
  
4. 예:  
  
   ```  
   c1:[type=="x1", value==1, valuetype=="boolean"]=>Issue(claim=c1);  
   ```  
  
   이 예제의 숫자 **1** 은 언어의 유효한 토큰이 아니므로 이러한 사용은 일치 조건에 사용할 수 없습니다. 문자열을 만들려면 큰따옴표로 묶어야 합니다.   
   **오류 메시지:**  
   *POLICY0002: 정책 데이터를 구문 분석할 수 없습니다.*  
   *줄 번호: 1, 열 번호: 23, 오류 토큰: 1. 줄: ' c1: [type = = "x1", 값 = = 1, valuetype = = "bool"] = > Issue (클레임 = c1); '.* @ no__t-1 파서 오류: 'POLICY0029: 예기치 않은 입력입니다. </em>  
  
5. 예:  
  
   ```  
   c1:[type == "x1", value == "1", valuetype == "boolean"] =>   
  
        Issue(type = c1.type, value="0", valuetype == "boolean");  
   ```  
  
   이 예에서는 단일 등호 (=) 대신 이중 등호 (= =)를 사용 했습니다.   
   **오류 메시지:**  
   *POLICY0002: 정책 데이터를 구문 분석할 수 없습니다.*  
   *줄 번호: 1, 열 번호: 91, 오류 토큰: = = 줄: ' c1: [type = = "x1", 값 = = "1",*  
   *valuetype = = "boolean"] = > Issue (type = c1. type, value = "0", valuetype = = "boolean"); '.*  
   *Parser 오류: 'POLICY0030: 구문 오류, 예기치 않은 ' = = ', 다음 중 하나가 필요 합니다. ' = '*  
  
6. 예:  
  
   ```  
   c1:[type=="x1", value=="boolean", valuetype=="string"] =>   
  
         Issue(type=c1.type, value=c1.value, valuetype = "string");  
   ```  
  
   이 예는 구문상 및 의미 체계가 올바릅니다. 그러나 문자열 값으로 "boolean"을 사용 하면 혼동을 발생 시킬 수 있으므로이를 피해 야 합니다. 앞에서 설명한 것 처럼 가능한 경우에는 언어 터미널을 클레임 값으로 사용 하지 않아야 합니다.  
  
## <a name="BKMK_LT"></a>언어 터미널  
다음 표에서는 클레임 변환 규칙 언어에서 사용 되는 터미널 문자열 및 관련 언어 터미널의 전체 집합을 보여 줍니다. 이러한 정의는 대/소문자를 구분 하지 않는 UTF-16 문자열을 사용 합니다.  
  
|문자열|터미널과|  
|----------|------------|  
|"= >"|의미|  
|";"|;|  
|":"|탑재|  
|","|쉼표로|  
|"."|점과|  
|"["|O_SQ_BRACKET|  
|"]"|C_SQ_BRACKET|  
|"("|O_BRACKET|  
|")"|C_BRACKET|  
|"=="|EQ|  
|"!="|NEQ|  
|"=~"|REGEXP_MATCH|  
|"!~"|REGEXP_NOT_MATCH|  
|"="|할당|  
|"& &"|AND|  
|문제|문제|  
|입력할|TYPE|  
|기본값|값|  
|system.valuetype|VALUE_TYPE|  
|요청할|요청할|  
|"[_A] [_A-a-za-z0-9] *"|한정자|  
|"\\" [^ \\ "\n] * \\" "|문자열|  
|작아|UINT64_TYPE|  
|푸시하고|INT64_TYPE|  
|문자열|STRING_TYPE|  
|부울|BOOLEAN_TYPE|  
  
## <a name="language-syntax"></a>언어 구문  
다음 클레임 변환 규칙 언어는 ABNF 형식으로 지정 됩니다. 이 정의는 여기에 정의 된 ABNF 생성 뿐만 아니라 이전 표에 지정 된 터미널을 사용 합니다. 규칙은 u t f-16으로 인코딩되고 문자열 비교는 대/소문자를 구분 하지 않는 것으로 처리 해야 합니다.  
  
```  
Rule_set        = ;/*Empty*/  
             / Rules  
Rules         = Rule  
             / Rule Rules  
Rule          = Rule_body  
Rule_body       = (Conditions IMPLY Rule_action SEMICOLON)  
Conditions       = ;/*Empty*/  
             / Sel_condition_list  
Sel_condition_list   = Sel_condition  
             / (Sel_condition_list AND Sel_condition)  
Sel_condition     = Sel_condition_body  
             / (IDENTIFIER COLON Sel_condition_body)  
Sel_condition_body   = O_SQ_BRACKET Opt_cond_list C_SQ_BRACKET  
Opt_cond_list     = /*Empty*/  
             / Cond_list  
Cond_list       = Cond  
             / (Cond_list COMMA Cond)  
Cond          = Value_cond  
             / Type_cond  
Type_cond       = TYPE Cond_oper Literal_expr  
Value_cond       = (Val_cond COMMA Val_type_cond)  
             /(Val_type_cond COMMA Val_cond)  
Val_cond        = VALUE Cond_oper Literal_expr  
Val_type_cond     = VALUE_TYPE Cond_oper Value_type_literal  
claim_prop       = TYPE  
             / VALUE  
Cond_oper       = EQ  
             / NEQ  
             / REGEXP_MATCH  
             / REGEXP_NOT_MATCH  
Literal_expr      = Literal  
             / Value_type_literal  
  
Expr          = Literal  
             / Value_type_expr  
             / (IDENTIFIER DOT claim_prop)  
Value_type_expr    = Value_type_literal  
             /(IDENTIFIER DOT VALUE_TYPE)  
Value_type_literal   = INT64_TYPE  
             / UINT64_TYPE  
             / STRING_TYPE  
             / BOOLEAN_TYPE  
Literal        = STRING  
Rule_action      = ISSUE O_BRACKET Issue_params C_BRACKET  
Issue_params      = claim_copy  
             / claim_new  
claim_copy       = CLAIM ASSIGN IDENTIFIER  
claim_new       = claim_prop_assign_list  
claim_prop_assign_list = (claim_value_assign COMMA claim_type_assign)  
             /(claim_type_assign COMMA claim_value_assign)  
claim_value_assign   = (claim_val_assign COMMA claim_val_type_assign)  
             /(claim_val_type_assign COMMA claim_val_assign)  
claim_val_assign    = VALUE ASSIGN Expr  
claim_val_type_assign = VALUE_TYPE ASSIGN Value_type_expr  
Claim_type_assign   = TYPE ASSIGN Expr  
  
```  
  


