---
title: Hyper-v 네트워크 i/o 성능
description: Hyper-v 성능 조정의 네트워크 i/o 성능 고려 사항
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: asmahi; sandysp; jopoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 17551da6cd270f05cf2d6b1a8147958f82b2c9b3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851806"
---
# <a name="hyper-v-network-io-performance"></a>Hyper-v 네트워크 i/o 성능

서버 2016에는 Hyper-v에서 네트워크 성능을 최적화 하기 위한 몇 가지 향상 된 기능과 새로운 기능이 포함 되어 있습니다.  네트워크 성능을 최적화 하는 방법에 대 한 설명서는이 문서의 이후 버전에 포함 될 예정입니다.

## <a name="live-migration"></a>실시간 마이그레이션

실시간 마이그레이션를 사용 하면 네트워크 연결을 중단 하거나 가동 중지 시간 없이 장애 조치 (failover) 클러스터의 한 노드에서 실행 중인 가상 컴퓨터를 동일한 클러스터의 다른 노드로 투명 하 게 이동할 수 있습니다.

> [!NOTE]
> 장애 조치 (Failover) 클러스터링에는 클러스터 노드에 대 한 공유 저장소가 필요 합니다.

실행 중인 가상 컴퓨터를 이동 하는 프로세스는 두 가지 주요 단계로 나눌 수 있습니다. 첫 번째 단계는 가상 머신의 메모리를 현재 호스트에서 새 호스트로 복사 합니다. 두 번째 단계는 현재 호스트에서 새 호스트로 가상 컴퓨터 상태를 전송 합니다. 두 단계의 기간은 데이터를 현재 호스트에서 새 호스트로 전송할 수 있는 속도에 따라 크게 결정 됩니다.

실시간 마이그레이션 트래픽에 대 한 전용 네트워크를 제공 하면 실시간 마이그레이션을 완료 하는 데 필요한 시간을 최소화 하 고 마이그레이션 시간을 일관성 있게 유지할 수 있습니다.

![hyper-v 실시간 마이그레이션 구성 예제](../../media/perftune-guide-live-migration.png)

또한 마이그레이션과 관련 된 각 네트워크 어댑터에서 송신 및 수신 버퍼 수를 늘려도 마이그레이션 성능을 향상 시킬 수 있습니다.

Windows Server 2012 r 2에서는 네트워크를 통해 전송 하기 전에 메모리를 압축 하거나, 하드웨어에서 지 원하는 경우 RDMA (원격 직접 메모리 액세스)를 사용 하 여 실시간 마이그레이션를 가속화 하는 옵션을 도입 했습니다.

## <a name="see-also"></a>참고 항목

-   [Hyper-V 용어](terminology.md)

-   [Hyper-V 아키텍처](architecture.md)

-   [Hyper-V 서버 구성](configuration.md)

-   [Hyper-V 프로세서 성능](processor-performance.md)

-   [Hyper-V 메모리 성능](memory-performance.md)

-   [Hyper-V 스토리지 I/O 성능](storage-io-performance.md)

-   [가상화된 환경의 병목 상태 탐지](detecting-virtualized-environment-bottlenecks.md)

-   [Linux Virtual Machines](linux-virtual-machine-considerations.md)
