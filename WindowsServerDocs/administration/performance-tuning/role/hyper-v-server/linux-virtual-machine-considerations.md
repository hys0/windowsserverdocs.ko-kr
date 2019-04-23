---
title: Linux 가상 머신 고려 사항
description: Linux 및 BSD 가상 머신
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: cc6aab7825754579269eb05e591ca2a3cf5a561b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869684"
---
# <a name="linux-virtual-machine-considerations"></a>Linux 가상 머신 고려 사항

Linux 및 BSD virtual machines에는 Hyper-v에서 Windows 가상 머신에 비해 하는 추가 고려 사항이 있습니다.

첫 번째 고려 Integration Services 있는지 여부를 인지 하지 계몽을 사용 하 여 에뮬레이트된 하드웨어에서 단순히 VM이 실행 하는 경우. 기본 제공 또는 다운로드할 수 있는 Integration Services가 있는 Linux 및 BSD 버전의 테이블은 영어로 [Windows의 Hyper-v에 대 한 지원 되는 Linux 및 FreeBSD 가상 컴퓨터](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows)합니다. 이러한 페이지에 해당 하는 경우 Linux 배포 릴리스 및 이러한 기능에 대 한 정보를 사용할 수 있는 Hyper-v 기능 표입니다.

게스트 통합 서비스가 실행 중일 때에 최상의 성능을 나타내지 않습니다 레거시 하드웨어를 사용 하 여 구성할 수 있습니다. 예를 들어, 구성 및 레거시 네트워크 어댑터를 사용 하는 대신 게스트에 가상 이더넷 어댑터를 사용 합니다. Windows Server 2016을 사용 하 여 고급 네트워킹 같은 SR-IOV도 사용할 수 있습니다.

## <a name="linux-network-performance"></a>Linux 네트워크 성능

기본적으로 Linux 하드웨어 가속을 사용 하도록 설정 하 고 기본적으로 오프 로드 합니다. VRSS는 호스트에서 NIC의 속성에서 사용할 수 있고 Linux 게스트 vRSS를 사용 하는 기능에는 기능을 사용할 수 있습니다. Powershell에서이 동일한 매개 변수를 변경할 수는 `EnableNetAdapterRSS` 명령입니다.

마찬가지로, 게스트 사용 된 실제 NIC에 VMMQ (가상 스위치 RSS) 기능을 사용할 수 있습니다 **속성** > **구성 하는 중...**   >  **고급** 탭 > 설정 **가상 스위치 RSS** 에 **Enabled** 또는 다음을 사용 하 여 Powershell에서 VMMQ 사용:

```PowerShell
 Set-VMNetworkAdapter -VMName **$VMName** -VmmqEnabled $True
 ```

게스트에서 추가 TCP 조정을 수행할 수 있습니다 제한을 늘려. 최상의 성능을 위해 워크 로드를 여러 Cpu를 분산 하 고 전체 워크 로드는 최상의 처리량을 생성 가상화 된 워크 로드의 대기 시간이 길어집니다 "베어 메탈" 보다 것입니다.

네트워크 벤치 마크에서 유용한 몇 가지 예제 튜닝 매개 변수는 다음과 같습니다.

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

네트워크 microbenchmarks에 대 한 유용한은 ntttcp를 Linux 및 Windows 모두에서 사용할 수 있습니다. Linux 버전은 오픈 소스에서 사용할 수 있습니다 [github.com에서 linux에 대 한 ntttcp](https://github.com/Microsoft/ntttcp-for-linux)합니다. Windows 버전에서 찾을 수 있습니다 합니다 [다운로드 센터](https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769)합니다. 작업을 튜닝 하는 경우 필요에 따라 최상의 처리량을 가져오려는 만큼 스트림을 사용 하는 것이 적합 합니다. 모델 트래픽에 ntttcp를 사용 하 여는 `-P` 매개 변수가 사용 되는 병렬 연결 수를 설정 합니다.

## <a name="linux-storage-performance"></a>Linux 저장소 성능

다음과 같은 몇 가지 모범 사례에 나열 됩니다 [Hyper-v의 Linux를 실행에 대 한 모범 사례](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/best-practices-for-running-linux-on-hyper-v)합니다. Linux 커널에는 다양 한 알고리즘을 사용 하 여 요청을 다시 정렬 하려면 다른 I/O 스케줄러입니다. NOOP는 하이퍼바이저 수행 하기 위해 일정 의사 결정을 전달 하는 선입 선출 방식입니다. Hyper-v의 Linux 가상 컴퓨터를 실행 하는 경우 NOOP 스케줄러로 사용 하는 것이 좋습니다. 부팅 로더가 구성에서 특정 장치에 대 한 스케줄러를 변경 하려면 (/ 예를 들어 grub.conf), 추가 `elevator=noop` 커널 매개 변수를 다음 다시 시작 합니다.

네트워킹와 마찬가지로 Linux 게스트 성능 저장소를 사용 하 여 사용 중인 호스트를 유지 하려면 충분 한 깊이 사용 하 여 여러 큐에서 가장 이점을 제공 합니다. Microbenchmarking 저장소 성능은 libaio 엔진과 fio 벤치 마크 도구를 사용 하 여 것이 가장 좋습니다.

## <a name="see-also"></a>참조

-   [Hyper-v 용어](terminology.md)

-   [Hyper-v 아키텍처](architecture.md)

-   [Hyper-v 서버-구성](configuration.md)

-   [Hyper-v 프로세서 성능](processor-performance.md)

-   [Hyper-v 메모리 성능](memory-performance.md)

-   [Hyper-v 저장소 I/O 성능](storage-io-performance.md)

-   [Hyper-v 네트워크 I/O 성능](network-io-performance.md)

-   [가상화 된 환경에서 병목 상태를 검색합니다.](detecting-virtualized-environment-bottlenecks.md)
