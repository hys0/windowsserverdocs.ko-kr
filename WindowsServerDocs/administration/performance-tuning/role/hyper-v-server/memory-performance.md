---
title: Hyper-v 메모리 성능
description: 성능 튜닝 Hyper-v의 메모리 고려 사항
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: asmahi; sandysp; jopoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 5f683b85657b8dd263e93380b71c646ad677950c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851726"
---
# <a name="hyper-v-memory-performance"></a>Hyper-v 메모리 성능


하이퍼바이저는 게스트 실제 메모리를 가상화 하 여 가상 컴퓨터를 서로 격리 하 고 가상화 되지 않은 시스템에서와 마찬가지로 각 게스트 운영 체제에 대해 0부터 시작 하는 연속 메모리 공간을 제공 합니다.

## <a name="correct-memory-sizing-for-child-partitions"></a>자식 파티션의 메모리 크기 수정

물리적 컴퓨터의 서버 응용 프로그램에 대해 일반적으로 수행 하는 가상 컴퓨터 메모리 크기를 조정 해야 합니다. 메모리가 부족 하면 응답 시간 및 CPU 또는 i/o 사용량이 크게 증가할 수 있으므로 예상 부하를 일반 및 피크 시간에 합리적으로 처리할 수 있도록 크기를 조정 해야 합니다.

동적 메모리 사용 하도록 설정 하 여 Windows에서 가상 컴퓨터 메모리를 동적으로 크기를 조정 하도록 할 수 있습니다. 동적 메모리를 사용 하는 경우 가상 컴퓨터의 응용 프로그램에서 갑작스러운 메모리 할당을 수행 하는 데 문제가 발생 하는 경우 가상 컴퓨터의 페이지 파일 크기를 늘려 동적 메모리 메모리 압력에 응답 하는 동안 일시적으로 백업할 수 있습니다.

동적 메모리에 대 한 자세한 내용은 [hyper-v 동적 메모리 개요]( https://go.microsoft.com/fwlink/?linkid=834434) 및 [Hyper-v 동적 메모리 구성 가이드](https://go.microsoft.com/fwlink/?linkid=834435)를 참조 하세요.

자식 파티션에서 Windows를 실행 하는 경우 자식 파티션 내에서 다음 성능 카운터를 사용 하 여 자식 파티션에 메모리 압력이 발생 하 고 더 높은 가상 컴퓨터 메모리 크기를 사용 하 여 더 잘 수행 될 수 있는지 여부를 확인할 수 있습니다.

| 성능 카운터                                                         | 제안 된 임계값                                                                                                                                                           |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 메모리 – 대기 캐시 예약 바이트                                        | 대기 캐시 예약 바이트 수와 사용 가능한 0 페이지 목록 바이트의 합계는 1gb 이상의 RAM 300이 있는 시스템에서 200 MB 이상 이어야 합니다. |
| Memory – Free & 0 페이지 목록 바이트                                        | 대기 캐시 예약 바이트 수와 사용 가능한 0 페이지 목록 바이트의 합계는 1gb 이상의 RAM 300이 있는 시스템에서 200 MB 이상 이어야 합니다. |
| Memory – Pages Input/Sec                                                    | 1 시간 동안의 평균은 10 보다 낮습니다.                                                                                                                                       | 

## <a name="correct-memory-sizing-for-root-partition"></a>루트 파티션에 대 한 메모리 크기 수정

루트 파티션에는 i/o 가상화, 가상 머신 스냅숏 및 관리와 같은 서비스를 제공 하 여 자식 파티션을 지원할 수 있는 충분 한 메모리가 있어야 합니다.

Windows Server 2016의 hyper-v는 루트 파티션의 높은 성능과 안정성을 보장 하면서 자식 파티션에 안전 하 게 할당할 수 있는 메모리 양을 확인 하기 위해 루트 파티션의 관리 운영 체제의 런타임 상태를 모니터링 합니다.

## <a name="see-also"></a>참고 항목

-   [Hyper-V 용어](terminology.md)

-   [Hyper-V 아키텍처](architecture.md)

-   [Hyper-V 서버 구성](configuration.md)

-   [Hyper-V 프로세서 성능](processor-performance.md)

-   [Hyper-V 스토리지 I/O 성능](storage-io-performance.md)

-   [Hyper-V 네트워크 I/O 성능](network-io-performance.md)

-   [가상화된 환경의 병목 상태 탐지](detecting-virtualized-environment-bottlenecks.md)

-   [Linux Virtual Machines](linux-virtual-machine-considerations.md)
