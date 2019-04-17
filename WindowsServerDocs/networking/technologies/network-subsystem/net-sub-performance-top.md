---
title: 네트워크 하위 시스템 성능을 조정
description: 이 항목은 Windows Server 2016 용 네트워크 하위 시스템 성능 조정 가이드의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 45217fce-bfb9-47e8-9814-88ffdb3c7b7d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c7ef50335a6dcc7dc5187cc30ff1b2dc2c5cdfed
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="network-subsystem-performance-tuning"></a>네트워크 하위 시스템 성능을 조정

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 가이드의 기타 항목에 대 한 링크 및 네트워크 하위 시스템에 대 한 개요가이 항목을 사용할 수 있습니다.

>[!NOTE]
>이 항목 외에이 가이드는 다음 섹션 성능 조정 권장 네트워크 디바이스 및 네트워크 스택 제공합니다.
> - [네트워크 어댑터를 선택합니다.](net-sub-choose-nic.md)
> - [네트워크 인터페이스 순서를 구성](net-sub-interface-metric.md)
> - [성능 조정 네트워크 어댑터](net-sub-performance-tuning-nics.md)
> - [네트워크 관련 된 성능 카운터](net-sub-performance-counters.md)
> - [네트워크 작업에 대 한 성능 도구](net-sub-performance-tools.md)

성능 조정 네트워크 하위 네트워크 많이 작업에 대 한 특히 네트워크 스택 라고도 하는 네트워크 아키텍처 각 계층 포함 될 수 있습니다. 이러한 계층 다음 섹션으로 구분 광범위 하 게 됩니다.

1. **네트워크 인터페이스**합니다. 이 네트워크 스택의 낮은 계층을 직접 네트워크 어댑터와 통신 하는 네트워크 드라이버를 포함 합니다.

2. **네트워크 드라이버 인터페이스 사양 (NDIS)**합니다. NDIS 인터페이스 아래 드라이버에 대 한 및 프로토콜 스택에서 등을 위에 계층을 제공합니다.
  
3. **스택 프로토콜**합니다. 프로토콜 스택 TCP/IP UDP/IP 등 프로토콜을 구현 합니다. 이러한 계층 위에 계층 transport layer 인터페이스 노출 될 수 있습니다.
  
4. **시스템 드라이버**합니다. 일반적으로 전송 데이터 확장 (TDX) 또는 Winsock 커널 (WSK) 인터페이스 인터페이스 사용자 모드 응용 프로그램을 사용 하는 클라이언트입니다. Windows Server 2008 및 Windows WSK 인터페이스 도입 된&reg; Vista 및 것 AFD.sys에 표시 됩니다. 인터페이스는 사용자 모드 및 커널 모드 간에 전환 제거 하 여 성능을 개선 합니다.
  
5. **사용자 모드 응용 프로그램**합니다. 이 일반적으로 Microsoft 솔루션 또는 사용자 지정 응용 프로그램입니다.

아래 표에서 세로 그림 항목 각 계층을 실행 하는 몇 가지를 포함 하 여 네트워크 스택의 계층을 제공 합니다.  

![네트워크 스택 계층](../../media/Network-Subsystem/network-layers.jpg)

