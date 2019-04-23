---
title: 단계 2 EDGE1 구성
description: 이 항목은 일부 테스트 랩 가이드-Windows Server 2016 Windows NLB를 사용 하 여 클러스터에서 DirectAccess 시연
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84457351-1ca7-4e7c-8e2c-53d55b1fcdc0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6c31e65fc7210849564bd0541085322a7a6c284e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838584"
---
# <a name="step-2-configure-edge1"></a>단계 2 EDGE1 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다음 절차는 DirectAccess 서버에서 수행 됩니다.

## <a name="to-configure-directaccess-on-edge1"></a>EDGE1에서 DirectAccess를 구성 하려면
  
1.  에 **시작** 화면에서 입력**RAMgmtUI.exe**, 한 다음 ENTER를 누릅니다. **사용자 계정 컨트롤** 대화 상자가 나타나면 원하는 작업이 표시되었는지 확인한 다음 **예**를 클릭합니다.  
  
2.  왼쪽된 창에서 원격 액세스 관리 콘솔에서 클릭 **구성**합니다.  
  
3.  콘솔의 가운데 창에서에 **2 단계 원격 액세스 서버** 영역에서 클릭 **편집**합니다.  
  
4.  에 **원격 액세스 서버 설치** 마법사를 클릭 **접두사 구성**합니다. 에 **접두사 구성** 페이지 **DirectAccess 클라이언트 컴퓨터에 할당 된 IPv6 접두사**를 입력 **2001:db8:1:1000:: 59 /** 를 클릭 하 고 **다음** .  
  
5.  **마침**을 클릭합니다.  
  
6.  콘솔의 가운데 창에서 클릭 **마침**합니다.  
  
7.  에 **원격 액세스 검토** 대화 상자에서 구성 설정을 검토 하 고 클릭 한 다음 **적용**합니다. **원격 액세스 설정 마법사 설정 적용** 대화 상자에서 **닫기**를 클릭합니다.
