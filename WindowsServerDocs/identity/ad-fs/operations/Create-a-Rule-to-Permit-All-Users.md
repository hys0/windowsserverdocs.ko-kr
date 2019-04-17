---
ms.assetid: 8c179884-f0d9-4c7a-973d-820119cf3c38
title: "모든 사용자가 허용 하는 규칙 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: de85af27e699242977054420178dd3c424b2ddb3
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-permit-all-users"></a>모든 사용자가 허용 하는 규칙 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

Windows Server 2016 사용할 수는 **액세스 제어 정책** 에 액세스할 수 모든 사용자가 신뢰 하는 규칙 만들 수 있습니다.  Windows Server 2012 r 2에 사용 하는 **모든 사용자가 허용** 규칙 서식 Active Directory Federation Services \(AD FS\)에서 파일을는 모든 사용자에 게 당사자에 대 한 액세스 제공 하는 인증 규칙 만들 수 있습니다. 

추가 인증 규칙 액세스를 제한에 사용할 수 있습니다. 당사자 Federation 서비스에서 액세스할 수 있는 사용자를 계속 거부 될 수 있습니다 서비스 당사자가 있습니다.  
  
다음 절차 규칙을 만들려면 클레임 AD FS 관리 snap\에서 사용할 수 있습니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다. 

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2016"></a>Windows Server 2016에 모든 사용자가 허용 하는 규칙 만들려면

1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **파티 신뢰 의존**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall1.PNG)

3.  마우스 오른쪽 단추로 클릭는 **파티 신뢰 의존** 선택한에 대 한 액세스를 허용 하려는 **액세스 제어 정책 편집**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

4. 액세스를 제어 정책 선택 **모든 허용** 차례로 클릭 하 고 **적용** 및 **확인**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall3.PNG)
  
## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2012-r2"></a>Windows Server 2012 r 2의 모든 사용자가 허용 하는 규칙 만들려면 
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **광고 FS\\Trust Relationships\\Relying 파티 신뢰**,이 규칙 만들려는 목록에 특정 신뢰를 클릭 합니다.  

3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **편집 클레임 규칙**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall4.PNG)  

4.  **클레임 규칙 편집** 대화 상자를 클릭는 **발급 승인 규칙** 탭 또는 **위임 인증 규칙** 탭 \ (유형에 따라 인증 규칙을 require\), 클릭 한 다음 **규칙 추가** 시작 하는 **추가 승인 클레임 규칙 마법사**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)  
5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **모든 사용자가 허용** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall6.PNG)    
6.  에 **구성 규칙** 페이지, 클릭 **완료**합니다.  
  
7.  **편집 클레임 규칙** 대화 상자를 클릭 **확인** 규칙을 저장 해야 합니다.  

## <a name="additional-references"></a>추가 참조 
[클레임은 규칙 구성](Configure-Claim-Rules.md)  
 
[검사: 신뢰 파티 보안에 대 한 청구 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  
  
[승인 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임은 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
