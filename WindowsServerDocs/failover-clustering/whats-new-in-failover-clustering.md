---
ms.assetid: 350aa5a3-5938-4921-93dc-289660f26bad
title: Windows Server 장애 조치 (Failover) 클러스터링의 새로운 기능
ms.prod: windows-server
ms.technology: storage-failover-clustering
ms.topic: get-started-article
manager: lizross
author: JasonGerend
ms.author: jgerend
ms.date: 10/18/2018
ms.openlocfilehash: 431854f2e063454124092151c6788263db57b5f2
ms.sourcegitcommit: 568b924d32421256f64abfee171304f1daf320d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85070150"
---
# <a name="whats-new-in-failover-clustering"></a>장애 조치(failover) 클러스터링의 새로운 기능

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 Windows Server 2019 및 Windows Server 2016 장애 조치 (Failover) 클러스터링의 새로운 기능 및 변경 된 기능에 대해 설명 합니다.

## <a name="whats-new-in-windows-server-2019"></a>Windows Server 2019의 새로운 기능

- **클러스터 세트**

    클러스터 집합을 사용 하면 클러스터의 현재 한도를 초과 하는 단일 SDDC (소프트웨어 정의 데이터 센터) 솔루션의 서버 수를 늘릴 수 있습니다. 이렇게 하려면 여러 클러스터를 클러스터 집합으로 그룹화 합니다. 즉, 계산, 저장소 및 하이퍼 수렴 형 여러 장애 조치 (failover) 클러스터의 느슨하게 결합 된 그룹입니다.
    클러스터 집합을 사용 하면 클러스터 집합 내의 클러스터 간에 온라인 가상 컴퓨터 (실시간 마이그레이션)를 이동할 수 있습니다.

    자세한 내용은 [클러스터 집합](../storage/storage-spaces/cluster-sets.md)을 참조 하세요.

- **Azure 인식 클러스터**
  
    이제 장애 조치 (failover) 클러스터는 Azure IaaS 가상 머신에서 실행 되는 경우 자동으로 검색 하 고 Azure 계획 된 유지 관리 이벤트의 사전 장애 조치 (failover) 및 로깅을 제공 하 여 최고 수준의 가용성을 달성할 수 있도록 구성을 최적화 합니다 클러스터 이름에 대 한 동적 네트워크 이름으로 부하 분산 장치를 구성할 필요가 없으므로 배포도 간단해 집니다.

- **도메인 간 클러스터 마이그레이션**

    이제 장애 조치 (Failover) 클러스터가 Active Directory 한 도메인에서 다른 도메인으로 동적으로 이동 하 여 도메인 통합을 간소화 하 고 하드웨어 파트너가 클러스터를 만들고 나중에 고객의 도메인에 조인할 수 있습니다.

- **USB 감시**

    이제 네트워크 스위치에 연결 된 간단한 USB 드라이브를 미러링 모니터 서버로 사용 하 여 클러스터에 대 한 쿼럼을 결정할 수 있습니다. SMB2 규격 장치를 지원 하도록 파일 공유 감시를 확장 합니다.

- **클러스터 인프라 개선**

    이제는 CSV 캐시가 기본적으로 사용 하도록 설정 되어 가상 머신 성능을 향상 시킵니다. 이제 MSDTC는 클러스터 공유 볼륨을 지원 하므로 SQL Server와 같은 스토리지 공간 다이렉트에서 MSDTC 작업을 배포할 수 있습니다. 노드를 클러스터 멤버 자격으로 반환 하기 위해 자체 복구를 통해 분할 된 노드를 검색 하는 향상 된 논리 클러스터 네트워크 경로 검색 및 자동 복구 기능이 향상 되었습니다.

- **클러스터 인식 업데이트에서 스토리지 공간 다이렉트 지원**

    CAU (클러스터 인식 업데이트)는 현재 통합 되어 있으며 각 노드에서 데이터 다시 동기화가 완료 되었는지 확인 하 고 확인 하는 스토리지 공간 다이렉트을 인식 합니다. 클러스터 인식 업데이트는 필요한 경우에만 지능적으로 다시 시작 되도록 업데이트를 검사 합니다. 이렇게 하면 계획 된 유지 관리를 위해 클러스터의 모든 서버를 오케스트레이션 다시 시작할 수 있습니다.

- **파일 공유 감시 개선**

    다음 시나리오에서 파일 공유 감시를 사용할 수 있습니다.
  - 원격 위치로 인해 인터넷 액세스가 없거나 매우 저하 되어 클라우드 감시를 사용할 수 없습니다.
  - 디스크 감시에 대 한 공유 드라이브가 부족 합니다. 이는 스토리지 공간 다이렉트 하이퍼 수렴 형 구성, SQL Server AG (Always On 가용성 그룹) 또는 * Exchange Database Availability Group (DAG)입니다. 공유 디스크를 사용 하지 않습니다.
  - 클러스터가 DMZ 뒤에 있기 때문에 도메인 컨트롤러 연결이 부족 합니다.
  - Active Directory 클러스터 이름 개체가 없는 작업 그룹 또는 도메인 간 클러스터 (CNO). 서버 & 관리 블로그의 다음 게시물에서 이러한 향상 된 기능에 대해 자세히 알아보세요. 장애 조치 (Failover) 클러스터 파일 공유 감시 및 DFS.

    이제 DFS 네임 스페이스 공유를 위치로 사용 하는 것을 명시적으로 차단 합니다. DFS 공유에 파일 공유 감시를 추가 하면 클러스터에 대 한 안정성 문제가 발생할 수 있으며,이 구성은 지원 되지 않습니다. 공유에서 DFS 네임 스페이스를 사용 하는지 여부를 검색 하는 논리를 추가 하 고 DFS 네임 스페이스를 검색 하면 장애 조치(Failover) 클러스터 관리자는 미러링 모니터 서버 생성을 차단 하 고 지원 되지 않는에 대 한 오류 메시지를 표시 합니다.

- **클러스터 강화**

    클러스터 공유 볼륨 및 스토리지 공간 다이렉트에 대 한 SMB (서버 메시지 블록)를 통한 클러스터 간 통신은 이제 인증서를 활용 하 여 가장 안전한 플랫폼을 제공 합니다. 이렇게 하면 장애 조치 (Failover) 클러스터가 NTLM에 대 한 종속성 없이 작동 하 고 보안 기준을 사용 하도록 설정할 수 있습니다.

- **장애 조치(failover) 클러스터는 더 이상 NTLM 인증을 사용하지 않음**

    장애 조치 (Failover) 클러스터는 더 이상 NTLM 인증을 사용 하지 않습니다. 대신 Kerberos 및 인증서 기반 인증을 독점적으로 사용 합니다. 이러한 보안 기능을 활용 하기 위해 사용자 또는 배포 도구에 필요한 변경 사항은 없습니다. 또한 NTLM을 사용 하지 않도록 설정 된 환경에서 장애 조치 (failover) 클러스터를 배포할 수 있습니다.

## <a name="whats-new-in-windows-server-2016"></a>Windows Server 2016의 새로운 기능

### <a name="cluster-operating-system-rolling-upgrade"></a><a name="BKMK_RollingUpgrade"></a>클러스터 운영 체제 롤링 업그레이드

클러스터 운영 체제 롤링 업그레이드를 사용 하면 관리자가 Hyper-v 또는 스케일 아웃 파일 서버 작업을 중지 하지 않고 클러스터 노드의 운영 체제를 Windows Server 2012 r 2에서 최신 버전으로 업그레이드할 수 있습니다. 이 기능을 사용하면 SLA(서비스 수준 계약)의 가동 중지 시간 위반을 피할 수 있습니다.

**이와 같은 변경을 통해 더해지는 가치**  

Hyper-v 또는 스케일 아웃 파일 서버 클러스터를 Windows Server 2012 r 2에서 Windows Server 2016로 업그레이드 하는 데 더 이상 가동 중지 시간이 필요 하지 않습니다. 클러스터의 모든 노드가 Windows Server 2016를 실행할 때까지 클러스터는 Windows Server 2012 R2 수준에서 계속 작동 합니다. 클러스터 기능 수준은 Windows PowerShell cmdlet를 사용 하 여 Windows Server 2016로 업그레이드 됩니다 `Update-ClusterFunctionalLevel` .

> [!WARNING]  
> - 클러스터 기능 수준을 업데이트 한 후에는 Windows Server 2012 R2 클러스터 기능 수준으로 돌아갈 수 없습니다.
>
> - `Update-ClusterFunctionalLevel`Cmdlet이 실행 될 때까지 프로세스를 되돌릴 수 있으며 Windows server 2012 R2 노드를 추가 하 고 Windows server 2016 노드를 제거할 수 있습니다.

**달라진 기능**  

이제 가동 중지 시간 없이 Hyper-v 또는 스케일 아웃 파일 서버 장애 조치 (failover) 클러스터를 쉽게 업그레이드할 수 있습니다. 또는 Windows Server 2016 운영 체제를 실행 하는 노드를 사용 하 여 새 클러스터를 만들어야 합니다. 기존 클러스터를 오프 라인으로 전환 하 고 각 노드에 대해 새 운영 체제를 다시 설치한 다음 클러스터를 다시 온라인 상태로 전환 하는 것과 관련 된 클러스터를 Windows Server 2012 r 2로 마이그레이션합니다. 이전 프로세스는 복잡 하 고 가동 중지 시간이 필요 했습니다. 그러나 Windows Server 2016에서는 어떤 지점 에서도 클러스터가 오프 라인으로 전환 될 필요가 없습니다.

단계에서 업그레이드를 위한 클러스터 운영 체제는 클러스터의 각 노드에 대해 다음과 같이 수행 됩니다.  
-   노드가 일시 중지 되 고 해당 노드가 실행 되는 모든 가상 컴퓨터를 방전 했습니다. 
-   가상 컴퓨터 (또는 다른 클러스터 작업)는 클러스터의 다른 노드로 마이그레이션됩니다. 
-   기존 운영 체제가 제거 되 고 노드에서 Windows Server 2016 운영 체제를 새로 설치 하는 작업이 수행 됩니다. 
-   Windows Server 2016 운영 체제를 실행 하는 노드가 클러스터에 다시 추가 됩니다. 
-   이 시점에서 클러스터 노드가 Windows Server 2012 R2 또는 Windows Server 2016를 실행 하 고 있기 때문에 클러스터는 혼합 모드로 실행 되 고 있다고 합니다. 
-   클러스터 기능 수준은 Windows Server 2012 r 2에서 유지 됩니다. 이 기능 수준에서는 이전 버전의 운영 체제와의 호환성에 영향을 주는 Windows Server 2016의 새로운 기능을 사용할 수 없습니다. 
-   결국 모든 노드가 Windows Server 2016로 업그레이드 됩니다. 
-   그런 다음 Windows PowerShell cmdlet을 사용 하 여 클러스터 기능 수준이 Windows Server 2016로 변경 됩니다 `Update-ClusterFunctionalLevel` . 이제 Windows Server 2016 기능을 활용할 수 있습니다. 

자세한 내용은 [클러스터 운영 체제 롤링 업그레이드](cluster-operating-system-rolling-upgrade.md)를 참조 하세요. 

### <a name="storage-replica"></a><a name="BKMK_SR"></a>저장소 복제본  
저장소 복제본은 재해 복구를 위해 서버 또는 클러스터 간에 저장소에 상관 없는 블록 수준의 동기 복제를 지원 하 고 사이트 간 장애 조치 (failover) 클러스터를 확장 하는 새로운 기능입니다. 동기 복제를 사용하면 파일 시스템 수준에서 데이터가 손실되지 않고 크래시 일관성이 있는 볼륨을 사용하여 실제 사이트의 데이터를 미러링할 수 있습니다. 비동기 복제는 대도시 범위를 넘어 사이트를 확장합니다(데이터가 손실될 수도 있음). 

**이와 같은 변경을 통해 더해지는 가치**  

저장소 복제본을 사용 하면 다음 작업을 수행할 수 있습니다.  

-   중요 업무용 워크로드의 계획된 중단 및 계획되지 않은 중단을 위한 단일 공급업체 재해 복구 솔루션을 제공합니다. 

-   안정성, 확장성 및 성능이 검증된 SMB3 전송을 사용합니다. 

-   대도시 거리로 Windows 장애 조치(failover) 클러스터를 확장합니다. 

-   Microsoft 소프트웨어 종단을 사용 하 여 Hyper-v, 저장소 복제본, 저장소 공간, 클러스터, 스케일 아웃 파일 서버, SMB3, 데이터 중복 제거, ReFS/NTFS 등의 저장소 및 클러스터링을 종료 합니다. 

-   다음과 같이 비용 및 복잡성을 줄입니다.  

    -   하드웨어 제약이 없으므로 DAS 또는 SAN과 같은 특정 스토리지 구성에 대한 요구 사항이 없습니다. 

    -   상용 스토리지 및 네트워킹 기술을 허용합니다. 

    -   장애 조치(Failover) 클러스터 관리자를 통해 개별 노드 및 클러스터에 대한 그래픽 관리가 용이합니다. 

    -   Windows PowerShell을 통한 포괄적인 대규모 스크립팅 옵션을 포함합니다. 

-   가동 중지 시간을 줄이고, Windows의 고유한 안정성 및 생산성을 높입니다. 

-   지원 가능성, 성능 메트릭 및 진단 기능을 제공합니다. 

자세한 내용은 [Windows Server 2016의 스토리지 복제본](../storage/storage-replica/storage-replica-overview.md)을 참조하세요. 

### <a name="cloud-witness"></a><a name="BKMK_CloudWitness"></a>클라우드 감시

클라우드 감시는 중재 지점으로 Microsoft Azure를 활용하는 Windows Server 2016에서 새로운 유형의 장애 조치 클러스터 쿼럼 감시 기능입니다. 다른 쿼럼 감시와 마찬가지로 클라우드 감시는 응답을 가져오고 쿼럼 계산에 참여할 수 있습니다. 클러스터 쿼럼 구성 마법사를 사용하여 쿼럼 감시로 클라우드 감시를 구성할 수 있습니다. 

**이와 같은 변경을 통해 더해지는 가치**  

클라우드 감시를 장애 조치 (Failover) 클러스터 쿼럼 감시로 사용 하면 다음과 같은 이점이 있습니다.  

-   Microsoft Azure 활용 하 고 세 번째 별도의 데이터 센터에 대 한 필요성을 제거 합니다. 

-   는 공용 클라우드에서 호스트 되는 Vm의 추가 유지 관리 오버 헤드를 제거 하는 표준 공개적으로 사용 가능한 Microsoft Azure Blob Storage를 사용 합니다. 

-   동일한 Microsoft Azure Storage 계정을 여러 클러스터에 사용할 수 있습니다 (클러스터당 하나의 blob 파일, blob 파일 이름으로 사용 되는 클러스터 고유 id). 

-   저장소 계정에 대 한 매우 낮은 비용을 제공 합니다 (blob 파일당 매우 작은 데이터는 클러스터 노드의 상태가 변경 될 때 한 번만 업데이트 됨). 

자세한 내용은 [장애 조치 (Failover) 클러스터용 클라우드 감시 배포](deploy-cloud-witness.md)를 참조 하세요. 

**달라진 기능**  

이 기능은 Windows Server 2016의 새로운 기능입니다. 

### <a name="virtual-machine-resiliency"></a><a name="BKMK_VMs"></a>가상 컴퓨터 복원 력

**계산 복원 력** Windows Server 2016에는 다음과 같이 계산 클러스터에서 클러스터 간 통신 문제를 줄이는 데 도움이 되는 virtual machines 계산 복원 력이 증가 하 고 있습니다. 

-   **가상 컴퓨터에 사용할 수 있는 복원 력 옵션:**  이제 일시적으로 실패 하는 동안 가상 컴퓨터의 동작을 정의 하는 가상 컴퓨터 복원 력 옵션을 구성할 수 있습니다.  

    -   **복원 력 수준:** 일시적인 오류를 처리 하는 방법을 정의 하는 데 도움이 됩니다. 

    -   **복원 력 기간:**  모든 가상 컴퓨터를 격리 된 상태로 실행할 수 있는 기간을 정의 하는 데 도움이 됩니다. 

-   **비정상 노드의 격리:** 비정상 노드는 격리 되 고 더 이상 클러스터에 조인할 수 없습니다. 이렇게 하면 플 래핑 노드가 다른 노드와 전체 클러스터를 부정적으로 주는 수 없습니다. 

가상 컴퓨터 계산 복원 력 워크플로 및 노드가 격리 또는 격리에 배치 되는 방식을 제어 하는 노드 격리 설정에 대 한 자세한 내용은 [Windows Server 2016의 가상 컴퓨터 계산 복원](https://blogs.msdn.com/b/clustering/archive/2015/06/03/10619308.aspx)기능을 참조 하세요. 

**저장소 복원 력** Windows Server 2016에서는 임시 저장소 오류에 대 한 가상 컴퓨터의 복원 력이 향상 되었습니다. 향상 된 가상 컴퓨터 복원 력을 통해 저장소 중단이 발생 하는 경우 테 넌 트 가상 컴퓨터 세션 상태를 유지 하는 데 도움이 됩니다. 이는 저장소 인프라 문제에 대 한 지능형 및 빠른 가상 머신 응답을 통해 달성 됩니다. 

가상 컴퓨터가 기본 저장소에서 연결을 끊으면 일시 중지 되 고 저장소가 복구 될 때까지 대기 합니다. 일시 중지 된 동안 가상 머신은 실행 중인 응용 프로그램의 컨텍스트를 유지 합니다. 가상 컴퓨터의 저장소에 대 한 연결이 복원 되 면 가상 컴퓨터는 실행 중 상태로 돌아갑니다. 따라서 테 넌 트 컴퓨터의 세션 상태는 복구 시 보존 됩니다. 

Windows Server 2016에서는 게스트 클러스터에 대 한 가상 머신 저장소 복원 력이 인식 되 고 최적화 됩니다. 

### <a name="diagnostic-improvements-in-failover-clustering"></a><a name="BKMK_Diagnostics"></a>장애 조치 (Failover) 클러스터링의 진단 개선 사항

장애 조치 (failover) 클러스터 문제를 진단 하는 데 도움이 되도록 Windows Server 2016에는 다음이 포함 됩니다.  

- 장애 조치 (failover) 클러스터링 문제 해결을 용이 하 게 하는 클러스터 로그 파일 (예: 표준 시간대 정보 및 DiagnosticVerbose 로그)에 대 한 몇 가지 향상 된 기능 자세한 내용은 [Windows Server 2016 장애 조치 (Failover) 클러스터 문제 해결 향상-클러스터 로그](https://techcommunity.microsoft.com/t5/failover-clustering/windows-server-2016-failover-cluster-troubleshooting/ba-p/372005)를 참조 하세요.

- 가상 컴퓨터에 할당 된 대부분의 메모리 페이지를 필터링 하 여 memory.dmp를 훨씬 더 작고 저장 하거나 복사할 수 있도록 하는 **활성 메모리 덤프**의 새 덤프 유형입니다. 자세한 내용은 [Windows Server 2016 장애 조치 (Failover) 클러스터 문제 해결 향상-활성 덤프](https://techcommunity.microsoft.com/t5/failover-clustering/windows-server-2016-failover-cluster-troubleshooting/ba-p/372008)를 참조 하세요.

### <a name="site-aware-failover-clusters"></a><a name="BKMK_SiteAware"></a>사이트 인식 장애 조치(failover) 클러스터

Windows Server 2016에는 물리적 위치 (사이트)에 따라 스트레치 된 클러스터의 그룹 노드를 사용 하도록 설정 하는 사이트 인식 장애 조치 (failover) 클러스터가 포함 되어 있습니다. 클러스터 사이트 인식은 클러스터 수명 주기 동안 장애 조치 (failover) 동작, 배치 정책, 노드 간 하트 비트 및 쿼럼 동작과 같은 주요 작업을 향상 시킵니다. 자세한 내용은 [Windows Server 2016의 사이트 인식 장애 조치 (Failover) 클러스터](https://techcommunity.microsoft.com/t5/failover-clustering/site-aware-failover-clusters-in-windows-server-2016/ba-p/372060)를 참조 하세요.

### <a name="workgroup-and-multi-domain-clusters"></a><a name="BKMK_multidomainclusters"></a>작업 그룹 및 다중 도메인 클러스터

Windows Server 2012 R2 및 이전 버전에서는 동일한 도메인에 가입 된 구성원 노드 간에만 클러스터를 만들 수 있습니다. Windows Server 2016에는 이러한 장벽을 허물고 Active Directory 종속성 없이 장애 조치(failover) 클러스터를 만들 수 있는 기능이 도입되었습니다. 이제 다음 구성으로 장애 조치 (failover) 클러스터를 만들 수 있습니다.  

-   **단일 도메인 클러스터.** 모든 노드가 동일한 도메인에 가입 된 클러스터 

-   **다중 도메인 클러스터.** 다른 도메인의 멤버인 노드가 있는 클러스터 

-   **작업 그룹 클러스터.** 구성원 서버/작업 그룹 (도메인에 가입 되지 않음) 인 노드가 있는 클러스터 

자세한 내용은 [Windows Server 2016의 작업 그룹 및 다중 도메인 클러스터](https://techcommunity.microsoft.com/t5/failover-clustering/workgroup-and-multi-domain-clusters-in-windows-server-2016/ba-p/372059) 를 참조 하세요.

### <a name="virtual-machine-load-balancing"></a><a name="BKMK_VMLoadBalancing"></a>가상 컴퓨터 부하 분산  

가상 컴퓨터 부하 분산은 장애 조치 (Failover) 클러스터링의 새로운 기능으로, 클러스터의 노드 전체에서 가상 컴퓨터의 원활한 부하 분산을 용이 하 게 합니다. 오버 커밋된 노드는 노드의 가상 컴퓨터 메모리와 CPU 사용률을 기반으로 식별 됩니다. 그런 다음 가상 컴퓨터는 오버 커밋된 노드에서 사용 가능한 대역폭이 있는 노드 (해당 하는 경우)로 이동 (실시간 마이그레이션) 됩니다. 최적의 클러스터 성능과 사용률을 보장 하기 위해 분산의 강도를 튜닝할 수 있습니다. 부하 분산은 Windows Server 2016 Technical Preview에서 기본적으로 사용 하도록 설정 되어 있습니다. 그러나 SCVMM 동적 최적화를 사용 하도록 설정한 경우에는 부하 분산이 사용 되지 않습니다. 

### <a name="virtual-machine-start-order"></a><a name="BKMK_VMStartOrder"></a>가상 컴퓨터 시작 순서

가상 컴퓨터 시작 순서는 장애 조치 (Failover) 클러스터링의 새로운 기능으로 클러스터의 가상 컴퓨터 (및 모든 그룹)에 대 한 시작 주문 오케스트레이션을 도입 합니다. 이제 가상 머신을 계층으로 그룹화 할 수 있으며, 다른 계층 간에 시작 주문 종속성을 만들 수 있습니다. 이렇게 하면 가장 중요 한 가상 컴퓨터 (예: 도메인 컨트롤러 또는 유틸리티 가상 컴퓨터)가 먼저 시작 됩니다. 가상 컴퓨터는 종속성이 있는 가상 컴퓨터도 시작 될 때까지 시작 되지 않습니다. 

### <a name="simplified-smb-multichannel-and-multi-nic-cluster-networks"></a><a name="BKMK_SMBMultiChannel"></a>간소화 된 SMB 다중 채널 및 다중 NIC 클러스터 네트워크

장애 조치 (Failover) 클러스터 네트워크는 서브넷/네트워크 당 하나의 NIC로 더 이상 제한 되지 않습니다. 간소화 된 SMB 다중 채널 및 다중 NIC 클러스터 네트워크를 사용 하는 경우 네트워크 구성은 자동 이며, 서브넷의 모든 NIC를 클러스터 및 워크 로드 트래픽에 사용할 수 있습니다. 이러한 향상 된 기능을 통해 고객은 Hyper-v, SQL Server 장애 조치 (Failover) 클러스터 인스턴스 및 기타 SMB 워크 로드에 대 한 네트워크 처리량을 최대화할 수 있습니다. 

자세한 내용은 [간소화 된 SMB 다중 채널 및 다중 NIC 클러스터 네트워크](smb-multichannel.md)를 참조 하세요.

## <a name="see-also"></a>참고 항목

* [스토리지](../storage/storage.yml)  
* [Windows Server 2016에서 제공 되는 저장소의 새로운 기능](../storage/whats-new-in-storage.md)  
