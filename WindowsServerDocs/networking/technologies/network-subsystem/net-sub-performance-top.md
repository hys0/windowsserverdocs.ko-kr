---
title: 네트워크 하위 시스템 성능 튜닝
description: 이 항목은 Windows Server 2016에 대 한 네트워크 하위 시스템 성능 튜닝 지침의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 45217fce-bfb9-47e8-9814-88ffdb3c7b7d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c0706c6ddbb678eacd3e609cfad3ccdda943fbd3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857414"
---
# <a name="network-subsystem-performance-tuning"></a>네트워크 하위 시스템 성능 튜닝

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 네트워크 하위 시스템에 대 한 개요 및이 가이드의 다른 항목에 대 한 링크에 사용할 수 있습니다.

>[!NOTE]
>이 항목 외에이 가이드의 다음 섹션에는 네트워크 장치에 대 한 성능 튜닝 권장 사항 및 네트워크 스택을 제공합니다.
> - [네트워크 어댑터를 선택합니다.](net-sub-choose-nic.md)
> - [네트워크 인터페이스의 순서를 구성 합니다.](net-sub-interface-metric.md)
> - [네트워크 어댑터 성능 조정](net-sub-performance-tuning-nics.md)
> - [네트워크 관련 성능 카운터](net-sub-performance-counters.md)
> - [네트워크 워크 로드 용 성능 도구](net-sub-performance-tools.md)

성능 튜닝 네트워크 집약적인 워크 로드에 대 한 특히 네트워크 하위 시스템, 네트워크 스택 라고도 하는 네트워크 아키텍처의 레이어마다가 될 수 있습니다. 이러한 계층은 다음 섹션에서는 광범위 하 게 나뉩니다.

1. **네트워크 인터페이스**합니다. 이 네트워크 스택의 가장 낮은 계층을 네트워크 어댑터와 직접 통신 하는 네트워크 드라이버를 포함 합니다.

2. **네트워크 드라이버 인터페이스 사양 (NDIS)** 합니다. NDIS 아래 드라이버와 같은 프로토콜 스택 위의 계층에 대 한 인터페이스를 노출합니다.
  
3. **프로토콜 스택**합니다. 프로토콜 스택을 TCP/IP 및 UDP/IP와 같은 프로토콜을 구현합니다. 이러한 계층 상위 계층에 대 한 전송 계층 인터페이스를 노출 합니다.
  
4. **시스템 드라이버**합니다. 이들은 일반적으로 사용자 모드 응용 프로그램에 대 한 인터페이스를 공개 하는 전송 데이터 확장 프로그램 (TDX) 또는 WSK (Winsock Kernel) 인터페이스를 사용 하는 클라이언트입니다. WSK 인터페이스는 Windows Server 2008 및 Windows에 도입 된&reg; Vista 하며 AFD.sys에 의해 노출 됩니다. 인터페이스에는 사용자 모드와 커널 모드 간에 전환이 제거 하 여 성능을 향상 시킵니다.
  
5. **사용자 모드 응용 프로그램**합니다. 이들은 일반적으로 Microsoft 솔루션 또는 사용자 지정 응용 프로그램입니다.

다음 표에서 각 계층에서 실행 되는 항목의 예제를 비롯 한 네트워크 스택의 계층을 세로 보여 줍니다.  

![네트워크 스택 레이어](../../media/Network-Subsystem/network-layers.jpg)

