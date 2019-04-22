---
title: 저장소 공간 다이렉트 개요
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 03/06/2019
ms.assetid: 8bd0d09a-0421-40a4-b752-40ecb5350ffd
description: 저장소 공간 다이렉트를 사용 하면 내부 저장소를 사용 하 여 클러스터 서버에는 소프트웨어 정의 저장소 솔루션에는 Windows Server의 기능 개요.
ms.localizationpriority: medium
ms.openlocfilehash: 25de20b398f780f5da07b6b6cf4d396a7d12204a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823894"
---
# <a name="storage-spaces-direct-overview"></a>저장소 공간 다이렉트 개요

>적용 대상: Windows Server 2019, Windows Server 2016

저장소 공간 다이렉트는 로컬 연결 드라이브가 있는 업계 표준 서버를 사용하여, 기존의 SAN 또는 NAS 어레이에 비해 훨씬 저렴한 비용으로 확장성이 뛰어난 고가용성 소프트웨어 정의 저장소를 만듭니다. 수렴 형 또는 하이퍼 수렴 형 아키텍처를 극적으로 간소화 조달 및 기능 배포를 제공할 수 있는 RDMA 네트워킹 및 NVMe 드라이브와 같은 최신 하드웨어 혁신을 함께 캐싱, 저장소 계층 및 지우기 코딩 등 최고의 효율성 및 성능입니다.

Windows Server 2019 Datacenter, Windows Server 2016 데이터 센터에에서 포함 된 저장소 공간 다이렉트 및 [Windows Server Insider Preview 빌드](https://insider.windows.com/for-business-getting-started-server/)합니다. 

공유 SAS 클러스터 및 독립 실행형 서버와 같은 다른 응용 프로그램의 저장소 공간에 대해서 [저장소 공간 개요](overview.md)합니다. 찾으려는 경우에 대 한 정보에 대 한 저장소 공간을 사용 하 여 Windows 10 PC에서를 참조 하세요 [Windows 10의 저장소 공간](https://support.microsoft.com/help/12438/windows-10-storage-spaces)입니다.

<table>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>이해</a></strong>
            <ul>
              <li>개요(현재 위치)</li>
              <li><a href="understand-the-cache.md">캐시를 이해 합니다.</a></li>
              <li><a href="storage-spaces-fault-tolerance.md">오류 허용 하 고 저장소 효율성</a></li>
              <li><a href="drive-symmetry-considerations.md">드라이브 대칭 고려 사항</a></li>
              <li><a href="understand-storage-resync.md">이해 하 고 다시 동기화 저장소 모니터링</a></li>
              <li><a href="understand-quorum.md">클러스터 및 풀 쿼럼을 이해</a></li>
              <li><a href="cluster-sets.md">클러스터 설정</a></li>
            </ul>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>계획</a></strong>
            <ul>
              <li><a href="storage-spaces-direct-hardware-requirements.md">하드웨어 요구 사항</a></li>
              <li><a href="csv-cache.md">읽기 캐시를 CSV에 메모리를 사용 하 여</li>
              <li><a href="choosing-drives.md">드라이브를 선택 합니다.</a></li>
              <li><a href="plan-volumes.md">볼륨 계획</a></li>
              <li><a href="storage-spaces-direct-in-vm.md">게스트 VM 클러스터를 사용 하 여</a></li>
              <li><a href="storage-spaces-direct-disaster-recovery.md">재해 복구</a></li>
            </ul>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>배포</a></strong>
            <ul>
                    <li><a href="deploy-storage-spaces-direct.md">저장소 공간 다이렉트 배포</a></li>
                    <li><a href="create-volumes.md">볼륨을 만듭니다.</a></li>
              <li><a href="nested-resiliency.md">중첩 된 복원 력</a></li>
              <li><a href="../../failover-clustering/manage-cluster-quorum.md">쿼럼 구성</a></li>
              <li><a href="upgrade-storage-spaces-direct-to-windows-server-2019.md">Windows Server 2019에 저장소 공간 다이렉트 클러스터 업그레이드</a></li>
            </ul>
        </td>        
        <td style="padding: 5px; border: 0;">
            <strong>관리</a></strong>
            <ul>
              <li><a href="../../manage/windows-admin-center/use/manage-hyper-converged.md">Windows Admin Center 사용 하 여 관리</a></li>
              <li><a href="add-nodes.md">서버 또는 드라이브 추가</a></li>
              <li><a href="maintain-servers.md">유지 관리를 위해 서버를 오프 라인</li>
              <li><a href="remove-servers.md">서버 제거</a></li>
              <li><a href="resize-volumes.md">볼륨 확장</a></li>
              <li><a href="../update-firmware.md">드라이브 펌웨어 업데이트</a></li>
              <li><a href="performance-history.md">성능 기록</a></li>
              <li><a href="delimit-volume-allocation.md">볼륨 할당을 구분 합니다.</a></li>
            </ul>
        </td>
    </tr>
    <tr style="border: 0;">
         <td style="padding: 5px; border: 0;">
            <strong>문제 해결</a></strong>
            <ul>
              <li><a href="storage-spaces-states.md">상태 및 작동 상태 문제 해결</a></li>
              <li><a href="data-collection.md">저장소 공간 다이렉트를 사용 하 여 진단 데이터 수집</a></li>
            </ul>
         <td style="padding: 5px; border: 0;">
            <strong>최근 블로그 게시물</a></strong>
            <ul>
              <li><a href="https://blogs.technet.microsoft.com/filecab/2018/10/30/windows-server-2019-and-intel-optane-dc-persistent-memory/">저장소 공간 다이렉트를 사용 하 여 13.7 백만 IOPS: 하이퍼 수렴 형 인프라에 대 한 새 업계 레코드</a></li>
              <li><a href="https://blogs.technet.microsoft.com/filecab/2018/10/02/hci-the-countdown-clock-starts-now/">Windows Server 2019-에서 하이퍼 수렴 형 인프라 대신 카운트다운 시계가 나타납니다 시작할 수 있습니다.</a></li>
              <li><a href="https://blogs.technet.microsoft.com/filecab/2018/06/27/windows-server-summit-recap/">Windows Server Summit의 빅 공지를 5 개</a></li>
              <li><a href="https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum/">10,000 저장소 공간 다이렉트 클러스터 및 계산 하는 중...</a></li>
            </ul>
</table>

## <a name="videos"></a>비디오

**빠른 비디오 개요 (5 분)**

<iframe src="https://www.youtube-nocookie.com/embed/raeUiNtMk0E" width="560" height="315" allowfullscreen></iframe>

**Microsoft Ignite 2018 (1 시간)에서 저장소 공간 다이렉트**

[YouTube에서 시청](https://www.youtube.com/watch?v=5kaUiW3qo30)

**Microsoft Ignite 2017 (1 시간)에서 저장소 공간 다이렉트**

[YouTube에서 시청](https://www.youtube.com/watch?v=YDr2sqNB-3c)

**Microsoft Ignite 2016 (1 시간)에서 이벤트를 시작 합니다.**

[YouTube에서 시청](https://www.youtube.com/watch?v=-LK2ViRGbWs)

## <a name="key-benefits"></a>주요 이점

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/simplicity-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>간단 합니다.</b> Windows Server 2016을 실행하는 업계 표준 서버에서 첫 번째 저장소 공간 다이렉트 클러스터로 15분 내에 이동합니다. System Center 사용자의 경우 확인란 하나만으로 배포됩니다.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/performance-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>독보적인된 성능을 제공 합니다.</b> 전체 플래시 또는 하이브리드와 상관없이 저장소 공간 다이렉트는 하이퍼바이저 포함 아키텍처, 기본 제공되는 읽기/쓰기 캐시, PCIe 버스에 직접 탑재된 최첨단 NVMe 드라이브 지원 덕분에 일관되고 짧은 대기 시간과 함께 <a href="https://blogs.technet.microsoft.com/filecab/2016/07/26/storage-iops-update-with-storage-spaces-direct/">서버당 150,000 혼합 4k 임의 IOPS</a>를 쉽게 초과합니다.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/fault-tolerance-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>내결함성입니다. </b> 기본 제공 복원 력 지속적인 가용성을 사용 하 여 드라이브, 서버 또는 구성 요소 오류를 처리합니다. 더 큰 규모의 배포에서도 <a href="../../failover-clustering/fault-domains.md">섀시 및 랙 내결함성</a>을 구성할 수 있습니다. 하드웨어 오류가 발생할 경우 교체하면 됩니다. 소프트웨어는 복잡한 관리 단계 없이 자체적으로 수정됩니다.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/efficiency-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>리소스 효율성입니다.</b> 삭제 코딩(erasure coding)은 로컬 재구성 코드 및 ReFS 실시간 계층과 같은 고유한 혁신적인 기능으로 2.4배 이상의 저장소 효율성을 제공하여 이러한 이점을 하드 디스크 드라이브 및 혼합형 핫/콜드 워크로드로 확장하는 한편, CPU 사용을 최소화하여 가장 필요한 곳(VM)에 리소스를 돌려줍니다.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/manageability-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>관리 효율성입니다.</b> <a href="../storage-qos/storage-qos-overview.md">저장소 QoS 컨트롤</a>을 사용하여, 과부하 상태의 VM에서 VM당 최소 및 최대 IOPS 제한을 지속적으로 확인합니다. <a href="../../failover-clustering/health-service-overview.md">상태 관리 서비스</a>는 기본 제공 연속 모니터링 및 경고를 제공하며, 새로운 API를 사용하면 클러스터 전체의 풍부한 성능 및 용량 메트릭을 수집할 수 있습니다.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/scalability-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>확장성입니다.</b> 클러스터당 최대 16대의 서버 및 400개가 넘는 드라이브로 최대 1페타바이트(1,000테라바이트)의 저장소를 구성할 수 있습니다.  규모를 확장하려면 드라이브와 서버를 추가하기만 하면 됩니다. 저장소 공간 다이렉트가 자동으로 새 드라이브를 인식하여 사용하기 시작합니다. 규모에 따라 저장소 효율성과 성능이 예측 가능한 방식으로 개선됩니다.
        </td>
    </tr>
</table>

## <a name="deployment-options"></a>배포 옵션

저장소 공간 다이렉트는 두 가지 배포 옵션을 제공하도록 설계되었습니다.

### <a name="converged"></a>수렴형

**저장소 및 별도 클러스터에서 계산 됩니다.** '세분화'라고도 하는 수렴형 배포 옵션은 저장소 공간 다이렉트 위에 SoFS(스케일 아웃 파일 서버)를 올려두어 SMB3 파일 공유를 통해 네트워크 연결 저장소를 제공합니다. 이렇게 하면 저장소 클러스터와 독립적으로 계산/워크로드를 확장할 수 있습니다. 이러한 확장은 서비스 공급자 및 엔터프라이즈에 대한 Hyper-V IaaS(Infrastructure as a Service)와 같은 대규모 배포에 필요합니다.

![저장소 공간 다이렉트는 스케일 아웃 파일 서버 기능을 사용하여 다른 서버 또는 클러스터의 Hyper-V VM에 저장소를 제공합니다.](media/storage-spaces-direct-in-windows-server-2016/converged-minimal.png)

### <a name="hyper-converged"></a>하이퍼 수렴형

**계산 및 저장소에 대 한 하나의 클러스터입니다.** 하이퍼 수렴형 배포 옵션은 서버에서 직접 Hyper-V 가상 컴퓨터 또는 SQL Server 데이터베이스를 실행하여 저장소를 제공하고 로컬 볼륨에 파일을 저장합니다. 따라서 파일 서버 액세스 및 사용 권한을 구성할 필요가 없으며, 중소기업 또는 원격 사무소/지사 배포에 필요한 하드웨어 비용이 절감됩니다. 참조 [저장소 공간 다이렉트 배포](deploy-storage-spaces-direct.md)합니다.

![저장소 공간 다이렉트는 같은 클러스터 내의 Hyper-V VM에 저장소 제공](media/storage-spaces-direct-in-windows-server-2016/hyper-converged-minimal.png)

## <a name="how-it-works"></a>작동 방법

저장소 공간 다이렉트는 Windows Server 2012에서 처음 도입된 저장소 공간이 개선된 것으로, 장애 조치(Failover) 클러스터링, CSV(클러스터 공유 볼륨) 파일 시스템, SMB(서버 메시지 블록) 3, 저장소 공간을 비롯하여 오늘날 Windows Server에서 알려진 많은 기능을 활용합니다. 또한 가장 주목할 만한 새로운 기술인 소프트웨어 저장소 버스도 활용합니다.

저장소 공간 다이렉트 스택의 개요는 다음과 같습니다.

![저장소 공간 다이렉트 스택](media/storage-spaces-direct-in-windows-server-2016/converged-full-stack.png)

**네트워킹 하드웨어입니다.** 저장소 공간 다이렉트는 SMB 다이렉트 및 SMB 다중 채널을 비롯한 SMB3을 사용하여 이더넷을 통해 서버 간에 통신합니다. iWARP 또는 RoCE 중 하나로 RDMA(원격 직접 메모리 액세스)와 함께 10+ GbE를 사용하는 것이 좋습니다.

**저장소 하드웨어입니다.** 로컬 연결 SATA, SAS 또는 NVMe 드라이브와 함께 2~16대 서버. 각 서버에는 2개 이상의 반도체 드라이브 및 4개 이상의 추가 드라이브가 있어야 합니다. SATA 및 SAS 장치는 HBA(호스트 버스 어댑터) 및 SAS 확장기 뒤에 있어야 합니다. 신중하게 엔지니어링되고 광범위하게 검증된 파트너의 플랫폼을 사용하는 것이 좋습니다(출시 예정).

**장애 조치 클러스터링 합니다.** Windows Server의 기본 제공 클러스터링 기능이 서버를 연결하는 데 사용됩니다.

**소프트웨어 저장소 버스입니다.** 소프트웨어 저장소 버스는 저장소 공간 다이렉트의 새로운 기능으로, 클러스터 전반에 걸쳐 모든 서버가 다른 모든 서버의 로컬 드라이브를 볼 수 있는 소프트웨어 정의 저장소 패브릭을 설정합니다. 값비싸고 제한적인 파이버 채널 또는 공유 SAS 케이블링을 교체하는 것이라고 생각할 수 있습니다.

**저장소 버스 계층 캐시입니다.** 소프트웨어 저장소 버스는 IO를 가속화 하 고 처리량을 향상 하는 서버 쪽 읽기/쓰기 캐싱을 위해 더 느린 드라이브 (예: Hdd)에 가장 빠른 드라이브 있는 (예: SSD)를 동적으로 바인딩합니다.

**저장소 풀입니다.** 저장소 공간의 기반을 형성하는 드라이브의 컬렉션을 저장소 풀이라고 합니다. 저장소 풀은 자동으로 생성되며, 모든 적격 드라이브는 자동으로 검색되어 풀에 추가됩니다. 기본 설정과 함께 클러스터당 하나의 풀을 사용하는 것이 좋습니다. 자세히 알아보려면 [저장소 풀 자세히 살펴보기](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/)를 참조하세요.

**저장소 공간입니다.** 저장소 공간은 [미러링, 삭제 코딩(erasure coding) 또는 둘 다](storage-spaces-fault-tolerance.md)를 사용하여 가상 "디스크"에 내결함성을 제공합니다. 저장소 공간을 풀의 드라이브를 사용하는 분산된 소프트웨어 정의 RAID라고 생각할 수 있습니다. 섀시 및 랙 내결함성도 사용 가능하지만, 저장소 공간 다이렉트에서 이러한 가상 디스크는 일반적으로 두 개의 동시 드라이브 또는 서버 장애에 대한 복원력을 가지고 있습니다(예: 서로 다른 서버에 각 데이터 복사본이 있는 3방향 미러링).

**복원 파일 시스템 (ReFS)입니다.** ReFS는 가상화를 위해 구축된 뛰어난 파일 시스템으로, 비트 오류를 검색하고 수정하기 위한 만들기, 확장, 검사점 병합, 기본 제공 체크섬 등 .vhdx 파일 작업에 뛰어난 가속을 제공합니다. "핫" 저장소 계층과 "콜드" 저장소 계층 사이에서 사용량을 기반으로 실시간으로 데이터를 회전하는 실시간 계층도 제공합니다.

**클러스터 공유 볼륨입니다.** CSV 파일 시스템은 모든 ReFS 볼륨을 어느 서버에서나 액세스 가능한 단일 네임스페이스로 통합합니다. 따라서 각 서버의 모든 볼륨은 로컬에서 탑재된 것처럼 보이고 작동합니다.

**스케일 아웃 파일 서버입니다.** 이 마지막 계층은 수렴형 배포에만 필요합니다. SOFS는 네트워크를 통해 SMB3 액세스 프로토콜을 사용하는 원격 파일 액세스를 클라이언트(예: Hyper-V를 실행하는 또 다른 클러스터)에 제공하여, 저장소 공간 다이렉트를 NAS(네트워크 연결 저장소)로 효과적으로 전환합니다.

## <a name="customer-stories"></a>고객 사례

가지 [10,000 개 이상의 클러스터](https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum/) 전 세계 저장소 공간 다이렉트를 실행 합니다. 대규모 기업 및 정부 수백 개의 노드를 배포 하려면 두 개의 노드를 배포 하는 소규모 기업에서 모든 규모의 인프라와 중요 한 응용 프로그램에 대 한 저장소 공간 다이렉트에 따라 달라 집니다.

방문 [Microsoft.com/HCI](https://www.microsoft.com/hci) 이야기를 읽을 수 있습니다.

[![고객 로고의 표](media/storage-spaces-direct-in-windows-server-2016/customer-stories.png)](https://www.microsoft.com/hci)

## <a name="management-tools"></a>관리 도구

관리 및/또는 저장소 공간 다이렉트를 모니터링 하려면 다음 도구를 사용할 수 있습니다.

| 이름 | 그래픽 또는 명령줄? | 유료 또는 포함? |
|-----------------|----------------------------|-------------------|
| [Windows Admin Center](../../manage/windows-admin-center/overview.md)     | 그래픽    | 포함 |
| 서버 관리자 및 장애 조치 클러스터 관리자                                 | 그래픽    | 포함 |
| Windows PowerShell                                                        | 명령줄 | 포함 |
| [System Center Virtual Machine Manager (SCVMM)](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-storage-spaces-direct-vmm) & [Operations Manager (SCOM)](https://www.microsoft.com/download/details.aspx?id=54700) | 그래픽    | 유료     |

## <a name="get-started"></a>시작

[Microsoft Azure에서](https://blogs.technet.microsoft.com/filecab/2016/05/05/s2dazuretp5/) 저장소 공간 다이렉트를 사용해 보거나 [Windows Server 평가판](https://go.microsoft.com/fwlink/?linkid=842602)에서 Windows Server의 180일 라이선스 평가판 사본을 다운로드하세요.

## <a name="see-also"></a>참조

-   [오류 허용 하 고 저장소 효율성](storage-spaces-fault-tolerance.md)
-   [저장소 복제본](../storage-replica/storage-replica-overview.md)
-   [Microsoft 블로그 저장소](https://blogs.technet.microsoft.com/filecab/)
-   [Storage Spaces Direct throughput with iWARP(iWARP 이용 시 저장소 공간 다이렉트의 처리량)](https://blogs.technet.microsoft.com/filecab/2017/03/13/storage-spaces-direct-throughput-with-iwarp)(TechNet 블로그)
-   [Windows Server에서 장애 조치 클러스터링의 새로운 기능](../../failover-clustering/whats-new-in-failover-clustering.md)  
-   [저장소 서비스 품질](../storage-qos/storage-qos-overview.md)
-   [Windows IT Pro 지원](https://www.microsoft.com/itpro/windows/support)
