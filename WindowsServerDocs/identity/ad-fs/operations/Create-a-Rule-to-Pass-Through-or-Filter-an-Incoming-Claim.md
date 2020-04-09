---
ms.assetid: 6127963f-71b2-4d8f-8b53-7c525bf06521
title: 통과 또는 들어오는 클레임을 필터링 하는 규칙 만들기
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: fb885d8b822faf4bd5ee82ad70c59b99678a58e9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816836"
---
# <a name="create-a-rule-to-pass-through-or-filter-an-incoming-claim"></a>통과 또는 들어오는 클레임을 필터링 하는 규칙 만들기

Active Directory Federation Services \(AD FS\)에서 들어오는 클레임 통과 또는 필터링 규칙 템플릿을 사용 하 여 선택한 클레임 유형으로 들어오는 클레임을 모두 전달할 수 있습니다. 선택한 클레임 유형의 들어오는 클레임 값을 필터링할 수도 있습니다. 예를 들어, 이 규칙 템플릿을 사용하여 모든 들어오는 클레임을 전송하는 규칙을 만들 수 있습니다. 또한이 규칙을 사용 하 여 사용자 계정 이름 \(UPN\) @fabrikam으로 끝나는 클레임만 보낼 수 있습니다.  
  
다음 절차를 사용 하 여 AD FS 관리 스냅인을 사용 하 여 클레임 규칙을 만들려면\-에 있습니다.  
  
이 절차를 완료하려면 최소한 로컬 컴퓨터의 **Administrators** 구성원 자격 또는 동급의 권한이 필요합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>통과 또는 들어오는 클레임을 신뢰 당사자 트러스트 Windows Server 2016에서 필터링 하는 규칙을 만들려면 

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **신뢰 당사자 트러스트**합니다. 
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG) 만들기 ![  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 발급 정책 편집**합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG) 만들기 ![   
  
4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG) 만들기 ![    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **통과 또는 들어오는 클레임 필터링** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG) 만들기 ![    

6.  에 **규칙 구성** 페이지 **클레임 규칙 이름** 에이 규칙에 대 한 표시 이름을 입력 **들어오는 클레임 유형** 클레임 유형을 목록에서 선택 하 고 조직의 요구에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 클레임 값 통과**  
  
    -   **특정 클레임 값만 통과**  
  
    -   **특정 전자 메일 접미사 값과 일치 하는 클레임 값만 통과**  
  
    -   **특정 값으로 시작 하는 클레임 값만 통과**  
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG) 만들기 ![    

7.  클릭 하 고 **마침** 단추입니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>통과 또는 Windows Server 2016에서 클레임 공급자 트러스트에 들어오는 클레임을 필터링 하는 규칙을 만들려면 
  
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **클레임 공급자 트러스트**합니다. 
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG) 만들기 ![  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG) 만들기 ![   
  
4.  에 **클레임 규칙 편집** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG) 만들기 ![    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **통과 또는 들어오는 클레임 필터링** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG) 만들기 ![    

6.  에 **규칙 구성** 페이지 **클레임 규칙 이름** 에이 규칙에 대 한 표시 이름을 입력 **들어오는 클레임 유형** 클레임 유형을 목록에서 선택 하 고 조직의 요구에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 클레임 값 통과**  
  
    -   **특정 클레임 값만 통과**  
  
    -   **특정 전자 메일 접미사 값과 일치 하는 클레임 값만 통과**  
  
    -   **특정 값으로 시작 하는 클레임 값만 통과**  
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG) 만들기 ![    

7.  클릭 하 고 **마침** 단추입니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.  

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-in-windows-server-2012-r2"></a>통과 또는 Windows Server 2012 r 2에서 들어오는 클레임을 필터링 하는 규칙을 만들려면

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **AD FS FSAD\\트러스트 관계**, 클릭 **클레임 공급자 트러스트** 또는 **신뢰 당사자 트러스트**, 이 규칙을 만드는 목록에서 특정 트러스트를 클릭 하 고 있습니다.  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 만들기 ![   
  
4.  에 **클레임 규칙 편집** 대화 상자는 다음과 같은 탭 하나를 선택, 편집 하 고 규칙 집합을 신뢰에 따라,이 규칙을 만들려고 할 및 클릭 **규칙 추가** 해당 규칙 집합에 연관 된 규칙 마법사를 시작 합니다.  
  
    -   **수락 변환 규칙**  
  
    -   **발급 변환 규칙**  
  
    -   **발급 권한 부여 규칙**  
  
    -   **위임 권한 부여 규칙**  
규칙](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) 만들기 ![    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **통과 또는 들어오는 클레임 필터링** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG) 만들기 ![    

6.  에 **규칙 구성** 페이지 **클레임 규칙 이름** 에이 규칙에 대 한 표시 이름을 입력 **들어오는 클레임 유형** 클레임 유형을 목록에서 선택 하 고 조직의 요구에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 클레임 값 통과**  
  
    -   **특정 클레임 값만 통과**  
  
    -   **특정 전자 메일 접미사 값과 일치 하는 클레임 값만 통과**  
  
    -   **특정 값으로 시작 하는 클레임 값만 통과**  
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule8.PNG) 만들기 ![    

7.  클릭 하 고 **마침** 단추입니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.  



  
## <a name="additional-references"></a>추가 참조  
[클레임 규칙 구성](Configure-Claim-Rules.md)  
  
[통과 또는 필터 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)  
  
[클레임의 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
  
