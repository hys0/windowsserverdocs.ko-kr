---
title: 4 단계 APP1 구성
description: 이 항목에서는 테스트 랩 가이드의 일부인-DirectAccess 멀티 사이트 배포에 대 한 Windows Server 2016를 보여 줍니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7000e80f-31b1-43c5-b51e-1469d26909e5
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 208839b827965d5fdbef4927f25a2477e117999b
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283188"
---
# <a name="step-4-configure-app1"></a>4 단계 APP1 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

APP1 2 Corpnet 서브넷에 대 한 액세스를 사용 하도록 설정 하려면 정적 IPv6 주소 지정 및 게이트웨이 설정을 구성 합니다.  
  
- 기본 게이트웨이 및 DNS 서버를 구성 합니다. ROUTER1 컴퓨터 기본 게이트웨이로 사용 하는 멀티 사이트 구성 합니다. APP1에서 기본 게이트웨이 구성 합니다.  
  
## <a name="to-configure-the-default-gateway-and-dns-server"></a>기본 게이트웨이 및 DNS 서버를 구성 하려면  
  
1.  서버 관리자 콘솔에서 클릭 **로컬 서버**를 선택한 다음는 **속성** 영역에서 다음을 **유선 이더넷 연결**, 링크를 클릭 합니다.  
  
2.  에 **네트워크 연결** 창에서 마우스 오른쪽 단추로 클릭 **유선 이더넷 연결**를 클릭 하 고 **속성**합니다.  
  
3.  에 **유선 이더넷 연결 속성** 대화 상자, 클릭 **인터넷 프로토콜 버전 4 (Tcp/ipv4)** 를 클릭 하 고 **속성**합니다.  
  
4.  **기본 게이트웨이**, 형식 **10.0.0.254**, 및 **대체 DNS 서버**, 형식 **10.2.0.1**를 클릭 하 고 **확인** .  
  
5.  에 **유선 이더넷 연결 속성** 대화 상자, 클릭 **인터넷 프로토콜 버전 6(ipv6) TCP/** 를 클릭 하 고 **속성**합니다.  
  
6.  **기본 게이트웨이**, 형식 **2001:db8:1::fe**합니다. **대체 DNS 서버**, 형식 **2001:db8:2::1**를 클릭 하 고 **확인**합니다.  
  
7.  에 **유선 이더넷 연결 속성** 대화 상자에서 클릭 **닫습니다**를 닫은 다음 합니다 **네트워크 연결** 창.  
  


