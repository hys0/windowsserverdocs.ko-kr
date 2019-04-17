---
ms.assetid: e831f781-3c45-4d44-b411-160d121d1324
title: "클레임 변환 규칙 언어"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4a6b378bc4aef180ebedd260008febaa2f2a76ae
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="claims-transformation-rules-language"></a>클레임 변환 규칙 언어

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

전체 숲 클레임 다리 수 주장 동적 액세스 제어를 위한 숲 경계 숲에서 신뢰에 변환 정책을 청구를 설정 하 여 변환 기능 수 있도록 합니다. 모든 정책의 기본 구성 요소가 규칙 클레임 변환 규칙 언어로 작성입니다. 이 항목이이 언어에 대 한 세부 정보를 제공 하 고 제작 클레임 변환 규칙에 대 한 지침을 제공 합니다.  
  
숲에서에 변환 정책에 대 한 Windows PowerShell cmdlet 신뢰 하는 않은 간단한 정책 설정 하는 옵션 필수 공통점 시나리오 합니다. 이러한 cmdlet 정책 및 청구 변환 규칙 언어로 규칙에 사용자 입력 하 고 규정 형식에서 Active Directory에 저장 합니다. 클레임 변환에 대 한 cmdlet에 대 한 자세한 내용은 참조는 [AD DS Cmdlet에 대 한 동적 액세스 제어](https://go.microsoft.com/fwlink/?LinkId=243150)합니다.  
  
클레임 구성 Active Directory 숲에 걸쳐 숲 신뢰에 배치 된 요구 사항에 따라 클레임 변환 정책 Windows PowerShell cmdlet Active Directory에 대 한 지원 정책은 보다 더 복잡 해야 할 수 있습니다. 이러한 정책 효과적으로 작성, 클레임 변환 규칙 언어 구문 및 의미를 이해 하 고이 합니다. 이 주장 Active Directory에 변환 규칙 언어 ("언어")에서 사용 되는 언어 중 일부는 [Active Directory Federation Services](https://go.microsoft.com/fwlink/?LinkId=243982) 매우 유사 구문 및 의미 유사한 목적을 있으며에 대 한 합니다. 그러나 적은 작업이 허용 있으며 추가 구문을 제한 언어의 Active Directory 버전에 포함 됩니다.  
  
이 여기서 구문 및 Active Directory와 고려 정책을 작성할 때에 클레임 변환 규칙 언어의 의미 간략하게 설명 합니다. 시작 하는 데 예제 규칙과 잘못 구문 및 규칙을 작성할 때 오류 메시지를 읽을 수 있도록 생성 메시지의 예의 제공 합니다.  
  
## <a name="tools-for-authoring-claims-transformation-policies"></a>도구를 작성 클레임 변환 정책  
**Windows PowerShell cmdlet에 대 한 Active Directory**:를 작성 및 청구 변환 정책 설정 기본 설정 및 권장 방법입니다. 이러한 cmdlet 간단한 정책에 대 한 스위치를 제공 하 고 더 복잡 한 정책에 대 한 설정 규칙을 확인 합니다.  
  
**LDAP**: 클레임 변환 정책 Active Directory LDAP(Lightweight Directory Access Protocol) (LDAP)을 통해에서 편집할 수 있습니다. 하지만,이 하지 되므로 권장는 여러 복잡 한 구성 요소 정책을 사용 하는 도구 Active Directory를 기록 하기 전에 정책을 확인할 수 있습니다. 이 문제를 진단 하는 데 시간이 상당한 이후 해야 합니다.  
  
## <a name="active-directory-claims-transformation-rules-language"></a>Active Directory 변환 규칙 언어 주장  
  
### <a name="syntax-overview"></a>구문 개요  
구문을 간략하게 설명 하 고 해당 언어의 의미는 다음과 같습니다.  
  
-   클레임 변환 규칙 집합 개 이상의 규칙 구성 됩니다. 각 규칙에 활성 두 가지 부분이: **조건 목록 선택** 및 **규칙 동작**합니다. 하는 경우는 **조건 목록 선택** 참로 평가 해당 규칙 작업이 실행 됩니다.  
  
-   **조건이 목록을 선택** 0 이상 **조건 선택**합니다. 모든는 **조건 선택** 여야 마찬가지입니다는 **조건 목록 선택** 참으로 평가 합니다.  
  
-   각 **조건 선택** 에 0 개 이상의 집합이 **일치 하는 조건**합니다. 모든는 **일치 하는 조건** 참으로 평가 선택 조건이 맞을 계산 해야 합니다. 모든 이러한 조건 하나의 클레임 평가 됩니다. 클레임와 일치 하는 **조건 선택** 태그가 지정 될 수는 **식별자** 에서 참조 하 고는 **규칙 동작**합니다.  
  
-   각 **일치 하는 조건** 조건을 일치 하도록 지정는 **종류** 또는 **값** 또는 **값** 다른를 사용 하 여 클레임 **조건 연산자** 및 **문자열 리터럴**합니다.  
  
    -   지정 하는 경우는 **일치 하는 조건** 에 대 한는 **값**를 지정 해야는 **일치 하는 조건** 특정 **값** 그 반대의 합니다. 이러한 조건이 나란히 구문을에 있어야 합니다.  
  
    -   **값** 조건와 일치 하는 특정 사용 해야 **값** 리터럴만 합니다.  
  
-   A **규칙 동작** 태그가 지정 된 하나의 클레임을 복사할 수는 **식별자** 하거나 발급 한 클레임 태그가 지정 된 식별자 클레임에 따라 및/또는 문자열 리터럴 자녀에 게 부여 합니다.  
  
**예제 규칙**  
  
이 이때에는 동일한 클레임 값 형식을 사용 하 고 있는이 유형에 대 한 값 청구에 대 한 같은 해석 하 두 숲 간에 유형 클레임 번역할 사용할 수 있는 규칙 보여 줍니다. 규칙 한 일치 하는 조건 및 문자열 리터럴와 일치 하는 클레임 참조 사용 하는 문제 문을 있습니다.  
  
```  
C1: [TYPE=="EmployeeType"]    
                 => ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE);  
[TYPE=="EmployeeType"] == Select Condition List with one Matching Condition for claims Type.  
ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE) == Rule Action that issues a claims using string literal and matching claim referred with the Identifier.  
  
```  
  
### <a name="runtime-operation"></a>런타임 작업  
것이 규칙 효과적으로 작성 클레임 변환의 런타임 작동 하는 것이 중요 합니다. 런타임 작업 세 가지 클레임을 사용합니다.  
  
1.  **입력 주장 설정**: 클레임 변환 작동이 권한이 부여 된 클레임 입력된 집합입니다.  
  
2.  **작업 설정 주장**:을 읽고 클레임 변환 하는 동안에 기록 된 청구에 대 한 약간 합니다.  
  
3.  **출력 주장 설정**: 출력 클레임 변환 작업 중입니다.  
  
런타임 클레임 변환 작업을 간략하게 설명 다음과 같습니다.  
  
1.  클레임 변환에 대 한 주장 입력된 클레임 작업 집합을 초기화 하는 데 사용 합니다.  
  
    1.  각 규칙을 처리할 때 입력된 클레임 클레임 작업 집합은 사용 됩니다.  
  
    2.  선택 조건 목록 규칙의 모든 가능한 집합이 클레임 작업 클레임 설정에서 일치 합니다.  
  
    3.  클레임 일치 하는 각 집합이 규칙에서 작업을 실행 하는 데 사용 됩니다.  
  
    4.  설정 하 고 작업 클레임 집합 주장 출력에 추가 하는 규칙 하나의 클레임을 작업 결과 실행 합니다. 따라서 집합은의 후속 규칙에 대 한 출력 규칙에서 입력으로 사용 됩니다.  
  
2.  첫 번째 규칙 부터는 순서 대로 규칙 집합에 규칙 처리 됩니다.  
  
3.  출력 클레임 설정 중복 청구를 제거 하려면 처리 전체 규칙 집합을 처리할 때 및 issues.The 결과 클레임은 청구 변환 프로세스 출력.  
  
되기 복잡 한 청구 변환을 기반 이전 런타임 동작으로 쓸 수 있습니다.  
  
**예: 런타임 작업**  
  
이 이때는 규칙이 두 개를 사용 하는 클레임 변환의 런타임 작업을 보여 줍니다.  
  
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
  
### <a name="special-rules-semantics"></a>특수 규칙 의미  
다음은 규칙에 대 한 특수 구문을입니다.  
  
1.  비우기 규칙 집합 출력 어떠한 보증도 = =  
  
2.  비우기 조건 목록 선택 = = 모든 클레임 일치 항목 선택 조건 목록  
  
    **예: 빈 선택 조건 목록**  
  
    다음 규칙의 작업 집합에 모든 청구를 찾습니다.  
  
    ```  
    => Issue (Type = "UserType", Value = "External", ValueType = "string")  
    ```  
  
3.  비우기와 일치 하는 목록을 선택 = = 모든 클레임 일치 항목 선택 조건 목록  
  
    **예: 빈와 일치 하는 조건**  
  
    다음 규칙의 작업 집합에 모든 청구를 찾습니다. 기본 "허용 모든" 규칙 그대로 사용 하는 경우입니다.  
  
    ```  
    C1:[] => Issule (claim = C1);  
    ```  
  
## <a name="security-considerations"></a>보안 고려  
**입력 한 숲 클레임**  
  
한 숲 수신 되 고 사용자가 제공 클레임 허용 했습니다 하거나만 올바른 요청을 실행할 수 있도록 철저 하 게 검사 해야 합니다. 부적절 한 클레임 숲 보안 손상 될 수 있습니다 한 입력 하 여 숲 청구에 대 한 정책을 변환 제작 상위 고려해 야이 합니다.  
  
Active Directory 잘못 입력 한 숲 클레임 방지 하기 위해 다음과 같은 기능을 사항은 다음과 같습니다.  
  
-   숲 보안 설정에 대 한 보안을 위해 숲을 입력 하는 클레임 클레임 변환 정책이 있으면 Active Directory 숲 입력 하는 모든 사용자 클레임 삭제 합니다.  
  
-   숲 결과 숲 속의 정의 되어 있지 않은 클레임에 입력 하는 청구에 대 한 설정 규칙을 실행 하는 경우, 지정 되지 않은 클레임 출력 클레임에서 삭제 됩니다.  
  
**한 숲 두고 클레임**  
  
한 숲 두고 클레임 숲 입력 클레임 보다 숲에 대 한 덜 보안 관심사를 제공 합니다. 클레임으로 숲 남길 수-경우에 해당 어떠한 보증도 변환 정책 장소에는 합니다. 숲 두고 클레임 변형의 일환으로 숲 속의 정의 되어 있지 않은 클레임 발급도 가능 합니다. 클레임 숲에서 신뢰 쉽게 설정입니다. 숲 입력 클레임 변형, 하 고 적절 한 정책을를 설정 해야 할 관리자 확인할 수 있습니다. 예를 들어, 관리자 정보 공개 되지 않도록 클레임 숨길 필요가 없는 경우 정책을 설정할 수 있습니다.  
  
**클레임 변환 규칙의 구문 오류**  
  
특정된 클레임 변환 정책 구문이 정확 하지 않은 규칙 들이 또는 다른 구문 또는 저장소 문제가 있을 경우 정책은 잘못 된 간주 됩니다. 이 앞에서 언급 한 기본 조건 다르게 처리 됩니다.  
  
Active Directory이 경우에 의도 알 수 없는 및 해당 신뢰 + 방향으로 이동 출력 어떠한 보증도 생성를 안전 모드로 전환 합니다. 문제를 해결 하려면 작업 관리자가 필요 합니다. LDAP 클레임 변환 정책을 편집 하는 데 사용 되는 경우 발생할 수 있습니다. Windows PowerShell cmdlet에 대 한 Active Directory 유효성 검사 구문 문제를 사용 하 여 정책을 쓸 수 없도록 적절 하 게 됩니다.  
  
## <a name="other-language-considerations"></a>다른 언어 고려  
  
1.  몇 가지 핵심 단어 또는 있는 (터미널 라고도 함)이 언어로 특수 문자를 가지가 있습니다. 여기에 표시 되는 [언어 터미널](Claims-Transformation-Rules-Language.md#BKMK_LT) 이 항목 뒷부분에서 표 합니다. 오류 메시지 명확성을 위해이 터미널에 태그를 사용 합니다.  
  
2.  터미널은 문자열 리터럴로 때때로 사용할 수 있습니다. 그러나 이러한 사용 언어 정의 충돌할 하거나 의도 하지 않은 결과 합니다. 이러한 종류의 사용 현황 권장 하지 않습니다.  
  
3.  규칙 작업을 수행할 수 없습니다 있는 형식 변환 클레임 값을 하 고 이러한 규칙 작업이 포함 된 규칙 집합 잘못 된 것으로 간주 됩니다. 런타임 오류가 발생 하면 및 출력 어떠한 보증도 생성 됩니다.  
  
4.  규칙 동작 규칙의 조건이 목록 선택 부분에 사용 하지 않는 식별자를 가리키는 경우 사용이 잘못 되었습니다. 이 구문을 오류가 발생 합니다.  
  
    **예: 잘못 식별자 참조**  
    다음 규칙 규칙 작업에 사용 되는 잘못 식별자를 보여 줍니다.  
  
    ```  
    C1:[] => Issue (claim = C2);  
    ```  
  
## <a name="sample-transformation-rules"></a>샘플 변환 규칙  
  
-   **특정 종류의 모든 클레임 허용**  
  
    정확한 유형  
  
    ```  
    C1:[type=="XYZ"] => Issue (claim = C1);  
    ```  
  
    Regex 사용  
  
    ```  
    C1: [type =~ "XYZ*"] => Issue (claim = C1);  
    ```  
  
-   **클레임은 특정 유형의 허용 안 함**  
    정확한 유형  
  
    ```  
    C1:[type != "XYZ"] => Issue (claim=C1);  
    ```  
  
    Regex 사용  
  
    ```  
    C1:[Type !~ "XYZ?"] => Issue (claim=C1);  
    ```  
  
## <a name="examples-of-rules-parser-errors"></a>구문 분석기 오류가 규칙의 예로  
클레임 변환 규칙 구문 오류 검사를 사용자 지정 파서에서 구문 분석 됩니다. 이 파서 Active Directory에 규칙 저장 하기 전에 Windows PowerShell cmdlet 관련된 하 여 실행 됩니다. 콘솔에 인쇄 되어 있음 오류 구문을 오류를 포함 한 규칙을 분석 합니다. 또한 도메인 컨트롤러 규칙 청구 변환에 대 한 사용 하기 전에 파서는 실행 하 고 오류 이벤트 로그에 기록 될 (이벤트 로그 번호를 추가).  
  
이 섹션 파서에서 생성 하는 오류 잘못 구문 및 해당 구문을으로 작성 된 규칙의 몇 가지 예를 보여 줍니다.  
  
1.  예:  
  
    ```  
    c1;[]=>Issue(claim=c1);  
    ```  
  
    이 이때에는으로 대신 사용된 잘못 세미콜론 있습니다.   
    **오류 메시지:**  
    *POLICY0002: 정책 데이터 분석할 수 없습니다.*  
    *줄 번호: 월 1 일 열 번호: 2 일 오류 토큰:; 합니다. 선: ' c 1. = > Issue(claim=c1);' 합니다.*  
    *구문 분석 오류가 발생: ' POLICY0030: 구문 오류, 예기치 않은 ','를 다음 중 하나를 필요: ':'.'*  
  
2.  예:  
  
    ```  
    c1:[]=>Issue(claim=c2);  
    ```  
  
    여기에서 식별자 태그 복사 발급 정책에서 정의 되지 않습니다.   
    **오류 메시지**:   
    *POLICY0011: 클레임 규칙의 조건이 일치 상태 태그는 CopyIssuanceStatement에 지정 된: 'c 2' 합니다.*  
  
3.  예:  
  
    ```  
    c1:[type=="x1", value=="1", valuetype=="bool"]=>Issue(claim=c1)  
    ```  
  
    "bool" 언어에서 터미널 아니며 올바르지 값 아닙니다. 유효한 터미널 다음과 같은 오류 메시지가 표시 됩니다.   
    **오류 메시지:**  
    *POLICY0002: 정책 데이터 분석할 수 없습니다.*  
    줄 번호: 월 1 일 열 번호: 39, 오류 토큰: "bool" 합니다. 선: ' c 1: [유형 값 "x1" = = = = "1," 값 = = "bool"] = > Issue(claim=c1);' 합니다.   
    *구문 분석 오류가 발생: ' POLICY0030: 구문 오류, 예기치 않은 '문자열'를 다음 중 하나를 기대: 'INT64_TYPE' 'UINT64_TYPE' 'STRING_TYPE' 'BOOLEAN_TYPE' '식별자'*  
  
4.  예:  
  
    ```  
    c1:[type=="x1", value==1, valuetype=="boolean"]=>Issue(claim=c1);  
    ```  
  
    숫자 **1** 이 예제 언어에서 올바른 토큰 아니며 등 사용 현황 일치 하는 조건에서 허용 되지 않습니다. 큰따옴표 문자열로를 포함 하는 있습니다.   
    **오류 메시지:**  
    *POLICY0002: 정책 데이터 분석할 수 없습니다.*  
    *줄 번호: 월 1 일 열 수: 23, 오류 토큰: 1. 선: ' c 1: [유형 값 "x1" = = = = 1 값 = = "bool"] = > Issue(claim=c1);' 합니다. **구문 분석 오류가 발생: ' POLICY0029: 예기치 않은 입력 합니다.*  
  
5.  예:  
  
    ```  
    c1:[type == "x1", value == "1", valuetype == "boolean"] =>   
  
         Issue(type = c1.type, value="0", valuetype == "boolean");  
    ```  
  
    이 이때 두 번 등호 (=) 단일 등호 (=) 대신 사용 합니다.   
    **오류 메시지:**  
    *POLICY0002: 정책 데이터 분석할 수 없습니다.*  
    *줄 번호: 월 1 일 열 번호: 91, 오류 토큰: = = 합니다. 선: ' c 1: [유형 값 "x1" = = = = "1"*  
    *값 = = "boolean"] = > 문제 (type=c1.type, 가치 = "0," 값 = = "boolean");' 합니다.*  
    *구문 분석 오류가 발생: ' POLICY0030: 구문 오류, 예기치 않게 '= ='를 다음 중 하나를 기대: '='*  
  
6.  예:  
  
    ```  
    c1:[type=="x1", value=="boolean", valuetype=="string"] =>   
  
          Issue(type=c1.type, value=c1.value, valuetype = "string");  
    ```  
  
    이 이때 구문적 및 의미가 정확있지 않습니다. 그러나를 사용 하 여 "boolean" 혼동에 바인딩된 문자열 값을 하 고 사용 하지 않아야 합니다. 에서 설명한 대로 언어 터미널 사용 하 여 가능한 클레임 값을 사용 하지 않아야 합니다.  
  
## <a name="BKMK_LT"></a>언어 터미널  
다음 표에서 터미널 문자열와 연결 된 언어 터미널 클레임 변환 규칙 언어에 사용 되는 완전 집합이 합니다. 이러한 정의 대/소문자 구분 UTF-16 문자열을 사용 합니다.  
  
|문자열|터미널|  
|----------|------------|  
|"=>"|의미|  
|";"|세미콜론|  
|":"|으로|  
|","|쉼표|  
|"."|점|  
|"["|O_SQ_BRACKET|  
|"]"|C_SQ_BRACKET|  
|"("|O_BRACKET|  
|")"|C_BRACKET|  
|"=="|EQ|  
|"!="|NEQ|  
|"=~"|REGEXP_MATCH|  
|"!~"|REGEXP_NOT_MATCH|  
|"="|지정|  
|"&&"|하 고|  
|"문제"|문제|  
|"입력"|입력|  
|"값"|값|  
|"값"|VALUE_TYPE|  
|"개인"|클레임|  
|"[_A-Za-z][_A-Za-z0-9]*"|식별자|  
|"\\"[^\\"\n]*\\""|문자열|  
|"uint64"|UINT64_TYPE|  
|"i n t 64"|INT64_TYPE|  
|"문자열"|STRING_TYPE|  
|"boolean"|BOOLEAN_TYPE|  
  
## <a name="language-syntax"></a>언어  
다음 청구 변환 규칙 언어 ABNF 양식에서 지정 됩니다. 이 정의 여기에 정의 된 ABNF 요소 뿐 아니라 이전 테이블에 지정 된 터미널 사용 합니다. 규칙 u t F 16에서 인코딩된 해야 하 고 문자열 비교도 소문자 처리 합니다.  
  
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
  


