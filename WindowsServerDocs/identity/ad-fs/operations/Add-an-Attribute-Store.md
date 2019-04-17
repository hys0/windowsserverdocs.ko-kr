---
ms.assetid: c60227a8-7b44-40f8-b807-a6532851a4a6
title: "특성 저장소 추가"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 11baba5bfdb699f120a506feb8361db21d26cff1
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="add-an-attribute-store"></a>특성 저장소 추가

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

사용자 계정 및 Active Directory Federation Services \(AD FS\)에 의해 보호 되는 리소스에 액세스 해야 하는 컴퓨터 계정을 Active Directory Domain Services 같은 특성 저장소, 저장 된 \ (AD DS \). 클레임 발급 엔진 특성 저장소를 사용 하 여 클레임 발행 해야 하는 데이터를 수집 합니다. 클레임으로 특성 상점에서 데이터 프로젝션 다음 됩니다.  
  
다음 절차 특성 저장소 서비스에 추가 하는 Federation 사용할 수 있습니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-an-attribute-store"></a>특성 저장소를 추가 하려면  
  
1.  열린 **AD FS 관리**합니다.  
  
2.  아래에서 **작업** 클릭 **특성 저장소를 추가**합니다.  

![특성 저장소 추가](media/Add-an-Attribute-Store/addstore1.PNG)
  
3.  에 **특성 저장소를 추가** 대화 상자에 추가 하려면 특성 스토어에 대 한 다음 속성을 구성 합니다.  
  
    -   **표시 이름**, 특성 스토어를 식별 하는 데 사용할 이름을 입력 합니다.  
  
    -   **특성 상점 유형**, 하거나 지원 되는 특성 상점 유형 선택 **Active Directory**, **LDAP**, 또는 **SQL**합니다.  
  
    -   **연결 문자열**LDAP(Lightweight Directory Access Protocol) \(LDAP\) 스토어 또는 구조적 쿼리 언어 \(SQL\) 스토어 선택한 경우, 특성 스토어에 연결 하는 데 사용 된 문자열을 입력 합니다. Active Directory 특성 스토어에 대 한 연결 문자열이 필요 합니다. 따라서이 필드 사용할 수 없습니다.  
  
        > [!NOTE]  
        > Adfs는 기본적으로 된 Active Directory 특성 저장소를 자동으로 만들어집니다.  
 
![특성 저장소 추가](media/Add-an-Attribute-Store/addstore2.PNG) 

4.  클릭 **확인**합니다.  
  
## <a name="additional-references"></a>추가 참조  

[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
  
[역할의 특성 스토어](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)  
