---
title: 네트워크 오프로드 및 최적화 기술
description: 이 항목의 오프 로드 및 최적화 기술을 Windows Server 2016의 개요를 제공 하 고 이러한 기술에 대 한 추가 설명서 링크가 포함 되어 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/20/2018
ms.openlocfilehash: 9cd63ae557eab6e8e4f69fedd20619d4e7af9184
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847854"
---
# <a name="network-offload-and-optimization-technologies"></a>네트워크 오프로드 및 최적화 기술

이 항목에서는 Windows Server 2016에서 사용할 수 있는 다른 네트워크 오프 로드 및 최적화 기능 개요를 제공 하 고 지 원하는 방식 보다 효율적으로 네트워킹에 설명 합니다. 하드웨어 (SH) 통합 기능 및 기술에 하드웨어만 (호스트) 기능 및 기술 및 소프트웨어만 (등) 기능과 기술을 소프트웨어 이러한 기술이 포함 됩니다.

네트워킹 기능 Windows Server 2016에서 사용할 수 있는 세 가지 범주는 같습니다. 

1.  [소프트웨어 전용 (등) 기능과 기술을](hpn-software-only-features.md): 이러한 기능 OS의 일부로 구현 되 고의 기본 NIC와 무관 합니다. 경우에 따라 이러한 기능 최적의 작업에 대 한 NIC의 몇 가지 조정 해야 합니다. 이러한의 예로 hyper-v 기능 vmQoS, Acl 및 NIC 팀 등의 비 Hyper-v 기능 등이 있습니다.   

2.  [소프트웨어 및 하드웨어 (SH) 통합 기능 및 기술](hpn-software-hardware-features.md): 이러한 기능이 소프트웨어 및 하드웨어 구성 요소입니다. 소프트웨어는 기능이 작동 하기 위해 필요한 하드웨어 기능으로 연결 됩니다. 이러한 예로 VMMQ, VMQ, 송신 측 IPv4 체크섬 오프 로드, 및 RSS를 들 수 있습니다.   

3.  [하드웨어 (호스트)만 기능 및 기술](hpn-hardware-only-features.md): 이러한 하드웨어 가속 소프트웨어와 함께에서 네트워킹 성능을 향상 시킬 있지만 포함 되지 않은 깊숙히 소프트웨어 기능입니다. 이러한 예로 인터럽트 조절, 제어 흐름 및 수신 측 IPv4 체크섬 오프 로드를 들 수 있습니다. 

4. [고급 속성 NIC](hpn-nic-advanced-properties.md): Nic 및 NetAdapter cmdlet을 사용 하 여 Windows PowerShell을 통해 모든 기능을 관리할 수 있습니다.  또한 Nic 및 네트워크 Control Panel (ncpa.cpl)를 사용 하 여 모든 기능을 관리할 수 있습니다. 

>[!TIP]
>- 따라서 기능 및 기술에 사용할 수 있습니다 NIC 속도 또는 NIC 기능에 관계 없이 모든 하드웨어 아키텍처.
>
>- SH 기능과 호스트 네트워크 어댑터에 기능이 나 기술을 지 원하는 경우에 사용할 수 있습니다.

---