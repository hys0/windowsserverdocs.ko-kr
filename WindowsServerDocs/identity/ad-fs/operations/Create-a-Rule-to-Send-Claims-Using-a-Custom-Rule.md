---
ms.assetid: 38eb3726-e97b-484e-9926-67e8a046b0c5
title: "사용 하 여 사용자 지정 규칙 클레임 보낼 규칙 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f0eef89e651585d48ba87d14bc782efa49087669
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-send-claims-using-a-custom-rule"></a>사용 하 여 사용자 지정 규칙 클레임 보낼 규칙 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

사용 하 여는 **클레임 사용자 지정 규칙을 사용 하 여 보낼** AD FS(Active Directory Federation Services)에 템플릿으로 표준 규칙 템플릿 조직의 요구 사항을 충족 하지 않는 경우에 대 한 사용자 지정 클레임 규칙 만들 수 있습니다. 사용자 지정 클레임 규칙 클레임 규칙 언어로 작성 하 고 다음에 복사 해야는 **사용자 지정 규칙** 텍스트 상자 규칙 집합에 사용할 수 있습니다. 고급 규칙에 대 한 구문을 구성에 대 한 내용은 [클레임 규칙 언어의 The 역할](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md)합니다.  
  
다음 절차 규칙을 만들려면 클레임 snap\에서 AD FS 관리를 사용 하 여 사용할 수 있습니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 최소 요구 사항을 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.



## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>통과 또는 필요로 하 파티 신뢰 Windows Server 2016에 들어오는 클레임 필터링을 규칙을 만들려면 

1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **파티 신뢰 의존**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **클레임 발급 정책 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **클레임 사용자 지정 규칙을 사용 하 여 보낼** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom3.PNG)   
  
6.  에 **구성 규칙** 페이지의 **클레임 규칙 이름**,이 규칙의 표시 이름을 입력 합니다. 아래에서 **사용자 지정 규칙**입력 하거나 붙여이 규칙에 대 한 원하는 클레임 규칙 언어 구문 합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom4.PNG)     

7.  클릭 **완료**합니다.  
  
8.  **편집 클레임 규칙** 대화 상자를 클릭 **확인** 규칙을 저장 해야 합니다.   
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>통과 또는 Windows Server 2016에 클레임 공급자 신뢰를 수신 클레임 필터링을 규칙을 만들려면 
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **클레임 공급자 신뢰**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **편집 클레임 규칙**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  에 **편집 클레임 규칙** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **클레임 사용자 지정 규칙을 사용 하 여 보낼** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom3.PNG)   
  
6.  에 **구성 규칙** 페이지의 **클레임 규칙 이름**,이 규칙의 표시 이름을 입력 합니다. 아래에서 **사용자 지정 규칙**입력 하거나 붙여이 규칙에 대 한 원하는 클레임 규칙 언어 구문 합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom4.PNG)     

7.  클릭 **완료**합니다.  
  
8.  **편집 클레임 규칙** 대화 상자를 클릭 **확인** 규칙을 저장 해야 합니다.   

















   
  
## <a name="to-create-a-rule-to-send-claims-by-using-a-custom-claim-in-windows-server-2012-r2"></a>Windows Server 2012 r 2에 사용자 지정 클레임을 사용 하 여 클레임 보내는 규칙을 만들려면 
  
1.  서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래에서 **광고 FS\\Trust 관계**, 클릭 **클레임 공급자 신뢰** 또는 **의존 파티 신뢰**, 클릭 한 다음이 규칙 만들려는 목록에 특정 신뢰 하 고 합니다.  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **편집 클레임 규칙**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  에 **클레임 규칙 편집** 대화 상자를 선택 하 고 편집 하는 어떤 규칙을 설정 하 고 신뢰에 따라 달라 집니다는 다음과 같은 탭 만들려는이 규칙을 클릭 한 다음 **규칙 추가** 해당 규칙 집합와 연결 된 규칙 마법사를 시작 합니다.  
  
    -   **승인 변환 규칙**  
  
    -   **발급 변환 규칙**  
  
    -   **발급 승인 규칙**  
  
    -   **위임 인증 규칙**  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
  
5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **클레임 사용자 지정 규칙을 사용 하 여 보낼** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom1.PNG)   
  
6.  에 **구성 규칙** 페이지의 **클레임 규칙 이름**,이 규칙의 표시 이름을 입력 합니다. 아래에서 **사용자 지정 규칙**입력 하거나 붙여이 규칙에 대 한 원하는 클레임 규칙 언어 구문 합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom2.PNG)     

7.  클릭 **완료**합니다.  
  
8.  **편집 클레임 규칙** 대화 상자를 클릭 **확인** 규칙을 저장 해야 합니다.  

## <a name="additional-references"></a>추가 참조 
[클레임은 규칙 구성](Configure-Claim-Rules.md)  
 
[검사: 신뢰 파티 보안에 대 한 청구 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  

[청구 공급자에 대 한 청구 규칙 만들기 신뢰 검사:](https://technet.microsoft.com/library/ee913564.aspx)  
  
[승인 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임은 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
