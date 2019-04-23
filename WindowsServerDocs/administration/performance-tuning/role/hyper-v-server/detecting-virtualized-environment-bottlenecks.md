---
title: 가상화 된 환경에서 병목 상태를 검색합니다.
description: 잠재적인 hyper-v에 대 한 성능 병목 상태를 감지 하는 방법
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: cdad5f0cc3b0e49ae46e975e3acc2c48a18e5f70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867534"
---
# <a name="detecting-bottlenecks-in-a-virtualized-environment"></a>가상화 된 환경에서 병목 상태를 검색합니다.

이 섹션에서는 성능 모니터를 사용 하 여 모니터링을 하 고 있는 것일 수 있습니다 예상한 대로 호스트 또는 가상 머신 일부를 수행 하지 않습니다 하는 경우를 식별 하는 방법에 대 한 몇 가지 힌트를 제공 해야 합니다.

## <a name="processor-bottlenecks"></a>프로세서 병목 지점

프로세서 병목 상태를 일으킬 수 있는 몇 가지 일반적인 시나리오는 다음과 같습니다.

-   하나 이상의 논리적 프로세서는 로드

-   하나 이상의 가상 프로세서 로드

호스트에서 다음 성능 카운터를 사용할 수 있습니다.

-   논리 프로세서 사용률 \\Hyper-v 하이퍼바이저 논리 프로세서 (\*)\\% 총 실행 시간

-   가상 프로세서 사용률 \\Hyper-v 하이퍼바이저 가상 프로세서 (\*)\\% 총 실행 시간

-   가상 프로세서 사용률-루트 \\Hyper-v 하이퍼바이저 루트 가상 프로세서 (\*)\\% 총 실행 시간

경우는 **Hyper-v 하이퍼바이저 논리 프로세서 (\_총)\\총 실행 시간 %** 카운터 90% 인 호스트는 오버 로드 됩니다. 강력한 처리 기능을 추가 하거나 일부 가상 컴퓨터를 다른 호스트로 이동 해야 합니다.

경우는 **Hyper-v 하이퍼바이저 가상 Processor(VM Name:VP x)\\% 총 런타임** 카운터는 모든 가상 프로세서의 90% 넘게, 다음을 수행 해야 합니다.

-   호스트는 오버 로드 확인

-   워크 로드를 가상 프로세서를 활용 하는 경우 확인

-   가상 컴퓨터에 더 많은 가상 프로세서를 할당

하는 경우 **Hyper-v 하이퍼바이저 가상 Processor(VM Name:VP x)\\% 총 런타임** 카운터는 90% 경우도 있지만 가상 프로세서의 전부는 아님, 다음을 수행 해야 합니다.

-   워크 로드는 네트워크 집약적인을 수신 하는 경우 vRSS를 사용 하는 것이 좋습니다.

-   가상 컴퓨터는 Windows Server 2012 R2를 실행 하지 않는, 경우에 더 많은 네트워크 어댑터를 추가 해야 합니다.

-   저장소 집약적 작업을 사용 하는 경우에 가상 NUMA를 사용 하 고 가상 디스크를 추가 해야 합니다.

경우는 **Hyper-v 하이퍼바이저 가상 프로세서 루트 (루트 VP x)\\% 총 런타임** 전부는 아니지만 일부 가상 프로세서의 90%가 넘는 카운터와 **프로세서 (x)\\% Interrupt Time 및 프로세서 (x)\\% DPC Time** 카운터 약 추가 대 한 값을 **루트 가상 Processor(Root VP x)\\총 실행 시간 %** 카운터를 확인 해야에서 VMQ를 사용 하도록 설정 네트워크 어댑터입니다.

## <a name="memory-bottlenecks"></a>메모리 병목 상태

메모리 병목 현상을 일으킬 수 있는 몇 가지 일반적인 시나리오는 다음과 같습니다.

-   호스트가 응답 하지 않습니다.

-   가상 컴퓨터를 시작할 수 없습니다.

-   가상 컴퓨터 메모리가 부족합니다.

호스트에서 다음 성능 카운터를 사용할 수 있습니다.

-   메모리\\Available Mbytes

-   Hyper-v 동적 메모리 부하 분산 장치 (\*)\\사용 가능한 메모리

가상 컴퓨터에서 다음 성능 카운터를 사용할 수 있습니다.

-   메모리\\Available Mbytes

경우는 **메모리\\Available Mbytes** 하 고 **Hyper-v 동적 메모리 부하 분산 장치 (\*)\\사용 가능한 메모리** 카운터 호스트 부족을 중지 해야 필수적이 지 않은 서비스 및 하나 이상의 가상 컴퓨터를 다른 호스트로 마이그레이션해야 합니다.

경우는 **메모리\\Available Mbytes** 카운터는 가상 컴퓨터에서 낮은, 가상 컴퓨터에 더 많은 메모리를 할당 해야 합니다. 동적 메모리를 사용 하는 경우에 최대 메모리 설정을 늘려야 합니다.

## <a name="network-bottlenecks"></a>네트워크 병목 상태

네트워크 병목 현상을 일으킬 수 있는 몇 가지 일반적인 시나리오는 다음과 같습니다.

-   호스트는 바인딩된 네트워크입니다.

-   가상 컴퓨터는 네트워크 연결입니다.

호스트에서 다음 성능 카운터를 사용할 수 있습니다.

-   네트워크 인터페이스 (*네트워크 어댑터 이름*)\\Bytes/sec

가상 컴퓨터에서 다음 성능 카운터를 사용할 수 있습니다.

-   Hyper-v 가상 네트워크 어댑터 (*가상 컴퓨터 이름&lt;GUID&gt;*)\\Bytes/sec

경우는 **실제 NIC Bytes/sec** 카운터 보다 크거나 같은 용량의 90%를 추가 해야 추가 네트워크 어댑터, 가상 머신을 다른 호스트로 마이그레이션 및 네트워크 QoS를 구성 합니다.

경우는 **Hyper-v 가상 네트워크 어댑터 바이트 수/초** 카운터 보다 크거나 같음 250 MBps, 추가 해야 가상 컴퓨터에서 추가 팀으로 구성 된 네트워크 어댑터 vRSS를 사용 하도록 설정 하 고 SR-IOV를 사용 합니다.

워크 로드는 해당 네트워크 대기 시간을 충족할 수 없으므로, 제공 되는 가상 컴퓨터에 실제 네트워크 어댑터 리소스에 SR-IOV를 사용 하도록 설정 합니다.

## <a name="storage-bottlenecks"></a>저장소 병목 상태

저장소 병목 상태를 일으킬 수 있는 몇 가지 일반적인 시나리오는 다음과 같습니다.

-   작업은 호스트 및 가상 머신 느리게 하거나 시간을 초과 합니다.

-   가상 컴퓨터가 느려지거나 있습니다.

호스트에서 다음 성능 카운터를 사용할 수 있습니다.

-   실제 디스크 (*디스크 문자*)\\avg. disk sec/Read

-   실제 디스크 (*디스크 문자*)\\avg. disk sec/Write

-   실제 디스크 (*디스크 문자*)\\평균 디스크 읽기 큐 길이

-   실제 디스크 (*디스크 문자*)\\평균 디스크 쓰기 큐 길이

대기 시간이 50ms 보다 일관 되 게 큰 경우에 다음을 수행 해야 합니다.

-   가상 컴퓨터를 추가 저장소에 분산

-   더 빠른 저장소를 구매 하는 것이 좋습니다.

-   Windows Server 2012 R2에 도입 된 계층화 된 저장소 공간을 고려 합니다.

-   Windows Server 2012 R2에 도입 된 저장소 QoS를 사용 하는 것이 좋습니다.

-   VHDX를 사용 합니다.

## <a name="see-also"></a>참조

-   [Hyper-v 용어](terminology.md)

-   [Hyper-v 아키텍처](architecture.md)

-   [Hyper-v 서버-구성](configuration.md)

-   [Hyper-v 프로세서 성능](processor-performance.md)

-   [Hyper-v 메모리 성능](memory-performance.md)

-   [Hyper-v 저장소 I/O 성능](storage-io-performance.md)

-   [Hyper-v 네트워크 I/O 성능](network-io-performance.md)

-   [Linux Virtual Machines](linux-virtual-machine-considerations.md)
