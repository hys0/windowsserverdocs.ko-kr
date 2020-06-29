---
title: 클러스터 간 스토리지 복제
ms.prod: windows-server
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
ms.assetid: 834e8542-a67a-4ba0-9841-8a57727ef876
author: nedpyle
ms.date: 04/26/2019
description: 저장소 복제본을 사용 하 여 한 클러스터의 볼륨을 Windows Server를 실행 하는 다른 클러스터로 복제 하는 방법입니다.
ms.openlocfilehash: 21e054d42d0264bb22fbd0e02382ee429958a597
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475670"
---
# <a name="cluster-to-cluster-storage-replication"></a>클러스터 간 스토리지 복제

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

저장소 복제본은 스토리지 공간 다이렉트를 사용 하 여 클러스터 복제를 포함 하 여 클러스터 간에 볼륨을 복제할 수 있습니다. 관리 및 구성은 서버 간 복제와 유사합니다.

하나의 클러스터에서 다른 클러스터와 해당 스토리지 집합으로 자체 스토리지 집합을 복제하는 클러스터 간 구성에서 이러한 컴퓨터와 스토리지를 구성합니다. 필수 사항은 아니지만 이러한 노드와 해당 스토리지는 별도의 실제 사이트에 있어야 합니다.

> [!IMPORTANT]
> 이 테스트에서는 4개의 서버를 사용합니다. 각 클러스터에서 Microsoft가 지 원하는 서버를 원하는 수 만큼 사용할 수 있습니다 .이는 현재 8 스토리지 공간 다이렉트 클러스터의 경우 8이 고 공유 저장소 클러스터의 경우 64입니다.
>
> 이 가이드에서는 스토리지 공간 다이렉트 구성을 다루지 않습니다. 스토리지 공간 다이렉트를 구성 하는 방법에 대 한 자세한 내용은 [스토리지 공간 다이렉트 개요](../storage-spaces/storage-spaces-direct-overview.md)를 참조 하세요.

이 연습에서는 다음 환경을 하나의 예로 사용합니다.

-   **SRV01** 및 **SRV02** 라는 두 개의 구성원 서버가 나중에 **sr-srvclusa**이라는 클러스터에 구성 됩니다.

-   **Sr-srv03** 및 **sr-srv04 서버가 bellevue** 라는 두 개의 구성원 서버가 나중에 **SRVCLUSB**이라는 클러스터에 형성 됩니다.

-   각각 **Redmond**와 **Bellevue**라는 두 개의 데이터 센터를 나타내는 논리적 “사이트" 쌍

![Redmond 사이트의 클러스터와 Bellevue 사이트의 클러스터가 복제되는 예제 환경을 보여 주는 다이어그램](./media/Cluster-to-Cluster-Storage-Replication/SR_ClustertoCluster.png)

**그림 1: 클러스터 간 복제**

## <a name="prerequisites"></a>전제 조건

* Active Directory Domain Services 포리스트(Windows Server 2016을 실행하지 않아도 됨).
* 4-128 서버 (2-64 서버의 두 클러스터) Windows Server 2019 또는 Windows Server 2016, Datacenter Edition을 실행 합니다. Windows Server 2019를 실행 하는 경우 최대 2tb 크기의 단일 볼륨만 복제 하는 경우 Standard Edition을 대신 사용할 수 있습니다.
* SAS Jbod, 파이버 채널 SAN, 공유 VHDX, 스토리지 공간 다이렉트 또는 iSCSI 대상을 사용 하는 저장소 집합 2 개. 스토리지에는 HDD 및 SSD 미디어가 혼합되어 있어야 합니다. 각 스토리지 집합은 각 클러스터에만 사용할 수 있으며 클러스터 간의 공유 액세스는 없습니다.
* 각 스토리지 집합에서 복제된 데이터용과 로그용으로 둘 이상의 가상 디스크를 만들 수 있어야 합니다. 실제 스토리지의 섹터 크기는 모든 데이터 디스크의 섹터 크기와 동일해야 합니다. 실제 스토리지의 섹터 크기는 모든 로그 디스크의 섹터 크기와 동일해야 합니다.
* 각 서버에 하나 이상의 동기 복제용 이더넷/TCP 연결(RDMA 권장)
* 모든 노드 간에 ICMP, SMB(포트 445 및 SMB 다이렉트용 5445) 및 WS-MAN(포트 5985) 양방향 트래픽을 허용하는 적절한 방화벽 및 라우터 규칙
* 동기 복제를 위해 IO 쓰기 워크로드가 포함된 충분한 대역폭 및 평균 5ms 왕복 대기 시간을 지원하는 서버 간의 네트워크. 비동기 복제에는 권장 대기 시간이 없습니다.
* 복제된 스토리지는 Windows 운영 체제 폴더가 포함된 드라이브에 있을 수 없습니다.
* 스토리지 공간 다이렉트 복제에 대 한 & 제한 사항에 대 한 중요 한 고려 사항이 있습니다. 자세한 내용은 아래를 참조 하세요.

이러한 요구 사항은 대부분 `Test-SRTopology` cmdlet을 사용하여 확인할 수 있습니다. 하나 이상의 서버에 스토리지 복제본 또는 스토리지 복제 관리 도구 기능을 설치한 경우 이 도구에 액세스할 수 있습니다. 이 도구를 사용하기 위해 스토리지 복제본을 구성할 필요는 없으며 cmdlet을 설치하기만 하면 됩니다. 자세한 내용은 아래 단계에 포함되어 있습니다.

## <a name="step-1-provision-operating-system-features-roles-storage-and-network"></a>1 단계: 운영 체제, 기능, 역할, 저장소 및 네트워크 프로 비전

1.  Windows Server **(데스크톱 환경)** 설치 유형으로 4 개의 서버 노드 모두에 windows server를 설치 합니다.

2.  네트워크 정보를 추가하고 도메인에 가입한 다음 다시 시작합니다.

    > [!IMPORTANT]
    > 이 시점부터는 항상 모든 서버에서 기본 제공 관리자 그룹의 구성원인 도메인 사용자로 로그온합니다. 그래픽 서버 설치 또는 Windows 10 컴퓨터에서 실행할 때는 항상 Windows PowerShell 및 명령줄 프롬프트를 관리자 권한으로 사용해야 합니다.

3.  JBOD 스토리지 엔클로저, iSCSI 대상, FC SAN 또는 DAS(로컬 고정 디스크) 스토리지의 첫 번째 집합을 **Redmond** 사이트의 서버에 연결합니다.

4.  두 번째 스토리지 집합을 **Bellevue** 사이트의 서버에 연결합니다.

5.  필요에 따라 4개의 노드 모두에 최신 공급업체 스토리지와 엔클로저 펌웨어 및 드라이버, 최신 공급업체 HBA 드라이버, 최신 공급업체 BIOS/UEFI 펌웨어, 최신 공급업체 네트워크 드라이버 및 최신 마더보드 칩셋 드라이버를 설치합니다. 필요에 따라 노드를 다시 시작합니다.

    > [!NOTE]
    > 공유 스토리지 및 네트워킹 하드웨어 구성은 하드웨어 공급업체 설명서를 참조하세요.

6.  서버의 BIOS/UEFI 설정이 고성능을 지원하는지 확인합니다(예: C-상태 사용 안 함, QPI 속도 설정, NUMA 사용, 가장 높은 메모리 주파수 설정 등). Windows Server의 전원 관리가 고성능으로 설정되었는지 확인합니다. 필요에 따라 다시 시작합니다.

7.  다음과 같이 역할을 구성합니다.

    -   **그래픽 사용**

        1.  **ServerManager.exe**를 실행하고 모든 서버 노드를 추가하여 서버 그룹을 만듭니다.

        2.  각 노드에 **파일 서버** 및 **스토리지 복제본** 역할과 기능을 설치하고 다시 시작합니다.

    -   **Windows PowerShell 방법**

        SR SRV04 또는 원격 관리 컴퓨터의 Windows PowerShell 콘솔에서 다음 명령을 실행하여 4개의 노드에 있는 확장 클러스터에 필요한 기능 및 역할을 설치하고 다시 시작합니다.

        ```PowerShell
        $Servers = 'SR-SRV01','SR-SRV02','SR-SRV03','SR-SRV04'

        $Servers | ForEach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,Failover-Clustering,FS-FileServer -IncludeManagementTools -restart }
        ```

        이러한 단계에 대 한 자세한 내용은 [역할, 역할 서비스 또는 기능 설치 또는 제거](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md) 를 참조 하세요.

9. 다음과 같이 스토리지를 구성합니다.

    > [!IMPORTANT]
    > -   각 엔클로저에 두 개의 볼륨(데이터용 볼륨과 로그용 볼륨)을 만들어야 합니다.
    > -   로그 및 데이터 디스크는 **MBR**이 아니라 **GPT**로 초기화되어야 합니다.
    > -   두 개의 데이터 볼륨이 동일한 크기여야 합니다.
    > -   두 개의 로그 볼륨이 동일한 크기여야 합니다.
    > -   복제된 데이터 디스크의 섹터 크기가 모두 동일해야 합니다.
    > -   로그 디스크의 섹터 크기가 모두 동일해야 합니다.
    > -   로그 볼륨에서 SSD와 같은 플래시 기반 스토리지를 사용해야 합니다.  로그 저장소는 데이터 저장소 보다 더 빠른 것을 권장 합니다. 로그 볼륨은 다른 작업에 사용 하면 안 됩니다.
    > -   데이터 디스크에서는 HDD, SSD 또는 계층형 조합을 사용할 수 있으며, 미러링된 공간이나 패리티 공간 또는 RAID 1 또는 10, RAID 5 또는 RAID 50을 사용할 수 있습니다.
    > -   로그 볼륨은 기본적으로 8GB 이상 이어야 하며, 로그 요구 사항에 따라 더 크거나 작을 수 있습니다.
    > -   NVME 또는 SSD 캐시에 스토리지 공간 다이렉트 (스토리지 공간 다이렉트)를 사용 하는 경우 스토리지 공간 다이렉트 클러스터 간에 저장소 복제본 복제를 구성 하는 동안 예상 되는 대기 시간이 증가 하는 것을 볼 수 있습니다. 대기 시간의 변화는 성능 + 용량 구성에서 NVME 및 SSD를 사용 하 고 HDD 계층 또는 용량 계층은 사용 하지 않는 것 보다 훨씬 더 높습니다.

    이 문제는 느린 미디어와 비교 했을 때 sr-iov의 대기 시간이 매우 짧은 상태에서 sr-iov 로그 메커니즘의 아키텍처 제한으로 인해 발생 합니다. 스토리지 공간 다이렉트 스토리지 공간 다이렉트 cache를 사용 하는 경우 응용 프로그램의 모든 최근 읽기/쓰기 IO와 함께 SR 로그의 모든 IO가 캐시에서 발생 하 고 성능 또는 용량 계층에는 사용 되지 않습니다. 즉, 모든 SR 활동이 동일한 속도 미디어에서 발생 합니다 .이 구성은 권장 되지 않습니다 ( https://aka.ms/srfaq 로그 권장 사항 참조).

    Hdd와 함께 스토리지 공간 다이렉트를 사용 하는 경우 캐시를 사용 하지 않도록 설정 하거나 방지할 수 없습니다. 해결 방법으로, SSD 및 NVME만 사용 하는 경우 성능 및 용량 계층만 구성할 수 있습니다. 해당 구성을 사용 하는 경우 성능 계층에 SR 로그를 서비스를 수행 하는 데이터 볼륨만 용량 계층에 배치 하면 위에서 설명한 대기 시간이 긴 문제를 피할 수 있습니다. 더 빠르고 느린 Ssd와 NVME를 혼합 하 여 동일한 작업을 수행할 수 있습니다.

    이 해결 방법은 유용 하지 않으며 일부 고객이 사용 하지 못할 수도 있습니다. SR 팀은 나중에 발생 하는 이러한 인공 병목 현상을 줄이기 위해 최적화 및 업데이트 된 로그 메커니즘에 대해 작업 하 고 있습니다. 이에 대 한 에타는 없으며, 테스트를 위해 고객을 탭 할 수 있는 경우이 FAQ가 업데이트 됩니다.

-   **JBOD 엔클로저:**

1. 각 클러스터에서 해당 사이트의 스토리지 엔클로저만 볼 수 있는지, 그리고 SAS 연결이 제대로 구성되어 있는지 확인합니다.

2. Windows PowerShell 또는 서버 관리자를 사용하여 [독립 실행형 서버에서 스토리지 공간 배포](../storage-spaces/deploy-standalone-storage-spaces.md)에 제공된 **1~3단계**에 따라 스토리지 공간을 사용하는 스토리지를 프로비전합니다.

-   **iSCSI 대상 스토리지:**

1. 각 클러스터에서 해당 사이트의 스토리지 엔클로저만 볼 수 있는지 확인합니다. iSCSI를 사용하는 경우 둘 이상의 단일 네트워크 어댑터를 사용해야 합니다.

2. 공급업체 설명서를 사용하여 스토리지를 프로비전합니다. Windows 기반 iSCSI 대상을 사용하는 경우 [iSCSI 대상 블록 스토리지, 방법](../iscsi/iscsi-target-server.md)을 참조하세요.

-   **FC SAN 스토리지:**

1. 각 서버에서 해당 사이트의 스토리지 엔클로저만 볼 수 있는지, 그리고 호스트의 영역을 제대로 설정했는지 확인합니다.

2. 공급업체 설명서를 사용하여 스토리지를 프로비전합니다.

-   **스토리지 공간 다이렉트:**

1. 각 클러스터에서 스토리지 공간 다이렉트 배포 하 여 해당 사이트의 저장소 엔클로저를 볼 수 있는지 확인 합니다. (https://docs.microsoft.com/windows-server/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)

2. SR 로그 볼륨이 가장 빠른 플래시 저장소 및 데이터 볼륨의 용량이 느린 저장소에 항상 있는지 확인 합니다.

3. Windows PowerShell을 시작하고 `Test-SRTopology` cmdlet을 사용하여 모든 스토리지 복제본 요구 사항을 충족하는지 확인합니다. 장기 실행 성능 평가 모드뿐만 아니라 빠른 테스트를 위해 요구 사항 전용 모드에서 cmdlet을 사용할 수 있습니다.
   예를 들면 다음과 같습니다.

   ```PowerShell
   MD c:\temp

   Test-SRTopology -SourceComputerName SR-SRV01 -SourceVolumeName f: -SourceLogVolumeName g: -DestinationComputerName SR-SRV03 -DestinationVolumeName f: -DestinationLogVolumeName g: -DurationInMinutes 30 -ResultPath c:\temp
   ```

     > [!IMPORTANT]
     > 평가 기간 동안 지정된 원본 볼륨에 쓰기 IO 로드가 없는 테스트 서버를 사용하는 경우 워크로드를 추가하는 것이 좋습니다. 그렇지 않으면 유용한 보고서가 생성되지 않습니다. 실제 숫자와 권장 로그 크기를 확인하기 위해 프로덕션과 유사한 워크로드로 테스트해야 합니다. 또는 테스트 하거나 다운로드 하는 동안 일부 파일을 원본 볼륨에 복사 하 고 [Diskspd](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223) 를 실행 하 여 쓰기 io를 생성 하기만 하면 됩니다. 예를 들어 쓰기 IO 워크 로드가 낮은 샘플은 D: 볼륨에 5 분이 소요 됩니다.`Diskspd.exe -c1g -d300 -W5 -C5 -b8k -t2 -o2 -r -w5 -h d:\test.dat`

4. **TestSrTopologyReport.html** 보고서를 검사하여 스토리지 복제본 요구 사항을 충족하는지 확인합니다.

   ![복제 토폴로지 보고서 결과를 보여 주는 화면](./media/Cluster-to-Cluster-Storage-Replication/SRTestSRTopologyReport.png)

## <a name="step-2-configure-two-scale-out-file-server-failover-clusters"></a>2 단계: 두 스케일 아웃 파일 서버 장애 조치 (Failover) 클러스터 구성
이제 두 개의 정상적인 장애 조치(failover) 클러스터를 만듭니다. 구성, 유효성 검사 및 테스트 후 스토리지 복제본을 사용하여 복제합니다. 아래의 모든 단계를 클러스터 노드에서 직접 수행 하거나 Windows Server 원격 서버 관리 도구이 포함 된 원격 관리 컴퓨터에서 수행할 수 있습니다.

### <a name="graphical-method"></a>그래픽 사용

1.  각 사이트의 노드에 대해 **cluadmin.msc**를 실행합니다.

2.  제안된 클러스터의 유효성을 검사하고 결과를 분석하여 계속할 수 있는지 확인합니다. 아래에서 사용된 예는 **SR-SRVCLUSA** 및 **SR-SRVCLUSB**입니다.

3.  두 개의 클러스터를 만듭니다. 클러스터 이름이 15자 이하인지 확인합니다.

4.  파일 공유 감시 또는 클라우드 감시를 구성합니다.

    > [!NOTE]
    > 이제 WIndows Server는 클라우드 (Azure) 기반 미러링 모니터 서버에 대 한 옵션을 포함 합니다. 파일 공유 감시 대신 이 쿼럼 옵션을 선택할 수 있습니다.

    > [!WARNING]
    > 쿼럼 구성에 대 한 자세한 내용은 [쿼럼 구성 및 관리](../../failover-clustering/manage-cluster-quorum.md)에서 **감시 구성** 섹션을 참조 하세요. `Set-ClusterQuorum` cmdlet에 대한 자세한 내용은 [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum)을 참조하세요.

5.  **Redmond** 사이트의 디스크 하나를 클러스터 CSV에 추가합니다. 이렇게 하려면 **스토리지** 섹션의 **디스크** 노드에서 원본 디스크를 마우스 오른쪽 단추로 클릭한 다음 **클러스터 공유 볼륨에 추가**를 클릭합니다.

6.  [스케일 아웃 파일 서버 구성](https://technet.microsoft.com/library/hh831718.aspx)의 지침을 사용하여 두 클러스터 모두에서 클러스터된 스케일 아웃 파일 서버를 만듭니다.

### <a name="windows-powershell-method"></a>Windows PowerShell 사용

1.  제안된 클러스터를 테스트하고 결과를 분석하여 계속할 수 있는지 확인합니다.

    ```PowerShell
    Test-Cluster SR-SRV01,SR-SRV02
    Test-Cluster SR-SRV03,SR-SRV04
    ```

2.  클러스터를 만듭니다(클러스터에 대해 고유한 고정 IP 주소를 지정해야 함). 각 클러스터 이름이 15자 이하인지 확인합니다.

    ```PowerShell
    New-Cluster -Name SR-SRVCLUSA -Node SR-SRV01,SR-SRV02 -StaticAddress <your IP here>
    New-Cluster -Name SR-SRVCLUSB -Node SR-SRV03,SR-SRV04 -StaticAddress <your IP here>
    ```

3.  각 클러스터에서 도메인 컨트롤러 또는 일부 다른 독립 서버에서 호스트되는 공유를 가리키는 파일 공유 감시 또는 클라우드(Azure) 감시를 구성합니다. 예를 들면 다음과 같습니다.

    ```PowerShell
    Set-ClusterQuorum -FileShareWitness \\someserver\someshare
    ```

    > [!NOTE]
    > 이제 WIndows Server는 클라우드 (Azure) 기반 미러링 모니터 서버에 대 한 옵션을 포함 합니다. 파일 공유 감시 대신 이 쿼럼 옵션을 선택할 수 있습니다.

    > [!WARNING]
    > 쿼럼 구성에 대 한 자세한 내용은 [쿼럼 구성 및 관리](../../failover-clustering/manage-cluster-quorum.md)에서 **감시 구성** 섹션을 참조 하세요. `Set-ClusterQuorum` cmdlet에 대한 자세한 내용은 [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum)을 참조하세요.

4.  [스케일 아웃 파일 서버 구성](https://technet.microsoft.com/library/hh831718.aspx)의 지침을 사용하여 두 클러스터 모두에서 클러스터된 스케일 아웃 파일 서버를 만듭니다.

## <a name="step-3-set-up-cluster-to-cluster-replication-using-windows-powershell"></a>3 단계: Windows PowerShell을 사용 하 여 클러스터에서 클러스터로 복제 설정
이제 Windows PowerShell을 사용 하 여 클러스터 간 복제를 설정 합니다. 아래의 모든 단계를 노드에서 직접 수행 하거나 Windows Server가 포함 된 원격 관리 컴퓨터에서 수행할 수 있습니다 원격 서버 관리 도구

1. 첫 번째 클러스터의 모든 노드에서 또는 원격으로 **grant-sraccess** cmdlet을 실행 하 여 첫 번째 클러스터에 다른 클러스터에 대 한 모든 권한을 부여 합니다.  Windows Server 원격 서버 관리 도구

   ```PowerShell
   Grant-SRAccess -ComputerName SR-SRV01 -Cluster SR-SRVCLUSB
   ```

2. 두 번째 클러스터의 모든 노드에서 또는 원격으로 **grant-sraccess** cmdlet을 실행 하 여 두 번째 클러스터에 다른 클러스터에 대 한 모든 권한을 부여 합니다.

   ```PowerShell
   Grant-SRAccess -ComputerName SR-SRV03 -Cluster SR-SRVCLUSA
   ```

3. 원본 및 대상 디스크, 원본 및 대상 로그, 원본 및 대상 클러스터 이름, 로그 크기 등을 지정하여 클러스터 간 복제를 구성합니다. 서버에서 로컬로 이 명령을 수행하거나 원격 관리 컴퓨터를 사용하여 수행할 수 있습니다.

   ```powershell
   New-SRPartnership -SourceComputerName SR-SRVCLUSA -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\Volume2 -SourceLogVolumeName f: -DestinationComputerName SR-SRVCLUSB -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\Volume2 -DestinationLogVolumeName f:
   ```

   > [!WARNING]
   > 기본 로그 크기는 8GB입니다. **Test-srtopology** cmdlet의 결과에 따라 값이 더 높거나 낮은 **-logsizeinbytes** 를 사용 하도록 결정할 수 있습니다.

4. 복제 원본 및 대상 상태를 가져오려면 다음과 같이 **Get-SRGroup** 및 **Get-SRPartnership**을 사용합니다.

   ```powershell
   Get-SRGroup
   Get-SRPartnership
   (Get-SRGroup).replicas
   ```

5. 다음과 같이 복제 진행률을 확인합니다.

   1.  원본 서버에서 다음 명령을 실행하고 5015, 5002, 5004, 1237, 5001 및 2200 이벤트를 확인합니다.

       ```PowerShell
       Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica -max 20
       ```
   2.  대상 서버에서 다음 명령을 실행하여 파트너 관계 생성을 표시하는 스토리지 복제본 이벤트를 확인합니다. 이 이벤트는 복사한 바이트 수와 걸린 시간을 알려 줍니다. 예:

       ```powershell
       Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | Where-Object {$_.ID -eq "1215"} | Format-List
       ```
       다음은 출력의 예입니다.

       ```
       TimeCreated  : 4/8/2016 4:12:37 PM
       ProviderName : Microsoft-Windows-StorageReplica
       Id           : 1215
       Message      : Block copy completed for replica.
           ReplicationGroupName: rg02
           ReplicationGroupId:
           {616F1E00-5A68-4447-830F-B0B0EFBD359C}
           ReplicaName: f:\
           ReplicaId: {00000000-0000-0000-0000-000000000000}
           End LSN in bitmap:
           LogGeneration: {00000000-0000-0000-0000-000000000000}
           LogFileId: 0
           CLSFLsn: 0xFFFFFFFF
           Number of Bytes Recovered: 68583161856
           Elapsed Time (seconds): 117
       ```
   3. 또는 복제본의 대상 서버 그룹은 복사할 남은 바이트 수를 알려 주며 PowerShell을 통해 쿼리할 수 있습니다. 예를 들면 다음과 같습니다.

      ```PowerShell
      (Get-SRGroup).Replicas | Select-Object numofbytesremaining
      ```

      진행률 샘플(종료되지 않음):

      ```PowerShell
        while($true) {
        $v = (Get-SRGroup -Name "Replication 2").replicas | Select-Object numofbytesremaining
        [System.Console]::Write("Number of bytes remaining: {0}`n", $v.numofbytesremaining)
        Start-Sleep -s 5
       }
       ```

6. 대상 클러스터의 대상 서버에서 다음 명령을 실행하고 5009, 1237, 5001, 5015, 5005 및 2200 이벤트를 확인하여 처리 진행률을 이해합니다. 이 시퀀스에는 오류 경고가 없어야 합니다. 여러 개의 1237 이벤트가 있습니다. 이는 진행률을 나타냅니다.

   ```PowerShell
   Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | FL
   ```
   > [!NOTE]
   > 복제된 경우 대상 클러스터 디스크는 항상 **온라인(액세스 없음)** 으로 표시됩니다.

## <a name="step-4-manage-replication"></a>4 단계: 복제 관리

이제 클러스터 간 복제를 관리하고 운영합니다. 아래의 모든 단계를 클러스터 노드에서 직접 수행 하거나 Windows Server 원격 서버 관리 도구이 포함 된 원격 관리 컴퓨터에서 수행할 수 있습니다.

1.  **Get-ClusterGroup** 또는 **장애 조치(Failover) 클러스터 관리자**를 사용하여 복제의 현재 원본과 대상 및 해당 상태를 확인합니다.  Windows Server 원격 서버 관리 도구

2.  복제 성능을 측정하려면 원본 및 대상 노드 모두에서 **Get-Counter** cmdlet을 사용합니다. 카운터 이름은 다음과 같습니다.

    -   \Storage Replica Partition I/O Statistics(*)\Number of times flush paused

    -   \Storage Replica Partition I/O Statistics(*)\Number of pending flush I/O

    -   \Storage Replica Partition I/O Statistics(*)\Number of requests for last log write

    -   \Storage Replica Partition i/o Statistics (*) \Avg. 플러시 큐 길이

    -   \Storage Replica Partition I/O Statistics(*)\Current Flush Queue Length

    -   \Storage Replica Partition I/O Statistics(*)\Number of Application Write Requests

    -   \Storage Replica Partition i/o Statistics (*) \Avg. 로그 쓰기 당 요청 수

    -   \Storage Replica Partition i/o Statistics (*) \Avg. 앱 쓰기 대기 시간

    -   \Storage Replica Partition i/o Statistics (*) \Avg. 앱 읽기 대기 시간

    -   \Storage Replica Statistics(*)\Target RPO

    -   \Storage Replica Statistics(*)\Current RPO

    -   \Storage 복제본 통계 (*) \Avg. 로그 큐 길이

    -   \Storage Replica Statistics(*)\Current Log Queue Length

    -   \Storage Replica Statistics(*)\Total Bytes Received

    -   \Storage Replica Statistics(*)\Total Bytes Sent

    -   \Storage 복제본 통계 (*) \Avg. 네트워크 전송 대기 시간

    -   \Storage Replica Statistics(*)\Replication State

    -   \Storage 복제본 통계 (*) \Avg. 메시지 왕복 대기 시간

    -   \Storage Replica Statistics(*)\Last Recovery Elapsed Time

    -   \Storage Replica Statistics(*)\Number of Flushed Recovery Transactions

    -   \Storage Replica Statistics(*)\Number of Recovery Transactions

    -   \Storage Replica Statistics(*)\Number of Flushed Replication Transactions

    -   \Storage Replica Statistics(*)\Number of Replication Transactions

    -   \Storage Replica Statistics(*)\Max Log Sequence Number

    -   \Storage Replica Statistics(*)\Number of Messages Received

    -   \Storage Replica Statistics(*)\Number of Messages Sent

    Windows PowerShell의 성능 카운터에 대한 자세한 내용은 [Get-Counter](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Diagnostics/Get-Counter)를 참조하세요.

3.  하나의 사이트에서 복제 방향을 이동하려면 **Set-SRPartnership** cmdlet을 사용합니다.

    ```PowerShell
    Set-SRPartnership -NewSourceComputerName SR-SRVCLUSB -SourceRGName rg02 -DestinationComputerName SR-SRVCLUSA -DestinationRGName rg01
    ```

    > [!NOTE]
    > 초기 동기화가 진행 중일 때 Windows Server는 역할 전환을 방지 합니다. 초기 복제를 완료 하기 전에 전환 하려고 하면 데이터가 손실 될 수 있기 때문입니다. 초기 동기화가 완료될 때까지 방향을 강제로 전환하지 마세요.

    이벤트 로그에서 복제 방향이 변경되고 복구 모드가 발생했는지 확인한 다음 조정합니다. 그런 다음 쓰기 IO에서 새 원본 서버가 소유한 스토리지에 쓸 수 있습니다. 복제 방향을 변경하면 이전 원본 컴퓨터에서 쓰기 IO가 차단됩니다.

    > [!NOTE]
    > 복제된 경우 대상 클러스터 디스크는 항상 **온라인(액세스 없음)** 으로 표시됩니다.

4.  로그 크기를 기본 8GB에서 변경 하려면 원본 및 대상 저장소 복제본 그룹 모두에 대해 **get-srgroup** 를 사용 합니다.

    > [!IMPORTANT]
    > 기본 로그 크기는 8GB입니다. **Test-SRTopology** cmdlet의 결과에 따라 값이 더 높거나 낮은 -LogSizeInBytes를 사용할 수도 있습니다.

5.  복제를 제거하려면 각 클러스터에서 **Get-SRGroup**, **Get-SRPartnership**, **Remove-SRGroup** 및 **Remove-SRPartnership**을 사용합니다.

    ```powershell
    Get-SRPartnership | Remove-SRPartnership
    Get-SRGroup | Remove-SRGroup
    ```

    > [!NOTE]
    > 저장소 복제본이 대상 볼륨을 분리 합니다. 이것은 의도적인 것입니다.

## <a name="additional-references"></a>추가 참조

-   [스토리지 복제본 개요](storage-replica-overview.md)
-   [공유 저장소를 사용 하 여 확장 클러스터 복제](stretch-cluster-replication-using-shared-storage.md)
-   [서버 간 저장소 복제](server-to-server-storage-replication.md)
-   [저장소 복제본: 알려진 문제](storage-replica-known-issues.md)
-   [스토리지 복제본: 질문과 대답](storage-replica-frequently-asked-questions.md)
-   [Windows Server 2016의 스토리지 공간 다이렉트](../storage-spaces/storage-spaces-direct-overview.md)
