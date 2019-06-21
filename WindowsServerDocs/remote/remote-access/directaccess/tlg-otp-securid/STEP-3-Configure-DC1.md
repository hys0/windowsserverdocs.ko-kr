---
title: 3 단계는 DC1 구성
description: 이 항목은 일부 테스트 랩 가이드-OTP 인증 및 Windows Server 2016 RSA SecurID를 사용한 DirectAccess 시연
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 836a2a08-3d22-48d2-873e-80d7e57ebbd6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 338e214ac10796d3f9864aef74190f2d27f173b7
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281352"
---
# <a name="step-3-configure-dc1"></a>3 단계는 DC1 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

DC1은 도메인 컨트롤러, DNS 서버 및 corp.contoso.com 도메인에 대 한 DHCP 서버 작동합니다. DC1을 다음과 같이 구성 합니다.  
  
## <a name="verify-user1-has-a-user-principal-name-defined-on-dc1"></a>User1이 DC1에 정의 된 사용자 보안 주체 이름을 확인 합니다.  
  
1.  Dc1에서 서버 관리자를 열고 클릭 **AD DS** 왼쪽된 창에서. 마우스 오른쪽 단추로 클릭 **DC1** 선택한 **Active Directory Users and Computers**합니다. 왼쪽된 창에서 **corp.contoso.com\Users**에 User1를 두 번 클릭 합니다.  
  
2.  에 **계정** 탭을 확인 하는 **사용자 로그온 이름** User1로 설정 됩니다. 그렇지 않은 경우 입력 한 다음 **User1** 에 **사용자 로그온 이름** 필드입니다.  
  
3.  **확인**을 클릭합니다. **Active Directory 사용자 및 컴퓨터** 콘솔을 닫습니다.  
  


