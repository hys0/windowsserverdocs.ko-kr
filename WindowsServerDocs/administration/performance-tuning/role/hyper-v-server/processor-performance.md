---
title: 하이퍼-V 프로세서 성능
description: Hyper-v 성능 튜닝에 프로세서 성능 고려 사항
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 2a49fdaba89a01c8daf6483f72dbc88daa91452b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843244"
---
# <a name="hyper-v-processor-performance"></a>하이퍼-V 프로세서 성능


## <a name="virtual-machine-integration-services"></a>가상 컴퓨터 통합 서비스

가상 컴퓨터 통합 서비스는 크게 i/o 에뮬레이트된 장치에 비해 CPU 오버 헤드 감소는 I/O 하이퍼-V-특정 장치에 대해 지원된 드라이버를 포함 합니다. 모든 지원 되는 가상 컴퓨터에서 가상 컴퓨터 통합 서비스의 최신 버전을 설치 해야 합니다. 유휴 상태에서 게스트의 CPU 사용량을 크게 게스트 서비스 감소 게스트를 사용 하 고 I/O 처리량을 향상 시킵니다. Hyper-v를 실행 하는 서버 성능 튜닝의 첫 번째 단계입니다. 지원 되는 게스트 운영 체제 목록은 참조 하세요 [Hyper-v 개요](https://technet.microsoft.com/library/hh831531.aspx)합니다.

## <a name="virtual-processors"></a>가상 프로세서

Windows Server 2016의 Hyper-v 가상 머신 당 240 가상 프로세서의 최대를 지원합니다. CPU를 많이 사용 되지 않는 로드를 가진 가상 컴퓨터는 한 개의 가상 프로세서를 사용 하도록 구성 되어야 합니다. 게스트 운영 체제에서 추가로 동기화 비용 등의 여러 가상 프로세서를 사용 하 여 연결 된 추가 오버 헤드 때문입니다.

가상 컴퓨터의 최대 부하 처리 둘 이상의 CPU를 요구 하는 경우에 가상 프로세서의 수를 늘립니다.

## <a name="background-activity"></a>백그라운드 작업

다른 가상 컴퓨터에서 다른 곳에서 사용할 수 있는 CPU 주기를 해제 유휴 가상 컴퓨터에서 백그라운드 작업을 최소화 합니다. Windows 게스트는 일반적으로 유휴 상태일 때 한 CPU의 1% 미만 사용 합니다. 다음은 백그라운드 가상 컴퓨터의 CPU 사용량을 최소화 하기 위한 몇 가지 모범 사례입니다.

-   가상 컴퓨터 통합 서비스의 최신 버전을 설치 합니다.

-   가상 머신 설정 대화 상자 (사용 하 여 Microsoft 하이퍼-V-특정 어댑터)를 통해 에뮬레이트된 네트워크 어댑터를 제거 합니다.

-   예: CD-ROM 및 COM 포트를 사용 하지 않는 장치를 제거 하거나 해당 미디어를 분리 합니다.

-   사용 하지 않으면 로그인 화면에서 Windows 게스트 운영 체제를 유지 하 고 화면 보호기를 사용 하지 않도록 설정 합니다.

-   예약 된 작업은 기본적으로 사용할 수 있는 서비스를 검토 합니다.

-   에 있는 기본적으로 실행 하 여 ETW 추적 공급자 검토 **logman.exe-ets 쿼리**

-   정기적인 작업 (예: 타이머)를 줄이기 위해 서버 응용 프로그램을 개선 합니다.

-   호스트 및 게스트 운영 체제에서 서버 관리자를 닫습니다.

-   Hyper-v 관리자를 실행 가상 컴퓨터의 축소판 그림을 지속적으로 새로 고치기 때문 둬서는 안 됩니다.

다음은 구성에 대 한 추가 모범 사례를 *클라이언트 버전* 전체 CPU 사용량을 줄이기 위해 가상 컴퓨터에서 Windows의:

-   SuperFetch 등 Windows Search 백그라운드 서비스를 사용 하지 않도록 설정 합니다.

-   예약 된 조각 모음 등의 예약 된 작업을 사용 하지 않도록 설정 합니다.

## <a name="virtual-numa"></a>가상 NUMA

대규모 스케일 업 워크 로드를 가상화를 사용 하려면 Windows Server 2016의 Hyper-v 가상 머신 규모 제한을 확장 합니다. 최대 240 개의 가상 프로세서와 12TB의 메모리를 단일 가상 컴퓨터를 할당할 수 있습니다. 이러한 큰 가상 컴퓨터를 만들 때 호스트 시스템에서 여러 NUMA 노드의 메모리를에서 사용 될 가능성이 높습니다. 이러한 가상 컴퓨터 구성, 가상 프로세서와 메모리가 동일한 NUMA 노드에서 할당 되지 않습니다 하는 경우 워크 로드에 NUMA 최적화를 활용할 수 없기 때문에 잘못 된 성능을 수 있습니다.

Windows Server 2016에서 Hyper-v 가상 컴퓨터에 가상 NUMA 토폴로지를 표시합니다. 기본적으로 이 가상 NUMA 토폴로지는 기본 호스트 컴퓨터의 NUMA 토폴로지와 일치하도록 최적화됩니다. 가상 NUMA 토폴로지를 가상 컴퓨터에 노출하면 게스트 운영 체제와 이 운영 체제 내에서 실행되는 모든 NUMA 인식 응용 프로그램이 실제 컴퓨터에서 실행될 때와 마찬가지로 NUMA 성능 최적화를 활용할 수 있습니다.

워크로드의 관점에서는 가상 NUMA와 실제 NUMA가 구별되지 않습니다. 가상 컴퓨터 내에서 워크로드가 데이터에 로컬 메모리를 할당하고 동일한 NUMA 노드에서 해당 데이터에 액세스할 경우 기본 실제 시스템에서 신속한 로컬 메모리 액세스가 발생합니다. 원격 메모리 액세스로 인해 성능 저하가 방지됩니다. VNUMA의 NUMA 인식 응용 프로그램에만 이용할 수 있습니다.

Microsoft SQL Server는 NUMA 인식 응용 프로그램의 예입니다. 자세한 내용은 참조 하세요. [4d565d225f3c">understanding non-uniform Memory Access](https://technet.microsoft.com/library/ms178144.aspx)합니다.

가상 NUMA와 동적 메모리 기능은 동시에 사용할 수 없습니다. 동적 메모리가 설정된 가상 컴퓨터는 가상 NUMA 노드를 하나만 포함할 수 있으며, 가상 NUMA 설정에 관계없이 가상 컴퓨터에 NUMA 토폴로지가 제공되지 않습니다.

가상 NUMA에 대 한 자세한 내용은 참조 하세요. [Hyper-v 가상 NUMA 개요](https://technet.microsoft.com/library/dn282282.aspx)합니다.

##<a name="see-also"></a>참조

-   [Hyper-v 용어](terminology.md)

-   [Hyper-v 아키텍처](architecture.md)

-   [Hyper-v 서버-구성](configuration.md)

-   [Hyper-v 메모리 성능](memory-performance.md)

-   [Hyper-v 저장소 I/O 성능](storage-io-performance.md)

-   [Hyper-v 네트워크 I/O 성능](network-io-performance.md)

-   [가상화 된 환경에서 병목 상태를 검색합니다.](detecting-virtualized-environment-bottlenecks.md)

-   [Linux Virtual Machines](linux-virtual-machine-considerations.md)
