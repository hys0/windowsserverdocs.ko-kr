---
title: 테 넌 트 VM 네트워크 어댑터에 대 한 서비스 품질 (QoS) 구성
description: 데이터 센터 브리징 사이 선택할 수 있습니다 테 넌 트 VM 네트워크 어댑터에 대 한 QoS를 구성할 때 \(DCB\)또는 소프트웨어 정의 네트워킹 \(SDN\) QoS 합니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6d783ff6-7dd5-496c-9ed9-5c36612c6859
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 0b9ce318c3d249b23d7560e0b6bb90a83e60d64d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880604"
---
# <a name="configure-quality-of-service-qos-for-a-tenant-vm-network-adapter"></a>테 넌 트 VM 네트워크 어댑터에 대 한 서비스 품질 (QoS) 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

데이터 센터 브리징 사이 선택할 수 있습니다 테 넌 트 VM 네트워크 어댑터에 대 한 QoS를 구성할 때 \(DCB\)또는 소프트웨어 정의 네트워킹 \(SDN\) QoS 합니다.

1.  **DCB**. Windows PowerShell NetQoS cmdlet을 사용 하 여 DCB를 구성할 수 있습니다. 예를 들어 항목의 "데이터 센터 브리징 사용 하도록 설정" 섹션을 참조 하세요 [원격 직접 메모리 액세스 (RDMA) 및 스위치 포함 된 팀 (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)합니다.

2.  **SDN QoS**. 트래픽이 많은 VM을 다른 사용자를 차단 하지 않도록 하려면 가상 인터페이스에서 대역폭 제한으로 설정할 수 있는 네트워크 컨트롤러를 사용 하 여 SDN QoS를 사용할 수 있습니다.  또한 특정 크기의 VM 네트워크 트래픽 양에 관계 없이 액세스할 수 있는지 확인 하 여 VM의 대역폭 예약 SDN QoS를 구성할 수 있습니다.  

네트워크 인터페이스 속성의 포트 설정을 통해 모든 SDN QoS 설정을 적용 합니다. 자세한 내용은 아래 표를 참조 하세요.

|요소 이름|설명|
|------------|-----------| 
|macSpoofing| Vm의 원본 미디어 액세스 제어를 변경 하도록 허용 \(MAC\) VM에 할당 되지 않은 MAC 주소로 나가는 패킷의 주소입니다.<p>허용되는 값:<ul><li>사용 – 다른 MAC 주소를 사용 합니다.</li><li>사용 안 함-할당 된 MAC 주소만을 사용 합니다.</li></ul>|
|arpGuard| ARP guard 포트를 통해 전달할 ArpFilter에 지정 된 유일한 주소를 허용 합니다.<p>허용되는 값:<ul><li>사용 하도록 설정-허용</li><li>사용 안 함 – 허용 되지 않습니다</li></ul>|
|dhcpGuard| 허용 하거나 DHCP 서버를 VM에서 모든 DHCP 메시지를 삭제 합니다. <p>허용되는 값:<ul><li>사용 – 삭제 DHCP 메시지 되므로 가상화 된 DHCP 서버는 신뢰할 수 없는 것으로 간주 됩니다.</li><li>사용 안 함 – 가상화 된 DHCP 서버는 신뢰할 수 있는 것으로 간주 되므로 받을 메시지를 허용 합니다.</li></ul>|
|stormLimit| 가상 네트워크 어댑터를 통해 보낼 수 (브로드캐스트, 멀티 캐스트 및 알 수 없는 유니캐스트) vm의 초당 패킷 수입니다. 해당 1 초 간격 동안 제한 초과한 패킷은 삭제 합니다. 값이 0 \(0\) 제한이 있다는 것을 나타냅니다.|
|portFlowLimit| 포트에 대해 실행 하도록 허용 하는 흐름의 최대 수입니다. 0 또는 빈 값 \(0\) 제한이 없음을 의미 합니다. |
|vmqWeight| 상대적 가중치는 가상 머신 큐 (VMQ)를 사용 하도록 가상 네트워크 어댑터의 선호도 설명 합니다. 값의 범위는 0부터 100입니다.<p>허용되는 값:<ul><li>0 – 가상 네트워크 어댑터에서 VMQ를 사용 하지 않도록 설정 합니다.</li><li>1-100 – 가상 네트워크 어댑터에서 VMQ 사용 합니다.</li></ul>|
|iovWeight| 할당 된 단일 루트 I/O 가상화를 가상 네트워크 어댑터의 선호도 설정 하는 상대적 가중치 \(SR-IOV\) 가상 함수입니다. <p>허용되는 값:<ul><li>0-사용 하지 않도록 설정의 SR-IOV 가상 네트워크 어댑터입니다.</li><li>1-100 – 사용 하도록 설정의 SR-IOV 가상 네트워크 어댑터입니다.</li></ul>|
|iovInterruptModeration|<p>허용되는 값:<ul><li>기본 – 설정을 실제 네트워크 어댑터 공급 업체의 값을 결정합니다.</li><li>adaptive - </li><li>끕니다 </li><li>낮음</li><li>보통</li><li>고가용성</li></ul><p>선택 하면 **기본**, 실제 네트워크 어댑터 공급 업체의 설정 값을 결정 합니다.  원하는 경우 **적응**, 런타임 트래픽 패턴 였다면 인터럽트 조절 속도가 결정 합니다.|
|iovQueuePairsRequested| SR-IOV 가상 함수에 할당 된 하드웨어 큐 쌍의 수입니다. 경우 수신측 크기 조정을 \(RSS\) 필요 하 고 실제 네트워크 어댑터가 가상 스위치에 바인딩되는 경우 RSS를 지 원하는 SR-IOV 가상 함수를 둘 이상의 큐 쌍이 필요 합니다. <p>허용되는 값: 1에서 4294967295 합니다.|
|QosSettings| 다음 설정을 구성 합니다 Qos에는 모두 선택 사항: <ul><li>**outboundReservedValue** -outboundReservedMode가 "absolute" 값 (mbps)를 전송 (송신)에 대 한 가상 포트에 보장 된 대역폭을 나타냅니다. OutboundReservedMode "가중치" 이면 값은 보장 된 대역폭 중 가중치가 적용 된 일부를 나타냅니다.</li><li>**outboundMaximumMbps** -허용 되는 최대 송신 쪽 대역폭 (mbps)를 가상 포트 (송신)를 나타냅니다.</li><li>**InboundMaximumMbps** -수신측 대역폭 (mbps) 가상 포트 (수신)에 대해 허용 되는 최대값을 나타냅니다.</li></ul> |

---