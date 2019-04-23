---
title: 9 단계 EDGE1 구성
description: 이 항목에서는 테스트 랩 가이드의 일부인-DirectAccess 멀티 사이트 배포에 대 한 Windows Server 2016를 보여 줍니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6e8d85b-de65-43b3-bf3e-ec84471a1fcc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f5d216934f0d09cdef97ce4405161862b112d632
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864874"
---
# <a name="step-9-configure-edge1"></a>9 단계 EDGE1 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다음 절차는 EDGE1 서버에서 수행 됩니다.  
  
1. EDGE1에서 DNS 서버를 구성 합니다. EDGE1에서 corp2.corp.contoso.com 도메인에서 DNS 서버를 구성 하는 것이 반드시 합니다.  
  
2. 서브넷 간 라우팅을 구성 합니다. Corpnet 및 2 Corpnet 서브넷 간의 통신이 가능 하도록 EDGE1에 라우팅을 구성 합니다.  
  
## <a name="IPv6"></a>EDGE1에서 DNS 서버를 구성 합니다.  
  
1.  서버 관리자 콘솔에서 클릭 **로컬 서버**를 선택한 다음는 **속성** 영역에서 다음을 **Corpnet**, 링크를 클릭 합니다.  
  
2.  네트워크 연결 창에서 마우스 오른쪽 단추로 클릭 **Corpnet**를 클릭 하 고 **속성**합니다.  
  
3.  **Internet Protocol Version 4(TCP/IPv4)** 를 클릭하고 **속성**을 클릭합니다.  
  
4.  **대체 DNS 서버**, 형식 **10.2.0.1**합니다. **확인**을 클릭합니다.  
  
5.  **인터넷 프로토콜 버전 6(TCP/IPv6)**, **속성**을 차례로 클릭합니다.  
  
6.  **대체 DNS 서버**, 형식 **2001:db8:2::1** 을 클릭 한 다음 **확인**합니다.  
  
7.  에 **Corpnet 속성** 대화 상자, 클릭 **닫기**합니다.  
  
8.  **네트워크 연결** 창을 닫습니다.  
  
## <a name="ConfigRouting"></a>서브넷 간 라우팅 구성  
  
1.  에 **시작** 화면에서 입력**cmd.exe**를 마우스 오른쪽 단추로 클릭 **cmd**, 클릭 **고급**를 클릭 하 고 **으로 실행 관리자**합니다. **사용자 계정 컨트롤** 대화 상자가 나타나면 원하는 작업이 표시되었는지 확인한 다음 **예**를 클릭합니다.  
  
2.  명령 프롬프트 창에서 다음 명령을 입력 합니다. 각 명령을 입력 한 후 enter 키를 누릅니다.  
  
    ```  
    netsh interface IPv4 add route 10.2.0.0/24 Corpnet 10.0.0.254  
    netsh interface IPv6 add route 2001:db8:2::/64 Corpnet 2001:db8:1::fe  
    ```  
  
3.  명령 프롬프트 창을 닫습니다.  
  


