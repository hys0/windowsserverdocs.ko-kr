---
ms.assetid: 3d770385-9834-4ebe-b66c-b684e0245971
title: "허용 하거나 사용자가 수신 클레임에 따라 거부할 규칙 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: afcbb8c7a08a84eda2a794c9565061d7d61d470b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim"></a>허용 하거나 사용자가 수신 클레임에 따라 거부할 규칙 만들기 

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

Windows Server 2016 사용할 수는 **액세스 제어 정책** 의 수 있도록 규칙을 만들 수신 클레임에 따라 사용자의 거부 합니다.  Windows Server 2012 r 2에 사용 하는 **허용 또는 거부 들어오는 요구에 따라 사용자에 게** 규칙 서식 Active Directory Federation Services \(AD FS\)에서 파일을 허용 하거나 당사자 유형과 수신 클레임 값에 따라 사용자의 액세스 거부 인증 규칙 만들 수 있습니다. 

예를 들어, 그룹 주장 값이 도메인 관리자 당사자 액세스할 수 있는 사용자만 수 있도록 규칙이 사용할 수 있습니다. 당사자 액세스를 사용 하 여 모든 사용자가 허용 하는 경우는 **모든 허용** 액세스 제어 정책 또는 **모든 사용자가 허용** Windows Server의 버전에 따라 규칙 서식 합니다. 당사자 Federation 서비스에서 액세스할 수 있는 사용자를 계속 거부 될 수 있습니다 서비스 당사자가 있습니다.  
  
다음 절차 규칙을 만들려면 클레임 AD FS 관리 snap\에서 사용할 수 있습니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.  

## <a name="to-create-a-rule-to-permit-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Windows Server 2016에 수신 클레임에 따라 사용자가 허용 하는 규칙 만들려면
 
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **액세스 제어 정책을**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. 마우스 오른쪽 단추로 클릭 하 고 선택 **액세스 제어 정책 추가**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. 이름 상자에서 설명 및 클릭 정책에 따라 이름을 입력 **추가**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny5.PNG)

5. 에 **규칙 편집기**, 장소 체크 인 사용자에서 **요청에서 특정 클레임** 에서 밑줄이 그어진 클릭 하 고 **특정** 맨 아래에 있습니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny6.PNG)

6. 에 **선택 클레임** 화면을 클릭는 **클레임** 라디오 단추를 선택은 **클레임 유형**, **통신사**, 및 **클레임 값** 클릭 한 다음 **확인**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny7.PNG)

7.  에 **규칙 편집기** 클릭 **확인**합니다.  에 **액세스 제어 정책 추가** 화면에서 클릭 **확인**합니다.

8. 에 **AD FS 관리** 의 콘솔 트리에서, **ADFS**, 클릭 **파티 신뢰 의존**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  마우스 오른쪽 단추로 클릭는 **파티 신뢰 의존** 선택한에 대 한 액세스를 허용 하려는 **액세스 제어 정책 편집**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. 액세스 제어 정책 정책에 따라 선택 하 고 클릭 한 다음 **적용** 및 **확인**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny8.PNG)

## <a name="to-create-a-rule-to-deny-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Windows Server 2016에 수신 클레임에 따라 사용자의 거부 하려면 규칙을 만들려면
 
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **액세스 제어 정책을**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. 마우스 오른쪽 단추로 클릭 하 고 선택 **액세스 제어 정책 추가**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. 이름 상자에서 설명 및 클릭 정책에 따라 이름을 입력 **추가**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny9.PNG)

5. 에 **규칙 편집기**, 모든 사용자가 선택 되어 있는지 확인 고 **제외 하 고** 의 확인란을 선택 **요청에서 특정 클레임** 에서 밑줄이 그어진 클릭 하 고 **특정** 맨 아래에 있습니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny10.PNG)

6. 에 **선택 클레임** 화면을 클릭는 **클레임** 라디오 단추를 선택은 **클레임 유형**, **통신사**, 및 **클레임 값** 클릭 한 다음 **확인**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny11.PNG)

7.  에 **규칙 편집기** 클릭 **확인**합니다.  에 **액세스 제어 정책 추가** 화면에서 클릭 **확인**합니다.

8. 에 **AD FS 관리** 의 콘솔 트리에서, **ADFS**, 클릭 **파티 신뢰 의존**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  마우스 오른쪽 단추로 클릭는 **파티 신뢰 의존** 선택한에 대 한 액세스를 허용 하려는 **액세스 제어 정책 편집**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. 액세스 제어 정책 정책에 따라 선택 하 고 클릭 한 다음 **적용** 및 **확인**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny12.PNG)

  
## <a name="to-create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim-on-windows-server-2012-r2"></a>허용 하거나 사용자가 수신 클레임 Windows Server 2012 r 2에 따라 거부할 규칙을 만들려면
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.    
  
2.  콘솔 트리에서 **광고 FS\\Trust Relationships\\Relying 파티 신뢰**,이 규칙 만들려는 목록에 특정 신뢰를 클릭 합니다.  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **편집 클레임 규칙**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)   

4.  **클레임 규칙 편집** 대화 상자를 클릭는 **발급 승인 규칙** 탭 또는 **위임 인증 규칙** 탭 \ (유형에 따라 인증 규칙을 require\), 클릭 한 다음 **규칙 추가** 시작 하는 **추가 승인 클레임 규칙 마법사**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **허용 또는 사용자가 거부 수신 클레임에 따라** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny1.PNG)

6.  에 **구성 규칙** 페이지에서 **클레임 규칙 이름** 이 규칙의 표시 이름을 입력 **수신 클레임 유형** 클레임 유형을 목록에서 선택 **클레임 값을 수신** 값을 입력 하거나 찾아보기를 \ (available\ 경우) 값을 선택 하 고 조직의 요구에 따라 다음 옵션 중 하나를 선택:  
  
    -   **이 들어오는 클레임 있는 사용자에 게 액세스 권한을**  
  
    -   **액세스를 사용자에 게가 들어오는 클레임 거부**  
![규칙 만들기](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny2.PNG)  
7.  클릭 **완료**합니다.  
  
8.  **편집 클레임 규칙** 대화 상자를 클릭 **확인** 규칙을 저장 해야 합니다.  

## <a name="additional-references"></a>추가 참조 
[클레임은 규칙 구성](Configure-Claim-Rules.md)  
 
[검사: 신뢰 파티 보안에 대 한 청구 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  
  
[승인 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임은 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
