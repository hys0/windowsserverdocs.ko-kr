---
title: 가상 네트워크 및 Vlan 사용 이해
description: 이 항목에서는 Hyper-v 네트워크 가상화에 대 한 가상 네트워크 및 가상 로컬 영역 네트워크 (Vlan)에서 서로 어떻게 배웁니다. Hyper-v 네트워크 가상화를 사용 하 여 가상 네트워크 라고도 하는 오버레이 가상 네트워크를 만들 수 있습니다.
manager: dougkim
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
ms.date: 08/26/2018
ms.openlocfilehash: d126e97a91e4c61ecff00cc2b5a527618b2d4d0f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875534"
---
# <a name="understand-the-usage-of-virtual-networks-and-vlans"></a>가상 네트워크 및 Vlan 사용 이해

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 Hyper-v 네트워크 가상화에 대 한 가상 네트워크 및 가상 로컬 영역 네트워크 (Vlan)에서 서로 어떻게 배웁니다. Hyper-v 네트워크 가상화를 사용 하 여 가상 네트워크 라고도 하는 오버레이 가상 네트워크를 만들 수 있습니다.



  
소프트웨어 정의 네트워킹 (SDN) Windows Server 2016에서 Hyper-v 가상 스위치 내의 오버레이 가상 네트워크에 대 한 정책을 프로그래밍은 기반으로 합니다. Hyper-v 네트워크 가상화를 사용 하 여 가상 네트워크 라고도 하는 오버레이 가상 네트워크를 만들 수 있습니다. 
  
Hyper-v 네트워크 가상화를 배포할 때 오버레이 네트워크를 오버레이 또는 터널 헤더 (예: VXLAN 또는 NVGRE) 및 계층 3 IP 계층 2 이더넷 원래 테 넌 트 가상 컴퓨터의 계층 2 이더넷 프레임을 캡슐화 하 여 만들어집니다. 헤더 언더레이 (또는 물리적)에서 네트워크입니다. 오버레이 가상 네트워크를 여는 24 비트 가상 네트워크 식별자 (vni) 또는 테 넌 트 트래픽 격리를 유지 하 고 겹치는 IP 주소를 허용 하도록 식별 됩니다. VNI 이루어집니다 가상 서브넷 ID (VSID), 논리 스위치 ID 및 터널 id입니다.  
  
또한 여러 개의 가상 서브넷 접두사 (각각 표시는 VNI) 서로 직접 라우팅할 수 있도록 각 테 넌 트 (가상 라우팅 및 전달을-VRF에 유사한) 라우팅 도메인에 할당 됩니다. 교차 테 넌 트 (또는 라우팅 도메인 간) 게이트웨이 거치지 않고 라우팅이 지원 되지 않습니다.   
  
각 테 넌 트의 캡슐화 된 트래픽을 터널링 하는 실제 네트워크 공급자 논리 네트워크 라는 논리 네트워크로 표시 됩니다. 하나 이상의 서브넷이 공급자 논리 네트워크 구성, 각각 표시 하는 IP 접두사를 필요에 따라 802.1q VLAN 태그입니다.  
  
추가 논리 네트워크를 만들 수 있습니다 및 서브넷 관리 트래픽, 저장소 트래픽을 전달할 인프라용 실시간 마이그레이션 트래픽, 등입니다.  
  
Microsoft SDN Vlan을 사용 하 여 테 넌 트 네트워크의 격리를 지원 하지 않습니다. 테 넌 트 격리는 Hyper-v 네트워크 가상화 오버레이 가상 네트워크 및 캡슐화를 사용 하 여 전적으로 수행 됩니다. 


