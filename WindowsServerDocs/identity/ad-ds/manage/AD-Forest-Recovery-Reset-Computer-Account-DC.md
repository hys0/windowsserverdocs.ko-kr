---
title: AD 포리스트 복구-DC의 컴퓨터 계정 다시 설정
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 4e1a6070-df0a-4dfe-8773-899a010bfabd
ms.technology: identity-adds
ms.openlocfilehash: 388b460196888d4ca0cd12218972197afb6d49c5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852764"
---
# <a name="ad-forest-recovery---resetting-the-computer-account-on-the-dc"></a>AD 포리스트 복구-DC의 컴퓨터 계정 다시 설정

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

 DC의 컴퓨터 계정 암호를 재설정 하려면 다음 절차를 따르십시오. 
  
## <a name="to-reset-the-computer-account-password-of-the-domain-controller"></a>도메인 컨트롤러의 컴퓨터 계정 암호를 재설정 하려면  

1. 명령 프롬프트에 다음 명령을 입력한 후 Enter 키를 누릅니다.  

   ```
   netdom help resetpwd  
   ```
  
2. 이 명령은 Netdom 명령줄 도구를 사용 하 여 예를 들어 컴퓨터 계정 암호를 재설정 하는 구문 사용 합니다.  

   ```
   netdom resetpwd /server:domain controller name /userD:administrator /passwordd:*  
   ```  
  
    여기서 *도메인 컨트롤러 이름* 복구 하는 로컬 DC입니다. 
  
   > [!NOTE]
   > 이 명령은 두 번 실행 해야 합니다.
  
## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)
