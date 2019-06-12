---
title: Hyper-V 구성
description: 성능 튜닝을 위한 Hyper-v 구성 고려 사항
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: baea091482818c581414ba1d9c1c01db2a52e3d7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435658"
---
# <a name="hyper-v-configuration"></a>Hyper-V 구성

## <a name="hardware-selection"></a>하드웨어 선택

일반적으로 Hyper-v를 실행 하는 서버에 대 한 하드웨어 고려 사항 가상화 되지 않은 서버와 비슷하지만 Hyper-v를 실행 하는 서버는 CPU 사용량이 더 높으며, 더 많은 메모리를 소비 하며 서버 통합으로 인해 큰 I/O 대역폭 요구 사항이 필요 합니다.

-   **프로세서**

    Windows Server 2016의 Hyper-v는 각 활성 가상 컴퓨터에 하나 이상의 가상 프로세서로 논리적 프로세서를 제공합니다. Hyper-v에는 이제 테이블 EPT (Extended Page) 또는 테이블 NPT (Nested Page)와 같은 두 번째 수준 주소 변환 (SLAT) 기술을 지 원하는 프로세서에 필요 합니다.

-   **캐시**

    Hyper-v는 많은 작업 메모리에 가상 머신 구성을 가상 프로세서 대 논리 프로세서의 비율이 높습니다 집합이 있는 로드에 대 한 특히 더 큰 프로세서 캐시에서 이용할 수 있습니다.

-   **메모리**

    실제 서버는 루트 및 자식 파티션에 대 한 충분 한 메모리가 필요합니다. 루트 파티션에 필요한 메모리를 효율적으로 가상 머신 및 가상 머신 스냅숏 등의 작업을 대신 하 여 I/o를 수행 합니다. 하이퍼-V 하면 충분 한 메모리 루트 파티션에 사용할 수 있고 나머지 메모리 자식 파티션에 할당할 수 있습니다. 자식 파티션에 각 가상 머신에 대 한 예상 되는 부하의 필요에 따라 크기가 조정 됩니다.

-   **저장소**

    저장소 하드웨어에는 충분 한 I/O 대역폭 있어야 하 고 가상 현재와 미래의 수요에 맞게 용량을 하는 컴퓨터가 실제 서버가 호스트 합니다. 저장소 컨트롤러 및 디스크 선택 하 고 RAID 구성을 선택할 때 이러한 요구 사항을 고려해 야 합니다. 서로 다른 물리적 디스크에 높은 디스크 사용량이 많은 워크 로드를 사용 하 여 virtual machines 배치 전반적인 성능이 개선 될 가능성이 높습니다. 예를 들어, 가상 머신 4 대 단일 디스크를 공유 하 고 적극적으로 사용 하 여, 각 가상 머신 디스크의 대역폭의 25%만 얻을 수 있습니다.

## <a name="power-plan-considerations"></a>전원 계획 고려 사항

핵심 기술에 가상화는 서버 워크 로드 밀도 증가, 데이터 센터에 필요한 실제 서버의 수를 줄이면, 운영 효율성 향상 및 전력 소비 비용을 줄이는 데 도움이 강력한 도구를 사용 합니다. 전원 관리는 cost management를 위한 중요 합니다. 

이상적인 데이터 센터 환경에서 전력 소비 될 때까지 주로 사용 중인 컴퓨터에 작업을 통합 하 고 다음 유휴 컴퓨터를 해제 하 여 관리 됩니다. 이 방법이 적합 하지 않습니다, 경우 관리자가 필요한 것 보다 더 많은 power를 사용 하지 않는 하도록 실제 호스트에서 전원 계획을 활용할 수 있습니다. 

서버 전원 관리 기술 대가가, 테 넌 트로 특히 워크 로드는 호스터의 물리적 인프라에 대 한 정책에 따라 신뢰할 수 있는 합니다. 호스트 계층 소프트웨어 유추 전원 소비를 최소화 하는 동안 처리량을 최대화 하는 방법에 그대로 유지 됩니다. 대부분 유휴 컴퓨터의 물리적 인프라를 보통 power 그리기는 그렇지 않은 경우 있기 보다 더 느리게 실행 되는 개별 테 넌 트 워크 로드에 적합 한 종료 발생할 수 있습니다.

Windows Server는 다양 한 시나리오에서에서 가상화를 사용합니다. 약간 사용 중인 SQL Server에 부하가 IIS 서버에서 Hyper-v를 사용 하 여 클라우드 호스트에 수백 개의 서버별 가상 컴퓨터를 실행 합니다. 이러한 각 시나리오는 고유한 하드웨어, 소프트웨어 및 성능 요구 사항이 있을 수 있습니다. 기본적으로 사용 하 여 Windows Server 및 권장 합니다 **균형** CPU 사용률에 따라 프로세서 성능을 확장 하 여 전원 절약 이나 수 있도록 하는 전원 계획입니다.

사용 하 여 합니다 **균형** 전원 관리 옵션, 최고 전원 상태 (및 테 넌 트 워크 로드에서 가장 낮은 응답 대기 시간) 실제 호스트 비교적 많을 경우에 적용 됩니다. 모든 테 넌 트 워크 로드에 대 한 결정적, 지연율이 낮은 응답을 값을 하는 경우 기본값에서 전환 고려해 야 **부하 분산** 전원 계획을 합니다 **고성능** 전원 계획입니다. 합니다 **고성능** 전원 계획의 프로세서 속도로 실행 전체 항상 다른 전원 관리 기술 함께 전환 요청 기반을 효과적으로 사용 하지 않도록 설정 되며 전력 절감을 통해 성능을 최적화 합니다.

고객의 경우에서 실제 서버의 수를 줄이면 비용 절감에 만족 하 고 가상화 된 워크 로드에 대 한 최대 성능을 달성 하는지 확인 하려면, 사용을 고려해 야 합니다 **고성능** 전원 계획입니다.

추가 권장 사항 및 인프라 최적화를 위한 전원 관리 옵션을 활용 하 여에 대 한 정보를 읽기 [권장 되는 분산 된 전원 계획 매개 변수를 빠른 응답 시간](../../hardware/power/recommended-balanced-plan-parameters.md)



## <a name="server-core-installation-option"></a>Server Core 설치 옵션

Windows Server 2016의 Server Core 설치 옵션을 기능입니다. Server Core는 Hyper-v를 비롯 한 서버 역할의 선택 집합을 호스트 하기 위한 최소 환경을 제공 합니다. 호스트 OS에 대 한 디스크 공간이 더 작은 및 공격을 더 작은 화면 서비스를 제공 합니다. 따라서 Hyper-v 가상화 서버 Server Core 설치 옵션을 사용 하는 것이 좋습니다.

Server Core 설치를 사용자가 로그온 했지만 하이퍼-V 포함 하는 원격 관리 기능을 제공 하는 경우에 콘솔 창이 제공 [Windows Powershell](https://technet.microsoft.com/library/hh848559.aspx) 관리자가 원격으로 관리할 수 있도록 합니다.

## <a name="dedicated-server-role"></a>전용된 서버 역할

루트 파티션에 Hyper-v 전용 전용 여야 합니다. 특히 중요 한 CPU, 메모리 또는 I/O 대역폭을 차지 하는 경우 Hyper-v를 실행 하는 서버에서 추가 서버 역할을 실행 가상화 서버의 성능에 부정적인 발생할 수 있습니다. 루트 파티션에 서버 역할을 최소화 하는 것에 공격 노출 영역 감소와 같은 추가 이점이 있습니다.

시스템 관리자는 일부 소프트웨어의 Hyper-v를 실행 하는 서버 전체 성능이 저하 될 수 있으므로 루트 파티션에 설치 된 소프트웨어 신중 하 게 고려해 야 합니다.

## <a name="guest-operating-systems"></a>게스트 운영 체제

Hyper-v를 지원 하며 여러 게스트 운영 체제의 수에 대 한 조정 되었습니다. 지원 되는 게스트 당 가상 프로세서 수가 게스트 운영 체제에 따라 달라 집니다. 지원 되는 게스트 운영 체제 목록은 참조 하세요 [Hyper-v 개요](https://technet.microsoft.com/library/hh831531.aspx)합니다.

## <a name="cpu-statistics"></a>CPU 통계

Hyper-v는 가상화 서버의 동작 및 리소스 사용량을 보고 하는 데 성능 카운터를 게시 합니다. 성능 모니터 및 Logman.exe를 표시 하 고 Hyper-v 성능 카운터를 기록할 수 있는 표준 Windows에서 성능 카운터를 보기 위한 도구 집합에 포함 됩니다. 관련 된 카운터 개체 이름 접두사가 붙습니다 **Hyper-v**합니다.

항상 Hyper-v 하이퍼바이저 논리 프로세서 성능 카운터를 사용 하 여 실제 시스템의 CPU 사용량을 측정 해야 합니다. CPU 사용률 카운터 루트에서 해당 작업 관리자 및 성능 모니터가 보고 하 고 자식 파티션에 실제 물리적 CPU 사용량을 반영 하지 않습니다. 성능을 모니터링 하는 다음 성능 카운터를 사용 합니다.

- **Hyper-v 하이퍼바이저 논리 프로세서 (\*)\\총 실행 시간 %** 논리적 프로세서의 총 비 유휴 시간

- **Hyper-v 하이퍼바이저 논리 프로세서 (\*)\\게스트 실행 시간 %** 호스트 또는 게스트 내에서 실행 중인 주기는 데 걸린 시간

- **Hyper-v 하이퍼바이저 논리 프로세서 (\*)\\하이퍼바이저 실행 시간 %** 하이퍼바이저 내에서 실행 소요 시간

- **Hyper-v 하이퍼바이저 가상 프로세서 루트 (\*)\\\\** * 루트 파티션의 CPU 사용량 측정

- **Hyper-v 하이퍼바이저 가상 프로세서 (\*)\\\\** * 게스트 파티션의 CPU 사용량 측정


## <a name="see-also"></a>참조

-   [Hyper-V 용어](terminology.md)

-   [Hyper-V 아키텍처](architecture.md)

-   [Hyper-V 프로세서 성능](processor-performance.md)

-   [Hyper-V 메모리 성능](memory-performance.md)

-   [Hyper-V 스토리지 I/O 성능](storage-io-performance.md)

-   [Hyper-V 네트워크 I/O 성능](network-io-performance.md)

-   [가상화된 환경의 병목 상태 탐지](detecting-virtualized-environment-bottlenecks.md)

-   [Linux Virtual Machines](linux-virtual-machine-considerations.md)
