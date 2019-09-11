---
ms.assetid: af16e847-47c2-461e-9df1-cc352a322043
title: 그룹 구성원을 클레임으로 보내기 규칙을 사용할 경우
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 546507254f796e6a2fbe71e3ba30a7597ea51295
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869266"
---
# <a name="when-to-use-a-send-group-membership-as-a-claim-rule"></a>그룹 구성원을 클레임으로 보내기 규칙을 사용할 경우
지정 된 Active Directory 보안 그룹의 구성원 \(인\) 사용자 에게만 새 나가는 클레임 값을 발급 하려는 경우 Active Directory Federation Services AD FS에서이 규칙을 사용할 수 있습니다. 이 규칙을 사용하는 경우 다음 표에 설명된 대로 직접 지정하고 규칙 논리와 일치하는 그룹에 대한 단일 클레임만 발급합니다.  
  
|규칙 옵션|규칙 논리|  
|---------------|--------------|  
|나가는 클레임 값|사용자의 그룹 구성원이 *지정 된 그룹과* 같고 나가는 클레임 유형이 *지정 된 클레임 유형*과 같으면 기존 그룹 이름 값을 *지정 된 나가는 클레임 값* 으로 바꾸고 클레임을 발급 합니다.|  
  
다음 섹션에서는 클레임 규칙에 대한 기본 사항을 소개합니다. 또한 그룹 구성원을 클레임으로 보내기 규칙을 사용하는 경우에 대해 자세하게 설명합니다.  
  
## <a name="about-claim-rules"></a>클레임 규칙 정보  
클레임 규칙은 들어오는 클레임에 조건을 적용 하는 비즈니스 논리의 인스턴스를 나타냅니다 \(다음 y x if\) 조건 매개 변수를 기반으로 하는 나가는 클레임을 생성 합니다. 다음 목록은 이 항목을 더 읽기 전에 클레임 규칙에 대해 알아야 하는 중요한 팁을 간략하게 설명합니다.  
  
-   AD FS 관리 스냅인에서\-클레임 규칙을 다시 만든 클레임 규칙 템플릿을 사용 하 여  
  
-   클레임 규칙 프로세스 들어오는 클레임을 클레임 공급자에서 직접 \(Active Directory 또는 다른 페더레이션 서비스와 같은\) 또는 수용의 출력에서 클레임 공급자 트러스트에 대 한 규칙을 변환 합니다.  
  
-   클레임 규칙은 지정된 규칙 집합 내의 시간 순서대로 클레임 발급 엔진에 의해 처리됩니다. 규칙에 우선 순위를 설정하여 지정된 규칙 집합 내의 이전 규칙에 의해 생성된 클레임을 더욱 구체화하거나 필터링할 수 있습니다.  
  
-   클레임 규칙 템플릿에서는 항상 들어오는 클레임 유형을 지정해야 합니다. 그러나 단일 규칙을 사용하여 동일한 클레임 유형 내의 여러 클레임 값을 처리할 수 있습니다.  
  
클레임 규칙 및 클레임 규칙 집합에 대 한 정보를 자세한 참조 [규칙의 역할 클레임](The-Role-of-Claim-Rules.md)합니다. 규칙은 처리 하는 방법에 대 한 자세한 내용은 참조 [클레임 엔진의 역할](The-Role-of-the-Claims-Engine.md)합니다. 자세한 내용은 클레임 규칙 집합을 처리 하는 방법을 참조 하십시오 [클레임 파이프라인의 역할](The-Role-of-the-Claims-Pipeline.md)합니다.  
  
## <a name="outgoing-claim-value"></a>나가는 클레임 값  
그룹 구성원을 클레임으로 보내기 규칙 템플릿을 사용하여 사용자가 지정한 그룹의 구성원인지에 따라 클레임을 발급할 수 있습니다.  
  
즉,이 규칙 템플릿은 사용자에 게 관리자가 지정 하는 Active Directory 그룹과 일치 하는 그룹 \(보안\) ID SID가 있는 경우에만 클레임을 발급 합니다. Active Directory Domain Services \(ADDS\) 에 대해 인증 하는 모든 사용자는 자신이 속한 각 그룹에 대 한 들어오는 그룹 SID 클레임을 갖게 됩니다. 기본적으로 Active Directory 클레임 공급자 트러스트의 수용 변환 규칙은 이러한 그룹 SID 클레임을 통과합니다. 이러한 그룹 Sid를 클레임 발급 기준으로 사용 하는 것은 AD DS에서 사용자 그룹을 조회 하는 것 보다 훨씬 빠릅니다.  
  
이 규칙을 사용하면 선택한 Active Directory 그룹에 따라 단일 클레임만 전송됩니다. 예를 들어 이 규칙 템플릿을 사용하여 사용자가 Domain Admins 보안 그룹의 구성원인 경우 값이 “Admins”인 그룹 클레임을 보내는 규칙을 만들 수 있습니다.  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>클레임 공급자 트러스트에서 이 규칙 구성  
관리자는 그룹 SID가 Active Directory 또는 AD DS를 제외한 모든 클레임 공급자에게는 일반적이지 않은 클레임 공급자에서 수신될 때만 클레임 공급자 트러스트의 수용 변환 규칙에서 이 규칙 유형을 사용합니다.  
  
## <a name="how-to-create-this-rule"></a>이 규칙을 만드는 방법  
클레임 규칙 언어를 사용 하거나 AD FS 관리 스냅인\-에서 LDAP 그룹 구성원을 클레임으로 보내기 규칙 템플릿을 사용 하 여이 규칙을 만듭니다. 이 규칙 템플릿은 다음과 같은 구성 옵션을 제공합니다.  
  
-   클레임 규칙 이름 지정  
  
-   개체 선택기를 사용 하 여 사용자 그룹 선택  
  
-   나가는 클레임 유형 선택  
  
-   보내는 클레임 유형 필드에서 이름 \(id를 선택한 경우에만 사용할 수 있는 나가는 이름 id 형식을 선택 합니다.\)  
  
-   나가는 클레임 값 선택  
  
이 규칙을 만드는 방법에 대 한 자세한 내용은 [그룹 구성원을 클레임으로 전송 하는 규칙 만들기](https://technet.microsoft.com/library/ee913569.aspx)를 참조 하세요.  
  
## <a name="using-the-claim-rule-language"></a>클레임 규칙 언어 사용  
그룹 SID가 아닌 들어오는 SID에 따라 클레임을 발급하려면 들어오는 클레임 변환 규칙 템플릿을 사용합니다. 관리자가 사용자가 구성원으로 속한 모든 그룹의 이름을 검색하려면 **tokenGroups** 특성 대신 LDAP 특성을 클레임으로 보내기 규칙 템플릿을 사용합니다.  
  
### <a name="example-how-to-issue-group-claims-based-on-the-users-group-membership"></a>예: 사용자의 그룹 멤버 자격에 따라 그룹 클레임을 발급 하는 방법  
다음 규칙은 들어오는 그룹 SID에 따라 사용자에 대한 그룹 클레임을 발급합니다.  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-21-397933417-626991126-188441444-512", Issuer == "AD AUTHORITY"]  
=> issue(Type = "http://schemas.xmlsoap.org/claims/Group", Value = "administrators", Issuer = c.Issuer, OriginalIssuer = c.OriginalIssuer, ValueType = c.ValueType);  
```  
  
## <a name="additional-references"></a>추가 참조  
[LDAP 특성을 클레임으로 전송 하는 규칙 만들기](https://technet.microsoft.com/library/dd807115.aspx)  
  

