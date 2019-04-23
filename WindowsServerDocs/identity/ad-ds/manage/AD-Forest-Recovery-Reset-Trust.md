---
title: AD 포리스트 복구-전체 서버 백업
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adds
ms.openlocfilehash: 455c930a90cd443cf1fe62f436abca88384f79c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865564"
---
# <a name="resetting-a-trust-password-on-one-side-of-the-trust"></a>트러스트의 한 쪽에서 트러스트 암호를 재설정  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

 보안 위반에 관련 되는 포리스트 복구 하는 경우 트러스트의 한 쪽에서 트러스트 암호를 재설정 하려면 다음 절차를 따르십시오. (트러스팅 도메인)이 도메인과 다른 도메인 (트러스트 된 도메인) 간의 트러스트를 명시적 뿐만 아니라 자식 및 부모 도메인 간에 암시적 트러스트가 포함 됩니다. 
  
 우변만 트러스팅 도메인의 신뢰를 받는 트러스트 (이 도메인이 속해 있는 쪽) 라고도 하며 암호를 다시 설정 합니다. 그런 다음 같은 암호를 사용 하 여를 보내는 트러스트 라고도 트러스트의 트러스트 된 도메인 우변. 각각 다른 (신뢰할 수 있는) 도메인의 첫 번째 DC를 복원 하는 경우 보내는 트러스트 암호를 재설정 합니다. 
  
 트러스트 암호를 다시 설정 하면 해당 도메인 외부의 잠재적으로 잘못 된 Dc를 사용 하 여 DC 복제 하지 않습니다. 각 도메인에 첫 번째 DC를 복원 하는 동안 동일한 트러스트 암호를 설정 하면 각 복구 된 Dc를 사용 하 여이 DC가 있는지 확인 합니다. 후속 도메인의 Dc에서에서 AD DS를 설치 하 여 복구 되는 설치 과정에서 이러한 새 암호를 자동으로 복제 됩니다. 
  
## <a name="to-reset-a-trust-password-on-one-side-of-the-trust"></a>트러스트의 한 쪽에서 트러스트 암호를 재설정 하려면  
  
1. 명령 프롬프트에 다음 명령을 입력한 후 Enter 키를 누릅니다.  

   ```  
   netdom experthelp trust  
   ```  
  
2. 이 명령은 NetDom 도구를 사용 하 여 트러스트 암호를 재설정 하는 구문 사용 합니다.
   예를 들어, 두 도메인 포리스트에 있는 경우-부모 및 자식-부모 도메인에서 복원된 된 DC에서이 명령을 실행 하 고 다음 명령 구문을 사용 합니다.  

   ```  
   netdom trust parent domain name /domain:child domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*  
   ```  

   이 명령은 자식 도메인에서를 실행 하면 다음 명령 구문을 사용 합니다.  

   ```  
   netdom trust child domain name /domain:parent domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*  
   ```  

   > [!NOTE]
   > **passwordT** 트러스트의 양쪽 모두에 동일한 값 이어야 합니다. 이 명령을 한 번만 실행 (달리 합니다 **netdom resetpwd** 명령) 자동으로 다시 설정 암호를 두 번 때문에 있습니다. 
  
## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)
