---
title: 스토리지 공간 다이렉트 개요
ms.prod: windows-server
ms.author: cosdar
manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 06/26/2019
ms.assetid: 8bd0d09a-0421-40a4-b752-40ecb5350ffd
description: 내부 저장소를 사용 하는 서버를 소프트웨어 정의 저장소 솔루션으로 클러스터링 할 수 있도록 하는 Windows Server의 기능인 스토리지 공간 다이렉트에 대 한 개요입니다.
ms.localizationpriority: medium
ms.openlocfilehash: f3af42e2dde5b137ab2d49c1385dfa178f224ed8
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474480"
---
# <a name="storage-spaces-direct-overview"></a>스토리지 공간 다이렉트 개요

>적용 대상: Windows Server 2019, Windows Server 2016

스토리지 공간 다이렉트는 로컬 연결 드라이브가 있는 업계 표준 서버를 사용하여, 기존의 SAN 또는 NAS 어레이에 비해 훨씬 저렴한 비용으로 확장성이 뛰어난 고가용성 소프트웨어 정의 스토리지를 만듭니다. 수렴 형 또는 하이퍼 수렴 형 아키텍처는 조달 및 배포를 크게 간소화 하 고, 캐싱, 저장소 계층, 지우기 코딩 등의 기능은 RDMA 네트워킹 및 NVMe 드라이브와 같은 최신 하드웨어 혁신을 제공 하 고,이를 통해 효율성과 성능을 향상 시킵니다.

스토리지 공간 다이렉트는 Windows Server 2019 Datacenter, Windows Server 2016 Datacenter 및 [Windows Server Insider Preview 빌드](https://insider.windows.com/for-business-getting-started-server/)에 포함 되어 있습니다.

공유 SAS 클러스터 및 독립 실행형 서버와 같은 다른 저장소 공간 응용 프로그램의 경우 [저장소 공간 개요](overview.md)를 참조 하세요. Windows 10 PC에서 저장소 공간 사용에 대 한 정보를 찾고 [있는 경우 windows 10의 저장소 공간](https://support.microsoft.com/help/12438/windows-10-storage-spaces)을 참조 하세요.

|       |       |
|   -   |   -   |
| **이해**<br><ul><li>개요 (여기에 표시 됨)</li><li>[캐시 이해](understand-the-cache.md)</li><li>[내결함성 및 스토리지 효율성](storage-spaces-fault-tolerance.md)<li>[드라이브 대칭 고려 사항](drive-symmetry-considerations.md)</li><li>[스토리지 다시 동기화 이해 및 모니터링](understand-storage-resync.md)</li><li>[클러스터 및 풀 쿼럼의 이해](understand-quorum.md)</li><li>[클러스터 세트](cluster-sets.md)</li> | **계획**<br><ul><li>[하드웨어 요구 사항](storage-spaces-direct-hardware-requirements.md)</li><li>[CSV 메모리 내 읽기 캐시 사용](csv-cache.md)</li><li>[드라이브 선택](choosing-drives.md)</li><li>[볼륨 계획](plan-volumes.md)</li><li>[게스트 VM 클러스터 사용](storage-spaces-direct-in-vm.md)</li><li>[재해 복구](storage-spaces-direct-disaster-recovery.md)</li> |
| **배포**<br><ul><li>[스토리지 공간 다이렉트 배포](deploy-storage-spaces-direct.md)</li><li>[볼륨 만들기](create-volumes.md)</li><li>[중첩된 복원력](nested-resiliency.md)</li><li>[쿼럼 구성](../../failover-clustering/manage-cluster-quorum.md)</li><li>[스토리지 공간 다이렉트 클러스터를 Windows Server 2019로 업그레이드](upgrade-storage-spaces-direct-to-windows-server-2019.md)</li><li>[영구 메모리 이해 및 배포](deploy-pmem.md)</li> | **관리**<br><ul><li>[Windows Admin Center를 통해 관리](../../manage/windows-admin-center/use/manage-hyper-converged.md)</li><li>[서버 또는 드라이브 추가](add-nodes.md)</li><li>[유지 관리를 위해 서버를 오프라인으로 전환](maintain-servers.md)</li><li>[서버 제거](remove-servers.md)</li><li>[볼륨 확장](resize-volumes.md)</li><li>[볼륨 삭제](delete-volumes.md)</li><li>[드라이브 펌웨어 업데이트](../update-firmware.md)</li><li>[성능 기록](performance-history.md)</li><li>[볼륨 할당 구분](delimit-volume-allocation.md)</li><li>[하이퍼 수렴 형 클러스터에서 Azure Monitor 사용](configure-azure-monitor.md)</li> |
| **문제 해결**<br><ul><li>[문제 해결 시나리오](troubleshooting-storage-spaces.md)</li><li>[상태 및 작동 상태 문제 해결](storage-spaces-states.md)</li><li>[스토리지 공간 다이렉트를 사용 하 여 진단 데이터 수집](data-collection.md)</li><li>[스토리지 클래스 메모리 상태 관리](Storage-class-memory-health.md)</li> | **최근 블로그 게시물**<br><ul><li>[1370만 IOPS 스토리지 공간 다이렉트: 하이퍼 수렴 형 인프라의 새 산업 레코드](https://blogs.technet.microsoft.com/filecab/2018/10/30/windows-server-2019-and-intel-optane-dc-persistent-memory/)</li><li>[Windows Server 2019의 하이퍼 수렴 형 인프라-카운트다운 클록이 지금 시작 됩니다.](https://blogs.technet.microsoft.com/filecab/2018/10/02/hci-the-countdown-clock-starts-now/)</li><li>[Windows Server Summit의 다섯 가지 큰 공지 사항](https://blogs.technet.microsoft.com/filecab/2018/06/27/windows-server-summit-recap)</li><li>[1만 스토리지 공간 다이렉트 클러스터 및 계산 하는 동안 ...](https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum/)</li> |

## <a name="videos"></a>동영상

**빠른 비디오 개요 (5 분)**

> [!Video https://www.youtube-nocookie.com/embed/raeUiNtMk0E]

**스토리지 공간 다이렉트 Microsoft Ignite 2018 (1 시간)**

> [!Video https://www.youtube-nocookie.com/embed/5kaUiW3qo30]

**스토리지 공간 다이렉트 Microsoft Ignite 2017 (1 시간)**

> [!Video https://www.youtube-nocookie.com/embed/YDr2sqNB-3c]

**Microsoft Ignite 2016 (1 시간)에 시작 이벤트**

> [!Video https://www.youtube-nocookie.com/embed/LK2ViRGbWs]

## <a name="key-benefits"></a>주요 이점

|       |       |
|   -   |   -   |
| ![단순함](media/storage-spaces-direct-in-windows-server-2016/simplicity-icon.png)   | **간소화.** Windows Server 2016을 실행하는 업계 표준 서버에서 첫 번째 스토리지 공간 다이렉트 클러스터로 15분 내에 이동합니다. System Center 사용자의 경우 확인란 하나로 배포됩니다.       |
| ![성능 저하](media/storage-spaces-direct-in-windows-server-2016/performance-icon.png)   | **독보적인 성능을 제공합니다.** 전체 플래시 또는 하이브리드와 상관없이 스토리지 공간 다이렉트는 하이퍼바이저 포함 아키텍처, 기본 제공되는 읽기/쓰기 캐시, PCIe 버스에 직접 탑재된 최첨단 NVMe 드라이브 지원 덕분에 일관되고 짧은 대기 시간과 함께 [서버당 150,000 혼합 4k 임의 IOPS](https://blogs.technet.microsoft.com/filecab/2016/07/26/storage-iops-update-with-storage-spaces-direct/)를 쉽게 초과합니다.      |
| ![내결함성](media/storage-spaces-direct-in-windows-server-2016/fault-tolerance-icon.png)   | **내결함성.** 지속적인 가용성과 함께 기본 제공 복원력이 드라이브, 서버 또는 구성 요소 오류를 처리합니다. 더 큰 규모의 배포에서도 [섀시 및 랙 내결함성](../../failover-clustering/fault-domains.md)을 구성할 수 있습니다. 하드웨어 오류가 발생할 경우 교체하면 됩니다. 소프트웨어는 복잡한 관리 단계 없이 자체적으로 수정됩니다.       |
| ![리소스 효율성](media/storage-spaces-direct-in-windows-server-2016/efficiency-icon.png)   | **리소스 효율성입니다.** 지우기 코딩은 하드 디스크 드라이브 및 혼합 된 핫/콜드 워크 로드에 대 한 이러한 이득을 확장 하기 위해 로컬 재구성 코드 및 ReFS 실시간 계층과 같은 고유한 혁신을 통해 최대 2.4 x 이상의 저장소 효율성을 제공 하며,이를 통해 CPU 사용량을 최소화 하 여 대부분의 Vm이 필요한 위치에 리소스를 다시 제공 합니다.       |
| ![관리 효율](media/storage-spaces-direct-in-windows-server-2016/manageability-icon.png)   | **관리 효율성**. [스토리지 QoS 컨트롤](../storage-qos/storage-qos-overview.md)을 사용하여, 과부하 상태의 VM에서 VM당 최소 및 최대 IOPS 제한을 지속적으로 확인합니다. [상태 관리 서비스](../../failover-clustering/health-service-overview.md)는 기본 제공 연속 모니터링 및 경고를 제공하며, 새로운 API를 사용하면 클러스터 전체의 풍부한 성능 및 용량 메트릭을 수집할 수 있습니다.      |
| ![확장성](media/storage-spaces-direct-in-windows-server-2016/scalability-icon.png)   | **확장성**. 클러스터 당 최대 1 페타바이트 (1000 테라바이트)의 저장소에 대해 최대 16 개의 서버 및 400 드라이브로 이동 합니다. 규모를 확장하려면 드라이브와 서버를 추가하기만 하면 됩니다. 스토리지 공간 다이렉트가 자동으로 새 드라이브를 인식하여 사용하기 시작합니다. 규모에 따라 스토리지 효율성과 성능이 예측 가능한 방식으로 개선됩니다.       |

## <a name="deployment-options"></a>배포 옵션

스토리지 공간 다이렉트는 두 가지 배포 옵션을 제공하도록 설계되었습니다.

### <a name="converged"></a>수렴됨

**별도의 클러스터에서 저장소 및 계산.** ' Disaggregated '이 라고도 하는 수렴 형 배포 옵션인 SoFS (스케일 아웃 파일 서버 스토리지 공간 다이렉트) 계층은 SMB3 파일 공유를 통해 네트워크에 연결 된 저장소를 제공 합니다. 이렇게 하면 스토리지 클러스터와 독립적으로 컴퓨팅/워크로드를 확장할 수 있습니다. 이러한 확장은 서비스 공급자 및 엔터프라이즈에 대한 Hyper-V IaaS(Infrastructure as a Service)와 같은 대규모 배포에 필요합니다.

![스토리지 공간 다이렉트는 다른 서버 또는 클러스터의 Hyper-v Vm에 스케일 아웃 파일 서버 기능을 사용 하 여 저장소를 제공 합니다.](media/storage-spaces-direct-in-windows-server-2016/converged-minimal.png)

### <a name="hyper-converged"></a>하이퍼 수렴 형

**계산 및 저장소에 대 한 하나의 클러스터.** 하이퍼 수렴형 배포 옵션은 서버에서 직접 Hyper-V 가상 컴퓨터 또는 SQL Server 데이터베이스를 실행하여 스토리지를 제공하고 로컬 볼륨에 파일을 저장합니다. 따라서 파일 서버 액세스 및 사용 권한을 구성할 필요가 없으며, 중소기업 또는 원격 사무소/지사 배포에 필요한 하드웨어 비용이 절감됩니다. [스토리지 공간 다이렉트 배포](deploy-storage-spaces-direct.md)를 참조 하세요.

![스토리지 공간 다이렉트는 동일한 클러스터의 Hyper-v Vm에 저장소를 제공 합니다.](media/storage-spaces-direct-in-windows-server-2016/hyper-converged-minimal.png)

## <a name="how-it-works"></a>작동 방법

스토리지 공간 다이렉트는 Windows Server 2012에서 처음 도입된 스토리지 공간이 개선된 것으로, 장애 조치(failover) 클러스터링, CSV(클러스터 공유 볼륨) 파일 시스템, SMB(서버 메시지 블록) 3, 스토리지 공간을 비롯하여 오늘날 Windows Server에서 알려진 많은 기능을 활용합니다. 또한 가장 주목할 만한 새로운 기술인 소프트웨어 스토리지 버스도 활용합니다.

스토리지 공간 다이렉트 스택의 개요는 다음과 같습니다.

![스토리지 공간 다이렉트 스택](media/storage-spaces-direct-in-windows-server-2016/converged-full-stack.png)

**네트워킹 하드웨어.** 스토리지 공간 다이렉트는 SMB 다이렉트 및 SMB 다중 채널을 비롯한 SMB3을 사용하여 이더넷을 통해 서버 간에 통신합니다. iWARP 또는 RoCE 중 하나로 RDMA(원격 직접 메모리 액세스)와 함께 10+ GbE를 사용하는 것이 좋습니다.

**저장소 하드웨어.** 로컬 연결 SATA, SAS 또는 NVMe 드라이브와 함께 2~16대 서버. 각 서버에는 2개 이상의 반도체 드라이브 및 4개 이상의 추가 드라이브가 있어야 합니다. SATA 및 SAS 디바이스는 HBA(호스트 버스 어댑터) 및 SAS 확장기 뒤에 있어야 합니다. 신중하게 엔지니어링되고 광범위하게 검증된 파트너의 플랫폼을 사용하는 것이 좋습니다(출시 예정).

**장애 조치 (Failover) 클러스터링.** Windows Server의 기본 제공 클러스터링 기능이 서버를 연결하는 데 사용됩니다.

**소프트웨어 저장소 버스.** 소프트웨어 스토리지 버스는 스토리지 공간 다이렉트의 새로운 기능으로, 클러스터를 확장 하 고 모든 서버가 서로의 로컬 드라이브를 모두 볼 수 있는 소프트웨어 정의 저장소 패브릭을 설정 합니다. 값비싸고 제한적인 파이버 채널 또는 공유 SAS 케이블링을 교체하는 것이라고 생각할 수 있습니다.

**스토리지 버스 계층 캐시.** 소프트웨어 스토리지 버스는 가장 빠른 드라이브(예: SSD)를 더 느린 드라이브(예: HDD)에 바인딩하여, IO를 가속화하고 처리량을 높이는 서버 쪽 읽기/쓰기 캐싱을 제공합니다.

**저장소 풀.** 저장소 공간의 기반을 형성 하는 드라이브의 컬렉션을 저장소 풀 이라고 합니다. 저장소 풀은 자동으로 생성되며, 모든 적격 드라이브는 자동으로 검색되어 풀에 추가됩니다. 기본 설정과 함께 클러스터당 하나의 풀을 사용하는 것이 좋습니다. 자세한 내용은 [저장소 풀에](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/) 대 한 심층 조사를 참조 하세요.

**저장소 공간.** 저장소 공간은 [미러링, 지우기 코딩 또는 둘 다](storage-spaces-fault-tolerance.md)를 사용 하는 가상 "디스크"에 내결함성을 제공 합니다. 저장소 공간을 풀의 드라이브를 사용하는 분산된 소프트웨어 정의 RAID라고 생각할 수 있습니다. 섀시 및 랙 내결함성도 사용 가능하지만, 스토리지 공간 다이렉트에서 이러한 가상 디스크는 일반적으로 두 개의 동시 드라이브 또는 서버 장애에 대한 복원력을 가지고 있습니다(예: 서로 다른 서버에 각 데이터 복사본이 있는 3방향 미러링).

**ReFS (복원 파일 시스템).** ReFS는 가상화를 위해 구축된 뛰어난 파일 시스템으로, 비트 오류를 검색하고 수정하기 위한 만들기, 확장, 검사점 병합, 기본 제공 체크섬 등 .vhdx 파일 작업에 뛰어난 가속을 제공합니다. 또한 사용량에 따라 실시간으로 "핫" 및 "콜드" 저장소 계층 간에 데이터를 회전 하는 실시간 계층이 도입 되었습니다.

**클러스터 공유 볼륨.** CSV 파일 시스템은 모든 ReFS 볼륨을 서버에서 액세스할 수 있는 단일 네임 스페이스로 통합 하므로 각 서버에서 모든 볼륨이 로컬로 탑재 된 것 처럼 보이고 작동 합니다.

**스케일 아웃 파일 서버.** 이 마지막 계층은 수렴형 배포에만 필요합니다. SOFS는 네트워크를 통해 SMB3 액세스 프로토콜을 사용하는 원격 파일 액세스를 클라이언트(예: Hyper-V를 실행하는 또 다른 클러스터)에 제공하여, 스토리지 공간 다이렉트를 NAS(네트워크 연결 스토리지)로 효과적으로 전환합니다.

## <a name="customer-stories"></a>고객 사례

전 세계적으로 스토리지 공간 다이렉트를 실행 하는 [1만 클러스터가](https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum/) 있습니다. 두 개의 노드를 배포 하는 중소기업에서 수백 개의 노드를 배포 하는 중소기업에 이르기까지 모든 규모의 조직은 중요 한 응용 프로그램 및 인프라에 대 한 스토리지 공간 다이렉트에 따라 달라 집니다.

[Microsoft.com/HCI](https://www.microsoft.com/hci) 을 방문 하 여 해당 스토리를 읽어 보세요.

[![고객 로고 그리드](media/storage-spaces-direct-in-windows-server-2016/customer-stories.png)](https://www.microsoft.com/hci)

## <a name="management-tools"></a>관리 도구

다음 도구를 사용 하 여 스토리지 공간 다이렉트를 관리 및/또는 모니터링할 수 있습니다.

| 이름 | 그래픽 또는 명령줄 인가요? | 유료 또는 포함 됩니까? |
|-----------------|----------------------------|-------------------|
| [Windows Admin Center](../../manage/windows-admin-center/overview.md)     | 그래픽    | 포함 |
| 서버 관리자 & 장애 조치(Failover) 클러스터 관리자                                 | 그래픽    | 포함 |
| Windows PowerShell                                                        | 명령줄 | 포함 |
| [System Center Virtual Machine Manager (SCVMM)](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-storage-spaces-direct-vmm) <br>& [Operations Manager (SCOM)](https://www.microsoft.com/download/details.aspx?id=54700) | 그래픽    | 지급     |

## <a name="get-started"></a>시작하기

[Microsoft Azure에서](https://blogs.technet.microsoft.com/filecab/2016/05/05/s2dazuretp5/)스토리지 공간 다이렉트을 시도 하거나 [windows Server 평가판](https://go.microsoft.com/fwlink/?linkid=842602)에서 windows server의 180 일 라이선스 평가판 사본을 다운로드 합니다.

## <a name="additional-references"></a>추가 참조

- [내결함성 및 스토리지 효율성](storage-spaces-fault-tolerance.md)
- [스토리지 복제본](../storage-replica/storage-replica-overview.md)
- [Microsoft 블로그의 저장소](https://blogs.technet.microsoft.com/filecab/)
- [IWARP를 사용 하 여 스토리지 공간 다이렉트 처리량](https://blogs.technet.microsoft.com/filecab/2017/03/13/storage-spaces-direct-throughput-with-iwarp) (TechNet 블로그)
- [Windows Server 장애 조치(failover) 클러스터링의 새로운 기능](../../failover-clustering/whats-new-in-failover-clustering.md)
- [스토리지 서비스 품질](../storage-qos/storage-qos-overview.md)
- [Windows IT 전문가 지원](https://www.microsoft.com/itpro/windows/support)
