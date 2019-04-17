---
ms.assetid: ef83960f-d2cf-441f-b2b6-d97822ec7149
title: "수신 클레임 변환할 규칙 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e982b7608f7602268657ceae74f641bbaaaec939
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-transform-an-incoming-claim"></a>수신 클레임 변환할 규칙 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

사용 하 여는 **들어오는 주장 변환** 규칙 템플릿 Active Directory Federation Services \(AD FS\) 수신 클레임 선택, 클레임 형식을 변경 하 고 수 클레임 값을 변경 합니다. 예를 들어, 수신 그룹 클레임 클레임 값 같은 역할 클레임 보내는 규칙을 만드는이 규칙 템플릿을 사용할 수 있습니다. 이 규칙 값이 관리자, 수신 그룹 클레임 또는 사용자 이름 \(UPN\) 주장으로 끝나는 보낼 수 있는 경우 구매자 클레임 값 그룹 주장 보내려면 사용할 수도 @fabrikam합니다.  
  
다음 절차 규칙을 만들려면 클레임 AD FS 관리 snap\에서 사용할 수 있습니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 최소 요구 사항을 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다. 

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

6.  에 **구성 규칙** 페이지의 **클레임 규칙 이름**,이 규칙의 표시 이름을 입력 합니다. **수신 클레임 유형**, 클레임 목록을 입력 합니다. **보내는 클레임 유형**클레임 유형을 목록에서 선택 하 고 조직의 요구 사항에 따라 달라 지 며 하 고 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 통과 값 주장**  
  
    -   **들어오는 클레임 값을 바꿉니다 다른 보내는 클레임**  
  
    -   **새 메일 e\ 접미사 들어오는 e\ 메일 접미사 클레임 교체**  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)   

7.  클릭 하 고 **완료** 단추.  
  
8.  **편집 클레임 규칙** 대화 상자를 클릭 **확인** 규칙을 저장 해야 합니다.
  
> [!NOTE]  
> 광고 FS\ 발급 클레임을 사용 하 여 동적 액세스 제어 시나리오를 설정 하는 경우 먼저 변환을 규칙 만들기 클레임 공급자 보안 및 **수신 클레임 유형**, 수신 클레임에 대해 이름을 입력 하거나, 클레임 설명 이전에 만든 경우 목록에서 선택 합니다. 두 번째로 **보내는 클레임 유형**원하는 클레임 URL 선택한 다음 장치 클레임 문제를 신뢰 파티 신뢰에 변환을 규칙을 만듭니다.  
>   
> 동적 액세스 제어 시나리오에 대 한 자세한 내용은 참조 [동적 액세스 제어 콘텐츠 로드맵](../../solution-guides/dynamic-access-control--scenario-overview.md) 또는 [Adfs로 사용 하 여 AD DS 클레임](https://technet.microsoft.com/library/hh831504.aspx)합니다. 

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

6.  에 **구성 규칙** 페이지의 **클레임 규칙 이름**,이 규칙의 표시 이름을 입력 합니다. **수신 클레임 유형**, 클레임 목록을 입력 합니다. **보내는 클레임 유형**클레임 유형을 목록에서 선택 하 고 조직의 요구 사항에 따라 달라 지 며 하 고 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 통과 값 주장**  
  
    -   **들어오는 클레임 값을 바꿉니다 다른 보내는 클레임**  
  
    -   **새 메일 e\ 접미사 들어오는 e\ 메일 접미사 클레임 교체**  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)       

7.  클릭 하 고 **완료** 단추.  
  
8.  **편집 클레임 규칙** 대화 상자를 클릭 **확인** 규칙을 저장 해야 합니다.  

> [!NOTE]  
> 광고 FS\ 발급 클레임을 사용 하 여 동적 액세스 제어 시나리오를 설정 하는 경우 먼저 변환을 규칙 만들기 클레임 공급자 보안 및 **수신 클레임 유형**, 수신 클레임에 대해 이름을 입력 하거나, 클레임 설명 이전에 만든 경우 목록에서 선택 합니다. 두 번째로 **보내는 클레임 유형**원하는 클레임 URL 선택한 다음 장치 클레임 문제를 신뢰 파티 신뢰에 변환을 규칙을 만듭니다.  
>   
> 동적 액세스 제어 시나리오에 대 한 자세한 내용은 참조 [동적 액세스 제어 콘텐츠 로드맵](../../solution-guides/dynamic-access-control--scenario-overview.md) 또는 [Adfs로 사용 하 여 AD DS 클레임](https://technet.microsoft.com/library/hh831504.aspx)합니다.   
  
## <a name="to-create-a-rule-to-transform-an-incoming-claim-in-windows-server-2012-r2"></a>Windows Server 2012 r 2에서 수신 클레임 변환할 규칙을 만들려면 
  
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

6.  에 **구성 규칙** 페이지의 **클레임 규칙 이름**,이 규칙의 표시 이름을 입력 합니다. **수신 클레임 유형**, 클레임 목록을 입력 합니다. **보내는 클레임 유형**클레임 유형을 목록에서 선택 하 고 조직의 요구 사항에 따라 달라 지 며 하 고 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 통과 값 주장**  
  
    -   **들어오는 클레임 값을 바꿉니다 다른 보내는 클레임**  
  
    -   **새 메일 e\ 접미사 들어오는 e\ 메일 접미사 클레임 교체**  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform2.PNG)  

> [!NOTE]  
> 광고 FS\ 발급 클레임을 사용 하 여 동적 액세스 제어 시나리오를 설정 하는 경우 먼저 변환을 규칙 만들기 클레임 공급자 보안 및 **수신 클레임 유형**, 수신 클레임에 대해 이름을 입력 하거나, 클레임 설명 이전에 만든 경우 목록에서 선택 합니다. 두 번째로 **보내는 클레임 유형**원하는 클레임 URL 선택한 다음 장치 클레임 문제를 신뢰 파티 신뢰에 변환을 규칙을 만듭니다.  
>   
> 동적 액세스 제어 시나리오에 대 한 자세한 내용은 참조 [동적 액세스 제어 콘텐츠 로드맵](../../solution-guides/dynamic-access-control--scenario-overview.md) 또는 [Adfs로 사용 하 여 AD DS 클레임](https://technet.microsoft.com/library/hh831504.aspx)합니다.  
  
7.  클릭 **완료**합니다.  
  
8.  **편집 클레임 규칙** 대화 상자를 클릭 **확인** 규칙을 저장 해야 합니다.  

## <a name="additional-references"></a>추가 참조 
[클레임은 규칙 구성](Configure-Claim-Rules.md)  
 
[검사: 신뢰 파티 보안에 대 한 청구 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  

[청구 공급자에 대 한 청구 규칙 만들기 신뢰 검사:](https://technet.microsoft.com/library/ee913564.aspx)  
  
[승인 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임은 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
