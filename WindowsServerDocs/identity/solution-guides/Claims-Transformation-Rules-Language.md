---
ms.assetid: e831f781-3c45-4d44-b411-160d121d1324
title: 클레임 변환 규칙 언어
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4a6b378bc4aef180ebedd260008febaa2f2a76ae
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856214"
---
# <a name="claims-transformation-rules-language"></a>클레임 변환 규칙 언어

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포리스트 간 클레임 변환 기능을 사용 하면 브리지 수 클레임 동적 Access Control에 대 한 포리스트 경계를 넘어 포리스트 간 트러스트에 클레임 변환 정책 설정입니다. 모든 정책의 기본 구성 요소는 클레임 변환 규칙 언어 작성 된 규칙. 이 항목에서는이 언어에 대 한 세부 정보를 제공 하 고 클레임 변환 규칙을 작성 하는 방법에 대 한 지침을 제공 합니다.  
  
포리스트 간에서 변환 정책에 대 한 Windows PowerShell cmdlet을 간단한 정책을 설정 하는 옵션을 위해서는 공통 시나리오를 신뢰 합니다. 이러한 cmdlet는 클레임 변환 규칙 언어의 정책 및 규칙에 사용자 입력을 변환 하 고 지정 된 형식으로 Active Directory에 저장 합니다. 클레임 변환에 대 한 cmdlet에 대 한 자세한 내용은 참조는 [동적 Access Control에 대 한 AD DS Cmdlet](https://go.microsoft.com/fwlink/?LinkId=243150)합니다.  
  
클레임 구성 및 Active Directory 포리스트에 포리스트 간 트러스트에 배치 요구 사항에 따라 클레임 변환 정책 활성 Windows PowerShell cmdlet을 통해 지원 되는 정책 보다 더 복잡 한 해야 할 수 있습니다. 디렉터리입니다. 이러한 정책을 효과적으로 작성 하려면 클레임 변환 규칙 언어 구문 및 의미 체계를 이해 하려면 반드시 합니다. 이 클레임 변환 규칙 언어 ("언어") Active Directory에서 사용 되는 언어의 하위 집합인 [Active Directory Federation Services](https://go.microsoft.com/fwlink/?LinkId=243982) 비슷한 목적으로 하며이 매우 유사한 구문 및 의미 체계에 대 한 합니다. 그러나 몇 가지 더 적은 작업을 허용 하 고 추가 구문 제한을 Active Directory 버전의 언어에 배치 됩니다.  
  
이 항목에는 간단 하 게 구문 및 의미 체계 가능 하도록 정책을 작성 하는 경우 Active Directory 및 고려 사항에서 클레임 변환 규칙 언어를 설명 합니다. 시작 하는 데 규칙 예제 및 예제는 잘못 된 구문 및 생성 하는 규칙을 작성할 때 오류 메시지를 해독할 수 있도록 메시지의 여러 집합을 제공 합니다.  
  
## <a name="tools-for-authoring-claims-transformation-policies"></a>클레임 변환 정책 작성을 위한 도구  
**Active Directory 용 Windows PowerShell cmdlet**: 이것이 작성 하 고 클레임 변환 정책 설정에 기본 및 권장 방법입니다. 이러한 cmdlet는 간단한 정책에 대 한 스위치를 제공 하 고 더 복잡 한 정책에 대 한 설정 된 규칙을 확인 합니다.  
  
**LDAP**: 클레임 변환 정책 Active Directory를 통해 액세스 프로토콜 LDAP (Lightweight Directory)에서 편집할 수 있습니다. 그러나이 권장 되지 않습니다 정책을 여러 복잡 한 구성 요소가 있으며 Active Directory에 쓰기 전에 정책을 사용 하는 도구에 입증 되지 않을 때문에. 이 문제를 진단 하는 상당한 기간 이후에 해야 합니다.  
  
## <a name="active-directory-claims-transformation-rules-language"></a>Active Directory 클레임 변환 규칙 언어  
  
### <a name="syntax-overview"></a>구문 개요  
구문에 간략하게 설명 및 언어의 의미 체계 다음과 같습니다.  
  
-   클레임 변환 규칙 집합을 0 개 이상의 규칙으로 구성 됩니다. 각 규칙에 두 개의 활성 부분이 있습니다. **선택 조건 목록** 하 고 **규칙 작업**합니다. 경우는 **조건 목록 선택** TRUE로 평가 해당 규칙 작업이 실행 됩니다.  
  
-   **선택 조건 목록** 에 0 개 이상의 **선택 조건**합니다. 모든는 **선택 조건을** 에 대해 TRUE로 계산 되어야 합니다는 **조건 목록 선택** TRUE로 평가 합니다.  
  
-   각 **조건 선택** 에 0 개 이상의 집합이 **일치 조건**합니다. 모든 합니다 **일치 조건이** 선택 조건이 TRUE로 평가 대해 TRUE로 계산 되어야 합니다. 이러한 조건을 모두는 단일 클레임에 대해 평가 됩니다. 일치 하는 클레임을 **조건 선택** 에서 태그를 지정할 수는 **식별자** 에서 참조 하 고는 **규칙 작업**.  
  
-   각 **일치 조건을** 일치 하는 조건을 지정 합니다 **유형** 또는 **값** 또는 **ValueType** 다른을사용하여클레임 **조건 연산자** 하 고 **문자열 리터럴**합니다.  
  
    -   지정 하는 경우는 **일치 조건을** 에 대 한를 **값**도 지정 해야 합니다는 **일치 하는 조건** 특정 **ValueType** 및 그 반대의 경우도 마찬가지입니다. 이러한 조건은 서로 옆에 있는 구문에 있어야 합니다.  
  
    -   **ValueType** 조건과 일치 하는 특정 사용 해야 합니다 **ValueType** 리터럴만 합니다.  
  
-   A **규칙 작업** 태그가 지정 된 클레임을 복사할 수는 **식별자** 하거나 식별자로 태그가 지정 되는 클레임에 따라 및/또는 문자열 리터럴을 지정 된 클레임을 발급 합니다.  
  
**예제 규칙**  
  
이 예제에는 Valuetype 동일한 클레임을 사용 하며이 형식에 대 한 클레임 값에 대 한 동일한 해석을 제공한 두 포리스트 간 클레임 유형을 변환 하는 규칙을 보여 줍니다. 규칙에 일치 하는 조건을 두 개 및 문자열 리터럴과 일치 하는 클레임 대 한 참조를 사용 하는 문제 문을 있습니다.  
  
```  
C1: [TYPE=="EmployeeType"]    
                 => ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE);  
[TYPE=="EmployeeType"] == Select Condition List with one Matching Condition for claims Type.  
ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE) == Rule Action that issues a claims using string literal and matching claim referred with the Identifier.  
  
```  
  
### <a name="runtime-operation"></a>런타임 작업  
클레임 변환 규칙을 효과적으로 작성할의 런타임 작업을 이해 하는 것이 반드시 합니다. 런타임 작업에서는 세 개의 클레임 집합을 사용합니다.  
  
1.  **입력 클레임 집합**: 입력된 클레임 변환 작업에 지정 된 클레임 집합이 있습니다.  
  
2.  **클레임 집합을 작업**: 읽고 클레임 변환 중에 기록 하는 중간 클레임입니다.  
  
3.  **출력 클레임 집합**: 클레임 변환 작업의 출력입니다.  
  
런타임 클레임 변환 작업의 간략 한 개요는 다음과 같습니다.  
  
1.  클레임 변환에 대 한 입력된 클레임 작업 클레임 집합을 초기화 하는 데 사용 됩니다.  
  
    1.  각 규칙을 처리할 때 작업 클레임 집합은 입력된 클레임에 사용 됩니다.  
  
    2.  선택 조건 목록 규칙은 가능한 모든 작업 클레임 집합의 클레임 집합에 대해 일치 합니다.  
  
    3.  클레임을 일치 하는 각 집합은 해당 규칙에 작업을 실행 하려면 사용 됩니다.  
  
    4.  작업 클레임 집합 및 클레임 출력에 추가 되는 규칙을 한 클레임을 작업 결과 실행 합니다. 따라서 규칙의 출력을 후속 규칙 규칙 집합에 대 한 입력으로 사용 됩니다.  
  
2.  규칙 규칙 집합에 첫 번째 규칙을 사용 하 여 시작 하는 순서 대로 처리 됩니다.  
  
3.  중복 된 클레임을 제거 하려면 출력 클레임 집합은 처리 전체 규칙 집합을 처리할 때 및 기타 보안 문제에 대 한 합니다. 결과 클레임이 클레임 변환 프로세스의 출력을 보여 줍니다.  
  
이전 런타임 동작을 기반으로 하는 복잡 한 클레임 변환을 작성 하는 것이 가능 합니다.  
  
**예: 런타임 작업**  
  
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
  
### <a name="special-rules-semantics"></a>특별 한 규칙이 의미 체계  
다음은 규칙에 대 한 특수 구문입니다.  
  
1.  규칙 집합을 빈 없는 출력 클레임 = =  
  
2.  빈 조건 목록 선택의 모든 클레임이 일치 조건이 선택 목록 = =  
  
    **예: 빈 선택 조건 목록**  
  
    다음 규칙 작업 집합의 모든 클레임을 찾습니다.  
  
    ```  
    => Issue (Type = "UserType", Value = "External", ValueType = "string")  
    ```  
  
3.  일치 하는 Select List 빈 모든 클레임이 일치 조건이 선택 목록 = =  
  
    **예: 빈 일치 조건**  
  
    다음 규칙 작업 집합의 모든 클레임을 찾습니다. 이 단독으로 사용 하는 경우 기본 "허용-모든" 규칙입니다.  
  
    ```  
    C1:[] => Issule (claim = C1);  
    ```  
  
## <a name="security-considerations"></a>보안 고려 사항  
**포리스트를 입력 하는 클레임**  
  
포리스트에 들어오는 보안 주체에서 클레임에서는 허용 하거나 올바른 클레임을 발급 하도록 철저 하 게 검사 해야 합니다. 잘못 된 클레임에는 포리스트 보안을 손상 시킬 수 있습니다 하 고 포리스트를 입력 하는 클레임에 대 한 변환 정책을 작성 하는 경우 상위 고려 사항 이어야 합니다.  
  
Active Directory에 포리스트를 입력 하는 클레임의 잘못 된 구성 하지 않으려면 다음 기능이 있습니다.  
  
-   포리스트 트러스트에 보안상의 이유로 포리스트를 입력 하는 클레임에 대 한 설정 클레임 변환 정책이 없는 경우 Active Directory 포리스트를 입력 하는 모든 사용자 클레임을 삭제 합니다.  
  
-   포리스트의 정의 되어 있지 않은 클레임에서 포리스트 결과 입력 하는 규칙 클레임 집합을 실행 하는 경우 정의 되지 않은 클레임을 출력 클레임에서 삭제 됩니다.  
  
**포리스트를 유지 하는 클레임**  
  
포리스트를 입력 하는 클레임 보다 포리스트에 대 한 낮은 보안 문제가 있는 포리스트를 유지 하는 클레임입니다. 클레임으로 포리스트 그대로 수-경우에 해당 없는 클레임 변환 정책 진행에서 됩니다. 포리스트의 포리스트를 유지 하는 클레임을 변환의 일부로 정의 되어 있지 않은 클레임을 발급 하는 것도 가능 합니다. 이 클레임을 사용 하 여 포리스트 간 트러스트를 쉽게 설정 하는 것입니다. 관리자는 포리스트를 입력 하는 클레임을 변환 하 고 적절 한 정책을 설정 해야 하는 경우 확인할 수 있습니다. 예를 들어, 정보 공개를 방지 하기 위해 클레임을 숨기려면 필요한 경우에 관리자 정책을 설정할 수 있습니다.  
  
**클레임 변환 규칙에서 구문 오류**  
  
지정 된 클레임 변환 정책에 구문적으로 올바르지 않은 하는 규칙 집합 또는 다른 구문 또는 저장소 문제가 있는 경우 정책은 잘못 간주 됩니다. 이 작업은 앞에서 언급 한 기본 조건을 다르게 처리 됩니다.  
  
Active Directory 의도 여기서 확인할 수 없는 및 해당 신뢰 +의 탐색 방향을 없는 출력 클레임이 생성 되는 위치를 유사 시 대기 모드로 전환 합니다. 문제를 해결 하려면 관리자 개입이 필요 합니다. 이 클레임 변환 정책 편집 하려면 LDAP가 사용 하는 경우 발생할 수 있습니다. Active Directory 용 Windows PowerShell cmdlet에 유효성 검사 구문 문제를 사용 하 여 정책을 직접 쓸 수 없도록 합니다.  
  
## <a name="other-language-considerations"></a>다른 언어 관련 고려 사항  
  
1.  여러 키 단어 또는 특수 (터미널 라고도 함)이 언어로 된 문자가 있습니다. 이러한 표시 됩니다는 [언어 터미널](Claims-Transformation-Rules-Language.md#BKMK_LT) 이 항목의 뒷부분에 테이블입니다. 오류 메시지는 명확성을 위해이 터미널에 대 한 태그를 사용합니다.  
  
2.  경우에 따라 터미널 문자열 리터럴로 사용할 수 있습니다. 그러나 해당 사용량을 언어 정의와 충돌 있을 수도 있고 의도 하지 않은 결과가 발생 합니다. 이러한 종류의 사용은 권장 되지 않습니다.  
  
3.  규칙 작업에서 모든 형식 변환을 수행할 수 없습니다 값을 클레임 및 이러한 규칙 작업이 포함 된 규칙 집합을 잘못 된 것으로 간주 됩니다. 이 인해 런타임 오류가 및 없는 출력 클레임이 생성 됩니다.  
  
4.  규칙 작업 규칙의 조건 목록 선택 부분에서 사용 되지 않은 식별자를 참조 이면 사용이 잘못 되었습니다. 이렇게 하면 구문 오류가 있습니다.  
  
    **예: 잘못 된 식별자 참조**  
    다음 규칙은 규칙 작업에서 사용 되는 잘못 된 식별자를 보여 줍니다.  
  
    ```  
    C1:[] => Issue (claim = C2);  
    ```  
  
## <a name="sample-transformation-rules"></a>샘플 변환 규칙  
  
-   **특정 유형의 모든 클레임을 허용**  
  
    정확한 형식  
  
    ```  
    C1:[type=="XYZ"] => Issue (claim = C1);  
    ```  
  
    Regex를 사용 하 여  
  
    ```  
    C1: [type =~ "XYZ*"] => Issue (claim = C1);  
    ```  
  
-   **특정 클레임 유형을 허용 안 함**  
    정확한 형식  
  
    ```  
    C1:[type != "XYZ"] => Issue (claim=C1);  
    ```  
  
    Regex를 사용 하 여  
  
    ```  
    C1:[Type !~ "XYZ?"] => Issue (claim=C1);  
    ```  
  
## <a name="examples-of-rules-parser-errors"></a>파서 오류 규칙의 예  
클레임 변환 규칙은 사용자 지정 파서 구문 오류를 검사 하 여 구문 분석 됩니다. 이 구문 분석기는 Active Directory에서 규칙을 저장 하기 전에 관련된 Windows PowerShell cmdlet을 통해 실행 됩니다. 구문 오류를 포함 한 규칙을 구문 분석 오류는 콘솔에 인쇄 됩니다. 도메인 컨트롤러가 클레임 변환 규칙을 사용 하기 전에 파서를 실행할 수도 및 이벤트 로그에 오류 로그 (이벤트 로그 번호 추가).  
  
이 섹션에서는 몇 가지 예가 파서에서 생성 되는 오류 잘못 된 구문과 해당 구문을 사용 하 여 작성 된 규칙을 보여 줍니다.  
  
1.  예:  
  
    ```  
    c1;[]=>Issue(claim=c1);  
    ```  
  
    이 예제를 잘못 사용 되는 세미콜론 콜론 대신에 있습니다.   
    **오류 메시지:**  
    *POLICY0002: 정책 데이터를 구문 분석 하지 못했습니다.*  
    *줄 번호: 1, 열 번호: 2 오류 토큰이:;. Line: 'c1;[]=>Issue(claim=c1);'.*  
    *파서 오류: ' POLICY0030: 구문 오류입니다. 예기치 않은 ';', 다음 중 하나를 필요 합니다: ':'.'*  
  
2.  예:  
  
    ```  
    c1:[]=>Issue(claim=c2);  
    ```  
  
    이 예제에서는 복사 발급 문에 식별자 태그 정의 되지 않습니다.   
    **오류 메시지**:   
    *POLICY0011: 클레임 규칙의 조건이 CopyIssuanceStatement에 지정 된 조건을 태그와 일치 합니다. 'c2'.*  
  
3.  예:  
  
    ```  
    c1:[type=="x1", value=="1", valuetype=="bool"]=>Issue(claim=c1)  
    ```  
  
    "bool" 언어에서 터미널 아니며 유효한 ValueType 아닙니다. 올바른 터미널에서 다음 오류 메시지가 나열 됩니다.   
    **오류 메시지:**  
    *POLICY0002: 정책 데이터를 구문 분석 하지 못했습니다.*  
    줄 번호: 1, 열 번호: 39, 오류 토큰이: "bool"입니다. Line: 'c1:[type=="x1", value=="1",valuetype=="bool"]=>Issue(claim=c1);'.   
    *파서 오류: ' POLICY0030: 구문 오류입니다. 예기치 않은 'STRING', 다음 중 하나가 필요 합니다. 'INT64_TYPE' 'UINT64_TYPE' 'STRING_TYPE' 'BOOLEAN_TYPE' 'IDENTIFIER'*  
  
4.  예:  
  
    ```  
    c1:[type=="x1", value==1, valuetype=="boolean"]=>Issue(claim=c1);  
    ```  
  
    숫자 **1** 이 예제의 토큰이 아닙니다. 유효한 언어에서 하며 해당 사용량 일치 조건에서 허용 되지 않습니다. 이를 문자열로를 큰따옴표로 묶어야 합니다.   
    **오류 메시지:**  
    *POLICY0002: 정책 데이터를 구문 분석 하지 못했습니다.*  
    *줄 번호: 1, 열 번호: 23 오류 토큰: 1. Line: 'c1:[type=="x1", value==1, valuetype=="bool"]=>Issue(claim=c1);'.**Parser error: ' POLICY0029: 예기치 않은 입력 합니다.*  
  
5.  예:  
  
    ```  
    c1:[type == "x1", value == "1", valuetype == "boolean"] =>   
  
         Issue(type = c1.type, value="0", valuetype == "boolean");  
    ```  
  
    이 예제에서는 단일 등호 (=) 대신 이중 등호 (= =)를 사용합니다.   
    **오류 메시지:**  
    *POLICY0002: 정책 데이터를 구문 분석 하지 못했습니다.*  
    *줄 번호: 1, 열 번호: 91, 오류 토큰이: = =. Line: 'c1:[type=="x1", value=="1",*  
    *valuetype=="boolean"]=>Issue(type=c1.type, value="0", valuetype=="boolean");'.*  
    *파서 오류: ' POLICY0030: 구문 오류, 예기치 않은 '= =', 다음 중 하나가 필요 합니다. '='*  
  
6.  예:  
  
    ```  
    c1:[type=="x1", value=="boolean", valuetype=="string"] =>   
  
          Issue(type=c1.type, value=c1.value, valuetype = "string");  
    ```  
  
    이 예제는 구문 및 의미 체계가 올바른. 그러나 혼동 하기 바인딩되는 문자열 값 및 피해 야 합니다 "부울"을 사용 합니다. 앞서 언급 했 듯이, 언어 터미널 사용 하 여 가능한 경우 클레임 값을 피해 야 합니다.  
  
## <a name="BKMK_LT"></a>언어 터미널  
다음 표에서 터미널 문자열과 클레임 변환 규칙 언어에 사용 되는 관련 된 언어 터미널의 전체 집합을 나열 합니다. 이러한 정의 utf-16 문자열 대/소문자를 사용합니다.  
  
|문자열|터미널|  
|----------|------------|  
|"=>"|의미|  
|";"|세미콜론으로|  
|":"|콜론|  
|","|COMMA|  
|"."|점|  
|"["|O_SQ_BRACKET|  
|"]"|C_SQ_BRACKET|  
|"("|O_BRACKET|  
|")"|C_BRACKET|  
|"=="|EQ|  
|"!="|NEQ|  
|"=~"|REGEXP_MATCH|  
|"!~"|REGEXP_NOT_MATCH|  
|"="|할당|  
|"&&"|AND|  
|"문제"|문제|  
|"type"|TYPE|  
|"value"|값|  
|"valuetype"|VALUE_TYPE|  
|"클레임"|클레임|  
|"[_A-Za-z][_A-Za-z0-9]*"|식별자|  
|"\\"[^\\"\n]*\\""|문자열|  
|"uint64"|UINT64_TYPE|  
|"int64"|INT64_TYPE|  
|"string"|STRING_TYPE|  
|"부울"|BOOLEAN_TYPE|  
  
## <a name="language-syntax"></a>언어 구문  
다음 클레임 변환 규칙 언어는 ABNF 형태로 지정 됩니다. 이 정의 여기에 정의 된 ABNF 프로덕션 외에도 이전 표에 지정 된 터미널을 사용 합니다. 규칙은 u t F-16이 고 인코딩해야 및 문자열 비교와 대/소문자 구분 처리 해야 합니다.  
  
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
  


