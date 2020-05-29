---
title: DHCP (동적 호스트 구성 프로토콜) 기본 사항
description: ''
ms.date: 5/26/2020
ms.prod: windows-server
ms.service: na
manager: dcscontentpm
ms.technology: server-general
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.reviewer: ''
ms.openlocfilehash: c7e4f385472c9078c49fcfd7aeab28b1b70c5a13
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150211"
---
# <a name="dhcp-dynamic-host-configuration-protocol-basics"></a>DHCP (동적 호스트 구성 프로토콜) 기본 사항

DHCP (Dynamic Host Configuration Protocol)는 서버에서 IP 주소 지정 및 구성 정보를 클라이언트에 동적으로 배포할 수 있도록 하는 RFC 1541 (RFC 2131로 교체 됨)에서 정의 되는 표준 프로토콜입니다. 일반적으로 DHCP 서버는 다음과 같은 기본 정보를 클라이언트에 제공 합니다.

- IP 주소

- 서브넷 마스크

- DNS (Domain Name Service) 서버 주소 및 WINS (Windows Internet Name Service) 서버 주소와 같은 기본 게이트웨이 기타 정보도 제공할 수 있습니다. 시스템 관리자는 클라이언트에 구문 분석 되는 옵션을 사용 하 여 DHCP 서버를 구성 합니다.

## <a name="more-information"></a>추가 정보

다음 Microsoft 제품은 DHCP 클라이언트 기능을 제공 합니다.

- Windows NT Server 버전 3.5, 3.51 및 4.0

- Windows NT 워크스테이션 버전 3.5, 3.51 및 4.0

- Windows 95

- MS-DOS 용 Microsoft 네트워크 클라이언트 버전 3.0

- MS-DOS 용 Microsoft LAN Manager 클라이언트 버전 2.2 c

- 작업 그룹 버전 3.11, 3.11 a 및 3.11 b의 Windows 용 Microsoft TCP/IP-32

Dhcp 클라이언트는 DHCP 서버에서 받을 수 있는 다양 한 옵션을 지원 합니다. 

다음 Microsoft 서버 운영 체제는 DHCP 서버 기능을 제공 합니다.

- Windows NT Server 버전 3.5

- Windows NT Server 버전 3.51

- Windows NT Server 버전 4.0

클라이언트가 DHCP 정보를 수신 하도록 구성 된 후 처음으로 초기화 되 면 서버와의 대화를 시작 합니다.

다음은 클라이언트와 서버 간의 대화에 대 한 요약 테이블 이며 그 다음에는 프로세스에 대 한 패킷 수준 설명이 나옵니다.

```
Source Dest Source Dest Packet
 MAC addr MAC addr IP addr IP addr Description
 -----------------------------------------------------------------
 Client Broadcast 0.0.0.0 255.255.255.255 DHCP Discover
 DHCPsrvr Broadcast DHCPsrvr 255.255.255.255 DHCP Offer
 Client Broadcast 0.0.0.0 255.255.255.255 DHCP Request
 DHCPsrvr Broadcast DHCPsrvr 255.255.255.255 DHCP ACK
```

DHCP 클라이언트와 DHCP 서버 간의 자세한 대화는 다음과 같습니다.

### <a name="dhcpdiscover"></a>DHCPDISCOVER

클라이언트에서 DHCPDISCOVER 패킷을 보냅니다. 다음은 DHCPDISCOVER 패킷의 IP 및 DHCP 부분을 보여 주는 네트워크 모니터 캡처에서 발췌 한 것입니다. IP 섹션에서 대상 주소가 255.255.255.255이 고 원본 주소가 0.0.0.0 인 것을 볼 수 있습니다. DHCP 섹션에서는 패킷을 검색 패킷으로 식별 하 고 네트워크 카드의 실제 주소를 사용 하 여 두 위치에서 클라이언트를 식별 합니다. CHADDR 필드와 DHCP: 클라이언트 식별자 필드의 값은 동일 합니다.

```

IP: ID = 0x0; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 0 (0x0)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x39A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Discover (xid=21274A1D)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Discover
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

### <a name="dhcpoffer"></a>DHCPOFFER

DHCP 서버는 DHCPOFFER 패킷을 전송 하 여 응답 합니다. 아래 발췌 한 캡처의 IP 섹션에서 원본 주소는 이제 DHCP 서버 IP 주소이 고, 대상 주소는 브로드캐스트 주소 255.255.255.255입니다. DHCP 섹션에서는 패킷을 제안으로 식별 합니다. YIADDR 필드는 서버가 클라이언트를 제공 하는 IP 주소로 채워집니다. CHADDR 필드는 여전히 요청 하는 클라이언트의 실제 주소를 포함 합니다. 또한 DHCP 옵션 필드 섹션에는 서버에서 IP 주소와 함께 전송 되는 다양 한 옵션이 표시 됩니다. 이 경우 서버는 서브넷 마스크, 기본 게이트웨이 (라우터), 임대 시간, WINS 서버 주소 (NetBIOS 이름 서비스) 및 NetBIOS 노드 유형을 전송 합니다.

```

IP: ID = 0x3C30; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 15408 (0x3C30)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x2FA8
 IP: Source Address = 157.54.48.151
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Offer (xid=21274A1D)
 DHCP: Op Code (op) = 2 (0x2)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 157.54.50.5
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Offer
 DHCP: Subnet Mask = 255.255.240.0
 DHCP: Renewal Time Value (T1) = 8 Days, 0:00:00
 DHCP: Rebinding Time Value (T2) = 14 Days, 0:00:00
 DHCP: IP Address Lease Time = 16 Days, 0:00:00
 DHCP: Server Identifier = 157.54.48.151
 DHCP: Router = 157.54.48.1
 DHCP: NetBIOS Name Service = 157.54.16.154
 DHCP: NetBIOS Node Type = (Length: 1) 04
 DHCP: End of this option field

```

### <a name="dhcprequest"></a>DHCPREQUEST

클라이언트는 DHCPREQUEST를 전송 하 여 DHCPOFFER에 응답 합니다. 아래 캡처의 IP 섹션에서 클라이언트의 원본 주소는 여전히 0.0.0.0 이며 패킷의 대상은 여전히 255.255.255.255입니다. 클라이언트는 제공 된 주소를 사용 하 여 시작 해도 괜찮습니다. 서버에서 확인을 받지 못해 0.0.0.0을 유지 합니다. 하나 이상의 DHCP 서버가 응답 했 고 클라이언트에 대 한 예약을 보유 하 고 있을 수 있으므로 대상은 여전히 브로드캐스트 됩니다. 이렇게 하면 다른 DHCP 서버에서 제공 된 주소를 해제 하 고 해당 주소를 사용 가능한 풀로 되돌릴 수 있습니다. DHCP 섹션에서는 패킷을 요청으로 식별 하 고 DHCP: 요청 된 주소 필드를 사용 하 여 제공 된 주소를 확인 합니다. DHCP: 서버 식별자 필드는 임대를 제공 하는 DHCP 서버의 IP 주소를 표시 합니다.

```

IP: ID = 0x100; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 256 (0x100)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x38A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Request (xid=21274A1D)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Request
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Requested Address = 157.54.50.5
 DHCP: Server Identifier = 157.54.48.151
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

### <a name="dhcpack"></a>DHCPACK

DHCP 서버는 DHCPACK를 사용 하 여 DHCPREQUEST에 응답 하므로 초기화 주기를 완료 합니다. 원본 주소는 DHCP 서버 IP 주소이 고 대상 주소는 여전히 255.255.255.255입니다. YIADDR 필드는 클라이언트의 주소를 포함 하 고 CHADDR 및 DHCP: 클라이언트 식별자 필드는 요청 클라이언트에서 네트워크 카드의 실제 주소입니다. DHCP 옵션 섹션에서는 패킷을 ACK로 식별 합니다.

```

IP: ID = 0x3D30; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 15664 (0x3D30)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x2EA8
 IP: Source Address = 157.54.48.151
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: ACK (xid=21274A1D)
 DHCP: Op Code (op) = 2 (0x2)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 157.54.50.5
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP ACK
 DHCP: Renewal Time Value (T1) = 8 Days, 0:00:00
 DHCP: Rebinding Time Value (T2) = 14 Days, 0:00:00
 DHCP: IP Address Lease Time = 16 Days, 0:00:00
 DHCP: Server Identifier = 157.54.48.151
 DHCP: Subnet Mask = 255.255.240.0
 DHCP: Router = 157.54.48.1
 DHCP: NetBIOS Name Service = 157.54.16.154
 DHCP: NetBIOS Node Type = (Length: 1) 04
 DHCP: End of this option field

```

클라이언트에 이전에 DHCP 할당 된 IP 주소가 있고 다시 시작 되 면 클라이언트는 특수 한 DHCPREQUEST 패킷에서 이전에 임대 된 IP 주소를 특별히 요청 합니다. 원본 주소는 0.0.0.0 이며 대상은 브로드캐스트 주소 255.255.255.255입니다. Microsoft 클라이언트는 dhcp 옵션 필드인 DHCP: 요청 된 주소를 이전에 할당 된 주소로 채웁니다. 엄격한 RFC 규격 클라이언트는 요청 된 주소를 사용 하 여 CIADDR 필드를 채웁니다. Microsoft DHCP 서버는를 허용 합니다.

```

IP: ID = 0x0; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 0 (0x0)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x39A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Request (xid=2757554E)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 660034894 (0x2757554E)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Request
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Requested Address = 157.54.50.5
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

이 시점에서 서버는 응답 하지 않을 수도 있습니다. Windows NT DHCP 서버의 동작은 사용 중인 운영 체제의 버전 및 superscoping와 같은 기타 요소에 따라 달라 집니다. 서버에서 클라이언트가 주소를 계속 사용할 수 있는 것으로 확인 되 면 자동으로 유지 되거나 DHCPREQUEST를 승인 합니다. 서버에서 클라이언트가 주소를 가질 수 없는 것으로 확인 되 면 NACK를 보냅니다.

```

IP: ID = 0x3F1A; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 16154 (0x3F1A)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x2CBE
 IP: Source Address = 157.54.48.151
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: NACK (xid=74A005CE)
 DHCP: Op Code (op) = 2 (0x2)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 1956644302 (0x74A005CE)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP NACK
 DHCP: Server Identifier = 157.54.48.151
 DHCP: End of this option field

```

그러면 클라이언트는 검색 프로세스를 시작 하지만 DHCPDISCOVER 패킷은 여전히 동일한 주소를 임대 하려고 시도 합니다. 대부분의 경우 tth 클라이언트는 동일한 주소를 가져오지만 그렇지 않을 수도 있습니다.

```

IP: ID = 0x100; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 256 (0x100)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x38A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Discover (xid=3ED14752)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 1053902674 (0x3ED14752)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Discover
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Requested Address = 157.54.51.5
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

DHCP 서버의 클라이언트에서 가져온 DHCP 정보는 임대 시간을 연결 합니다. 임대 시간은 클라이언트에서 DHCP 할당 정보를 사용할 수 있는 기간을 정의 합니다. 임대가 특정 마일스 톤에 도달 하면 클라이언트는 DHCP 정보를 갱신 하려고 시도 합니다.

Windows 또는 작업 그룹 클라이언트용 Windows에서 IP 정보를 보려면 IPCONFIG 유틸리티를 사용 합니다. 클라이언트가 Windows 95 인 경우 WINIPCFG를 사용 합니다.

## <a name="references"></a>참조

DHCP에 대 한 자세한 내용은 RFC1541 및 RFC2131를 참조 하세요. Rfc는 다음과 같은 다양 한 사이트에서 인터넷을 통해 가져올 수 있습니다. [http://www.rfc-editor.org/](http://www.rfc-editor.org/)[http://www.tech-nic.qc.ca/](http://www.tech-nic.qc.ca/)
