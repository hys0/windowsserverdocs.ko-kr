---
title: Hyper-v 프로세서 성능
description: Hyper-v 성능 조정의 프로세서 성능 고려 사항
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: asmahi; sandysp; jopoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: fc1d6bdb848ea9662ba9b3d3119f286af3476688
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851756"
---
# <a name="hyper-v-processor-performance"></a>Hyper-v 프로세서 성능


## <a name="virtual-machine-integration-services"></a>가상 컴퓨터 통합 서비스

가상 컴퓨터 Integration Services에는 Hyper-v 관련 i/o 장치용 지원 드라이버가 포함 되어 있어 에뮬레이트된 장치에 비해 i/o의 CPU 오버 헤드가 크게 감소 합니다. 지원 되는 모든 가상 컴퓨터에 Integration Services 최신 버전의 가상 컴퓨터를 설치 해야 합니다. 서비스는 유휴 게스트에서 자주 사용 하는 게스트에 대 한 게스트의 CPU 사용량을 줄이고 i/o 처리량을 향상 시킵니다. Hyper-v를 실행 하는 서버의 성능 튜닝에 대 한 첫 번째 단계입니다. 지원 되는 게스트 운영 체제 목록은 [Hyper-v 개요](https://technet.microsoft.com/library/hh831531.aspx)를 참조 하세요.

## <a name="virtual-processors"></a>가상 프로세서

Windows Server 2016의 hyper-v는 가상 컴퓨터당 최대 240 개의 가상 프로세서를 지원 합니다. CPU를 많이 사용 하지 않는 부하가 있는 가상 머신은 하나의 가상 프로세서를 사용 하도록 구성 해야 합니다. 이는 게스트 운영 체제의 추가 동기화 비용과 같이 여러 가상 프로세서와 관련 된 추가 오버 헤드로 인해 발생 합니다.

최대 부하 상태에서 가상 컴퓨터의 처리 CPU가 둘 이상 필요한 경우 가상 프로세서의 수를 늘립니다.

## <a name="background-activity"></a>백그라운드 작업

유휴 가상 컴퓨터의 백그라운드 작업 최소화는 다른 가상 컴퓨터의 다른 곳에서 사용할 수 있는 CPU 주기를 해제 합니다. 일반적으로 Windows 게스트는 유휴 상태일 때 하나의 CPU를 1% 미만으로 사용 합니다. 다음은 가상 컴퓨터의 백그라운드 CPU 사용량을 최소화 하기 위한 몇 가지 모범 사례입니다.

-   Integration Services 가상 컴퓨터의 최신 버전을 설치 합니다.

-   가상 컴퓨터 설정 대화 상자 (Microsoft Hyper-V 관련 어댑터 사용)를 통해 에뮬레이트된 네트워크 어댑터를 제거 합니다.

-   CD-ROM 및 COM 포트와 같은 사용 하지 않는 장치를 제거 하거나 해당 미디어의 연결을 끊습니다.

-   Windows 게스트 운영 체제를 사용 하지 않는 경우 로그인 화면에 유지 하 고 화면 보호기를 사용 하지 않도록 설정 합니다.

-   기본적으로 사용 하도록 설정 된 예약 된 작업 및 서비스를 검토 합니다.

-   **Logman 쿼리** 를 실행 하 여 기본적으로 설정 된 ETW 추적 공급자를 검토 합니다.

-   정기 작업 (예: 타이머)을 줄이기 위해 서버 응용 프로그램을 개선 합니다.

-   호스트 및 게스트 운영 체제에서 서버 관리자를 닫습니다.

-   Hyper-v 관리자는 계속 해 서 가상 컴퓨터의 미리 보기를 새로 고치 므로 실행 하지 마세요.

다음은 전체 CPU 사용량을 줄이기 위해 가상 머신에서 Windows *클라이언트 버전* 을 구성 하기 위한 추가 모범 사례입니다.

-   SuperFetch 및 Windows Search와 같은 백그라운드 서비스를 사용 하지 않도록 설정 합니다.

-   예약 된 조각 모음과 같은 예약 된 작업을 사용 하지 않도록 설정 합니다.

## <a name="virtual-numa"></a>가상 NUMA

대규모 확장 워크 로드 가상화를 사용 하도록 설정 하기 위해 Windows Server 2016의 Hyper-v는 가상 머신 확장 제한을 확장 했습니다. 단일 가상 머신에 최대 240 개의 가상 프로세서와 12tb의 메모리를 할당할 수 있습니다. 이러한 큰 가상 컴퓨터를 만들 때 호스트 시스템의 여러 NUMA 노드에 있는 메모리가 사용 될 가능성이 높습니다. 이러한 가상 컴퓨터 구성에서 가상 프로세서와 메모리가 동일한 NUMA 노드에서 할당 되지 않은 경우 NUMA 최적화를 활용할 수 없어 워크 로드의 성능이 저하 될 수 있습니다.

Windows Server 2016에서 Hyper-v는 가상 컴퓨터에 가상 NUMA 토폴로지를 제공 합니다. 기본적으로 이 가상 NUMA 토폴로지는 기본 호스트 컴퓨터의 NUMA 토폴로지와 일치하도록 최적화됩니다. 가상 NUMA 토폴로지를 가상 컴퓨터에 노출하면 게스트 운영 체제와 이 운영 체제 내에서 실행되는 모든 NUMA 인식 애플리케이션이 실제 컴퓨터에서 실행될 때와 마찬가지로 NUMA 성능 최적화를 활용할 수 있습니다.

워크 로드의 관점에서 가상 및 실제 NUMA는 차이가 없습니다. 가상 컴퓨터 내에서 워크로드가 데이터에 로컬 메모리를 할당하고 동일한 NUMA 노드에서 해당 데이터에 액세스할 경우 기본 실제 시스템에서 신속한 로컬 메모리 액세스가 발생합니다. 원격 메모리 액세스로 인해 성능 저하가 방지됩니다. NUMA 인식 응용 프로그램만 vNUMA를 활용할 수 있습니다.

Microsoft SQL Server은 NUMA 인식 응용 프로그램의 예입니다. 자세한 내용은 [균일 하지 않은 메모리 액세스 이해](https://technet.microsoft.com/library/ms178144.aspx)를 참조 하세요.

가상 NUMA와 동적 메모리 기능은 동시에 사용할 수 없습니다. 동적 메모리가 설정된 가상 컴퓨터는 가상 NUMA 노드를 하나만 포함할 수 있으며, 가상 NUMA 설정에 관계없이 가상 컴퓨터에 NUMA 토폴로지가 제공되지 않습니다.

가상 NUMA에 대 한 자세한 내용은 [Hyper-v 가상 Numa 개요](https://technet.microsoft.com/library/dn282282.aspx)를 참조 하세요.

## <a name="see-also"></a>참고 항목

-   [Hyper-V 용어](terminology.md)

-   [Hyper-V 아키텍처](architecture.md)

-   [Hyper-V 서버 구성](configuration.md)

-   [Hyper-V 메모리 성능](memory-performance.md)

-   [Hyper-V 스토리지 I/O 성능](storage-io-performance.md)

-   [Hyper-V 네트워크 I/O 성능](network-io-performance.md)

-   [가상화된 환경의 병목 상태 탐지](detecting-virtualized-environment-bottlenecks.md)

-   [Linux Virtual Machines](linux-virtual-machine-considerations.md)
