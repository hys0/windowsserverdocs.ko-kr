---
title: 가상 네트워크와 Vlan 이해 사용
description: 이 항목은 관리 테 작업 및 Windows Server 2016에 가상 네트워크 방법에 대해 소프트웨어 네트워킹 정의 가이드 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84ac2458-3fcf-4c4f-acfe-6105443dd83f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fcf84c5c1f0be2fa1c7524592f8d02e4b11d3a2b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="understanding-usage-of-virtual-networks-and-vlans"></a>가상 네트워크와 Vlan 이해 사용

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Hyper-v 네트워크 가상화 가상 네트워크와 가상 영역 로컬 네트워크 (Vlan)의 차이점에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.  
  
소프트웨어 정의 네트워킹 (SDN) Windows Server 2016에는 프로그래밍 Hyper-v 가상 스위치를 내 오버레이 가상 네트워크에 대 한 정책을 따릅니다. 네트워크 가상화 Hyper-v의 가상 네트워크 라고도 오버레이 가상 네트워크 만들 수 있습니다.   
  
Hyper-v 네트워크 가상화 배포 하는 경우 (예: VXLAN 또는 NVGRE) 오버레이-또는 터널-헤더 및 계층 3 IP와 2 계층 이더넷 언더레이 (또는 물리적)에서 머리글 네트워크 원래 테 가상 컴퓨터의 계층 2 이더넷 프레임 캡슐화 오버레이 네트워크 만들어집니다. 오버레이 가상 네트워크도 한 24 비트 가상 네트워크 식별자 (vni) 또는 테 교통 격리 유지 하 고 겹치는 IP 주소를 표시 됩니다. VNI 이루어져 가상 서브넷 ID (VSID), 논리 스위치 ID 및 터널 id입니다.  
  
또한 각 테 서로 여러 가상 서브넷 접두사 (으로 VNI 나타나는)를 직접 전달 수 있도록 (와 유사 가상 경로 및 전달-VRF) 라우팅 도메인을 지정 됩니다. 크로스 테 (또는 상호 라우팅 도메인) 게이트웨이 통해 연결 되지 않고 경로 지원 되지 않습니다.   
  
각 테 캡슐화 교통 터널링 실제 네트워크 공급자 논리 네트워크 이라고 논리 네트워크로 표시 됩니다. 하나 이상의 서브넷이 공급자 논리 네트워크로, IP 접두사을 하 고 필요에 따라 VLAN 802.1 q 각 표시 태그 합니다.  
  
마이그레이션 교통 체증 등 관리 교통, 저장소, 교통 상황을 갖고 갔 죠 인프라 목적을 위해 서브넷 라이브 및 추가 논리 네트워크 만들 수 있습니다.  
  
Microsoft SDN Vlan를 사용 하 여 테 네트워크를 분리 하 여 지원 하지 않습니다. 테 격리 Hyper-v 네트워크 가상화 오버레이 가상 네트워크와 캡슐화 사용 하 여 단독으로 수행 됩니다. 


