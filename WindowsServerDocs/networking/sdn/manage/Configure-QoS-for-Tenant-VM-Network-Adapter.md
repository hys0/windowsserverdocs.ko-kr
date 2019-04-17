---
title: 테 VM 네트워크 어댑터에 대 한 서비스의 품질을 구성 합니다.
description: 이 항목은 관리 테 작업 및 Windows Server 2016에 가상 네트워크 방법에 대해 소프트웨어 네트워킹 정의 가이드 일부입니다.
manager: brianlic
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
ms.openlocfilehash: cde4e21beaec58a98a5d5fbe5c4631e2f113dbf7
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-quality-of-service-qos-for-a-tenant-vm-network-adapter"></a>테 VM 네트워크 어댑터에 대 한 서비스의 품질을 구성 합니다.

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

데이터 센터 브리지 중에서 선택 있는 QoS 테 VM 네트워크 어댑터에 대 한를 구성 \ (DCB\) 또는 소프트웨어 네트워킹 정의 \(SDN\) QoS 합니다.

1.  **DCB**합니다. Windows PowerShell NetQoS cmdlet 사용 하 여 DCB 구성할 수 있습니다. 예를 들어 항목에 "데이터 센터 브리지 사용" 섹션을 참조 [원격 직접 메모리 Access (RDMA) 및 스위치 Embedded 팀 (설정)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)합니다.

2.  **SDN QoS**합니다. SDN QoS 대역폭 높은 교통 VM 다른 사용자를 차단 하지 못하도록 가상 인터페이스를 제한 하도록 설정할 수 있는 네트워크 컨트롤러를 사용 하 여 사용할 수 있습니다.  또한 특정 VM 네트워크 교통 기간 액세스할 수 있는지 확인 하려면 vm 대역폭 기간을 예약 하도록 SDN QoS 구성할 수 있습니다.  

다음 표에서에 따라 네트워크 인터페이스 속성 포트 설정을 통해 모든 SDN Qos 설정이 적용 됩니다.

|요소 이름|설명|
|------------|-----------| 
|macSpoofing|Vm에서 보내는 패킷 소스 미디어 액세스 제어 \(MAC\) 주소 VM에 할당 되지 않은 MAC 주소를 변경할 수 있는지 여부를 지정 합니다. 값은 "설정" 허용 \ (VM 다른 MAC address\ 사용을 허용) "사용할 수 없습니다"와 \ (VM만 it\에 할당 MAC 주소를 사용 하도록 허용).|
|arpGuard|ARP 가드를 사용할 수 있는지 여부를 지정 합니다.  ARP 보호 ArpFilter 포트를 통해 전달 하기 위해에 지정 된 주소만 수 있게 합니다.  허용 되는 "활성화" 또는 "사용 안 함".
|dhcpGuard|DHCP를 것인지 VM에서 DHCP 메시지 핀을 지정 합니다. 허용 되는 "를 사용 하도록 설정" 가상화 DHCP 서버 것으로 간주 됩니다 신뢰할 수 없는 또는 "사용 안 함"를 메시지를 신뢰할 수 있는 것으로 간주는 가상화 DHCP 서버 하기 때문에 받으려면 수 있는 이므로 DHCP 메시지를 삭제 하는 합니다.
|stormLimit|VM 지정 된 가상 네트워크 어댑터를 통해 보낼 수 있는 초당 브로드캐스트 멀티 캐스트 및 알 수 없는 유니캐스트 패킷 지정 합니다. 이 한 두 번째 기간 동안 제한 초과 브로드캐스트 멀티 캐스트 및 알 수 없는 유니캐스트 패킷이 삭제 됩니다. 0 \(0\) 값 제한이 의미 합니다.
|portFlowLimit|포트 실행 될 수 있는 흐름 최대 수를 지정 합니다.  빈 또는 0 \(0\) 제한이 의미 합니다.
|vmqWeight|가상 네트워크 어댑터에서 가상 컴퓨터 대기열 (VMQ)를 사용할 수 있는지 여부를 지정 합니다. 상대적 두께 VMQ 사용 하 여 가상 네트워크 어댑터의 선호도 설명 합니다. 값 영역은 0-100 됩니다. 가상 네트워크 어댑터에 VMQ 하지 않으려면 0을 지정 합니다.
|iovWeight|인지를 지정 단일 루트 I/O virtualization \(SR-IOV\)가 가상 네트워크 어댑터에서 사용할 수 있습니다. 가상 네트워크 어댑터의 선호도 s R IOV 가상 할당 된 기능을 설정 하는 상대적 두께 합니다. 값 영역은 0-100 됩니다. S R IOV 가상 네트워크 어댑터에서 사용 하지 않도록 하려면 0을 지정 합니다. 
|iovInterruptModeration|가상 네트워크 어댑터에 할당 단일 루트 I/O virtualization \(SR-IOV\) 가상 함수 인터럽트 중재 값을 지정 합니다. 허용 "기본", "자동", "끄기", "부족", "보통" 및 "고급" 됩니다.   기본 채택 되 면 값 실제 네트워크 어댑터 공급 업체의 설정에 따라 결정 됩니다.  적응 채택 되 면 인터럽트 조정 속도가 런타임 교통 패턴을 기반으로 합니다. 
|iovQueuePairsRequested|하드웨어 큐 쌍 s R IOV 가상 기능에 할당 될 수를 지정 합니다. 수신 측면 크기 조정 \(RSS\) 필요 하 고 가상 스위치를 연결 하는 실제 네트워크 어댑터 RSS 가상 s R IOV에 있으면 다음 개 이상의 하나의 큐 페어링 기능을가 필요 합니다. 1 값 범위 4294967295부터 사용할 수 있습니다. 
|QosSettings|모든 데이터 옵션은 다음과 같은 Qos 설정을 구성할 수 있습니다.  <br/><br />**outboundReservedValue:**<br/>"절대"으로 간주 outboundReservedMode 값 대역폭 전송 (송신)에 대 한 가상 포트 보장 m b p s 나타냅니다. OutboundReservedMode "무게"는 값 보장 대역폭의가 중된 일부를 나타냅니다. <br/><br />**outboundMaximumMbps:**  <br/>허용 되는 최대 보내기 측 대역폭 m b p s에서 가상 포트 (송신)에 대 한 나타냅니다. <br/><br/>**InboundMaximumMbps:**  <br/>최대 m b p s에서 가상 포트 (수신)에 대 한 받을 측 대역폭 사용할 수 없음을 나타냅니다. |