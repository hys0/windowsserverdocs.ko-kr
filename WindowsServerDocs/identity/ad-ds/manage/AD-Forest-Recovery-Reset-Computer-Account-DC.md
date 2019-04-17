---
title: "광고 숲 복구-DC에서 컴퓨터 계정을 다시 설정"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 4e1a6070-df0a-4dfe-8773-899a010bfabd
ms.technology: identity-adfs
ms.openlocfilehash: 588510a27f56abb4497b2f80fa0281a858a7e8eb
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---resetting-the-computer-account-on-the-dc"></a>광고 숲 복구-DC에서 컴퓨터 계정을 다시 설정 

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

 다음 절차 dc 컴퓨터 계정 암호 다시 설정 합니다.  
  
## <a name="to-reset-the-computer-account-password-of-the-domain-controller"></a>도메인 컨트롤러의 컴퓨터 계정 암호 다시 설정  
  
1.  명령 프롬프트에서 다음 명령을 입력 하 고 enter 다음과 같습니다.  
  
    ```  
    netdom help resetpwd  
    ```  
  
2.  이 명령을 Netdom 명령줄 도구를 사용 하 여 예를 들어 컴퓨터 계정 암호 다시 설정 하는 구문 사용:  
  
    ```  
    netdom resetpwd /server:domain controller name /userD:administrator /passwordd:*  
    ```  
  
     여기서 *도메인 컨트롤러의 이름을* 복구 하는 로컬 DC입니다.  
  
    > [!NOTE]
    >  두 번이 명령을 실행 해야 합니다.  
  
## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
