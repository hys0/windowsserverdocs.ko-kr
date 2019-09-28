---
title: 가상 네트워크 및 Vlan 사용에 대 한 이해
description: 이 항목에서는 Hyper-v 네트워크 가상화 가상 네트워크 및 Vlan (virtual local area network)과 어떻게 다른 지에 대해 알아봅니다. Hyper-v 네트워크 가상화를 사용 하면 가상 네트워크 라고도 하는 오버레이 가상 네트워크를 만들 수 있습니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84ac2458-3fcf-4c4f-acfe-6105443dd83f
ms.author: pashort
author: shortpatti
ms.date: 08/26/2018
ms.openlocfilehash: 854adf0e7bb2a8715e3d447c04e2f09c3470a781
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355826"
---
# <a name="understand-the-usage-of-virtual-networks-and-vlans"></a>가상 네트워크 및 Vlan 사용에 대 한 이해

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 Hyper-v 네트워크 가상화 가상 네트워크 및 Vlan (virtual local area network)과 어떻게 다른 지에 대해 알아봅니다. Hyper-v 네트워크 가상화를 사용 하면 가상 네트워크 라고도 하는 오버레이 가상 네트워크를 만들 수 있습니다.



  
Windows Server 2016의 SDN (소프트웨어 정의 네트워킹)은 Hyper-v 가상 스위치 내의 오버레이 가상 네트워크에 대 한 프로그래밍 정책을 기반으로 합니다. Hyper-v 네트워크 가상화를 사용 하 여 가상 네트워크 라고도 하는 오버레이 가상 네트워크를 만들 수 있습니다. 
  
Hyper-v 네트워크 가상화를 배포할 때 오버레이 네트워크는 오버레이 또는 터널 헤더 (예: VXLAN 또는 NVGRE) 및 계층 3 IP 및 계층 2 Ethernet을 사용 하 여 원래 테 넌 트 가상 컴퓨터의 계층 2 이더넷 프레임을 캡슐화 하 여 만들어집니다. 언더레이 (또는 실제) 네트워크의 헤더입니다. 오버레이 가상 네트워크는 테 넌 트 트래픽 격리를 유지 하 고 겹치는 IP 주소를 허용 하기 위해 VNI (24 비트 Virtual Network Identifier)으로 식별 됩니다. VNI은 VSID (가상 서브넷 ID), 논리 스위치 ID 및 터널 ID로 구성 됩니다.  
  
또한 각 테 넌 트에는 여러 가상 서브넷 접두사 (각각 VNI으로 표시 됨)를 직접 라우팅할 수 있도록 라우팅 도메인 (가상 라우팅 및 전달-VRF)이 할당 됩니다. 게이트웨이를 통하지 않고 교차 테 넌 트 (또는 라우팅 도메인 간) 라우팅이 지원 되지 않습니다.   
  
각 테 넌 트의 캡슐화 된 트래픽이 터널링 되는 실제 네트워크는 공급자 논리 네트워크 라고 하는 논리 네트워크로 표시 됩니다. 이 공급자 논리 네트워크는 하나 이상의 서브넷으로 구성 되며, 각각 IP 접두사로 표시 되 고 선택적으로 VLAN 802.1 q 태그가 표시 됩니다.  
  
인프라를 위한 추가 논리 네트워크 및 서브넷을 만들어 관리 트래픽, 저장소 트래픽, 실시간 마이그레이션 트래픽 등을 수행할 수 있습니다.  
  
Microsoft SDN은 Vlan을 사용 하 여 테 넌 트 네트워크의 격리를 지원 하지 않습니다. 테 넌 트 격리는 Hyper-v 네트워크 가상화 오버레이 가상 네트워크 및 캡슐화를 사용 하는 경우에만 수행 됩니다. 


