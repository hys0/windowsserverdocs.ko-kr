---
ms.assetid: c60227a8-7b44-40f8-b807-a6532851a4a6
title: 특성 저장소 추가
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b197268de3c5335e30c2a24a74c5a7b01224b500
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859696"
---
# <a name="add-an-attribute-store"></a>특성 저장소 추가


Active Directory Federation Services \(AD FS\)에 의해 보호 되는 리소스에 액세스 해야 하는 사용자 계정 및 컴퓨터 계정은 특성 저장소에 저장 됩니다 (예: Active Directory Domain Services \(AD DS\)). 클레임 발급 엔진 특성 저장소를 사용 하 여 클레임을 발급 하는 데 필요한 데이터를 수집 합니다. 그런 다음 특성 저장소의 데이터는 클레임으로 투영 됩니다.  
  
다음 절차를 사용 하 여 페더레이션 서비스에 특성 저장소를 추가할 수 있습니다.  
  
이 절차를 완료하려면 최소한 로컬 컴퓨터의 **Administrators** 구성원 자격 또는 동급의 권한이 필요합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-an-attribute-store"></a>특성 저장소를 추가 하려면  
  
1.  열기 **AD FS 관리**합니다.  
  
2.  아래에서 **작업** 클릭 **특성 저장소 추가**합니다.  

![특성 저장소 추가](media/Add-an-Attribute-Store/addstore1.PNG)
  
3. 에 **특성 저장소 추가** 대화 상자에서 추가 하려는 특성 저장소에 대 한 다음 속성을 구성 합니다.  
  
   -   **표시 이름**, 특성 저장소를 식별 하는 데 사용할 이름을 입력 합니다.  
  
   -   **특성 저장소 유형**, 를 하거나 지원 되는 특성 저장소 유형을 선택 **Active Directory**, **LDAP**, 또는 **SQL**합니다.  
  
   -   **연결 문자열**, Lightweight Directory Access Protocol을 선택한 경우, \(LDAP\) 저장소 또는 구조적 쿼리 언어 \(SQL\) 저장, 특성 저장소에 대 한 연결을 설정 하는 데 사용 하는 문자열을 입력 합니다. Active Directory 특성 저장소에 대 한 연결 문자열은 필요 합니다. 따라서이 필드가 비활성화 됩니다.  
  
       > [!NOTE]  
       > AD FS는 기본적으로 Active Directory 특성 저장소를 자동으로 만듭니다.  
 
![특성 저장소 추가](media/Add-an-Attribute-Store/addstore2.PNG) 

4. **확인**을 클릭합니다.  
  
## <a name="additional-references"></a>추가 참조  

[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
  
[특성 저장소의 역할](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)  
