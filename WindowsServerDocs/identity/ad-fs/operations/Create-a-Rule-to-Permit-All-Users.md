---
ms.assetid: 8c179884-f0d9-4c7a-973d-820119cf3c38
title: 모든 사용자를 허용하는 규칙 만들기
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 1356218c5f9f47073f007286e8acfdf4c3608b73
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407621"
---
# <a name="create-a-rule-to-permit-all-users"></a>모든 사용자를 허용하는 규칙 만들기

Windows Server 2016에서 사용할 수 있습니다는 **액세스 제어 정책** 을 액세스할 모든 사용자가 신뢰 당사자에 게는 규칙을 만듭니다.  Windows Server 2012 r 2에서 Active Directory Federation Services의 **모든 사용자 허용** 규칙 템플릿을 사용 하 여 \(ad FS @ no__t-2를 사용 하는 경우 모든 사용자가 신뢰 당사자에 액세스할 수 있도록 하는 권한 부여 규칙을 만들 수 있습니다. 

권한을 더욱 제한 하려면 추가 권한 부여 규칙을 사용할 수 있습니다. 페더레이션 서비스에서 신뢰 당사자에 대한 액세스가 허용된 사용자도 신뢰 당사자에 의해 서비스가 거부될 수 있습니다.  
  
다음 절차를 사용 하 여 AD FS 관리 스냅인을 사용 하 여 클레임 규칙을 만들려면\-에 있습니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다. 

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2016"></a>Windows Server 2016에서 모든 사용자를 허용 하는 규칙을 만들려면

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **신뢰 당사자 트러스트**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall1.PNG)

3.  마우스 오른쪽 단추로 클릭는 **신뢰 당사자 트러스트** 에 대 한 액세스를 허용 하 고 선택 하려는 **액세스 제어 정책 편집**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

4. 액세스 제어 정책 선택 **모든 사용자 허용** 클릭 하 고 **적용** 및 **확인**합니다.
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall3.PNG)
  
## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2012-r2"></a>Windows Server 2012 r 2의 모든 사용자를 허용 하는 규칙을 만들려면 
  
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS\\트러스트 관계\\신뢰 당사자 트러스트**, 이 규칙을 만들려는 위치 목록에 특정 한 신뢰를 클릭 합니다.  

3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall4.PNG)  

4.  에 **클레임 규칙 편집** 대화 상자를 클릭는 **발급 권한 부여 규칙** 탭 또는 **위임 권한 부여 규칙** 탭 \(필요한 권한 부여 규칙의 형식에 따라\), 클릭 하 고 **규칙 추가** 시작 하는 **권한 부여 클레임 규칙 추가 마법사**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)  
5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **모든 사용자 허용** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall6.PNG)    
6.  에 **규칙 구성** 페이지에서 클릭 **마침**합니다.  
  
7.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.  

## <a name="additional-references"></a>추가 참조 
[클레임 규칙 구성](Configure-Claim-Rules.md)  
 
[검사 목록: 신뢰 당사자 트러스트를 위한 클레임 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  
  
[권한 부여 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임의 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
