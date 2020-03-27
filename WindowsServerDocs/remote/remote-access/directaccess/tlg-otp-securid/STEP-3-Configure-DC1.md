---
title: 3 단계 DC1 구성
description: 이 항목은 테스트 랩 가이드-OTP 인증을 사용 하는 DirectAccess 시연 및 Windows Server 2016에 대 한 RSA SecurID의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 836a2a08-3d22-48d2-873e-80d7e57ebbd6
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8104868103fff29044041136b48c59d966cc7bd0
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314403"
---
# <a name="step-3-configure-dc1"></a>3 단계 DC1 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

DC1은 corp.contoso.com 도메인에 대 한 도메인 컨트롤러, DNS 서버 및 DHCP 서버 역할을 합니다. DC1을 다음과 같이 구성 합니다.  
  
## <a name="verify-user1-has-a-user-principal-name-defined-on-dc1"></a>U s e r 1에 사용자 계정 이름이 정의 되어 있는지 확인 합니다.  
  
1.  DC1에서 서버 관리자를 열고 왼쪽 창에서 **AD DS** 를 클릭 합니다. **DC1** 을 마우스 오른쪽 단추로 클릭 하 고 **Active Directory 사용자 및 컴퓨터**를 선택 합니다. 왼쪽 창에서 **com\Users**를 확장 하 고 User1을 두 번 클릭 합니다.  
  
2.  **계정** 탭에서 **사용자 로그온 이름** 이 User1으로 설정 되어 있는지 확인 합니다. 그렇지 않으면 **사용자 로그온 이름** 필드에 **User1** 을 입력 합니다.  
  
3.  **확인**을 클릭합니다. **Active Directory 사용자 및 컴퓨터** 콘솔을 닫습니다.  
  


