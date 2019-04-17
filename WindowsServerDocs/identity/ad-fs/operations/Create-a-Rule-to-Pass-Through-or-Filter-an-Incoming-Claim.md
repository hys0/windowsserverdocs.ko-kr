---
ms.assetid: 6127963f-71b2-4d8f-8b53-7c525bf06521
title: "규칙을 통해 전달 하거나 수신 클레임 필터링 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 50f50cd4e096b107a2b58ac05328ff8ed413f2dc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-pass-through-or-filter-an-incoming-claim"></a>규칙을 통해 전달 하거나 수신 클레임 필터링 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

통과 또는 전자 들어오는 주장 규칙 템플릿 필터를 사용 하 여 Active Directory Federation Services \(AD FS\)의, 선택한 클레임 형식을 사용 하 여 모든 들어오는 클레임 통해 전달할 수 있습니다. 선택한 클레임 형식의 들어오는 클레임 값 필터링 할 수 있습니다. 예를 들어 모든 들어오는 그룹 클레임 보낼 규칙을 만들려면이 규칙 템플릿을 사용할 수 있습니다. 이 규칙와 함께 종료 하는 계정 이름 \(UPN\) 클레임 사용자만을 보내려면 사용할 수도 @fabrikam합니다.  
  
다음 절차 규칙을 만들려면 클레임 AD FS 관리 snap\에서 사용할 수 있습니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>통과 또는 필요로 하 파티 신뢰 Windows Server 2016에 들어오는 클레임 필터링을 규칙을 만들려면 

1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **파티 신뢰 의존**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **클레임 발급 정책 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **통과 또는 필터 수신 클레임** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  에 **구성 규칙** 페이지에서 **클레임 규칙 이름** 이 규칙의 표시 이름을 입력 **수신 클레임 유형** 목록 클레임 종류를 선택한 다음 조직의 요구에 따라 다음 옵션 중 하나를 선택:  
  
    -   **모든 통과 값 주장**  
  
    -   **특정 주장 값만 통과합니다**  
  
    -   **만 클레임에 맞는 값은 특정 메일이 접미사 값을 통해 전달**  
  
    -   **클레임은 값 값을 시작 하는 통과합니다**  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  클릭 하 고 **완료** 단추.  
  
8.  **편집 클레임 규칙** 대화 상자를 클릭 **확인** 규칙을 저장 해야 합니다.
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>통과 또는 Windows Server 2016에 클레임 공급자 신뢰를 수신 클레임 필터링을 규칙을 만들려면 
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **클레임 공급자 신뢰**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **편집 클레임 규칙**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  에 **편집 클레임 규칙** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **통과 또는 필터 수신 클레임** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  에 **구성 규칙** 페이지에서 **클레임 규칙 이름** 이 규칙의 표시 이름을 입력 **수신 클레임 유형** 목록 클레임 종류를 선택한 다음 조직의 요구에 따라 다음 옵션 중 하나를 선택:  
  
    -   **모든 통과 값 주장**  
  
    -   **특정 주장 값만 통과합니다**  
  
    -   **만 클레임에 맞는 값은 특정 메일이 접미사 값을 통해 전달**  
  
    -   **클레임은 값 값을 시작 하는 통과합니다**  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  클릭 하 고 **완료** 단추.  
  
8.  **편집 클레임 규칙** 대화 상자를 클릭 **확인** 규칙을 저장 해야 합니다.  

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-in-windows-server-2012-r2"></a>통과 또는 Windows Server 2012 r 2에서 수신 클레임 필터링을 규칙을 만들려면

1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래에서 **광고 FSAD FS\\Trust 관계**, 클릭 **클레임 공급자 신뢰** 또는 **의존 파티 신뢰**, 클릭 한 다음이 규칙 만들려는 목록에 특정 신뢰 하 고 합니다.  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **편집 클레임 규칙**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)   
  
4.  에 **클레임 규칙 편집** 대화 상자에서 하나 다음 탭, 규칙을 설정 및 편집 하는 보안 따라를 만들려면이 규칙을 선택한 다음 **규칙 추가** 해당 규칙 집합와 연결 된 규칙 마법사를 시작 합니다.  
  
    -   **승인 변환 규칙**  
  
    -   **발급 변환 규칙**  
  
    -   **발급 승인 규칙**  
  
    -   **위임 인증 규칙**  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **통과 또는 필터 수신 클레임** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG)    

6.  에 **구성 규칙** 페이지에서 **클레임 규칙 이름** 이 규칙의 표시 이름을 입력 **수신 클레임 유형** 목록 클레임 종류를 선택한 다음 조직의 요구에 따라 다음 옵션 중 하나를 선택:  
  
    -   **모든 통과 값 주장**  
  
    -   **특정 주장 값만 통과합니다**  
  
    -   **만 클레임에 맞는 값은 특정 메일이 접미사 값을 통해 전달**  
  
    -   **클레임은 값 값을 시작 하는 통과합니다**  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule8.PNG)    

7.  클릭 하 고 **완료** 단추.  
  
8.  **편집 클레임 규칙** 대화 상자를 클릭 **확인** 규칙을 저장 해야 합니다.  



  
## <a name="additional-references"></a>추가 참조  
[클레임은 규칙 구성](Configure-Claim-Rules.md)  
  
[한 통과 사용 하는 경우 또는 필터 클레임 규칙](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)  
  
[클레임 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임은 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
  
