---
title: Linux 가상 머신 고려 사항
description: Linux 및 BSD 가상 컴퓨터
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: asmahi; sandysp; jopoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 1109eb50bbe052b39fe7a91903fa0aea58b6e4f1
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471388"
---
# <a name="linux-virtual-machine-considerations"></a>Linux 가상 머신 고려 사항

Linux 및 BSD 가상 컴퓨터에는 Hyper-v의 Windows 가상 컴퓨터와 비교 하 여 추가 고려 사항이 있습니다.

첫 번째 고려 사항은 Integration Services 있는지 또는 VM이 계몽이 없는 에뮬레이트된 하드웨어 에서만 실행 되 고 있는지 여부입니다. [Windows의 hyper-v에 대 한 지원 되는 linux 및 FreeBSD 가상 머신에서 지원](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows)되는 기본 제공 또는 다운로드 가능 Integration Services 있는 LINUX 및 BSD 릴리스 표 이러한 페이지에는 Linux 배포 릴리스에 제공 되는 사용 가능한 Hyper-v 기능의 표 및 해당 하는 경우 해당 기능에 대 한 설명이 있습니다.

게스트가 Integration Services 실행 되는 경우에도 최상의 성능을 보이는 레거시 하드웨어로 구성할 수 있습니다. 예를 들어 레거시 네트워크 어댑터를 사용 하는 대신 게스트에 대 한 가상 이더넷 어댑터를 구성 하 고 사용 합니다. Windows Server 2016를 사용 하 여 SR-IOV와 같은 고급 네트워킹도 사용할 수 있습니다.

## <a name="linux-network-performance"></a>Linux 네트워크 성능

기본적으로 Linux는 하드웨어 가속 및 오프 로드를 기본적으로 사용 하도록 설정 합니다. 호스트의 NIC 속성에서 vRSS를 사용 하도록 설정 하 고 Linux 게스트에 vRSS를 사용 하는 기능이 있는 경우 기능을 사용할 수 있습니다. Powershell에서 명령을 사용 하 여 동일한 매개 변수를 변경할 수 있습니다 `EnableNetAdapterRSS` .

마찬가지로, 게스트 **속성**  >  **구성 ...**  >  에서 사용 되는 실제 NIC에서 VMMQ (가상 스위치 RSS) 기능을 사용 하도록 설정할 수 있습니다. **고급** 탭 > 다음을 사용 하 여 **가상 스위치 RSS** 를 **사용** 으로 설정 하거나 Powershell에서 VMMQ를 사용 하도록 설정 합니다.

```PowerShell
 Set-VMNetworkAdapter -VMName **$VMName** -VmmqEnabled $True
 ```

게스트에서 추가 TCP 튜닝은 제한 값을 높여 수행할 수 있습니다. 가상화 된 워크 로드는 "운영 체제 미 설치" 보다 대기 시간이 더 높기 때문에 여러 Cpu에 대 한 최상의 성능을 극대화 하 고 심층 워크 로드를 통해 최상의 처리량을 얻을 수 있습니다.

네트워크 벤치 마크에 유용한 몇 가지 예의 튜닝 매개 변수는 다음과 같습니다.

```PowerShell
net.core.netdev_max_backlog = 30000
net.core.rmem_max = 67108864
net.core.wmem_max = 67108864
net.ipv4.tcp_wmem = 4096 12582912 33554432
net.ipv4.tcp_rmem = 4096 12582912 33554432
net.ipv4.tcp_max_syn_backlog = 80960
net.ipv4.tcp_slow_start_after_idle = 0
net.ipv4.tcp_tw_reuse = 1
net.ipv4.ip_local_port_range = 10240 65535
net.ipv4.tcp_abort_on_overflow = 1
```

네트워크 마이크로 벤치 마크에 유용한 도구는 Linux 및 Windows 모두에서 사용할 수 있는 ntttcp입니다. Linux 버전은 오픈 소스 이며 [github.com의 ntttcp-linux](https://github.com/Microsoft/ntttcp-for-linux)에서 사용할 수 있습니다. Windows 버전은 [다운로드 센터](https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769)에서 찾을 수 있습니다. 작업을 튜닝 하는 경우 최적의 처리량을 얻기 위해 필요한 만큼의 스트림을 사용 하는 것이 가장 좋습니다. Ntttcp를 사용 하 여 트래픽을 모델링 하는 경우 `-P` 매개 변수는 사용 되는 병렬 연결 수를 설정 합니다.

## <a name="linux-storage-performance"></a>Linux 저장소 성능

[Hyper-v에서 Linux를 실행 하기 위한 모범 사례](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/best-practices-for-running-linux-on-hyper-v)에는 다음과 같은 몇 가지 모범 사례가 나와 있습니다. Linux 커널에는 서로 다른 알고리즘을 사용 하 여 요청을 다시 정렬 하는 서로 다른 i/o 스케줄러가 있습니다. NOOP는 하이퍼바이저 수행 하기 위해 일정 의사 결정을 전달 하는 선입 선출 방식입니다. Hyper-v의 Linux 가상 머신을 실행하는 경우 NOOP 스케줄러로 사용하는 것이 좋습니다. 특정 장치의 스케줄러를 변경 하려면 부팅 로더에서 구성 (예:/etc/grub.conf)에서 커널 매개 변수에를 추가 하 고를 `elevator=noop` 다시 시작 합니다.

네트워킹의 경우와 유사 하 게 저장소를 사용 하는 Linux 게스트 성능에는 호스트를 계속 사용 하는 데 충분 한 깊이가 있는 여러 큐의 이점이 있습니다. Libaio 엔진을 사용 하는 fio 벤치 마크 도구를 사용 하면 마이크로 벤치마킹 저장소 성능이 가장 적합할 수 있습니다.

## <a name="additional-references"></a>추가 참조

-   [Hyper-V 용어](terminology.md)

-   [Hyper-V 아키텍처](architecture.md)

-   [Hyper-V 서버 구성](configuration.md)

-   [Hyper-V 프로세서 성능](processor-performance.md)

-   [Hyper-V 메모리 성능](memory-performance.md)

-   [Hyper-V 스토리지 I/O 성능](storage-io-performance.md)

-   [Hyper-V 네트워크 I/O 성능](network-io-performance.md)

-   [가상화된 환경의 병목 상태 탐지](detecting-virtualized-environment-bottlenecks.md)
