---
title: Datacenter 방화벽 개요
description: 이 항목에 대해 자세히 알아보려면 Datacenter 방화벽 하는 경우 네트워크 계층, 5 튜플을 (원본과 대상, 프로토콜 포트 번호, IP 주소 원본과 대상), Windows Server 2016에 상태를 넌 방화벽 사용할 수 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67576533-206b-428a-956c-ed8c53218d9b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0c9b9fb5b0fb9aa09ed783b2b66a8ad370a627c3
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="datacenter-firewall-overview"></a>Datacenter 방화벽 개요

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Datacenter 방화벽은 Windows Server 2016에 포함 된 새로운 서비스입니다. 네트워크 계층, 5 튜플을 (프로토콜, 원본과 대상 포트 번호, IP 주소 원본과 대상), 상태를 넌 방화벽입니다. 배포 서비스 공급자가 서비스를 제공 하는 경우 테 관리자가 설치 하 고 인터넷에서 가져온 원하지 않는 교통에서 가상 네트워크와 인트라넷 네트워크의 보호를 위해 방화벽 정책을 구성 수 있습니다.  
  
![네트워크 스택에서 Datacenter 방화벽](../../../media/Datacenter-Firewall-Overview/MultitenantFirewallOverview2.png)  
  
서비스 공급자 관리자 또는 테 관리자 네트워크 컨트롤러 및 northbound Api를 통해 데이터 센터 방화벽 정책 관리할 수 있습니다.  
  
Datacenter 방화벽 클라우드 서비스 공급자에 대 한 다음 이점이 있습니다.  
  
-   테 넌 제공 될 수 있는 소프트웨어 기반 매우 확장 하 고 관리 diagnosable 방화벽 솔루션을  
  
-   마음껏 테 방화벽 정책을 중단 하지 않고 다른 컴퓨팅 호스트 테 가상 컴퓨터 이동 하려면  
  
    -   VSwitch 포트 호스트 에이전트 방화벽 배포  
  
    -   테 가상 컴퓨터 vSwitch 호스트 에이전트 방화벽에 할당 된 정책을 받기  
  
    -   가상 컴퓨터를 실행 하는 실제 호스트 독립적인 각 vSwitch 포트에서 방화벽 규칙은 구성  
  
-   가상 컴퓨터 테 게스트 운영 체제의 독립 테 넌 트을 보호합니다  
  
Datacenter 방화벽 테 넌에 대 한 다음 이점이 있습니다.  
  
-   인터넷에 연결 가상 네트워크에서 작업을 보호 하기 위해 방화벽 규칙 정의 하는 기능  
  
-   방화벽 규칙 같은 l 2 가상 서브넷도 서로 다른 l 2 가상 서브넷에서 가상 컴퓨터: 사이 가상 컴퓨터 간에 교통 보호 하기 위해 정의 하는 기능  
  
-   방화벽 규칙을 보호 하 고 테 간의 네트워크 트래픽을 분리 정의 하는 기능 온-프레미스 네트워크와의 가상 네트워크 서비스 공급자에  
  


