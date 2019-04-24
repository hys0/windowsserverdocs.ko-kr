---
title: Hyper-V 서버 성능 튜닝
description: Hyper-V 성능 튜닝 지침
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 0d850ba198d269888dfa0ad323546541983b88e1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891754"
---
# <a name="performance-tuning-hyper-v-servers"></a>Hyper-V 서버 성능 튜닝


Hyper-V는 Windows Server 2016의 가상화 서버 역할입니다. 가상화 서버는 프로세서, 메모리 및 I/O 디바이스를 가상화하여 서로 격리되지만 기본 하드웨어 리소스를 공유하는 여러 가상 머신을 호스트할 수 있습니다. 서버를 단일 머신에 통합하면 가상화를 통해 리소스 사용률 및 에너지 효율을 높이고 서버의 운영 및 유지 관리 비용을 줄일 수 있습니다. 뿐만 아니라 가상 머신과 관리 API는 보다 유연하게 리소스를 관리하고, 부하를 분산하고, 시스템을 프로비저닝할 수 있습니다.

## <a name="see-also"></a>참고 항목

-   [Hyper-V 용어](terminology.md)

-   [Hyper-V 아키텍처](architecture.md)

-   [Hyper-V 서버 구성](configuration.md)

-   [Hyper-V 프로세서 성능](processor-performance.md)

-   [Hyper-V 메모리 성능](memory-performance.md)

-   [Hyper-V 스토리지 I/O 성능](storage-io-performance.md)

-   [Hyper-V 네트워크 I/O 성능](network-io-performance.md)

-   [가상화된 환경의 병목 상태 탐지](detecting-virtualized-environment-bottlenecks.md)

-   [Linux Virtual Machines](linux-virtual-machine-considerations.md)
