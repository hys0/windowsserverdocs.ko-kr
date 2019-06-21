---
title: NIC 팀 설정
description: 이 항목에서는 팀 같은 NIC 팀 속성의 개요를 제공 하 고 부하 분산 모드. 또한 제공 대기 어댑터 설정 및 기본 팀 인터페이스 속성에 대 한 세부 정보입니다. NIC 팀을 두 개 이상의 네트워크 어댑터가 있는 경우 내결함성을 위해 대기 어댑터를 지정할 필요가 없습니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4caaa86-5799-4580-8775-03ee213784a3
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: dd222cdbcd8b4eee19da6b79e12bd11f6bdd8629
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283732"
---
# <a name="nic-teaming-settings"></a>NIC 팀 설정
이 항목에서는 팀 같은 NIC 팀 속성의 개요를 제공 하 고 부하 분산 모드. 또한 제공 대기 어댑터 설정 및 기본 팀 인터페이스 속성에 대 한 세부 정보입니다. NIC 팀을 두 개 이상의 네트워크 어댑터가 있는 경우 내결함성을 위해 대기 어댑터를 지정할 필요가 없습니다.


  
![NIC 팀 속성](../../media/Create-a-New-NIC-Team-on-a-Host-Computer-or-VM/nict_06_properties.jpg)  

## <a name="teaming-modes"></a>팀 모드 
팀 모드에 대 한 옵션은 **독립 스위치** 하 고 **스위치 종속**합니다. 스위치 종속 모드 포함 **정적 팀** 하 고 **집계 제어 프로토콜 (LACP (링크)** 합니다. 

>[!TIP]
>NIC 팀 성능의 동적 배포의 부하 분산 모드를 사용 하는 것이 좋습니다.  
  
### <a name="switch-independent"></a>독립 스위치
  
[!INCLUDE [switch-independent-shortdesc-include](../../includes/switch-independent-shortdesc-include.md)] 
  
동적 배포와 함께 스위치 독립 모드를 사용 하면 네트워크 트래픽 부하를 동적 부하 분산 알고리즘에 의해 수정 된 TCP 포트 주소 해시에 따라 분산 됩니다. 동적 부하 분산 알고리즘을 개별 흐름 전송 간에 하나의 활성 팀 구성원에서 이동할 수 있도록 팀 멤버 대역폭 사용률을 최적화 하는 흐름을 재배포 합니다. 알고리즘은 트래픽을 재배포 초래할 패킷 순서가 배달 가능성을 최소화 하는 단계를 사용 하도록 작은 가능성을 고려 합니다.  
  
### <a name="switch-dependent"></a>스위치 종속  

[!INCLUDE [switch-dependent-shortdesc-include](../../includes/switch-dependent-shortdesc-include.md)]  
  
> [!IMPORTANT]  
> 스위치 종속 팀을 선택 하려면 모든 팀원이 동일한 물리적 스위치에 연결 되어 있거나 다중 섀시 스위치를 여러 섀시 간의 스위치 ID를 공유 합니다.


- **정적 팀 구성 합니다.** 정적 팀 스위치와 식별에 호스트를 수동으로 구성 해야 링크 팀을 구성 합니다. 정적으로 구성 된 솔루션 이기 때문에 스위치를 지원 하기 위해 추가 프로토콜이 없습니다를 올바르게 식별에 호스트 연결 된 케이블 또는 팀이 하는 데 실패를 일으킬 수 있는 다른 오류 대개 서버급 스위치에서 이 모드를 지원합니다.

- **링크 집계 제어 프로토콜 (LACP)입니다.** 달리 정적 팀, LACP 팀 모드는 호스트와 스위치 간에 연결 된 링크를 동적으로 식별 합니다. 이 동적 연결 전송 또는 피어 엔터티에서 LACP 패킷의 수신 하면 팀을 이론상에서 하지만 거의 연습, 확장 및 팀에서 자동으로 만들을 수 있습니다. 모든 서버급 스위치 LACP를 지원 하 고 스위치 포트에 대해 LACP 관리 목적으로 사용할 수 있도록 네트워크 운영자 모두 필요 합니다. LACP 팀 모드를 구성한 경우 NIC 팀 항상 간단한 타이머를 사용 하 여 LACP의 활성 모드에서 작동 됩니다.  없음 옵션은 타이머를 수정 하거나 LACP 모드를 변경 하려면 현재 사용할 수 있습니다.


스위치 종속 모드를 사용 하 여 동적 배포를 사용 하 여 동적 부하 분산 알고리즘에 의해 수정 된 TransportPorts 주소 해시에 따라 네트워크 트래픽 부하를 분배 됩니다.  동적 부하 분산 알고리즘 팀 멤버 대역폭 사용률을 최적화 하는 흐름을 재배포 합니다. 개별 흐름 전송 동적 배포의 일부로 다른 활성 팀 멤버에서 이동할 수 있습니다. 알고리즘은 트래픽을 재배포 초래할 패킷 순서가 배달 가능성을 최소화 하는 단계를 사용 하도록 작은 가능성을 고려 합니다.  
  
모든 스위치 종속 구성 하는 스위치 팀 구성원 간에 트래픽을 분산 하는 방법을 결정 합니다.  스위치는 팀 멤버에 트래픽을 분산의 적절 한 작업을 수행 해야 하지만 수행 하는 방법을 확인 하려면 완료 독립성입니다.  


## <a name="load-balancing-modes"></a>부하 분산 모드  
부하 분산 배포 모드에 대 한 옵션은 **주소 해시**하십시오 **Hyper-v 포트**, 및 **동적**합니다.  
  
### <a name="address-hash"></a>주소 해시
  
[!INCLUDE [address-hash-shortdesc-include](../../includes/address-hash-shortdesc-include.md)]
  
Windows PowerShell을 사용 하 여 다음 해시 함수 구성 요소에 대 한 값을 지정 합니다.  
  
-   원본 및 대상 TCP 포트 및 원본 및 대상 IP 주소입니다. 선택 하는 경우 이것이 기본값 **주소 해시** 로드 균형 조정 모드입니다.  
  
-   원본 및 대상 IP 주소에만 합니다.  
  
-   원본 및 대상 MAC 주소만 합니다.  
  
TCP 포트 해시는 트래픽 스트림, 독립적으로 이동할 수 NIC 팀 구성원 간에 더 작은 스트림이 생성의 가장 세분화 된 배포를 만듭니다. 그러나 없는 TCP 트래픽에 대해 TCP 포트 해시를 사용할 수 없습니다 또는 UDP 기반 있는 TCP 및 UDP 포트는 숨기 거 나 스택에서 같은 트래픽이 IPsec 보호 합니다. 이러한 경우에 IP 주소 해시를 자동으로 사용 하는 해시 또는 MAC 주소 해시는 트래픽을 IP 트래픽이 없는 경우.  
  
### <a name="hyper-v-port"></a>Hyper-v 포트
  
[!INCLUDE [hyper-v-port-shortdesc-include](../../includes/hyper-v-port-shortdesc-include.md)]  
  
인접 스위치가 항상 특정 MAC 주소를 하나의 포트에서을 인식 하기 때문에 스위치를 수신 부하 (트래픽 스위치에서 호스트에) 대상 MAC (VM의 MAC) 주소에 따라 여러 링크에서 분산 합니다. 특히 유용 가상 컴퓨터 큐 (Vmq)를 사용 하는 큐 트래픽이 도착 하는 데 필요한 특정 NIC에 배치할 수 있으므로 합니다.  
  
그러나 호스트에 몇 가지 Vm만 있는 경우이 모드는 균형이 분포를 달성 하기 위해 충분히 세부적인 아닐 수도 있습니다. 이 모드는 항상 단일 인터페이스에서 사용할 수 있는 대역폭을 단일 VM (즉, 단일 스위치 포트에서 트래픽)를 제한 합니다. NIC 팀 따라서는 VM 스위치 포트에 대해 둘 이상의 MAC 주소를 사용 하 여 구성 될 수 있습니다 때문에 원본 MAC 주소를 사용 하는 대신 식별자로에서 Hyper-v 가상 스위치 포트를 사용 합니다.  
  
### <a name="dynamic"></a>Dynamic
  
[!INCLUDE [dynamic-shortdesc-include](../../includes/dynamic-shortdesc-include.md)]
  
이 모드에서는 아웃 바운드 로드는 동적으로 flowlets의 개념에 따라 분산 됩니다. 실제 음성 단어 및 문장 끝에 자연 스러운 나누기가 하는 것 처럼 TCP 흐름 (TCP 통신 스트림을)는 또한 자연스럽 게 발생 나누기를 가집니다. 이러한 두 나누기 사이 TCP 흐름의 부분을 flowlet 라고 합니다.  
  
동적 모드 알고리즘을 flowlet 경계 발생 했습니다.-TCP 흐름-에서 충분 한 길이의 중단 발생 했을 때와 같은 검색 하는 경우 알고리즘은 자동으로 변경 다른 팀 멤버에 해당 하는 경우.  경우에 따라 알고리즘 흐름 어떤 flowlets를 포함 하지 않는 균형 다시 맞추기 정기적으로 될 수 있습니다. 이 때문에 TCP 흐름 및 팀 멤버 간에 선호도 팀 멤버의 부하를 분산 동적 분산 알고리즘에 따라 언제 든 지 변경할 수 있습니다.  
  
팀은 독립 스위치 또는 스위치 종속 모드 중 하나를 사용 하 여 구성 하는지 여부를 동적 배포 모드를 사용 하 여 최상의 성능을 위해 하는 것이 좋습니다.  
  
NIC 팀에 두 팀 멤버, 스위치 독립 모드에서 구성 되어 있고 활성/대기 모드 active 하나의 nic를 설정 하 고 대기 모드에 대해 구성 된 다른 경우에이 규칙에 예외가 있습니다. 이 NIC 팀 구성을 사용 하 여 주소 해시 배포 배포 동적 보다 성능이 약간 향상을 제공합니다.  


## <a name="standby-adapter-setting"></a>대기 중인 어댑터 설정  
대기 어댑터에 대 한 옵션은 **없음 (모든 어댑터 활성)** 또는 Standby 어댑터로 작동 하는 NIC 팀에서 특정 네트워크 어댑터를 선택 합니다. 대기 어댑터로 NIC를 구성한 경우 다른 모든 선택 되지 않은 팀 멤버는 활성 및 네트워크 트래픽이 전송 되었거나 활성 NIC를 실패할 때까지 어댑터에서 처리 합니다. 활성 NIC를 실패 한 후에 대기 NIC 활성화 되 고 네트워크 트래픽 프로세스입니다. 모든 팀 멤버 가져오기 서비스를 복원할 때 대기 상태로 대기 팀 멤버를 반환 합니다.  

두 개의 NIC 팀이 하나의 NIC는 대기 어댑터로 구성 하려는 경우 두 개의 활성 Nic를 사용 하 여 존재 하는 집계 장점 대역폭 손실 있습니다.  내결함성; 달성 하기 위해 대기 어댑터를 지정할 필요가 없습니다. 내결함성 항상 때마다 생성 되는 NIC 팀에 두 개 이상의 네트워크 어댑터가 있습니다.
 
  
## <a name="primary-team-interface-property"></a>기본 팀 인터페이스 속성  
주 팀 인터페이스 대화 상자에 액세스 하려면 아래 그림에 강조 표시 되는 링크를 클릭 해야 합니다.  
  
![기본 팀 인터페이스 속성](../../media/Create-a-New-NIC-Team-on-a-Host-Computer-or-VM/nict_10_primaryteaminterface.jpg)  
  
다음 강조 표시 된 링크를 클릭 한 후 **새 팀 인터페이스** 대화 상자가 열립니다.  
  
![새 팀 인터페이스 대화 상자](../../media/Create-a-New-NIC-Team-on-a-Host-Computer-or-VM/nict_newteaminterface.jpg)  
  
Vlan을 사용 하는 경우 VLAN 번호를 지정 하려면이 대화 상자를 사용할 수 있습니다.  
  
Vlan을 사용 하는 여부, NIC 팀에 tNIC 이름을 지정할 수 있습니다.  
  


---