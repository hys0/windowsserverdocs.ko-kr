---
title: Hyper-v 네트워크 I/O 성능
description: 네트워크 Hyper-v 성능 튜닝의 i/o 성능 고려 사항
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: d52c4fff6c7e06fb0a9f2b44ea51a0a790e6674d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814364"
---
# <a name="hyper-v-network-io-performance"></a>Hyper-v 네트워크 I/O 성능

Server 2016에는 몇 가지 향상 된 기능 및 새로운 기능-Hyper-v에서 네트워크 성능을 최적화 하기 위해 포함 되어 있습니다.  이 문서의 이후 버전에서 네트워크 성능을 최적화 하는 방법에 대 한 문서가 포함 됩니다.

## <a name="live-migration"></a>실시간 마이그레이션

실시간 마이그레이션을 사용 하면 투명 하 게 가동 또는 네트워크 연결이 없는 동일한 클러스터의 다른 노드로 장애 조치 클러스터의 한 노드에서 실행 중인 가상 컴퓨터를 이동할 수 있습니다.

**참고**    장애 조치 클러스터링 공유 storage 클러스터 노드에 대 한에 필요 합니다.

실행 중인 가상 컴퓨터를 이동 하는 프로세스는 두 가지 주요 단계로 나눌 수 있습니다. 첫 번째 단계는 새 호스트에 현재 호스트에서 가상 머신의 메모리를 복사합니다. 두 번째 단계는 새 호스트에 현재 호스트에서 가상 머신 상태를 전송합니다. 두 단계의 기간 삽입할 데이터 전송할 수 있습니다 새 호스트에 현재 호스트에서 속도로 크게 결정 됩니다.

전용된 네트워크를 제공 합니다. 실시간 마이그레이션에 대 한 트래픽을 실시간 마이그레이션을 완료 하는 데 필요한 시간을 최소화 주며 일관 된 마이그레이션 시간을 보장 합니다.

![hyper-v 실시간 마이그레이션 구성 예](../../media/perftune-guide-live-migration.png)

또한 늘리면 송신 및 수신 버퍼에서 각 네트워크 어댑터 마이그레이션에 관련 된 마이그레이션 성능을 개선할 수 있습니다.

Windows Server 2012 R2 하드웨어가 지 원하는 경우 네트워크를 통해 전송 하기 전에 메모리를 압축 하 여 실시간 마이그레이션 속도 또는 원격 직접 메모리 액세스 (RDMA)를 사용 하는 옵션을 도입 했습니다.

## <a name="see-also"></a>참조

-   [Hyper-v 용어](terminology.md)

-   [Hyper-v 아키텍처](architecture.md)

-   [Hyper-v 서버-구성](configuration.md)

-   [Hyper-v 프로세서 성능](processor-performance.md)

-   [Hyper-v 메모리 성능](memory-performance.md)

-   [Hyper-v 저장소 I/O 성능](storage-io-performance.md)

-   [가상화 된 환경에서 병목 상태를 검색합니다.](detecting-virtualized-environment-bottlenecks.md)

-   [Linux Virtual Machines](linux-virtual-machine-considerations.md)
