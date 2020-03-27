---
title: 네트워크 오프로드 및 최적화 기술
description: 이 항목에서는 Windows Server 2016의 오프 로드 및 최적화 기술에 대 한 개요를 제공 하며, 이러한 기술에 대 한 추가 지침에 대 한 링크를 제공 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/20/2018
ms.openlocfilehash: 04e924190170bbd3c841b452a27dc586bb69024e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316859"
---
# <a name="network-offload-and-optimization-technologies"></a>네트워크 오프로드 및 최적화 기술

이 항목에서는 Windows Server 2016에서 사용할 수 있는 다양 한 네트워크 오프 로드 및 최적화 기능에 대 한 개요를 제공 하 고 네트워킹의 효율성을 향상 하는 방법을 설명 합니다. 이러한 기술에는 소프트웨어 전용 (따라서) 기능 및 기술, SH (소프트웨어 및 하드웨어) 통합 기능 및 기술, 하드웨어 전용 (호) 기능 및 기술이 포함 됩니다.

Windows Server 2016에서 사용할 수 있는 세 가지 네트워크 기능 범주는 다음과 같습니다. 

1.  [소프트웨어만 () 기능 및 기술](hpn-software-only-features.md): 이러한 기능은 OS의 일부로 구현 되며 기본 NIC와는 독립적입니다. 이러한 기능에는 최적의 작업을 위해 NIC를 조정 해야 하는 경우가 있습니다. 여기에는 vmQoS, Acl 및 NIC 팀과 같은 Hyper-v 이외의 기능과 같은 Hyper-v 기능이 포함 됩니다.   

2.  [소프트웨어 및 하드웨어 (SH) 통합 기능 및 기술](hpn-software-hardware-features.md): 이러한 기능에는 소프트웨어와 하드웨어 구성 요소가 모두 포함 되어 있습니다. 이 소프트웨어는 기능을 작동 하는 데 필요한 하드웨어 기능에 깊이 됩니다. 이러한 예로는 VMMQ, VMQ, 송신 측 IPv4 체크섬 오프 로드 및 RSS가 있습니다.   

3.  [하드웨어 전용 (호) 기능 및 기술](hpn-hardware-only-features.md): 이러한 하드웨어 가속은 소프트웨어와 함께 네트워킹 성능을 향상 시키지만 소프트웨어 기능의 일부가 깊이 않습니다. 이러한 예로는 인터럽트 중재, 흐름 제어 및 수신 측 IPv4 체크섬 오프 로드 등이 있습니다. 

4. [Nic 고급 속성](hpn-nic-advanced-properties.md): get-netadapter cmdlet을 사용 하 여 Windows PowerShell을 통해 nic 및 모든 기능을 관리할 수 있습니다.  네트워크 제어판 (ncpa.cpl)을 사용 하 여 Nic 및 모든 기능을 관리할 수도 있습니다. 

>[!TIP]
>- 따라서 기능 및 기술은 NIC 속도 또는 NIC 기능에 관계 없이 모든 하드웨어 아키텍처에서 사용할 수 있습니다.
>
>- SH 및 호 기능은 네트워크 어댑터에서 기능 또는 기술을 지 원하는 경우에만 사용할 수 있습니다.

---