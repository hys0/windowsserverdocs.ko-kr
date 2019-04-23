---
title: Hyper-V 아키텍처
description: 성능 튜닝에 대 한 hyper-v 아키텍처 condsiderations
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: fcc87b04698a44e115c8f49150fe33443f8e6a88
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890284"
---
# <a name="hyper-v-architecture"></a>Hyper-V 아키텍처

Hyper-v 기능 유형 1 하이퍼바이저 기반 아키텍처. 하이퍼바이저는 프로세서 및 메모리를 가상화 하 고 자식 파티션에 (가상 머신)을 관리 하 고 가상 컴퓨터에 대 한 I/O 장치 등의 서비스를 노출 하 여 루트 파티션에의 가상화 스택 메커니즘을 제공 합니다.

루트 파티션에 소유 하 고 실제 I/O 장치에 대 한 직접 액세스 권한이 있습니다. 루트 파티션에 가상화 스택 virtual machines, Api, 관리 및 가상화 된 I/O 장치에 대 한 메모리 관리자를 제공합니다. 또한 성능 향상된을 위해 하이퍼-V-특정 가상 장치를 지원 하 고 오버 헤드 감소 통합된 장치 electronics (IDE) 디스크 컨트롤러 및 PS/2 입력된 장치 포트와 같은 에뮬레이트된 장치를 구현 합니다.

![hyper-v 하이퍼바이저 기반 아키텍처](../../media/perftune-guide-hyperv-arch.png)

하이퍼-V-특정 I/O 아키텍처 가상화 서비스 공급자 (Vsp) 루트 파티션 및 가상화 서비스 클라이언트 (Vsc)는 자식 파티션에 이루어져 있습니다. 각 서비스는 I/O 버스는 역할을 하며 공유 메모리와 같은 메커니즘을 사용 하는 가상 머신 간의 고성능 통신을 사용 하도록 설정 하는 vmbus 장치로 노출 됩니다. 게스트 운영 체제의 플러그 앤 플레이 관리자 VMBus를 포함 하 여 이러한 장치를 열거 하 고, 해당 장치 드라이버 (가상 서비스 클라이언트)를 로드 합니다. I/O 이외의 서비스가이 아키텍처를 통해 노출 됩니다.

Windows Server 2008 virtual machines에서 실행 되는 경우 해당 동작을 최적화 하기 위해 운영 체제 기능 enlightenments부터 시작 합니다. 다중 코어 확장성을 개선 하 고 백그라운드 게스트 운영 체제의 CPU 사용을 줄이면 메모리 가상화의 비용을 절감 합니다.

다음 섹션에서는 Hyper-v 역할을 실행 하는 서버의 성능 향상된을 생성 하는 모범 사례를 제안 합니다.

## <a name="see-also"></a>참조

-   [Hyper-v 용어](terminology.md)

-   [Hyper-v 서버-구성](configuration.md)

-   [Hyper-v 프로세서 성능](processor-performance.md)

-   [Hyper-v 메모리 성능](memory-performance.md)

-   [Hyper-v 저장소 I/O 성능](storage-io-performance.md)

-   [Hyper-v 네트워크 I/O 성능](network-io-performance.md)

-   [가상화 된 환경에서 병목 상태를 검색합니다.](detecting-virtualized-environment-bottlenecks.md)

-   [Linux Virtual Machines](linux-virtual-machine-considerations.md)
