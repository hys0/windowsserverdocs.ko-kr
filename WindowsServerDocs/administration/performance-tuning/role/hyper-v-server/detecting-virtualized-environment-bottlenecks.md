---
title: 가상화 된 환경에서 병목 상태 검색
description: 잠재적 Hyper-v 성능 병목 상태를 검색 하 고 해결 하는 방법
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 53ec6159d177284773f17a05a37dd89184ef3c12
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370118"
---
# <a name="detecting-bottlenecks-in-a-virtualized-environment"></a>가상화 된 환경에서 병목 상태 검색

이 섹션에서는 성능 모니터를 사용 하 여 모니터링할 항목에 대 한 몇 가지 힌트와 호스트 또는 가상 컴퓨터가 예상 대로 작동 하지 않는 경우 문제가 발생할 수 있는 위치를 식별 하는 방법을 설명 합니다.

## <a name="processor-bottlenecks"></a>프로세서 병목 상태

프로세서 병목 상태를 발생 시킬 수 있는 몇 가지 일반적인 시나리오는 다음과 같습니다.

-   하나 이상의 논리 프로세서가 로드 되었습니다.

-   하나 이상의 가상 프로세서가 로드 되었습니다.

호스트에서 다음 성능 카운터를 사용할 수 있습니다.

-   논리 프로세서 사용률-\\Hyper-v 하이퍼바이저 논리 프로세서 (\*)\\% 총 실행 시간

-   가상 프로세서 사용률-\\Hyper-v 하이퍼바이저 가상 프로세서 (\*)\\% 총 실행 시간

-   루트 가상 프로세서 사용률-\\Hyper-v 하이퍼바이저 루트 가상 프로세서 (\*)\\% 총 실행 시간

**Hyper-v 하이퍼바이저 논리 프로세서 (\_합계)\\% Total Runtime** 카운터가 90%를 초과 하면 호스트가 오버 로드 됩니다. 처리 능력을 추가 하거나 일부 가상 컴퓨터를 다른 호스트로 이동 해야 합니다.

**Hyper-v 하이퍼바이저 가상 프로세서 (VM 이름: VP x)\\% Total 런타임** 카운터가 모든 가상 프로세서에 대해 90%를 초과 하는 경우 다음을 수행 해야 합니다.

-   호스트가 오버 로드 되지 않았는지 확인 합니다.

-   워크 로드에서 더 많은 가상 프로세서를 활용할 수 있는지 확인

-   가상 컴퓨터에 가상 프로세서를 더 할당 합니다.

**Hyper-v 하이퍼바이저 가상 프로세서 (VM 이름: VP x)\\% Total Runtime** 카운터가 가상 프로세서 중 일부에 대해 90%를 초과 하는 경우 다음을 수행 해야 합니다.

-   워크 로드가 네트워크를 많이 수신할 경우 vRSS를 사용 하는 것이 좋습니다.

-   가상 컴퓨터에서 Windows Server 2012 r 2를 실행 하지 않는 경우 더 많은 네트워크 어댑터를 추가 해야 합니다.

-   작업 부하가 저장소 집약적 이면 가상 NUMA를 사용 하도록 설정 하 고 가상 디스크를 더 추가 해야 합니다.

**Hyper-v 하이퍼바이저 루트 가상 프로세서 (루트 VP x)\\% Total 런타임** 카운터가 일부에 대해 90%를 초과 하는 경우 그러나 모든 가상 프로세서와 **프로세서 (x)\\% DPC time 및 processor (x)\\% DPC time** 카운터의 값이 루트 **가상 프로세서 (루트 VP x)의** 값에 대 한 값 (%)을 더한 값이 됩니다.\\

## <a name="memory-bottlenecks"></a>메모리 병목 상태

메모리 병목 상태를 발생 시킬 수 있는 몇 가지 일반적인 시나리오는 다음과 같습니다.

-   호스트가 응답 하지 않습니다.

-   가상 컴퓨터를 시작할 수 없습니다.

-   가상 컴퓨터의 메모리가 부족 합니다.

호스트에서 다음 성능 카운터를 사용할 수 있습니다.

-   사용 가능한 메모리\\Mb

-   Hyper-v 동적 메모리 분산 장치 (\*)\\사용 가능한 메모리

가상 머신에서 다음 성능 카운터를 사용할 수 있습니다.

-   사용 가능한 메모리\\Mb

**사용 가능한 메모리\\mb** 및 **Hyper-v 동적 메모리 분산 장치 (\*)\\사용 가능한 메모리** 카운터가 호스트에 부족 한 경우에는 중요 하지 않은 서비스를 중지 하 고 하나 이상의 가상 컴퓨터를 다른 호스트로 마이그레이션해야 합니다.

가상 컴퓨터에서 **사용 가능한 메모리\\mb** 카운터가 부족 한 경우 가상 컴퓨터에 더 많은 메모리를 할당 해야 합니다. 동적 메모리를 사용 하는 경우 최대 메모리 설정을 늘려야 합니다.

## <a name="network-bottlenecks"></a>네트워크 병목 상태

네트워크 병목 상태를 발생 시킬 수 있는 몇 가지 일반적인 시나리오는 다음과 같습니다.

-   호스트가 네트워크에 바인딩되어 있습니다.

-   가상 컴퓨터가 네트워크에 바인딩되어 있습니다.

호스트에서 다음 성능 카운터를 사용할 수 있습니다.

-   네트워크 인터페이스 (*네트워크 어댑터 이름*)\\바이트/초

가상 머신에서 다음 성능 카운터를 사용할 수 있습니다.

-   Hyper-v Virtual Network 어댑터 (*가상 컴퓨터 이름 이름&lt;GUID&gt;* )\\바이트/초

**실제 NIC 바이트/초** 카운터가 용량의 90% 보다 크거나 같은 경우 추가 네트워크 어댑터를 추가 하 고, 가상 컴퓨터를 다른 호스트로 마이그레이션하고, 네트워크 QoS를 구성 해야 합니다.

**Hyper-v Virtual Network Adapter Bytes/sec** 카운터가 250 MBps 보다 크거나 같은 경우 가상 머신에 팀으로 구성 된 네트워크 어댑터를 추가 하 고 vRSS를 사용 하도록 설정 하 고 sr-iov를 사용 해야 합니다.

워크 로드가 네트워크 대기 시간을 충족할 수 없는 경우 SR-IOV를 사용 하도록 설정 하 여 실제 네트워크 어댑터 리소스를 가상 머신에 제공할 수 있습니다.

## <a name="storage-bottlenecks"></a>저장소 병목 상태

저장소 병목 상태를 발생 시킬 수 있는 몇 가지 일반적인 시나리오는 다음과 같습니다.

-   호스트 및 가상 컴퓨터 작업이 느리거나 시간이 초과 되었습니다.

-   가상 컴퓨터의 속도가 느려집니다.

호스트에서 다음 성능 카운터를 사용할 수 있습니다.

-   실제 디스크 (*디스크 문자*)\\Avg. Disk Sec/Read

-   실제 디스크 (*디스크 문자*)\\Avg. Disk Sec/Write

-   실제 디스크 (*디스크 문자*)\\평균 디스크 읽기 큐 길이

-   실제 디스크 (*디스크 문자*)\\평균 디스크 쓰기 큐 길이

대기 시간이 지속적으로 50ms 보다 큰 경우 다음을 수행 해야 합니다.

-   추가 저장소에 가상 컴퓨터 분산

-   더 빠른 저장소 구매 고려

-   Windows Server 2012 r 2에 도입 된 Tiered Storage 공간 고려

-   Windows Server 2012 r 2에 도입 된 저장소 QoS를 사용 하는 것이 좋습니다.

-   VHDX 사용

## <a name="see-also"></a>참고 항목

-   [Hyper-V 용어](terminology.md)

-   [Hyper-V 아키텍처](architecture.md)

-   [Hyper-V 서버 구성](configuration.md)

-   [Hyper-V 프로세서 성능](processor-performance.md)

-   [Hyper-V 메모리 성능](memory-performance.md)

-   [Hyper-V 스토리지 I/O 성능](storage-io-performance.md)

-   [Hyper-V 네트워크 I/O 성능](network-io-performance.md)

-   [Linux Virtual Machines](linux-virtual-machine-considerations.md)
