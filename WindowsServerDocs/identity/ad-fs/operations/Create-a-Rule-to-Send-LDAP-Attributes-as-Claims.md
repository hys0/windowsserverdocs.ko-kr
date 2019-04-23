---
ms.assetid: 66664b80-2590-46c0-bfca-82402088e42c
title: LDAP 특성을 클레임으로 전송 하는 규칙 만들기
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e9762e4bc50a1c2b862999af5269a0da376ec9a1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887614"
---
# <a name="create-a-rule-to-send-ldap-attributes-as-claims"></a>LDAP 특성을 클레임으로 전송 하는 규칙 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2

Active Directory Federation Services에 대 한 클레임 규칙 템플릿으로 보내기 LDAP 특성을 사용 하 여 \(AD FS\), Lightweight Directory Access Protocol에서 특성을 선택 하는 규칙을 만들 수 있습니다 \(LDAP\)신뢰 당사자에 대 한 클레임으로 보내기을 Active Directory와 같은 특성 저장소입니다. 클레임 규칙에서 인증 된 사용자에 대 한 특성 값을 추출 하는 보내기 LDAP 특성을 만들려면이 규칙 서식 파일을 사용할 수는 예를 들어 합니다 **displayName** 하 고 **telephoneNumber** Active 디렉터리 특성 및 두 개의 서로 다른 나가는 클레임으로 이러한 값을 보낼 수 있습니다.  
  
또한 이 규칙을 사용하여 모든 사용자 그룹의 구성원을 보낼 수도 있습니다. 개별 그룹 구성원만 보내려는 경우 그룹 구성원을 클레임으로 보내기 규칙 템플릿을 사용합니다. 다음 절차를 사용 하 여 AD FS 관리 스냅인을 사용 하 여 클레임 규칙을 만들려면\-에 있습니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.  

## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-relying-party-trust-in-windows-server-2016"></a>신뢰 당사자 트러스트에 Windows Server 2016에 대 한 클레임으로 LDAP 특성을 보내도록 규칙을 만들려면 

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **신뢰 당사자 트러스트**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 발급 정책 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**,  **LDAP 특성을 클레임으로 보내기** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)    

6.  에 **규칙 구성** 페이지 **클레임 규칙 이름** 선택이 규칙에 대 한 표시 이름을 입력는 **특성 저장소**, LDAP 특성을 선택 하 고 나가는 클레임 유형에를 매핑합니다. 
![규칙 만들기](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)    

7.  클릭 하 고 **마침** 단추입니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016에서 클레임 공급자 트러스트에 대 한 클레임으로 LDAP 특성을 보내도록 규칙을 만들려면 
  
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **클레임 공급자 트러스트**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  에 **클레임 규칙 편집** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**,  **LDAP 특성을 클레임으로 보내기** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)       

6.  에 **규칙 구성** 페이지 **클레임 규칙 이름** 선택이 규칙에 대 한 표시 이름을 입력는 **특성 저장소**, LDAP 특성을 선택 하 고 나가는 클레임 유형에를 매핑합니다. 
![규칙 만들기](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)      

7.  클릭 하 고 **마침** 단추입니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.  

 
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-windows-server-2012-r2"></a>Windows Server 2012 r 2에 대 한 클레임으로 LDAP 특성을 보내도록 규칙을 만들려면  
  
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **AD FS FSAD\\트러스트 관계**, 클릭 **클레임 공급자 트러스트** 또는 **신뢰 당사자 트러스트**, 이 규칙을 만드는 목록에서 특정 트러스트를 클릭 하 고 있습니다.  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  에 **클레임 규칙 편집** 대화 상자는 다음과 같은 탭 하나를 선택, 편집 하는 하는 규칙 집합을 신뢰에 따라,이 규칙을 만들려고 할 및 클릭 한 다음 **규칙 추가** 해당 규칙 집합에 연관 된 규칙 마법사를 시작 합니다.  
  
    -   **수용 변환 규칙**  
  
    -   **발급 변환 규칙**  
  
    -   **발급 권한 부여 규칙**  
  
    -   **위임 권한 부여 규칙**  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) 
  
5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**,  **LDAP 특성을 클레임으로 보내기** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap3.PNG)  
  
6.  에 **규칙 구성** 페이지 **클레임 규칙 이름** 아래에서이 규칙에 대 한 표시 이름을 입력 **특성 저장소** 선택 **Active Directory**, 아래에서 **LDAP의 매핑 특성을 보내는 클레임 유형** 원하는 **LDAP 특성** 및 해당 **나가는 클레임 유형** 드롭다운에서 형식\-목록 아래쪽 합니다.  
  
    새 LDAP 특성 및이 규칙의 일부로 클레임을 발급 하려는 각 Active Directory 특성에 대 한 다른 행에 대해 나가는 클레임 형식 쌍을 선택 해야 합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap4.PNG)    
7.  클릭 하 고 **마침** 단추입니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.  

## <a name="additional-references"></a>추가 참조 
[클레임 규칙 구성](Configure-Claim-Rules.md)  
 
[검사 목록: 신뢰 당사자 트러스트에 대 한 클레임 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  

[검사 목록: 클레임 공급자에 대 한 클레임 규칙 만들기 신뢰](https://technet.microsoft.com/library/ee913564.aspx)  
  
[권한 부여 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임의 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
