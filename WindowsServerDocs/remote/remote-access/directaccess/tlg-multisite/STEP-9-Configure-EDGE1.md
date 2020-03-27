---
title: 9 단계 EDGE1 구성
description: 이 항목은 테스트 랩 가이드-Windows Server 2016에 대 한 DirectAccess 멀티 사이트 배포 시연의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6e8d85b-de65-43b3-bf3e-ec84471a1fcc
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 74c4eae329698d33b160ac7180bbabd6d1d8fbad
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314510"
---
# <a name="step-9-configure-edge1"></a>9 단계 EDGE1 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

EDGE1 서버에서 수행 되는 절차는 다음과 같습니다.  
  
1. EDGE1에서 DNS 서버를 구성 합니다. EDGE1의 corp2.corp.contoso.com 도메인에서 DNS 서버를 구성 해야 합니다.  
  
2. 서브넷 간 라우팅을 구성 합니다. EDGE1에서 라우팅을 구성 하 여 Corpnet와 Corpnet 서브넷 간의 통신을 사용 하도록 설정 합니다.  
  
## <a name="configure-the-dns-servers-on-edge1"></a><a name="IPv6"></a>EDGE1에서 DNS 서버 구성  
  
1.  서버 관리자 콘솔에서 **로컬 서버**를 클릭 한 다음 **속성** 영역에서 **Corpnet**옆에 있는 링크를 클릭 합니다.  
  
2.  네트워크 연결 창에서 **Corpnet**를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.  
  
3.  **Internet Protocol Version 4(TCP/IPv4)** 를 클릭하고 **속성**을 클릭합니다.  
  
4.  **대체 DNS 서버**에 **10.2.0.1**를 입력 합니다. **확인**을 클릭합니다.  
  
5.  **인터넷 프로토콜 버전 6(TCP/IPv6)** , **속성**을 차례로 클릭합니다.  
  
6.  **대체 DNS 서버**에 **2001: db8:2:: 1** 을 입력 한 다음 **확인**을 클릭 합니다.  
  
7.  **Corpnet 속성** 대화 상자에서 **닫기**를 클릭 합니다.  
  
8.  **네트워크 연결** 창을 닫습니다.  
  
## <a name="configure-routing-between-subnets"></a><a name="ConfigRouting"></a>서브넷 간 라우팅 구성  
  
1.  **시작** 화면에서**cmd.exe**를 입력 하 고 **cmd**를 마우스 오른쪽 단추로 클릭 한 다음 **고급**을 클릭 하 고 **관리자 권한으로 실행**을 클릭 합니다. **사용자 계정 컨트롤** 대화 상자가 표시되면 원하는 작업이 표시되어 있는지 확인하고 **예**를 클릭합니다.  
  
2.  명령 프롬프트 창에서 다음 명령을 입력 합니다. 각 명령을 입력 한 후 ENTER 키를 누릅니다.  
  
    ```  
    netsh interface IPv4 add route 10.2.0.0/24 Corpnet 10.0.0.254  
    netsh interface IPv6 add route 2001:db8:2::/64 Corpnet 2001:db8:1::fe  
    ```  
  
3.  명령 프롬프트 창을 닫습니다.  
  


