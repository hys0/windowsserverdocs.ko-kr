---
title: 데이터 센터 방화벽 개요
description: 이 항목에 대해 자세히 알아보려면 데이터 센터 방화벽, 네트워크 계층, 5 개 튜플 (프로토콜, 원본 및 대상 포트 번호, 원본 및 대상 IP 주소), Windows Server 2016에서 상태 저장, 다중 테 넌 트 방화벽에는 사용할 수 있습니다.
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
ms.openlocfilehash: f1de50dc61639f4985c9d28fdde6072af650f42e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890834"
---
# <a name="datacenter-firewall-overview"></a>데이터 센터 방화벽 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016

데이터 센터 방화벽은 Windows Server 2016에 포함 된 새 서비스입니다. 것은 네트워크 계층, 5 개 튜플 (프로토콜, 원본 및 대상 포트 번호, 원본 및 대상 IP 주소) 상태 저장, 다중 테 넌 트 방화벽입니다. 를 배포 하 고 서비스 공급자가 서비스로 제공 하는 경우 테 넌 트 관리자를 설치 하 고 원치 않는 트래픽이 인터넷에서 가상 네트워크와 인트라넷 네트워크를 보호 하는 방화벽 정책을 구성할 수 있습니다.  
  
![네트워크 스택의 데이터 센터 방화벽](../../../media/Datacenter-Firewall-Overview/MultitenantFirewallOverview2.png)  
  
서비스 공급자 관리자 또는 테 넌 트 관리자는 네트워크 컨트롤러 및 northbound Api를 통해 데이터 센터 방화벽 정책을 관리할 수 있습니다.  
  
데이터 센터 방화벽 클라우드 서비스 공급자에 대 한 다음과 같은 이점이 있습니다.  
  
-   테 넌 트에 제공할 수 있는 고도로 확장 가능한, 관리성 및 diagnosable 소프트웨어 기반 방화벽 솔루션  
  
-   테 넌 트 방화벽 정책을 위반 하지 않고 테 넌 트 가상 컴퓨터를 다른 계산 호스트로 이동 자유롭게  
  
    -   VSwitch 포트 호스트 에이전트 방화벽 배포  
  
    -   테 넌 트 가상 컴퓨터는 vSwitch 호스트 에이전트 방화벽에 할당 된 정책 가져오기  
  
    -   가상 머신에서 실행 중인 실제 호스트의 독립적인 각 vSwitch 포트에 구성 된 방화벽 규칙  
  
-   테 넌 트 게스트 운영 체제에 관계 없이 가상 컴퓨터를 테 넌 트에 대 한 보호를 제공 합니다.  
  
데이터 센터 방화벽 테 넌 트에 대 한 다음과 같은 이점이 있습니다.  
  
-   인터넷 연결 virtual network의 워크 로드를 보호 하는 방화벽 규칙을 정의 하는 기능  
  
-   동일한 L2 가상 서브넷에도 다른 L2 가상 서브넷의 가상 컴퓨터 또는 가상 머신 간에 트래픽을 보호 하는 방화벽 규칙을 정의 하는 기능  
  
-   보호 하 고 테 넌 트 간 네트워크 트래픽을 격리 하는 방화벽 규칙을 정의 하는 기능 온-프레미스 네트워크 및 가상 네트워크 서비스 공급자에서  
  


