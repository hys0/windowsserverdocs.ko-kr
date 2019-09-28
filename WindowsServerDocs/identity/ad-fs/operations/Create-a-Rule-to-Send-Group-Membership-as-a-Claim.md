---
ms.assetid: 475e34f9-9399-43f4-a840-9dd77258e11a
title: 클레임으로 그룹 멤버 자격을 보내는 규칙 만들기
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b8217302cc0ec5bc6972004cb2f26ffae1371614
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407583"
---
# <a name="create-a-rule-to-send-group-membership-as-a-claim"></a>클레임으로 그룹 멤버 자격을 보내는 규칙 만들기

Active Directory Federation Services \(ADFS\)에서 그룹 구성원을 클레임으로 보내기 규칙 템플릿을 사용 하 여 클레임으로 보낼 Active Directory 보안 그룹을 선택할 수 있도록 하는 규칙을 만들 수 있습니다. 하나의 클레임을 선택 하는 그룹에 따라이 규칙에서 발생 합니다. 예를 들어 사용자가 Domain Admins 보안 그룹의 멤버인 경우이 값이 Admin 그룹 클레임을 전송할 규칙을 만들려면이 규칙 서식 파일을 사용할 수 있습니다. 이 규칙은 로컬 Active Directory 도메인의 사용자에 대해서만 사용 해야 합니다.  
  
다음 절차를 사용 하 여 AD FS 관리 스냅인을 사용 하 여 클레임 규칙을 만들려면\-에 있습니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   

## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-on-a-relying-party-trust-in-windows-server-2016"></a>그룹 구성원을 클레임을 신뢰 당사자 트러스트에 Windows Server 2016으로 보내도록 규칙을 만들려면 

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **신뢰 당사자 트러스트**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 발급 정책 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **그룹 구성원 클레임으로 보내기** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)      

6.   **규칙 구성** 페이지의 **클레임 규칙 이름** 에이 규칙에 대 한 표시 이름을 입력 합니다. **사용자의 그룹** 에서 **찾아보기** 를 클릭 하 고 그룹을 선택 하 고 **나가는 클레임 유형** 에서 원하는 클레임 유형을 선택한 후 다음 **을 클릭 합니다. 나가는 클레임 유형** 값을 입력 합니다.
![규칙 만들기](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)   

7.  클릭 하 고 **마침** 단추입니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.
  
## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016의 클레임 공급자 트러스트에 대 한 클레임으로 그룹 멤버 자격을 보내도록 규칙을 만들려면 
  
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **클레임 공급자 트러스트**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  에 **클레임 규칙 편집** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **그룹 구성원 클레임으로 보내기** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)     

6.   **규칙 구성** 페이지의 **클레임 규칙 이름** 에이 규칙에 대 한 표시 이름을 입력 합니다. **사용자의 그룹** 에서 **찾아보기** 를 클릭 하 고 그룹을 선택 하 고 **나가는 클레임 유형** 에서 원하는 클레임 유형을 선택한 후 다음 **을 클릭 합니다. 나가는 클레임 유형** 값을 입력 합니다. 
![규칙 만들기](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)      

7.  클릭 하 고 **마침** 단추입니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.  




  
## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-in-windows-server-2012-r2"></a>Windows Server 2012 r 2의 클레임으로 그룹 멤버 자격을 보내도록 규칙을 만들려면 
  
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **AD FS\\트러스트 관계**, 클릭 **클레임 공급자 트러스트** 또는 **신뢰 당사자 트러스트**, 이 규칙을 만드는 목록에서 특정 트러스트를 클릭 하 고 있습니다.  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  에 **클레임 규칙 편집** 대화 상자는 다음과 같은 탭 하나를 선택, 편집 하는 하는 규칙 집합을 신뢰에 따라,이 규칙을 만들려고 할 및 클릭 한 다음 **규칙 추가** 해당 규칙 집합에 연관 된 규칙 마법사를 시작 합니다.  
  
    -   **수락 변환 규칙**  
  
    -   **발급 변환 규칙**  
  
    -   **발급 권한 부여 규칙**  
  
    -   **위임 권한 부여 규칙**  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
    
5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **그룹 구성원을 클레임으로 보내기** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group1.PNG)

6.  **규칙 구성** 페이지의 **클레임 규칙 이름** 에이 규칙에 대 한 표시 이름을 입력 합니다. **사용자의 그룹** 에서 **찾아보기** 를 클릭 하 고 그룹을 선택 하 고 **나가는 클레임 유형** 에서 원하는 클레임 유형을 선택한 후 다음 **을 클릭 합니다. 나가는 클레임 유형** 값을 입력 합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group2.PNG)  

7.  **마침**을 클릭합니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.  



## <a name="additional-references"></a>추가 참조 
[클레임 규칙 구성](Configure-Claim-Rules.md)  
 
[검사 목록: 신뢰 당사자 트러스트를 위한 클레임 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  

[검사 목록: 클레임 공급자 트러스트를 위한 클레임 규칙 만들기](https://technet.microsoft.com/library/ee913564.aspx)  
  
[권한 부여 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임의 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
