---
title: 데이터 센터 방화벽 개요
description: 이 항목을 사용 하 여 네트워크 계층, 5 튜플 (프로토콜, 원본 및 대상 포트 번호, 원본 및 대상 IP 주소), 상태 저장, Windows Server 2016의 다중 테 넌 트 방화벽 인 데이터 센터 방화벽에 대해 알아볼 수 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67576533-206b-428a-956c-ed8c53218d9b
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 141057d2ee3e648f589d255ea04fdef179cedf3c
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317031"
---
# <a name="datacenter-firewall-overview"></a>데이터 센터 방화벽 개요

>적용 대상: Windows Server(반기 채널), Windows Server 2016

데이터 센터 방화벽은 Windows Server 2016에 포함 된 새로운 서비스입니다. 네트워크 계층, 5 튜플 (프로토콜, 원본 및 대상 포트 번호, 원본 및 대상 IP 주소), 상태 저장, 다중 테 넌 트 방화벽입니다. 서비스 공급자가 서비스를 배포 하 고 제공 하는 경우 테 넌 트 관리자는 인터넷 및 인트라넷 네트워크에서 발생 하는 원치 않는 트래픽 으로부터 가상 네트워크를 보호할 수 있도록 방화벽 정책을 설치 하 고 구성할 수 있습니다.  
  
![네트워크 스택의 데이터 센터 방화벽](../../../media/Datacenter-Firewall-Overview/MultitenantFirewallOverview2.png)  
  
서비스 공급자 관리자나 테 넌 트 관리자는 네트워크 컨트롤러 및 northbound Api를 통해 데이터 센터 방화벽 정책을 관리할 수 있습니다.  
  
데이터 센터 방화벽은 클라우드 서비스 공급자에 대해 다음과 같은 이점을 제공 합니다.  
  
-   테 넌 트에 제공할 수 있는 확장성, 관리 및 diagnosable의 확장성이 뛰어난 소프트웨어 기반 방화벽 솔루션  
  
-   테 넌 트 방화벽 정책을 중단 하지 않고 다른 계산 호스트로 테 넌 트 가상 컴퓨터를 자유롭게 이동할 수 있습니다.  
  
    -   VSwitch 포트 호스트 에이전트 방화벽으로 배포 됨  
  
    -   테 넌 트 가상 컴퓨터는 vSwitch 호스트 에이전트 방화벽에 할당 된 정책을 가져옵니다.  
  
    -   방화벽 규칙은 가상 컴퓨터를 실행 하는 실제 호스트와 관계 없이 각 vSwitch 포트에서 구성 됩니다.  
  
-   테 넌 트 게스트 운영 체제와 관계 없이 테 넌 트 가상 컴퓨터에 대 한 보호를 제공 합니다.  
  
데이터 센터 방화벽은 테 넌 트에 대해 다음과 같은 이점을 제공 합니다.  
  
-   가상 네트워크에서 인터넷 연결 작업을 보호 하는 데 도움이 되는 방화벽 규칙을 정의 하는 기능  
  
-   동일한 L2 가상 서브넷의 가상 컴퓨터와 다른 L2 가상 서브넷에 있는 가상 컴퓨터 간의 트래픽을 보호 하는 데 도움이 되는 방화벽 규칙을 정의 하는 기능  
  
-   서비스 공급자의 테 넌 트 온-프레미스 네트워크와 가상 네트워크 간에 네트워크 트래픽을 보호 하 고 격리 하는 데 도움이 되는 방화벽 규칙을 정의 하는 기능  
  


