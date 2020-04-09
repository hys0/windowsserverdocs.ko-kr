---
ms.assetid: 66664b80-2590-46c0-bfca-82402088e42c
title: LDAP 특성을 클레임으로 전송 하는 규칙 만들기
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6280ee1fb761b154cadb948d18c7b67cb6b8e784
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816656"
---
# <a name="create-a-rule-to-send-ldap-attributes-as-claims"></a>LDAP 특성을 클레임으로 전송 하는 규칙 만들기


Active Directory Federation Services \(AD FS\)에서 LDAP 특성을 클레임으로 보내기 규칙 템플릿을 사용 하 여 신뢰 당사자에 게 클레임으로 보낼 LDAP \(특성 저장소 (예:\))에서 특성을 선택 하는 규칙을 만들 수 있습니다. 예를 들어이 규칙 템플릿을 사용 하 여 **displayName** 및 **telephoneNumber** Active Directory 특성에서 인증 된 사용자에 대 한 특성 값을 추출 하 고 두 개의 서로 다른 나가는 클레임으로 해당 값을 전송 하는 클레임 규칙으로 LDAP 특성을 보내도록 클레임 규칙을 만들 수 있습니다.  
  
이 규칙을 사용 하 여 모든 사용자의 그룹 멤버 자격을 보낼 수도 있습니다. 개별 그룹 구성원만 보내려는 경우 그룹 구성원을 클레임으로 보내기 규칙 템플릿을 사용합니다. 다음 절차를 사용 하 여 AD FS 관리 스냅인을 사용 하 여 클레임 규칙을 만들려면\-에 있습니다.  
  
이 절차를 완료하려면 최소한 로컬 컴퓨터의 **Administrators** 구성원 자격 또는 동급의 권한이 필요합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.  

## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-relying-party-trust-in-windows-server-2016"></a>신뢰 당사자 트러스트에 Windows Server 2016에 대 한 클레임으로 LDAP 특성을 보내도록 규칙을 만들려면 

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **신뢰 당사자 트러스트**합니다. 
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG) 만들기 ![  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 발급 정책 편집**합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG) 만들기 ![   
  
4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG) 만들기 ![    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**,  **LDAP 특성을 클레임으로 보내기** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
규칙](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG) 만들기 ![    

6.  에 **규칙 구성** 페이지 **클레임 규칙 이름** 선택이 규칙에 대 한 표시 이름을 입력는 **특성 저장소**, LDAP 특성을 선택 하 고 나가는 클레임 유형에를 매핑합니다. 
규칙](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG) 만들기 ![    

7.  클릭 하 고 **마침** 단추입니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016에서 클레임 공급자 트러스트에 대 한 클레임으로 LDAP 특성을 보내도록 규칙을 만들려면 
  
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD FS**, 클릭 **클레임 공급자 트러스트**합니다. 
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG) 만들기 ![  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG) 만들기 ![   
  
4.  에 **클레임 규칙 편집** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG) 만들기 ![    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**,  **LDAP 특성을 클레임으로 보내기** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
규칙](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG) 만들기 ![       

6.  에 **규칙 구성** 페이지 **클레임 규칙 이름** 선택이 규칙에 대 한 표시 이름을 입력는 **특성 저장소**, LDAP 특성을 선택 하 고 나가는 클레임 유형에를 매핑합니다. 
규칙](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG) 만들기 ![      

7.  클릭 하 고 **마침** 단추입니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.  

 
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-windows-server-2012-r2"></a>Windows Server 2012 r 2에 대 한 클레임으로 LDAP 특성을 보내도록 규칙을 만들려면  
  
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **AD FS FSAD\\트러스트 관계**, 클릭 **클레임 공급자 트러스트** 또는 **신뢰 당사자 트러스트**, 이 규칙을 만드는 목록에서 특정 트러스트를 클릭 하 고 있습니다.  
  
3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 만들기 ![  
  
4.  에 **클레임 규칙 편집** 대화 상자는 다음과 같은 탭 하나를 선택, 편집 하는 하는 규칙 집합을 신뢰에 따라,이 규칙을 만들려고 할 및 클릭 한 다음 **규칙 추가** 해당 규칙 집합에 연관 된 규칙 마법사를 시작 합니다.  
  
    -   **수락 변환 규칙**  
  
    -   **발급 변환 규칙**  
  
    -   **발급 권한 부여 규칙**  
  
    -   **위임 권한 부여 규칙**  
규칙](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) 만들기 ![ 
  
5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**,  **LDAP 특성을 클레임으로 보내기** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
규칙](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap3.PNG) 만들기 ![  
  
6.  에 **규칙 구성** 페이지 **클레임 규칙 이름** 아래에서이 규칙에 대 한 표시 이름을 입력 **특성 저장소** 선택 **Active Directory**, 아래에서 **LDAP의 매핑 특성을 보내는 클레임 유형** 원하는 **LDAP 특성** 및 해당 **나가는 클레임 유형** 드롭다운에서 형식\-목록 아래쪽 합니다.  
  
    이 규칙의 일부로 클레임을 발급 하려는 각 Active Directory 특성에 대해 새 LDAP 특성 및 나가는 클레임 유형 쌍을 다른 행에서 선택 해야 합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap4.PNG)    
7.  클릭 하 고 **마침** 단추입니다.  
  
8.  에 **클레임 규칙 편집** 대화 상자를 클릭 **확인** 여 규칙을 저장 합니다.  

## <a name="additional-references"></a>추가 참조 
[클레임 규칙 구성](Configure-Claim-Rules.md)  
 
[검사 목록: 신뢰 당사자 트러스트에 대 한 클레임 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  

[검사 목록: 클레임 공급자 트러스트에 대 한 클레임 규칙 만들기](https://technet.microsoft.com/library/ee913564.aspx)  
  
[권한 부여 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임의 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
