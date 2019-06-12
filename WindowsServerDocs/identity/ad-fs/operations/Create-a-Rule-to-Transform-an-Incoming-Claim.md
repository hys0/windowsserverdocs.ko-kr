---
ms.assetid: ef83960f-d2cf-441f-b2b6-d97822ec7149
title: 들어오는 클레임 변환 규칙 만들기
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a29406880481f0e4e257105e94bc1a33ee661164
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444439"
---
# <a name="create-a-rule-to-transform-an-incoming-claim"></a>들어오는 클레임 변환 규칙 만들기


사용 하 여 합니다 **들어오는 클레임 변환** Active Directory Federation Services에서 규칙 템플릿을 \(AD FS\), 들어오는 클레임을 선택, 클레임 형식을 변경 및 해당 클레임 값을 변경할 수 있습니다. 예를 들어 들어오는 그룹 클레임의 동일한 클레임 값으로 역할 클레임을 전송 하는 규칙을 만들려면이 규칙 서식 파일을 사용할 수 있습니다. 관리자의 값을 사용 하 여 들어오는 그룹 클레임 하거나 사용자 계정 이름만 보낼 수 있습니다 구매자의 클레임 값을 사용 하 여 그룹 클레임을 보내도록이 규칙을 사용할 수도 있습니다 \(UPN\) 으로 끝나는 클레임 @fabrikam합니다.  
  
다음 절차를 사용 하 여 AD FS 관리 스냅인을 사용 하 여 클레임 규칙을 만들려면\-에 있습니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한 로컬 컴퓨터에서 최소한이이 절차를 완료 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다. 

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

6.  에 **규칙 구성** 페이지의 **클레임 규칙 이름**, 이 규칙에 대 한 표시 이름을 입력 합니다. **들어오는 클레임 유형**, 목록에 클레임 유형을 선택 합니다. **보내는 클레임 유형**, 클레임 유형을 목록에서 선택 하 고 조직의 요구 사항에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 클레임 값 통과**  
  
    -   **들어오는 클레임 값을 다른 나가는 클레임 값으로 바꿉니다.**  
  
    -   **들어오는 전자 바꾸기\-접미사를 클레임 새 전자 메일\-메일 접미사**  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)   

7.  클릭 하 고 **마침** 단추입니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.
  
> [!NOTE]  
> AD FS를 사용 하는 동적 액세스 제어 시나리오를 설정 하는 경우\-와 클레임 공급자 트러스트에서 변환 규칙을 먼저 만듭니다 클레임 발급 **들어오는 클레임 유형**, 들어오는 클레임에 대 한 이름을 입력 하거나, 클레임 설명 이전에 만든 경우 목록에서 선택 합니다. 두 번째 **보내는 클레임 유형**, 원하는 클레임 URL을 선택 하 고 다음 장치 클레임을 발급 하도록 신뢰 당사자 트러스트에 변환 규칙을 만듭니다.  
>   
> 동적 액세스 제어 시나리오에 대 한 자세한 내용은 참조 [동적 액세스 제어 콘텐츠 로드맵](../../solution-guides/dynamic-access-control--scenario-overview.md) 또는 [AD FS와 함께 사용 되는 AD DS 클레임 사용](https://technet.microsoft.com/library/hh831504.aspx)합니다. 

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

6.  에 **규칙 구성** 페이지의 **클레임 규칙 이름**, 이 규칙에 대 한 표시 이름을 입력 합니다. **들어오는 클레임 유형**, 목록에 클레임 유형을 선택 합니다. **보내는 클레임 유형**, 클레임 유형을 목록에서 선택 하 고 조직의 요구 사항에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 클레임 값 통과**  
  
    -   **들어오는 클레임 값을 다른 나가는 클레임 값으로 바꿉니다.**  
  
    -   **들어오는 전자 바꾸기\-접미사를 클레임 새 전자 메일\-메일 접미사**  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)       

7.  클릭 하 고 **마침** 단추입니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.  

> [!NOTE]  
> AD FS를 사용 하는 동적 액세스 제어 시나리오를 설정 하는 경우\-와 클레임 공급자 트러스트에서 변환 규칙을 먼저 만듭니다 클레임 발급 **들어오는 클레임 유형**, 들어오는 클레임에 대 한 이름을 입력 하거나, 클레임 설명 이전에 만든 경우 목록에서 선택 합니다. 두 번째 **보내는 클레임 유형**, 원하는 클레임 URL을 선택 하 고 다음 장치 클레임을 발급 하도록 신뢰 당사자 트러스트에 변환 규칙을 만듭니다.  
>   
> 동적 액세스 제어 시나리오에 대 한 자세한 내용은 참조 [동적 액세스 제어 콘텐츠 로드맵](../../solution-guides/dynamic-access-control--scenario-overview.md) 또는 [AD FS와 함께 사용 되는 AD DS 클레임 사용](https://technet.microsoft.com/library/hh831504.aspx)합니다.   
  
## <a name="to-create-a-rule-to-transform-an-incoming-claim-in-windows-server-2012-r2"></a>Windows Server 2012 r 2에서 들어오는 클레임 변환 규칙을 만들려면 
  
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

6.  에 **규칙 구성** 페이지의 **클레임 규칙 이름**, 이 규칙에 대 한 표시 이름을 입력 합니다. **들어오는 클레임 유형**, 목록에 클레임 유형을 선택 합니다. **보내는 클레임 유형**, 클레임 유형을 목록에서 선택 하 고 조직의 요구 사항에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **모든 클레임 값 통과**  
  
    -   **들어오는 클레임 값을 다른 나가는 클레임 값으로 바꿉니다.**  
  
    -   **들어오는 전자 바꾸기\-접미사를 클레임 새 전자 메일\-메일 접미사**  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform2.PNG)  

> [!NOTE]  
> AD FS를 사용 하는 동적 액세스 제어 시나리오를 설정 하는 경우\-와 클레임 공급자 트러스트에서 변환 규칙을 먼저 만듭니다 클레임 발급 **들어오는 클레임 유형**, 들어오는 클레임에 대 한 이름을 입력 하거나, 클레임 설명 이전에 만든 경우 목록에서 선택 합니다. 두 번째 **보내는 클레임 유형**, 원하는 클레임 URL을 선택 하 고 다음 장치 클레임을 발급 하도록 신뢰 당사자 트러스트에 변환 규칙을 만듭니다.  
>   
> 동적 액세스 제어 시나리오에 대 한 자세한 내용은 참조 [동적 액세스 제어 콘텐츠 로드맵](../../solution-guides/dynamic-access-control--scenario-overview.md) 또는 [AD FS와 함께 사용 되는 AD DS 클레임 사용](https://technet.microsoft.com/library/hh831504.aspx)합니다.  
  
7. **마침**을 클릭합니다.  
  
8. 에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.  

## <a name="additional-references"></a>추가 참조 
[클레임 규칙 구성](Configure-Claim-Rules.md)  
 
[검사 목록: 신뢰 당사자 트러스트를 위한 클레임 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  

[검사 목록: 클레임 공급자 트러스트를 위한 클레임 규칙 만들기](https://technet.microsoft.com/library/ee913564.aspx)  
  
[권한 부여 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임의 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
