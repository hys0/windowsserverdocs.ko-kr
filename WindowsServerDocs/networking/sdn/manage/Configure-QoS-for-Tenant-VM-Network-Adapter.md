---
title: 테 넌 트 VM 네트워크 어댑터에 대 한 QoS (서비스 품질) 구성
description: 테 넌 트 VM 네트워크 어댑터에 대 한 QoS를 구성 하는 경우 데이터 센터 \(브리징 DCB\)또는 소프트웨어 정의 네트워킹 \(SDN\) qos 중에서 선택할 수 있습니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6d783ff6-7dd5-496c-9ed9-5c36612c6859
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 1074525abe375e78ab0d2065ce8e98f894f50c61
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355849"
---
# <a name="configure-quality-of-service-qos-for-a-tenant-vm-network-adapter"></a>테 넌 트 VM 네트워크 어댑터에 대 한 QoS (서비스 품질) 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

테 넌 트 VM 네트워크 어댑터에 대 한 QoS를 구성 하는 경우 데이터 센터 \(브리징 DCB\)또는 소프트웨어 정의 네트워킹 \(SDN\) qos 중에서 선택할 수 있습니다.

1.  **DCB**. Windows PowerShell NetQoS cmdlet을 사용 하 여 DCB를 구성할 수 있습니다. 예제는 [RDMA (원격 직접 메모리 액세스) 및 스위치 포함 된 팀 (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)항목의 "데이터 센터 브리징 사용" 섹션을 참조 하세요.

2.  **SDN QoS**. 네트워크 컨트롤러를 사용 하 여 SDN QoS를 사용 하도록 설정할 수 있습니다 .이는 트래픽이 많은 VM이 다른 사용자를 차단 하지 않도록 하기 위해 가상 인터페이스의 대역폭을 제한 하도록 설정할 수 있습니다.  네트워크 트래픽 양에 관계 없이 VM에 액세스할 수 있도록 VM에 대 한 특정 대역폭을 예약 하도록 SDN QoS를 구성할 수도 있습니다.  

네트워크 인터페이스 속성의 포트 설정을 통해 모든 SDN QoS 설정을 적용 합니다. 자세한 내용은 아래 표를 참조 하세요.

|요소 이름|설명|
|------------|-----------| 
|macSpoofing| Vm이 송신 패킷에서 원본 미디어 액세스 제어 \(mac\) 주소를 vm에 할당 되지 않은 mac 주소로 변경 하도록 허용 합니다.<p>허용되는 값은 다음과 같습니다.<ul><li>사용 – 다른 MAC 주소를 사용 합니다.</li><li>사용 안 함 – 할당 된 MAC 주소만 사용 합니다.</li></ul>|
|arpGuard| ArpFilter에 지정 된 ARP 가드 주소만 포트를 통과 하도록 허용 합니다.<p>허용되는 값은 다음과 같습니다.<ul><li>사용-허용 됨</li><li>Disabled – 사용할 수 없음</li></ul>|
|dhcpGuard| DHCP 서버로 클레임 되는 VM에서 DHCP 메시지를 허용 하거나 삭제 합니다. <p>허용되는 값은 다음과 같습니다.<ul><li>사용 – 가상화 된 DHCP 서버를 신뢰할 수 없는 것으로 간주 하므로 DHCP 메시지를 삭제 합니다.</li><li>사용 안 함 – 가상화 된 DHCP 서버를 신뢰할 수 있는 것으로 간주 하므로 메시지를 수신할 수 있습니다.</li></ul>|
|stormLimit| VM이 가상 네트워크 어댑터를 통해 보낼 수 있는 초당 패킷 수 (브로드캐스트, 멀티 캐스트 및 알 수 없는 유니캐스트)입니다. 이 간격을 초과 하는 패킷은 1 초 간격으로 삭제 됩니다. 0 값 \(\) 은 제한이 없음을 의미 합니다.|
|portFlowLimit| 포트에 대해 실행할 수 있는 최대 흐름 수입니다. 값이 비어 있거나 \(0\) 이면 제한이 없음을 의미 합니다. |
|vmqWeight| 상대 가중치는 VMQ (가상 머신 큐)를 사용 하는 가상 네트워크 어댑터의 선호도를 설명 합니다. 값의 범위는 0에서 100 까지입니다.<p>허용되는 값은 다음과 같습니다.<ul><li>0 – 가상 네트워크 어댑터에서 VMQ를 사용 하지 않도록 설정 합니다.</li><li>1-100 – 가상 네트워크 어댑터에서 VMQ를 사용 하도록 설정 합니다.</li></ul>|
|iovWeight| 상대 가중치는 가상 네트워크 어댑터의 선호도를 할당 된 단일 루트 i/o 가상화 \(sr-iov\) 가상 함수로 설정 합니다. <p>허용되는 값은 다음과 같습니다.<ul><li>0 – 가상 네트워크 어댑터에서 SR-IOV를 사용 하지 않도록 설정 합니다.</li><li>1-100 – 가상 네트워크 어댑터에서 SR-IOV를 사용 하도록 설정 합니다.</li></ul>|
|iovInterruptModeration|<p>허용되는 값은 다음과 같습니다.<ul><li>기본값-실제 네트워크 어댑터 공급 업체의 설정에 따라 값이 결정 됩니다.</li><li>팔레트 </li><li>끕니다 </li><li>거의</li><li>보통</li><li>최고</li></ul><p>**기본값**을 선택 하는 경우 실제 네트워크 어댑터 공급 업체의 설정에 따라 값이 결정 됩니다.  **적응**을 선택 하는 경우 런타임 트래픽 패턴은 인터럽트 조정 률을 determins 합니다.|
|iovQueuePairsRequested| SR-IOV 가상 함수에 할당 된 하드웨어 큐 쌍의 수입니다. 수신측 배율 \(rss\) 가 필요 하 고 가상 스위치에 바인딩된 실제 네트워크 어댑터가 sr-iov 가상 함수에서 rss를 지 원하는 경우에는 둘 이상의 큐 쌍이 필요 합니다. <p>허용되는 값은 다음과 같습니다. 1 ~ 4294967295입니다.|
|QosSettings| 다음 Qos 설정을 구성 합니다. 모두 선택 사항입니다. <ul><li>**outboundReservedValue** -outboundReservedMode가 "absolute" 인 경우 값은 전송 (송신)에 대해 보장 되는 대역폭 (Mbps)을 나타냅니다. OutboundReservedMode가 "weight" 이면 값은 보장 된 대역폭의 가중치가 적용 된 부분을 나타냅니다.</li><li>**outboundMaximumMbps** -가상 포트 (송신)에 허용 되는 최대 송신 측 대역폭 (Mbps)을 나타냅니다.</li><li>**InboundMaximumMbps** -가상 포트 (수신)에 대해 허용 되는 최대 수신 측 대역폭 (Mbps)을 나타냅니다.</li></ul> |

---