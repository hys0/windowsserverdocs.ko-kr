---
title: AD 포리스트 복구-DC에서 컴퓨터 계정 다시 설정
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 4e1a6070-df0a-4dfe-8773-899a010bfabd
ms.technology: identity-adds
ms.openlocfilehash: 320d02f789b8dda771b648b0aa9a58f545f3358b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71368872"
---
# <a name="ad-forest-recovery---resetting-the-computer-account-on-the-dc"></a>AD 포리스트 복구-DC에서 컴퓨터 계정 다시 설정

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

 다음 절차를 사용 하 여 DC의 컴퓨터 계정 암호를 다시 설정할 수 있습니다. 
  
## <a name="to-reset-the-computer-account-password-of-the-domain-controller"></a>도메인 컨트롤러의 컴퓨터 계정 암호를 다시 설정 하려면  

1. 명령 프롬프트에 다음 명령을 입력한 후 Enter 키를 누릅니다.  

   ```
   netdom help resetpwd  
   ```
  
2. 이 명령이 Netdom 명령줄 도구를 사용 하 여 컴퓨터 계정 암호를 다시 설정 하기 위해 제공 하는 구문을 사용 합니다. 예를 들면 다음과 같습니다.  

   ```
   netdom resetpwd /server:domain controller name /userD:administrator /passwordd:*  
   ```  
  
    여기서 *도메인 컨트롤러 이름은* 복구 하려는 로컬 DC입니다. 
  
   > [!NOTE]
   > 이 명령을 두 번 실행 해야 합니다.
  
## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
