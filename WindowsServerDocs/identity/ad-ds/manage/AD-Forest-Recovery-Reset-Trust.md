---
title: AD 포리스트 복구-전체 서버 백업
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adds
ms.openlocfilehash: 6466fbc1caed7dc6efcbcd925eba1bd4e01135b6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823696"
---
# <a name="resetting-a-trust-password-on-one-side-of-the-trust"></a>트러스트의 한 쪽에서 트러스트 암호 다시 설정  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

 포리스트 복구가 보안 위반에 관련 된 경우 다음 절차를 사용 하 여 트러스트의 한 쪽에서 트러스트 암호를 다시 설정 합니다. 여기에는 자식 도메인과 부모 도메인 간의 암시적 트러스트 뿐만 아니라이 도메인 (트러스팅 도메인)과 다른 도메인 (트러스트 된 도메인) 간의 명시적 트러스트가 포함 됩니다. 
  
 트러스트의 트러스팅 도메인 쪽 에서만 암호를 다시 설정 합니다 .이 도메인은 들어오는 트러스트 (이 도메인이 속한 쪽) 라고도 합니다. 그런 다음 트러스트의 트러스트 된 도메인 측 (보내는 트러스트)에서 동일한 암호를 사용 합니다. 다른 (트러스트 된) 도메인 각각의 첫 번째 DC를 복원할 때 보내는 트러스트의 암호를 다시 설정 합니다. 
  
 트러스트 암호를 다시 설정 하면 DC가 도메인 외부의 잠재적으로 잘못 된 Dc로 복제 되지 않습니다. 각 도메인의 첫 번째 DC를 복원 하는 동안 동일한 트러스트 암호를 설정 하 여이 DC가 복구 된 각 Dc에 복제 되는지 확인 합니다. AD DS를 설치 하 여 복구 된 도메인의 후속 Dc는 설치 과정에서 이러한 새 암호를 자동으로 복제 합니다. 
  
## <a name="to-reset-a-trust-password-on-one-side-of-the-trust"></a>트러스트의 한 쪽에서 트러스트 암호를 다시 설정 하려면  
  
1. 명령 프롬프트에 다음 명령을 입력한 후 Enter 키를 누릅니다.  

   ```  
   netdom experthelp trust  
   ```  
  
2. NetDom 도구를 사용 하 여 트러스트 암호를 다시 설정 하기 위해이 명령이 제공 하는 구문을 사용 합니다.
   예를 들어 포리스트에 도메인 두 대 (부모 및 자식)가 있고 부모 도메인의 복원 된 DC에서이 명령을 실행 하는 경우 다음 명령 구문을 사용 합니다.  

   ```  
   netdom trust parent domain name /domain:child domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*  
   ```  

   자식 도메인에서이 명령을 실행 하는 경우 다음 명령 구문을 사용 합니다.  

   ```  
   netdom trust child domain name /domain:parent domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*  
   ```  

   > [!NOTE]
   > **Passwordt** 는 트러스트의 양쪽에서 같은 값 이어야 합니다. 이 명령은 자동으로 암호를 두 번 다시 설정 하기 때문에 ( **netdom resetpwd** 명령과 달리) 한 번만 실행 합니다. 
  
## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
