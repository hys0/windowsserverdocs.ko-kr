---
ms.assetid: 3d770385-9834-4ebe-b66c-b684e0245971
title: 들어오는 클레임에 따라 사용자를 허용 또는 거부하는 규칙 만들기
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 167e43d49c08d0e39549bf46888118f985e3876d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863774"
---
# <a name="create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim"></a>들어오는 클레임에 따라 사용자를 허용 또는 거부하는 규칙 만들기 

>적용 대상: Windows Server 2016, Windows Server 2012 R2

Windows Server 2016에서 사용할 수 있습니다는 **액세스 제어 정책** 됩니다 사용자 허용 또는 거부 들어오는 클레임을 기반으로 하는 규칙을 만들려고 합니다.  Windows Server 2012 R2에서 사용 하는 **허용 또는 거부 들어오는 클레임에 따라 사용자가** Active Directory Federation Services에서 규칙 템플릿을 \(AD FS\), 부여 됩니다.이 권한 부여 규칙을 만들 수 있습니다 또는 유형 및 들어오는 클레임의 값에 따라 신뢰 당사자에 대 한 사용자 액세스를 거부 합니다. 

예를 들어, 클레임 값이 신뢰 당사자에 액세스 하려면 Domain Admins 그룹에 있는 사용자만 있도록 규칙을 만들려면이 사용할 수 있습니다. 모든 사용자가 신뢰 당사자에 액세스를 사용 하도록 허용 하려는 경우는 **Everyone 허용** 액세스 제어 정책 또는 **모든 사용자 허용** 의 Windows Server 버전에 따라 규칙 템플릿. 페더레이션 서비스에서 신뢰 당사자에 대한 액세스가 허용된 사용자도 신뢰 당사자에 의해 서비스가 거부될 수 있습니다.  
  
다음 절차를 사용 하 여 AD FS 관리 스냅인을 사용 하 여 클레임 규칙을 만들려면\-에 있습니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.  

## <a name="to-create-a-rule-to-permit-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Windows Server 2016에서 들어오는 클레임에 따라 사용자를 허용 하는 규칙을 만들려면
 
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **액세스 제어 정책**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. 마우스 오른쪽 단추로 클릭 하 고 선택 **액세스 제어 정책 추가**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. 이름 상자에 정책, 설명 및 클릭에 대 한 이름을 입력 **추가**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny5.PNG)

5. 에 **규칙 편집기**, 사용자에서 체크 인을 배치 **요청에서 특정 클레임** 는 밑줄이 그어진 클릭 **특정** 맨 아래에 있습니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny6.PNG)

6. 에 **선택 클레임** 화면에서 **클레임** 라디오 단추를 선택은 **클레임 유형**,  **연산자**, 및 **클레임 값** 클릭 한 다음 **확인**.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny7.PNG)

7.  에 **규칙 편집기** 클릭 **확인**합니다.  에 **액세스 제어 정책 추가** 화면에서 **확인**합니다.

8. 에 **AD FS 관리** 콘솔 트리의 **AD FS**, 클릭 **신뢰 당사자 트러스트**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  마우스 오른쪽 단추로 클릭는 **신뢰 당사자 트러스트** 에 대 한 액세스를 허용 하 고 선택 하려는 **액세스 제어 정책 편집**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. 액세스 제어 정책에서 정책을 선택한 다음 클릭 **적용** 및 **확인**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny8.PNG)

## <a name="to-create-a-rule-to-deny-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Windows Server 2016에서 들어오는 클레임에 따라 사용자를 거부 하도록 규칙을 만들려면
 
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **액세스 제어 정책**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. 마우스 오른쪽 단추로 클릭 하 고 선택 **액세스 제어 정책 추가**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. 이름 상자에 정책, 설명 및 클릭에 대 한 이름을 입력 **추가**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny9.PNG)

5. 에 **규칙 편집기**, 모든 사용자가 선택 되어 있는지 확인 아래에서 **제외 하 고** 에 체크 **요청에서 특정 클레임** 는 밑줄이 그어진 클릭 **특정** 맨 아래에 있습니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny10.PNG)

6. 에 **선택 클레임** 화면에서 **클레임** 라디오 단추를 선택은 **클레임 유형**,  **연산자**, 및 **클레임 값** 클릭 한 다음 **확인**.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny11.PNG)

7.  에 **규칙 편집기** 클릭 **확인**합니다.  에 **액세스 제어 정책 추가** 화면에서 **확인**합니다.

8. 에 **AD FS 관리** 콘솔 트리의 **AD FS**, 클릭 **신뢰 당사자 트러스트**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  마우스 오른쪽 단추로 클릭는 **신뢰 당사자 트러스트** 에 대 한 액세스를 허용 하 고 선택 하려는 **액세스 제어 정책 편집**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. 액세스 제어 정책에서 정책을 선택한 다음 클릭 **적용** 및 **확인**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny12.PNG)

  
## <a name="to-create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim-on-windows-server-2012-r2"></a>Windows Server 2012 r 2에서 들어오는 클레임에 따라 사용자 허용 또는 거부 하는 규칙을 만들려면
  
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.    
  
2.  콘솔 트리에서 아래 **AD FS\\트러스트 관계\\신뢰 당사자 트러스트**, 이 규칙을 만들려는 위치 목록에 특정 한 신뢰를 클릭 합니다.  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)   

4.  에 **클레임 규칙 편집** 대화 상자를 클릭는 **발급 권한 부여 규칙** 탭 또는 **위임 권한 부여 규칙** 탭 \(필요한 권한 부여 규칙의 형식에 따라\), 클릭 하 고 **규칙 추가** 시작 하는 **권한 부여 클레임 규칙 추가 마법사**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **허용 또는 거부 들어오는 클레임에 따라 사용자가** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny1.PNG)

6.  에 **규칙 구성** 페이지의 **클레임 규칙 이름** 에이 규칙에 대 한 표시 이름을 입력 **들어오는 클레임 유형** 아래 목록에서 클레임 유형을 선택 **들어오는 클레임 값** 값을 입력 하거나 찾아보기를 클릭 \(가능 하다 면\) 값을 선택 하 고 조직의 요구에 따라 다음 옵션 중 하나를 선택 합니다.  
  
    -   **이 들어오는 클레임을 사용 하 여 사용자에 게 액세스를 허용 합니다.**  
  
    -   **이 들어오는 클레임을 사용 하 여 사용자에 게 액세스를 거부 합니다.**  
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny2.PNG)  
7.  **마침**을 클릭합니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.  

## <a name="additional-references"></a>추가 참조 
[클레임 규칙 구성](Configure-Claim-Rules.md)  
 
[검사 목록: 신뢰 당사자 트러스트에 대 한 클레임 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  
  
[권한 부여 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임의 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
