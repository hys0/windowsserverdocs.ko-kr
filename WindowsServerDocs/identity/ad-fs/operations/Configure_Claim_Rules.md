---
ms.assetid: 20d48afc-2623-43e9-8ed9-aeb9a0505630
title: 클레임 규칙 구성
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b46e228f202eeae7f8cbcf4c1a6851686f905e48
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407638"
---
# <a name="configure-claim-rules"></a>클레임 규칙 구성

클레임 @ no__t-0based identity 모델에서 페더레이션 서비스로 Active Directory Federation Services (AD FS) 함수는 클레임 집합을 포함 하는 토큰을 발급 하는 것입니다. 클레임 규칙은 문제를 AD FS 하는 클레임과 관련 하 여 결정을 제어 합니다. 클레임 규칙 및 모든 서버 구성 데이터는 AD FS 구성 데이터베이스에 저장 됩니다.  
  
AD FS는 클레임 및 기타 컨텍스트 정보 형식으로 제공 되는 id 정보를 기반으로 하는 발급 결정을 내립니다. 높은 수준에서 AD FS 클레임 집합 하나를 입력으로 가져오고, 많은 변환을 수행 하 고, 다른 클레임 집합을 출력으로 반환 하 여 규칙 프로세서로 작동 합니다. 

다음 항목은 AD FS에서 처리할 규칙을 만드는 데 도움이 됩니다. 
  
-   [들어오는 클레임을 통과 또는 필터링 하는 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [모든 사용자를 허용하는 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)  
  
-   [들어오는 클레임에 따라 사용자를 허용 또는 거부하는 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [LDAP 특성을 클레임으로 전송 하는 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [클레임으로 그룹 멤버 자격을 보내는 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [들어오는 클레임을 변환하는 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [인증 방법 클레임을 보내는 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)  
  
-   [사용자 지정 규칙을 사용하여 클레임을 보내는 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-rule.md)  

## <a name="see-also"></a>관련 항목  
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md) 
