---
title: 고성능 네트워킹
description: 이 항목에서는 Windows Server 2016의 오프 로드 및 최적화 기술에 대 한 개요를 제공 하며, 이러한 기술에 대 한 추가 지침에 대 한 링크를 제공 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/12/2018
ms.openlocfilehash: d5a4d5f06cd433fa92c617a3cb36e95d09be3b27
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950456"
---
# <a name="hardware-only-ho-features-and-technologies"></a>HO(하드웨어 전용) 기능 및 기술

이러한 하드웨어 가속은 소프트웨어와 함께 네트워킹 성능을 향상 시키지만 소프트웨어 기능의 깊이은 아닙니다. 이러한 예로는 인터럽트 중재, 흐름 제어 및 수신 측 IPv4 체크섬 오프 로드 등이 있습니다.

>[!TIP]
>설치 된 NIC에서 지원 되는 경우 SH 및 호 기능을 사용할 수 있습니다. 아래 기능 설명은 NIC가 기능을 지원 하는지 여부를 확인 하는 방법을 다룹니다.

## <a name="address-checksum-offload"></a>주소 체크섬 오프 로드

주소 체크섬 오프 로드는 송신 및 수신에 대해 주소 체크섬 (IP, TCP, UDP)의 계산을 NIC 하드웨어로 오프 로드 하는 NIC 기능입니다.

수신 경로에서 체크섬 오프 로드는 IP, TCP 및 UDP 헤더의 체크섬 (해당 하는 경우)을 계산 하 고 체크섬이 통과, 실패 또는 확인 되지 않는지를 OS에 나타냅니다. NIC에서 체크섬이 유효한 것으로 어설션하는 경우 OS는 패킷 unchallenged을 허용 합니다. NIC가 잘못 된 체크섬을 어설션 하거나 확인 하지 않은 경우 IP/TCP/UDP 스택은 내부적으로 체크섬을 다시 계산 합니다. 계산 된 체크섬이 실패 하면 패킷이 삭제 됩니다.

송신 경로에서 체크섬 오프 로드는 체크섬을 계산 하 고 적절 하 게 IP, TCP 또는 UDP 헤더에 삽입 합니다.

송신 경로에서 체크섬 오프 로드를 사용 하지 않도록 설정 해도 LSO (Large Send Offload) 기능을 사용 하 여 미니 포트 드라이버로 보낸 패킷에 대해서는 체크섬 계산 및 삽입이 사용 되지 않습니다.  모든 체크섬 오프 로드 계산을 사용 하지 않도록 설정 하려면 사용자가 LSO도 사용 하지 않도록 설정 해야 합니다.

_**주소 체크섬 오프 로드 관리**_

고급 속성에는 다음과 같은 여러 가지 고유한 속성이 있습니다.

-   IPv4 체크섬 오프 로드

-   TCP 체크섬 오프 로드 (IPv4)

-   TCP 체크섬 오프 로드 (IPv6)

-   UDP 체크섬 오프 로드 (IPv4)

-   UDP 체크섬 오프 로드 (IPv6)

기본적으로 항상 사용 하도록 설정 되어 있습니다. 항상 이러한 오프 로드를 모두 사용 하도록 설정 하는 것이 좋습니다.

NetAdapterChecksumOffload 및 NetAdapterChecksumOffload cmdlet을 사용 하 여 체크섬 오프 로드를 관리할 수 있습니다. 예를 들어 다음 cmdlet은 TCP (IPv4) 및 UDP (IPv4) 체크섬 계산을 사용 하도록 설정 합니다.

```PowerShell
Enable-NetAdapterChecksumOffload –Name * -TcpIPv4 -UdpIPv4
```

_**주소 체크섬 오프 로드 사용에 대 한 팁**_

주소 체크섬 오프 로드는 작업 또는 환경에 관계 없이 항상 사용 하도록 설정 해야 합니다. 모든 오프 로드 기술에 대 한 대부분의 기본은 항상 네트워크 성능을 향상 시킵니다. 또한, RSS (수신측 배율), RSC (수신 세그먼트 통합) 및 LSO (large send offload)를 비롯 한 다른 상태 비저장 오프 로드를 사용 하려면 체크섬 오프 로드가 필요 합니다.

## <a name="interrupt-moderation-im"></a>인터럽트 중재 (IM)

IM은 운영 체제를 중단 하기 전에 여러 개의 수신 된 패킷을 버퍼링 합니다. NIC는 패킷을 받으면 타이머를 시작 합니다. 버퍼가 가득 찼거나 타이머가 만료 되는 경우에는 NIC가 운영 체제를 중단 합니다. 

대부분의 Nic는 인터럽트 조정을 위해 설정/해제 이상의 기능을 지원 합니다. 대부분의 Nic는 IM에 대해 낮음, 중간 및 높음의 개념을 지원 합니다. 다른 속도는 대기 시간 (낮은 인터럽트 조정)을 줄이거나 인터럽트 (높은 인터럽트 조정)를 줄이기 위해 더 짧거나 긴 타이머와 적절 한 버퍼 크기 조정을 나타냅니다.

인터럽트 감소와 과도 지연 패킷 배달 사이에는 잔액이 있습니다. 일반적으로 패킷 처리는 인터럽트 중재를 사용 하는 경우 보다 효율적입니다. 고성능 또는 대기 시간이 짧은 응용 프로그램은 인터럽트 중재를 사용 하지 않거나 줄이는 영향을 평가 해야 할 수 있습니다.

## <a name="jumbo-frames"></a>Jumbo 프레임

점보 프레임은 응용 프로그램에서 기본 1500 바이트 보다 훨씬 큰 프레임을 보낼 수 있도록 하는 NIC 및 네트워크 기능입니다. 일반적으로 점보 프레임에 대 한 제한은 약 9000 바이트 이지만 작을 수 있습니다.

Windows Server 2012 r 2에서 점보 프레임 지원에 대 한 변경 내용이 없습니다.

Windows Server 2016에는 MTU_for_HNV 새 오프 로드가 있습니다. 이 새로운 오프 로드는 점보 프레임 설정에서 작동 하 여 캡슐화 된 트래픽이 호스트와 인접 스위치 사이에서 조각화가 필요 하지 않도록 합니다. SDN 스택의이 새로운 기능을 사용 하는 경우 NIC는 알릴 MTU와 네트워크에서 사용할 MTU를 자동으로 계산 합니다. 이러한 MTU 값은 HNV 오프 로드를 사용 중인 경우에 다릅니다. 기능 호환성 테이블에서 테이블 1 MTU_for_HNV는 HNVv2 오프 로드와 직접 관련 되기 때문에 HNVv2 오프 로드와 동일한 상호 작용을 갖습니다.

## <a name="large-send-offload-lso"></a>LSO(Large Send Offload)

LSO를 사용 하면 응용 프로그램에서 많은 데이터 블록을 NIC에 전달할 수 있으며, NIC는 네트워크의 MTU (최대 전송 단위) 내에 적합 한 패킷으로 데이터를 나눕니다.

## <a name="receive-segment-coalescing-rsc"></a>RSC(수신 세그먼트 통합)

대량 수신 오프 로드 라고도 하는 수신 세그먼트 통합은 네트워크 인터럽트 사이에 도착 하는 동일한 스트림의 일부인 패킷을 사용 하 고이를 운영 체제에 전달 하기 전에 단일 패킷에 결합 하는 NIC 기능입니다. Hyper-v 가상 스위치에 바인딩된 Nic에서는 RSC를 사용할 수 없습니다. 자세한 내용은 [RSC (수신 세그먼트 통합)](https://docs.microsoft.com/windows-server/networking/technologies/hpn/rsc-in-the-vswitch)를 참조 하세요.