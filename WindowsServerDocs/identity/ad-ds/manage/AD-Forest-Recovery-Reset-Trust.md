---
title: "전체 서버 백업-광고 숲 복구"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adfs
ms.openlocfilehash: 51b53e7348ae00ed2fc63711b9c3297279ebe033
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2017
---
# <a name="resetting-a-trust-password-on-one-side-of-the-trust"></a>한쪽의 보안 신뢰 암호 다시 설정  

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

 숲 복구와 관련 보안 위반 하는 경우 다음 절차 한쪽 신뢰 신뢰 암호 다시 설정 합니다. 이 자녀와 부모 도메인 뿐만 아니라이 도메인 (신뢰)와 다른 도메인 (신뢰할 수 있는) 간에 명시적 신뢰 간에 암묵적인 신뢰 포함 됩니다.  
  
 수신 신뢰 (이 도메인으로 표시 되 면) 라고 불립니다 신뢰 신뢰 도메인 측면에 암호를 재설정 합니다. 다음 보내는 신뢰 라고도 신뢰 신뢰할 수 있는 도메인 측면에 같은 암호를 사용 합니다. 각 (신뢰할 수 있는) 도메인의 첫 번째 DC 복원 보내는 신뢰 암호 다시 설정 합니다.  
  
 신뢰 암호를 재설정할 때 DC 해당 도메인 외부 잠재적으로 잘못 된 Dc와 복제 하지 않습니다 설치할 수 있도록 보장 합니다. 각는 도메인의 첫 번째 DC 복원 하는 동안 같은 신뢰 암호를 설정 하 여이 DC 각 복구 Dc 복제 있는지 확인 합니다. AD DS을 설치 하 여 복구 하는 도메인의 후속 Dc을 자동으로 설치 과정에서 이러한 새 암호를 복제 있습니다.  
  
## <a name="to-reset-a-trust-password-on-one-side-of-the-trust"></a>한쪽의 보안 신뢰 암호 다시 설정  
  
1.  명령 프롬프트에서 다음 명령을 입력 하 고 enter 다음과 같습니다.  
  
    ```  
    netdom experthelp trust  
    ```  
  
2.  이 명령을 NetDom 도구를 사용 하 여 보안 암호를 재설정할 제공 하는 구문 사용 합니다.  
  
     예를 들어 숲 두 도메인 경우-부모 및 자녀-부모 도메인에 복원된 DC의이 명령을 실행 하는 다음 명령을 구문을 사용 합니다.  
  
    ```  
    netdom trust parent domain name /domain:child domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*  
    ```  
  
     자녀가 도메인에 있는이 명령을 실행 하면 다음 명령을 구문을 사용.  
  
    ```  
    netdom trust child domain name /domain:parent domain name /resetOneSide /password:password /userO:administrator /passwordO:*  
    ```  
  
    > [!NOTE]
    >  **passwordT** trust의 양쪽 동일 해야 합니다. 한 번만 다음이 명령을 실행 (달리는 **netdom resetpwd** 명령) 자동으로 다시 설정 암호 두 번 하기 때문입니다.  
  
## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
