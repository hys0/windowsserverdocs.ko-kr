---
ms.assetid: 0039fbbb-b981-4526-a550-f3456ff27635
title: 들어오는 클레임 변환 규칙 만들기
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bda071be6668710361205643125fc8ad44246012
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453017"
---
# <a name="create-a-rule-to-send-an-ad-fs-1x-compatible-claim"></a>AD FS 1.x 호환 클레임을 보내도록 규칙 만들기

Active Directory Federation Services을 사용 하는 경우에서 \(AD FS\) AD FS 1.0을 실행 하는 페더레이션 서버에서 수신 됩니다 문제 클레임 \(Windows Server 2003 R2\) 또는 AD FS 1.1 \(Windows Server 2008 또는 Windows Server 2008 R2\), 다음을 수행 해야 합니다.  
  
-   UPN, 전자 메일, 또는 일반 이름 형식으로 이름 ID 클레임 형식을 전송할 규칙을 만듭니다.  
  
-   전송 된 다른 모든 클레임 다음 클레임 형식 중 하나가 있어야 합니다.  
  
    -   AD FS 1입니다. *x* 전자 메일 주소  
  
    -   AD FS 1.*x* UPN  
  
    -   일반 이름  
  
    -   그룹  
  
    -   시작 하는 다른 모든 클레임 유형을 https://schemas.xmlsoap.org/claims/와 같은 https://schemas.xmlsoap.org/claims/EmployeeID  
  
조직의 요구에 따라 AD FS 1를 만들려면 다음 절차 중 하나를 사용 합니다. *x* 호환 NameID 클레임:  
  
-   이 규칙 문제는 AD FS 1.x 이름 ID 클레임을 사용 하 여 **통과 또는 필터링 된 들어오는 클레임 규칙 템플릿**  
  
-   이 규칙 문제는 AD FS 1.x 이름 ID 클레임을 사용 하는 **는 들어오는 클레임 규칙 템플릿을 변환**합니다. AD FS 1와 작동 하는 새 클레임 형식을 기존 클레임 유형을 변경 하려는 경우에이 규칙 서식 파일을 사용할 수 있습니다.  *x* 클레임입니다.  
  
> [!NOTE]  
> 예상 대로 작동 하도록이 규칙에 대 한 신뢰 당사자 트러스트 또는이 규칙을 만들려는 클레임 공급자 트러스트에 사용 하도록 구성 되었는지 확인 합니다 **AD FS 1.0 및 1.1 프로필**합니다. 

## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>AD FS 1을 실행 하는 규칙 만들기 *x* 이름 ID 클레임은 통과 사용 하 여 또는 필터링 된 신뢰 당사자 트러스트에 Windows Server 2016에서 들어오는 클레임 규칙 템플릿을 

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **신뢰 당사자 트러스트**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 발급 정책 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **통과 또는 들어오는 클레임 필터링** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  에 **규칙 구성** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **들어오는 클레임 유형**, 선택, **이름 ID** 목록에 있습니다.  
  
8.  **들어오는 이름 ID 형식**, 다음 AD FS 1 중 하나를 선택 합니다. *x*\-호환 되는 클레임 형식 목록에서:  
  
    -   **UPN**  
  
    -   **E\-메일**  
  
    -   **일반 이름**  
  
9. 조직의 필요에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 클레임 값 통과**  
  
    -   **특정 클레임 값만 통과**  
  
    -   **특정 메일 접미사 값과 일치 하는 클레임 값만 통과**  
  
    -   **특정 값으로 시작 하는 클레임 값만 통과**  
![규칙 만들기](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. 클릭 **마침**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  

  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>AD FS 1을 실행 하는 규칙 만들기 *x* 이름 ID 클레임은 통과 사용 하 여 또는 필터링 Windows Server 2016에서 클레임 공급자 트러스트에 들어오는 클레임 규칙 템플릿을 
  
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **클레임 공급자 트러스트**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  에 **클레임 규칙 편집** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **통과 또는 들어오는 클레임 필터링** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  에 **규칙 구성** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **들어오는 클레임 유형**, 선택, **이름 ID** 목록에 있습니다.  
  
8.  **들어오는 이름 ID 형식**, 다음 AD FS 1 중 하나를 선택 합니다. *x*\-호환 되는 클레임 형식 목록에서:  
  
    -   **UPN**  
  
    -   **E\-메일**  
  
    -   **일반 이름**  
  
9. 조직의 필요에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 클레임 값 통과**  
  
    -   **특정 클레임 값만 통과**  
  
    -   **특정 메일 접미사 값과 일치 하는 클레임 값만 통과**  
  
    -   **특정 값으로 시작 하는 클레임 값만 통과**  
![규칙 만들기](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)

10. 클릭 **마침**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  


## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>신뢰 당사자 트러스트에 Windows Server 2016에서 들어오는 클레임 변환 규칙을 만들려면 

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **신뢰 당사자 트러스트**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 발급 정책 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)
  
4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **들어오는 클레임 변환** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)

6.  에 **규칙 구성** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **들어오는 클레임 유형**, 를 목록에서 변환 하려는 경우 들어오는 클레임의 유형을 선택 합니다.  
  
8.  **보내는 클레임 유형**, 선택, **이름 ID** 목록에 있습니다.  
  
9. **보내는 이름 ID 형식**, 다음 AD FS 1 중 하나를 선택 합니다. *x*\-호환 되는 클레임 형식 목록에서:  
  
    -   **UPN**  
  
    -   **E\-메일**  
  
    -   **일반 이름**  
  
10. 조직의 필요에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 클레임 값 통과**  
  
    -   **들어오는 클레임 값을 다른 나가는 클레임 값으로 바꿉니다.**  
  
    -   **들어오는 전자 바꾸기\-접미사를 클레임 새 전자 메일\-메일 접미사**  
![규칙 만들기](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)

11. 클릭 **마침**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  

  


## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016에서 클레임 공급자 트러스트에 들어오는 클레임 변환 규칙을 만들려면 
  
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **클레임 공급자 트러스트**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  에 **클레임 규칙 편집** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **들어오는 클레임 변환** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  에 **규칙 구성** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **들어오는 클레임 유형**, 를 목록에서 변환 하려는 경우 들어오는 클레임의 유형을 선택 합니다.  
  
8.  **보내는 클레임 유형**, 선택, **이름 ID** 목록에 있습니다.  
  
9. **보내는 이름 ID 형식**, 다음 AD FS 1 중 하나를 선택 합니다. *x*\-호환 되는 클레임 형식 목록에서:  
  
    -   **UPN**  
  
    -   **E\-메일**  
  
    -   **일반 이름**  
  
10. 조직의 필요에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 클레임 값 통과**  
  
    -   **들어오는 클레임 값을 다른 나가는 클레임 값으로 바꿉니다.**  
  
    -   **들어오는 전자 바꾸기\-접미사를 클레임 새 전자 메일\-메일 접미사**  
![규칙 만들기](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. 클릭 **마침**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  













  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-windows-server-2012-r2"></a>AD FS 1을 실행 하는 규칙 만들기 *x* 이름 ID 클레임은 통과 사용 하 여 또는 필터링 Windows Server 2012 R2에서 들어오는 클레임 규칙 템플릿을
  
1.  서버 관리자에서 클릭 **도구**, 를 클릭 하 고 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **AD FS\\트러스트 관계**, 클릭 **클레임 공급자 트러스트** 또는 **신뢰 당사자 트러스트**, 이 규칙을 만드는 목록에서 특정 트러스트를 클릭 하 고 있습니다.  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  에 **클레임 규칙 편집** 대화 상자는 다음과 같은 탭 하나를 선택, 편집 하 고 규칙 집합을 신뢰에 따라,이 규칙을 만들려고 할 및 클릭 **규칙 추가** 해당 규칙 집합에 연관 된 규칙 마법사를 시작 합니다.  
  
    -   **수용 변환 규칙**  
  
    -   **발급 변환 규칙**  
  
    -   **발급 권한 부여 규칙**  
  
    -   **위임 권한 부여 규칙**  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **통과 또는 들어오는 클레임 필터링** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG)  
  
6.  에 **규칙 구성** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **들어오는 클레임 유형**, 선택, **이름 ID** 목록에 있습니다.  
  
8.  **들어오는 이름 ID 형식**, 다음 AD FS 1 중 하나를 선택 합니다. *x*\-호환 되는 클레임 형식 목록에서:  
  
    -   **UPN**  
  
    -   **E\-메일**  
  
    -   **일반 이름**  
  
9. 조직의 필요에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 클레임 값 통과**  
  
    -   **특정 클레임 값만 통과**  
  
    -   **특정 메일 접미사 값과 일치 하는 클레임 값만 통과**  
  
    -   **특정 값으로 시작 하는 클레임 값만 통과**  
![규칙 만들기](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs1.PNG)

10. 클릭 **마침**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  

  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>AD FS 1을 실행 하는 규칙 만들기 *x* Windows Server 2012 R2에는 들어오는 클레임 규칙 템플릿 변환을 사용 하는 이름 ID 클레임  
  
1.  서버 관리자에서 클릭 **도구**, 를 클릭 하 고 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **AD FS\\트러스트 관계**, 클릭 **클레임 공급자 트러스트** 또는 **신뢰 당사자 트러스트**, 이 규칙을 만드는 목록에서 특정 트러스트를 클릭 하 고 있습니다.  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  에 **클레임 규칙 편집** 대화 상자에서 하나를 선택 했는지에 따라 편집 하는 규칙 수를 설정 하는 신뢰 하는 다음과 같은 탭이이 규칙을 만들고 연결할 클릭 **규칙 추가** 해당 규칙 집합에 연관 된 규칙 마법사를 시작 합니다.  
  
    -   **수용 변환 규칙**  
  
    -   **발급 변환 규칙**  
  
    -   **발급 권한 부여 규칙**  
  
    -   **위임 권한 부여 규칙**  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
  
5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **들어오는 클레임 변환** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform1.PNG)   
  
6.  에 **규칙 구성** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **들어오는 클레임 유형**, 를 목록에서 변환 하려는 경우 들어오는 클레임의 유형을 선택 합니다.  
  
8.  **보내는 클레임 유형**, 선택, **이름 ID** 목록에 있습니다.  
  
9. **보내는 이름 ID 형식**, 다음 AD FS 1 중 하나를 선택 합니다. *x*\-호환 되는 클레임 형식 목록에서:  
  
    -   **UPN**  
  
    -   **E\-메일**  
  
    -   **일반 이름**  
  
10. 조직의 필요에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 클레임 값 통과**  
  
    -   **들어오는 클레임 값을 다른 나가는 클레임 값으로 바꿉니다.**  
  
    -   **들어오는 전자 바꾸기\-접미사를 클레임 새 전자 메일\-메일 접미사**  
![규칙 만들기](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs2.PNG)    

11. 클릭 **마침**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  

## <a name="additional-references"></a>추가 참조 
[클레임 규칙 구성](Configure-Claim-Rules.md)  
 
[검사 목록: 신뢰 당사자 트러스트를 위한 클레임 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  

[검사 목록: 클레임 공급자 트러스트를 위한 클레임 규칙 만들기](https://technet.microsoft.com/library/ee913564.aspx)  
  
[권한 부여 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임의 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
