---
title: Hyper-v 메모리 성능
description: 성능 튜닝 Hyper-v에서에서 메모리 고려 사항
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 63a1b654b8ac52725cc5dd87c8b245f9dfaf40f0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848074"
---
# <a name="hyper-v-memory-performance"></a>Hyper-v 메모리 성능


하이퍼바이저는 가상화 되지 않은 시스템에만 가상 컴퓨터를 서로 격리 하 고 각 게스트 운영 체제에 대 한 연속 된 0부터 시작 메모리 공간을 제공 하는 게스트 물리적 메모리를 가상화 합니다.

## <a name="correct-memory-sizing-for-child-partitions"></a>자식 파티션에 대 한 올바른 메모리 크기 조정

물리적 컴퓨터에서 서버 응용 프로그램에 대 한 일반적인 방법으로 가상 컴퓨터 메모리를 크기를 결정 해야 합니다. 크기를 지정 해야 합니다를 합리적으로 일반적인에서 예상 되는 부하를 처리할 수 및 메모리가 부족 하 여 응답 시간과 CPU 또는 I/O 사용량이 크게 높일 수 최대 사용 시간입니다.

Windows 가상 컴퓨터 메모리를 동적으로 크기를 허용 하기 위한 동적 메모리를 사용할 수 있습니다. 가상 컴퓨터에서 응용 프로그램 문제가 큰 급격 한 메모리 할당을 수행 하는 경우 동적 메모리를 사용 하 여 가상 컴퓨터에 동적 메모리는 메모리 부족에 응답 하는 동안 임시 백업에 대 한 페이지 파일 크기를 늘릴 수 있습니다.

동적 메모리에 대 한 자세한 내용은 참조 하세요. [Hyper-v 동적 메모리 개요]( https://go.microsoft.com/fwlink/?linkid=834434) 하 고 [Hyper-v 동적 메모리 구성 가이드](https://go.microsoft.com/fwlink/?linkid=834435)합니다.

자식 파티션에 Windows를 실행 하는 경우에 자식 파티션 메모리 압력이 발생 이며 더 높은 가상 컴퓨터 메모리 크기를 사용 하 여 더 잘 수행할 수 있는지 여부를 나타내는 자식 파티션 내에서 다음 성능 카운터를 사용할 수 있습니다.

| 성능 카운터                                                         | 제안 된 임계값 값                                                                                                                                                           |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 메모리-대기 캐시 예약 (바이트)                                        | 대기 캐시 예약 바이트 및 무료 0 페이지 목록 바이트의 합계는 1 GB, 및 300MB 이상을 2GB 이상의 RAM을 볼 수 있는 시스템에서 사용 하 여 시스템에 200MB 이상의 이어야 합니다. |
| 메모리-사용 가능한와 0 개 페이지 목록 바이트                                        | 대기 캐시 예약 바이트 및 무료 0 페이지 목록 바이트의 합계는 1 GB, 및 300MB 이상을 2GB 이상의 RAM을 볼 수 있는 시스템에서 사용 하 여 시스템에 200MB 이상의 이어야 합니다. |
| 메모리-Pages Input/Sec                                                    | 1 시간 동안 평균 10 보다 작은 경우                                                                                                                                       | 

## <a name="correct-memory-sizing-for-root-partition"></a>루트 파티션에 대 한 올바른 메모리 크기 조정

루트 파티션에 I/O 가상화, 가상 머신 스냅숏 및 자식 파티션을 지원 하도록 관리와 같은 서비스를 제공 하는 데 충분 한 메모리가 있어야 합니다.

Windows Server 2016의 Hyper-v는 얼마나 안전 하 게 할당할 수 있는 메모리 자식 파티션에 여전히 루트 파티션에의 높은 성능 및 안정성을 보장 하는 동안 확인 하려면 루트 파티션 관리 운영 체제의 런타임 상태를 모니터링 합니다.

## <a name="see-also"></a>참조

-   [Hyper-v 용어](terminology.md)

-   [Hyper-v 아키텍처](architecture.md)

-   [Hyper-v 서버-구성](configuration.md)

-   [Hyper-v 프로세서 성능](processor-performance.md)

-   [Hyper-v 저장소 I/O 성능](storage-io-performance.md)

-   [Hyper-v 네트워크 I/O 성능](network-io-performance.md)

-   [가상화 된 환경에서 병목 상태를 검색합니다.](detecting-virtualized-environment-bottlenecks.md)

-   [Linux Virtual Machines](linux-virtual-machine-considerations.md)
