---
title: Hyper-v에 대 한 가상 로컬 영역 네트워크를 구성 합니다.
description: Hyper-v 호스트에서 virtual machines 사용에 대 한 가상 로컬 영역 네트워크 (VLAN)을 구성 하기 위한 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8510a709-001c-4eee-b6d6-c451e8a8a836
author: KBDAzure
ms.author: kathydav
ms.date: 10/11/2016
ms.openlocfilehash: 5b5eaf175e7c09124aaa3f7a33523e8b87a9ae84
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848464"
---
# <a name="configure-virtual-local-area-networks-for-hyper-v"></a>Hyper-v에 대 한 가상 로컬 영역 네트워크를 구성 합니다.
Virtual local area network \(Vlan\) 네트워크 트래픽을 격리 하는 방법을 제공 합니다. 스위치 및 라우터를 지 원하는 802.1 q Vlan 구성 됩니다. 여러 Vlan을 구성 하 고 해당 사이의 통신을 원하는 경우이 작업을 허용 하도록 네트워크 장치를 구성 해야 합니다. 

Vlan을 구성 하려면 다음이 필요 합니다.  
  
-   실제 네트워크 어댑터 및 드라이버를 지 원하는 802.1 q VLAN 태그를 지정 합니다.  
-   실제 네트워크 스위치를 지 원하는 802.1 q VLAN 태그를 지정 합니다.  
  
호스트에서 가상 스위치는 실제 스위치 포트에서 네트워크 트래픽을 허용 하도록 구성 합니다. 내부적으로 가상 컴퓨터를 사용 하려고 하는 VLAN Id입니다. 다음으로, 가상 컴퓨터에서 모든 네트워크 통신에 사용할 VLAN을 지정 하려면 가상 컴퓨터를 구성 합니다.  
  
#### <a name="to-allow-a-virtual-switch-to-use-a-vlan"></a>VLAN을 사용 하도록 가상 스위치를 허용 하려면  
  
1.  하이퍼 열기\-V 관리자입니다.  
  
2.  작업 메뉴에서 클릭 **가상 스위치 관리자**합니다.  
  
3.  아래에서 **가상 스위치**, Vlan을 지 원하는 실제 네트워크 어댑터에 연결 된 가상 스위치를 선택 합니다. 

4. VLAN ID를 아래에 있는 오른쪽 창에서 선택 **가상 LAN id 사용** 다음 VLAN ID에 대 한 숫자를 입력 하 고  
  
    가상 스위치에 연결 된 실제 네트워크 어댑터를 통해 이동 하는 모든 트래픽에 설정한 VLAN ID와 태그를 지정 합니다.  
  
#### <a name="to-allow-a-virtual-machine-to-use-a-vlan"></a>VLAN을 사용 하도록 가상 컴퓨터를 허용 하려면  
  
1.  하이퍼 열기\-V 관리자입니다.  
  
2.  결과 창에서 아래 **가상 컴퓨터**, 해당 가상 컴퓨터를 선택 하 고 마우스 오른쪽 단추로 클릭 한 다음 **설정을**합니다.  

3.  아래에서 **하드웨어**, vlan 설정 되는 가상 스위치를 선택 합니다.
  
4.  오른쪽 창에서 선택 **가상 LAN id 사용**, 가상 스위치에 대해 지정한 것과 동일한 VLAN ID를 입력 합니다. 

가상 컴퓨터를 더 많은 Vlan을 사용 해야 하는 경우 다음 중 하나를 수행 합니다.  
  
-   가상 스위치를 적절 한 VLAN Id 할당을 더 많은 가상 네트워크 어댑터를 연결 합니다. IP 주소를 올바르게 구성 되었는지 확인 하 고 올바른 IP 주소를 사용 하는 트래픽이 되도록 또한 VLAN을 통해 라우팅 합니다.  
  
-   트렁크 모드를 사용 하 여에서 가상 네트워크 word 어댑터를 구성 된 [설정\-VMNetworkAdapterVlan](https://technet.microsoft.com/library/hh848475.aspx) cmdlt 합니다.
  
## <a name="see-also"></a>관련 항목  
 
[하이퍼\-V 가상 스위치](https://technet.microsoft.com/windows-server-docs/networking/technologies/hyper-v-virtual-switch/hyper-v-virtual-switch)