---
ms.assetid: 0039fbbb-b981-4526-a550-f3456ff27635
title: "수신 클레임 변환할 규칙 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3745a0ab9d313223c611e58864dd6b4d747f0624
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="create-a-rule-to-send-an-ad-fs-1x-compatible-claim"></a>AD FS 1.x 호환 클레임 보내려면 규칙 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 r 2


Active Directory Federation Services을 사용 하는 경우에서를 발급 \(AD FS\) 주장 ADFS 1.0 실행 federation 서버에서 수신 되는 \ (Windows Server 2003 R2\) 또는 ADFS 1.1 \ (Windows Server 2008 또는 Windows Server 2008 R2\)에서 다음을 수행 해야 합니다.  
  
-   UPN, 메일 또는 일반 이름 형식으로 이름을 ID 클레임 형식을 보냅니다 규칙을 만듭니다.  
  
-   전송 된 모든 클레임 다음 클레임 종류 중 하나가 있어야 합니다.  
  
    -   ADFS 1입니다. *x* 메일 주소  
  
    -   ADFS 1입니다. *x* UPN  
  
    -   일반 이름  
  
    -   그룹  
  
    -   https://schemas.xmlsoap.org/claims/EmployeeID 등 https://schemas.xmlsoap.org/claims/로 시작 하는 다른 클레임 유형  
  
조직의 필요에 따라 ADFS 1 만드는 다음 절차 중 하나를 사용 합니다. *x* 호환 NameID 클레임:  
  
-   이 문제는 ADFS 1.x 이름 ID 클레임 사용 규칙의 **통과 또는 전자 들어오는 주장 규칙 템플릿 필터**  
  
-   이 문제는 ADFS 1.x 이름 ID 클레임 사용 규칙의 **는 들어오는 주장 규칙 템플릿을 변환**합니다. 이 규칙 템플릿을 ADFS 1 사용할 수 있는 새로운 클레임 형식으로 기존 클레임 유형을 변경 하려는 경우에 사용할 수 있습니다. *x* 청구 합니다.  
  
> [!NOTE]  
> 이 규칙 예상 대로 작동 되어 있는지 확인 신뢰 파티 신뢰 또는 클레임 공급자 신뢰 만들면이 규칙은 사용 하도록 구성는 **ADFS 1.0 및 1.1 프로필**합니다. 




## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>규칙을 만들려면 ADFS 1 실행할 수 있습니다. *x* 이름 ID를 통해 전달를 사용 하 여 주장 또는 필터 필요로 하 파티 신뢰 Windows Server 2016에 규칙 템플릿 들어오는 주장 

1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **파티 신뢰 의존**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **클레임 발급 정책 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **통과 또는 필터 수신 클레임** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  에 **구성 규칙** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **수신 클레임 유형**선택 **이름 ID** 목록에 있습니다.  
  
8.  **수신 이름 ID 형식**는 다음과 같은 ADFS 1 중 하나를 선택 합니다. *x*\-compatible 주장 목록에서 형식 있습니다.  
  
    -   **UPN**  
  
    -   **E\ 메일**  
  
    -   **일반 이름**  
  
9. 조직의 요구에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 통과 값 주장**  
  
    -   **특정 주장 값만 통과합니다**  
  
    -   **만 클레임에 맞는 값은 특정 메일이 접미사 값을 통해 전달**  
  
    -   **클레임은 값 값을 시작 하는 통과합니다**  
![규칙 만들기](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. 클릭 **완료**, 클릭 한 다음 **확인** 규칙 저장 합니다.  

  
## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>규칙을 만들려면 ADFS 1 실행할 수 있습니다. *x* 이름을 ID 통해 전달를 사용 하 여 주장 또는 Windows Server 2016에 클레임 공급자 신뢰에 규칙 템플릿 들어오는 주장 필터링 
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **클레임 공급자 신뢰**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **편집 클레임 규칙**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  에 **편집 클레임 규칙** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **통과 또는 필터 수신 클레임** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  에 **구성 규칙** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **수신 클레임 유형**선택 **이름 ID** 목록에 있습니다.  
  
8.  **수신 이름 ID 형식**는 다음과 같은 ADFS 1 중 하나를 선택 합니다. *x*\-compatible 주장 목록에서 형식 있습니다.  
  
    -   **UPN**  
  
    -   **E\ 메일**  
  
    -   **일반 이름**  
  
9. 조직의 요구에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 통과 값 주장**  
  
    -   **특정 주장 값만 통과합니다**  
  
    -   **만 클레임에 맞는 값은 특정 메일이 접미사 값을 통해 전달**  
  
    -   **클레임은 값 값을 시작 하는 통과합니다**  
![규칙 만들기](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. 클릭 **완료**, 클릭 한 다음 **확인** 규칙 저장 합니다.  

  

## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>순식간에 의존 파티 신뢰 Windows Server 2016에 들어오는 클레임 규칙을 만들려면 

1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **파티 신뢰 의존**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **클레임 발급 정책 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **수신 클레임 변환** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  에 **구성 규칙** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **수신 클레임 유형**를 목록에서 변형할 들어오는 클레임 유형을 선택 합니다.  
  
8.  **보내는 클레임 유형**선택 **이름을 ID** 목록에 있습니다.  
  
9. **보내는 이름 ID 형식**는 다음과 같은 ADFS 1 중 하나를 선택 합니다. *x*\-compatible 주장 목록에서 형식 있습니다.  
  
    -   **UPN**  
  
    -   **E\ 메일**  
  
    -   **일반 이름**  
  
10. 조직의 요구에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 통과 값 주장**  
  
    -   **들어오는 클레임 값을 바꿉니다 다른 보내는 클레임**  
  
    -   **새 메일 e\ 접미사 들어오는 e\ 메일 접미사 클레임 교체**  
![규칙 만들기](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. 클릭 **완료**, 클릭 한 다음 **확인** 규칙 저장 합니다.  

  


## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016에 클레임 공급자 신뢰를 수신 클레임 변환할 규칙을 만들려면 
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **클레임 공급자 신뢰**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **편집 클레임 규칙**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  에 **편집 클레임 규칙** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **수신 클레임 변환** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  에 **구성 규칙** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **수신 클레임 유형**를 목록에서 변형할 들어오는 클레임 유형을 선택 합니다.  
  
8.  **보내는 클레임 유형**선택 **이름을 ID** 목록에 있습니다.  
  
9. **보내는 이름 ID 형식**는 다음과 같은 ADFS 1 중 하나를 선택 합니다. *x*\-compatible 주장 목록에서 형식 있습니다.  
  
    -   **UPN**  
  
    -   **E\ 메일**  
  
    -   **일반 이름**  
  
10. 조직의 요구에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 통과 값 주장**  
  
    -   **들어오는 클레임 값을 바꿉니다 다른 보내는 클레임**  
  
    -   **새 메일 e\ 접미사 들어오는 e\ 메일 접미사 클레임 교체**  
![규칙 만들기](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. 클릭 **완료**, 클릭 한 다음 **확인** 규칙 저장 합니다.  













  
## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-windows-server-2012-r2"></a>규칙을 만들려면 ADFS 1 실행할 수 있습니다. *x* 이름을 ID 통해 전달를 사용 하 여 주장 또는 Windows Server 2012 r 2 규칙 템플릿 들어오는 주장 필터링
  
1.  서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래에서 **광고 FS\\Trust 관계**, 클릭 **클레임 공급자 신뢰** 또는 **의존 파티 신뢰**, 클릭 한 다음이 규칙 만들려는 목록에 특정 신뢰 하 고 합니다.  
  
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
  
6.  에 **구성 규칙** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **수신 클레임 유형**선택 **이름 ID** 목록에 있습니다.  
  
8.  **수신 이름 ID 형식**는 다음과 같은 ADFS 1 중 하나를 선택 합니다. *x*\-compatible 주장 목록에서 형식 있습니다.  
  
    -   **UPN**  
  
    -   **E\ 메일**  
  
    -   **일반 이름**  
  
9. 조직의 요구에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 통과 값 주장**  
  
    -   **특정 주장 값만 통과합니다**  
  
    -   **만 클레임에 맞는 값은 특정 메일이 접미사 값을 통해 전달**  
  
    -   **클레임은 값 값을 시작 하는 통과합니다**  
![규칙 만들기](media/\Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs1.PNG)   

10. 클릭 **완료**, 클릭 한 다음 **확인** 규칙 저장 합니다.  

  
## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>규칙을 만들려면 ADFS 1 실행할 수 있습니다. *x* Windows Server 2012 r 2에서는 수신 주장 규칙 템플릿의 변환의 사용 하 여 이름을 ID 청구  
  
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
  
5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **수신 클레임 변환** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform1.PNG)   
  
6.  에 **구성 규칙** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **수신 클레임 유형**를 목록에서 변형할 들어오는 클레임 유형을 선택 합니다.  
  
8.  **보내는 클레임 유형**선택 **이름을 ID** 목록에 있습니다.  
  
9. **보내는 이름 ID 형식**는 다음과 같은 ADFS 1 중 하나를 선택 합니다. *x*\-compatible 주장 목록에서 형식 있습니다.  
  
    -   **UPN**  
  
    -   **E\ 메일**  
  
    -   **일반 이름**  
  
10. 조직의 요구에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 통과 값 주장**  
  
    -   **들어오는 클레임 값을 바꿉니다 다른 보내는 클레임**  
  
    -   **새 메일 e\ 접미사 들어오는 e\ 메일 접미사 클레임 교체**  
![규칙 만들기](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs2.PNG)    

11. 클릭 **완료**, 클릭 한 다음 **확인** 규칙 저장 합니다.  

## <a name="additional-references"></a>추가 참조 
[클레임은 규칙 구성](Configure-Claim-Rules.md)  
 
[검사: 신뢰 파티 보안에 대 한 청구 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  

[청구 공급자에 대 한 청구 규칙 만들기 신뢰 검사:](https://technet.microsoft.com/library/ee913564.aspx)  
  
[승인 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임은 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
