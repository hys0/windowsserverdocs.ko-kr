---
title: 네트워크 하위 시스템 성능 튜닝
description: 이 항목은 Windows Server 2016에 대 한 네트워크 하위 시스템 성능 조정 가이드의 일부입니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 45217fce-bfb9-47e8-9814-88ffdb3c7b7d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 02a1abc9de04926740309081397e0bd92fe74b88
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401885"
---
# <a name="network-subsystem-performance-tuning"></a>네트워크 하위 시스템 성능 튜닝

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 네트워크 하위 시스템에 대 한 개요와이 가이드의 다른 항목에 대 한 링크를 사용할 수 있습니다.

>[!NOTE]
>이 항목 외에도이 가이드의 다음 섹션에서는 네트워크 장치 및 네트워크 스택에 대 한 성능 튜닝 권장 사항을 제공 합니다.
> - [네트워크 어댑터 선택](net-sub-choose-nic.md)
> - [네트워크 인터페이스의 순서 구성](net-sub-interface-metric.md)
> - [성능 튜닝 네트워크 어댑터](net-sub-performance-tuning-nics.md)
> - [네트워크 관련 성능 카운터](net-sub-performance-counters.md)
> - [네트워크 워크로드용 성능 도구](net-sub-performance-tools.md)

네트워크 하위 시스템에 특히 네트워크를 많이 사용 하는 워크 로드에 대 한 성능 조정은 네트워크 stack이 라고도 하는 네트워크 아키텍처의 각 계층을 포함할 수 있습니다. 이러한 레이어는 다음과 같은 섹션으로 크게 구분 됩니다.

1. **네트워크 인터페이스**. 네트워크 스택에서 가장 작은 계층 이며 네트워크 어댑터와 직접 통신 하는 네트워크 드라이버를 포함 합니다.

2. **NDIS (Network Driver Interface Specification)** . NDIS는 그 아래에 있는 드라이버와 프로토콜 위에 있는 계층 (예: 프로토콜 스택)의 인터페이스를 노출 합니다.
  
3. **프로토콜 스택입니다**. 프로토콜 스택은 TCP/IP 및 UDP/IP와 같은 프로토콜을 구현 합니다. 이러한 레이어는 위의 레이어에 대 한 전송 계층 인터페이스를 노출 합니다.
  
4. **시스템 드라이버**. 일반적으로 사용자 모드 응용 프로그램에 인터페이스를 노출 하기 위해 TDX (전송 데이터 확장 프로그램) 또는 WSK (Winsock 커널) 인터페이스를 사용 하는 클라이언트입니다. WSK 인터페이스는 Windows Server 2008 및 Windows&reg; Vista에서 도입 되었으며, AFD.SYS에 의해 제공 됩니다. 인터페이스는 사용자 모드와 커널 모드 간의 전환을 제거 하 여 성능을 향상 시킵니다.
  
5. **사용자 모드 응용 프로그램**. 일반적으로 Microsoft 솔루션 또는 사용자 지정 응용 프로그램입니다.

아래 표에서는 각 계층에서 실행 되는 항목의 예제를 포함 하 여 네트워크 스택의 계층을 수직으로 보여 줍니다.  

![네트워크 스택 계층](../../media/Network-Subsystem/network-layers.jpg)

