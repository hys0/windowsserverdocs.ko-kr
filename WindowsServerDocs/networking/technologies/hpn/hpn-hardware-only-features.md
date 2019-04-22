---
title: 고속 네트워킹
description: 이 항목의 오프 로드 및 최적화 기술을 Windows Server 2016의 개요를 제공 하 고 이러한 기술에 대 한 추가 설명서 링크가 포함 되어 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/12/2018
ms.openlocfilehash: 09e18a41452baa0add8e055ceb22d2f5c2ad886e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815834"
---
## <a name="hardware-only-ho-features-and-technologies"></a>HO(하드웨어 전용) 기능 및 기술

이러한 하드웨어 가속 소프트웨어와 함께에서 네트워킹 성능을 향상 시킬 있지만 포함 되지 않은 깊숙히 소프트웨어 기능입니다. 이러한 예로 인터럽트 조절, 제어 흐름 및 수신 측 IPv4 체크섬 오프 로드를 들 수 있습니다.

>[!TIP]
>SH 및 호스트 기능은 설치 된 NIC에서 지 원하는 경우 사용할 수 있습니다. 아래 기능 설명에서는 NIC 기능을 지 원하는 경우를 구별 하는 방법을 설명 합니다.

### <a name="address-checksum-offload"></a>주소 체크섬 오프 로드

주소 체크섬 오프 로드는 보내기 및 받기 모두에 대 한 주소 체크섬 (IP, TCP, UDP) NIC 하드웨어에 대 한 계산을 오프 로드 하는 NIC 기능.

수신 경로에 체크섬 오프 로드를 사용 하 여 적절 하 게 IP, TCP 및 UDP 헤더에 체크섬을 계산 하 고 체크섬 성공, 실패 여부 확인 하지 OS를 나타냅니다. NIC 체크섬 올바른지 개 어설션, OS는 시도 하지 않습니다 패킷을 허용 합니다. NIC는 체크섬이 잘못 되었거나 확인 되지 않음 개 어설션, IP/TCP/UDP 스택 내부적으로 계산 체크섬 다시 합니다. 계산된 된 체크섬 오류가 발생 하면 패킷이 삭제 됩니다.

송신 경로에 체크섬 오프 로드를 사용 하 여 계산한 적절 하 게 IP, TCP 또는 UDP 헤더에 체크섬을 삽입 합니다.

체크섬 계산 및 대규모 전송 오프 로드 LSO () 기능을 사용 하는 미니 포트 드라이버에 전송 된 패킷은 대 한 삽입 전송 경로의 체크섬 오프 로드를 사용 하지 않도록 설정 해제 되지 않습니다.  모든 체크섬 오프 로드 계산을 사용 하지 않으려면 사용자도 하도록 하므로 LSO를 해제 해야 합니다.

_**주소 체크섬 오프 로드를 관리 합니다.**_

고급 속성에서 여러 가지 고유한 속성이 있습니다.

-   IPv4 체크섬 오프 로드

-   TCP 체크섬 오프 로드 (IPv4)

-   TCP 체크섬 오프 로드 (IPv6)

-   UDP 체크섬 오프 로드 (IPv4)

-   UDP 체크섬 오프 로드 (IPv6)

기본적으로 이러한 모든 항상 설정 됩니다. 항상 이러한 오프 로드를 모두 사용 하도록 하는 것이 좋습니다.

체크섬 오프 로드 사용 NetAdapterChecksumOffload 및 사용 안 함-NetAdapterChecksumOffload cmdlet을 사용 하 여 관리할 수 있습니다. 예를 들어, 다음 cmdlet (IPv4) TCP 및 UDP (IPv4) 체크섬 계산 활성화합니다.

```PowerShell
Enable-NetAdapterChecksumOffload –Name * -TcpIPv4 -UdpIPv4
```

_**주소 체크섬 오프 로드를 사용 하 여에 대 한 팁**_

어떤 워크 로드 또는 상황에 관계 없이 주소 체크섬 오프 로드 항상 사용 해야 합니다. 대부분의 basic 모두의 오프 로드 하는이 기술은 항상 네트워크 성능을 향상 시킵니다. 다른 상태 비저장 오프 로드를 포함 하 여 작업에 필요한 이기도 체크섬 오프 로드 수신측 배율 (RSS), (RSC) 수신 세그먼트 통합 및 large send offload (LSO).

### <a name="interrupt-moderation-im"></a>인터럽트 조절 (IM)

IM 운영 체제를 중단 하기 전에 여러 받은 패킷에 버퍼링 합니다. NIC는 패킷을 받으면 타이머를 시작 합니다. 버퍼가 꽉 또는 타이머가 만료 되 면 먼저 도달 하는 경우 NIC는 운영 체제를 중단 합니다. 

이상만 설정/해제 인터럽트 조절에 대 한 여러 Nic를 지원합니다. 대부분의 nic가 IM에 낮음, 보통 및 높은 비율의 개념을 지원 합니다. 다양 한 전환율 짧거나 긴 타이머 및 적절 한 버퍼 크기 조정 (낮은 인터럽트 조절을) 대기 시간을 줄이고 또는 인터럽트 (높은 인터럽트 조절을) 축소 시킬 나타냅니다.

인터럽트를 줄이고 과도 하 게 패킷 배달 지연 간에 취소선 수를 균형이 있습니다. 일반적으로 패킷 처리는 사용 하도록 설정 하는 인터럽트 조절을 사용 하 여 더 효율적입니다. 고성능 또는 대기 시간이 짧은 응용 프로그램 사용 안 함 또는 인터럽트 조절 감소의 영향을 평가 해야 합니다.

### <a name="jumbo-frames"></a>Jumbo 프레임

Jumbo 프레임에는 프레임을 기본값 보다 훨씬 더 큰 1500 바이트를 보내도록 응용 프로그램을 허용 하는 NIC 및 네트워크 기능입니다. 일반적으로 jumbo 프레임에 대 한 제한을 약 9000 바이트 이지만 더 작을 수도 있습니다.

Windows Server 2012 R2에서 jumbo 프레임이 지원 되지 않습니다 변경 내용이 있습니다.

새로운 Windows Server 2016의 오프 로드 합니다. MTU_for_HNV. 이 새 오프 로드는 캡슐화 된 트래픽이 호스트와 인접 스위치 간에 구분 하지 않아도 되도록 Jumbo 프레임 설정을 사용 하 여 작동 합니다. SDN 스택의이 새로운 기능에 NIC를 보급 하도록 어떤 MTU 및 통신 중에 사용 하는 MTU를 자동으로 계산 합니다. 모든 HNV 오프 로드 사용 중인 경우 이러한 값에 대 한 MTU 서로 다릅니다. (표 1에 기능 호환성 표의 MTU_for_HNV 것 같은 상호 작용 직접 관련이 HNVv2 오프 로드 했으므로 HNVv2 오프 로드 하는 대로입니다.)

### <a name="large-send-offload-lso"></a>LSO(Large Send Offload)

하도록 하므로 LSO 전달할 데이터의 큰 블록이 NIC 및 NIC 나누기 데이터 내의 최대 전송 단위 (MTU) 네트워크의에 맞는 패킷으로 응용 프로그램을 허용 합니다.

### <a name="receive-segment-coalescing-rsc"></a>Receive Segment Coalescing (RSC)

수신 세그먼트 통합, 라고도 큰 수신 오프 로드, 네트워크 인터럽트 간의 도착 하 고 운영 체제에 게 배달 하기 전에 단일 패킷을에 결합 하는 동일한 스트림의 일부인 패킷을 사용 하는 NIC 기능입니다. RSC를 Hyper-v 가상 스위치에 바인딩된 Nic에 제공 되지 않습니다. 자세한 내용은 [수신 세그먼트 병합 (RSC)](https://docs.microsoft.com/windows-server/networking/technologies/hpn/rsc-in-the-vswitch)합니다.