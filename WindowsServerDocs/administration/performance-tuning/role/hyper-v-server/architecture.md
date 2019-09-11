---
title: Hyper-V 아키텍처
description: 성능 조정을 위한 hyper-v 아키텍처 condsiderations
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 7ed8522ec34e9e262f835530a248567ebbd0ddc9
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866672"
---
# <a name="hyper-v-architecture"></a>Hyper-V 아키텍처

Hyper-v 기능은 유형 1 하이퍼바이저 기반 아키텍처를 제공 합니다. 하이퍼바이저는 프로세서 및 메모리를 가상화 하 고 자식 파티션 (가상 컴퓨터)을 관리 하 고 i/o 장치와 같은 서비스를 가상 컴퓨터에 노출 하는 루트 파티션의 가상화 스택에 대 한 메커니즘을 제공 합니다.

루트 파티션은를 소유 하 고 실제 i/o 장치에 직접 액세스할 수 있습니다. 루트 파티션의 가상화 스택은 가상 컴퓨터, 관리 Api 및 가상화 된 i/o 장치에 대 한 메모리 관리자를 제공 합니다. 또한 IDE (통합 장치) 디스크 컨트롤러 및 PS/2 입력 장치 포트와 같은 에뮬레이트된 장치를 구현 하며, 향상 된 성능 및 감소 된 오버 헤드를 위해 Hyper-v 관련 가상 장치를 지원 합니다.

![hyper-v 하이퍼바이저 기반 아키텍처](../../media/perftune-guide-hyperv-arch.png)

Hyper-v 관련 i/o 아키텍처는 루트 파티션에 있는 .Vsps (가상화 서비스 공급자)와 자식 파티션의 VSCs (가상화 서비스 클라이언트)로 구성 됩니다. 각 서비스는 i/o 버스 역할을 하는 VMBus를 통해 장치로 노출 되며 공유 메모리와 같은 메커니즘을 사용 하는 가상 컴퓨터 간에 고성능 통신을 가능 하 게 합니다. 게스트 운영 체제의 플러그 앤 플레이 관리자는 VMBus를 비롯 하 여 이러한 장치를 열거 하 고 적절 한 장치 드라이버 (가상 서비스 클라이언트)를 로드 합니다. I/o 이외의 서비스도이 아키텍처를 통해 노출 됩니다.

Windows Server 2008부터 운영 체제는 가상 컴퓨터에서 실행 되는 경우 해당 동작을 최적화 하는 기능을 enlightenments 합니다. 이러한 이점으로는 메모리 가상화 비용 절감, 다중 코어 확장성 향상, 게스트 운영 체제의 백그라운드 CPU 사용량 감소 등이 있습니다.

다음 섹션에서는 Hyper-v 역할을 실행 하는 서버에서 성능이 향상 되는 모범 사례를 제안 합니다.

## <a name="see-also"></a>참조

-   [Hyper-V 용어](terminology.md)

-   [Hyper-V 서버 구성](configuration.md)

-   [Hyper-V 프로세서 성능](processor-performance.md)

-   [Hyper-V 메모리 성능](memory-performance.md)

-   [Hyper-V 스토리지 I/O 성능](storage-io-performance.md)

-   [Hyper-V 네트워크 I/O 성능](network-io-performance.md)

-   [가상화된 환경의 병목 상태 탐지](detecting-virtualized-environment-bottlenecks.md)

-   [Linux Virtual Machines](linux-virtual-machine-considerations.md)
