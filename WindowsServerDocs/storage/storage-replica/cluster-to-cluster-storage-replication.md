---
title: 클러스터 간 저장소 복제
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
ms.assetid: 834e8542-a67a-4ba0-9841-8a57727ef876
author: nedpyle
ms.date: 10/11/2017
description: 저장소 복제본을 사용하여 하나의 클러스터에서 Windows Server 2016 Datacenter Edition을 실행하는 다른 클러스터로 볼륨을 복제하는 방법을 알아봅니다.
ms.openlocfilehash: 46bd5a53ff0e704844f10264a9f3a6fbe0e4d512
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838664"
---
# <a name="cluster-to-cluster-storage-replication"></a>클러스터 간 저장소 복제

> 적용 대상: Windows Server (반기 채널), Windows Server 2016

이제 Windows Server 2016 Datacenter Edition에서 저장소 공간 다이렉트(즉, 공유 없이 직접 연결된 저장소)를 사용한 클러스터 복제를 포함하여 클러스터 간 복제를 사용할 수 있습니다. 관리 및 구성은 서버 간 복제와 유사합니다.  

하나의 클러스터에서 다른 클러스터와 해당 저장소 집합으로 자체 저장소 집합을 복제하는 클러스터 간 구성에서 이러한 컴퓨터와 저장소를 구성합니다. 필수 사항은 아니지만 이러한 노드와 해당 저장소는 별도의 실제 사이트에 있어야 합니다.  

Windows Server 2016 Datacenter Edition에는 클러스터 간 복제를 위한 저장소 복제본을 구성할 수 있는 그래픽 도구가 없지만 향후에는 Azure Site Recovery가 이 시나리오를 구성할 수 있게 됩니다.

> [!IMPORTANT]
> 이 테스트에서는 4개의 서버를 사용합니다. 원하는 만큼의 저장소 공간 다이렉트 클러스터에 대 한 8 및 64 공유 저장소 클러스터에 대 한 현재 상태인 각 클러스터에서 Microsoft에서 지 원하는 서버를 사용할 수 있습니다.  
>   
> 이 가이드에서는 저장소 공간 다이렉트 구성을 다루지 않습니다. 저장소 공간 다이렉트를 구성하는 방법에 대한 자세한 내용은 [Windows Server 2016의 저장소 공간 다이렉트](../storage-spaces/storage-spaces-direct-overview.md)를 참조하세요.  

이 연습에서는 다음 환경을 예로 사용합니다.  

-   나중에 **SR-SRVCLUSA**라는 클러스터로 구성되는 **SR-SRV01** 및 **SR-SRV02**라는 구성원 서버 2개  

-   나중에 **SR-SRVCLUSB**라는 클러스터로 구성되는 **SR-SRV03** 및 **SR-SRV04**라는 구성원 서버 2개  

-   각각 **Redmond**와 **Bellevue**라는 두 개의 데이터 센터를 나타내는 논리적 “사이트" 쌍  

![Redmond 사이트의 클러스터와 Bellevue 사이트의 클러스터가 복제되는 예제 환경을 보여 주는 다이어그램](./media/Cluster-to-Cluster-Storage-Replication/SR_ClustertoCluster.png)  

**그림 1: 클러스터 간 복제**  

## <a name="prerequisites"></a>사전 요구 사항  

* Active Directory 도메인 서비스 포리스트(Windows Server 2016을 실행하지 않아도 됨).  
* Windows Server 2016 Datacenter Edition이 설치된 서버 4개(두 클러스터에 2개씩) 이상. 최대 64개의 노드 클러스터 지원.  
* SAS JBOD, 파이버 채널 SAN, 공유 VHDX, 저장소 공간 다이렉트 또는 iSCSI 대상을 사용하는 저장소 집합 2개. 저장소에는 HDD 및 SSD 미디어가 혼합되어 있어야 합니다. 각 저장소 집합은 각 클러스터에만 사용할 수 있으며 클러스터 간의 공유 액세스는 없습니다.  
* 각 저장소 집합에서 복제된 데이터용과 로그용으로 둘 이상의 가상 디스크를 만들 수 있어야 합니다. 실제 저장소의 섹터 크기는 모든 데이터 디스크의 섹터 크기와 동일해야 합니다. 실제 저장소의 섹터 크기는 모든 로그 디스크의 섹터 크기와 동일해야 합니다.  
* 각 서버에 하나 이상의 동기 복제용 이더넷/TCP 연결(RDMA 권장)   
* 모든 노드 간에 ICMP, SMB(포트 445 및 SMB 다이렉트용 5445) 및 WS-MAN(포트 5985) 양방향 트래픽을 허용하는 적절한 방화벽 및 라우터 규칙  
* 동기 복제를 위해 IO 쓰기 워크로드가 포함된 충분한 대역폭 및 평균 5ms 왕복 대기 시간을 지원하는 서버 간의 네트워크. 비동기 복제에는 권장 대기 시간이 없습니다.  
* 복제된 저장소는 Windows 운영 체제 폴더가 포함된 드라이브에 있을 수 없습니다.
* 가지 중요 한 고려 사항 및 저장소 공간 다이렉트 복제에 대 한 제한 사항-아래의 세부 정보를 검토 하세요.

이러한 요구 사항은 대부분 `Test-SRTopology` cmdlet을 사용하여 확인할 수 있습니다. 하나 이상의 서버에 저장소 복제본 또는 저장소 복제 관리 도구 기능을 설치한 경우 이 도구에 액세스할 수 있습니다. 이 도구를 사용하기 위해 저장소 복제본을 구성할 필요는 없으며 cmdlet을 설치하기만 하면 됩니다. 자세한 내용은 아래 단계에 포함되어 있습니다.  

## <a name="step-1-provision-operating-system-features-roles-storage-and-network"></a>1단계: 운영 체제, 기능, 역할, 저장소 및 네트워크 프로비전

1.  Windows Server 2016 Datacenter **(데스크톱 환경)** 설치 유형으로 4개의 서버 노드 모두에 Windows Server 2016을 설치합니다. Standard Edition(사용 가능한 경우)에는 저장소 복제본이 포함되어 있지 않으므로 이 버전을 선택하지 마세요.  

2.  네트워크 정보를 추가하고 도메인에 가입한 다음 다시 시작합니다.  

    > [!IMPORTANT]  
    > 이 시점부터는 항상 모든 서버에서 기본 제공 관리자 그룹의 구성원인 도메인 사용자로 로그온합니다. 그래픽 서버 설치 또는 Windows 10 컴퓨터에서 실행할 때는 항상 Windows PowerShell 및 명령줄 프롬프트를 관리자 권한으로 사용해야 합니다.  

3.  JBOD 저장소 엔클로저, iSCSI 대상, FC SAN 또는 DAS(로컬 고정 디스크) 저장소의 첫 번째 집합을 **Redmond** 사이트의 서버에 연결합니다.  

4.  두 번째 저장소 집합을 **Bellevue** 사이트의 서버에 연결합니다.  

5.  필요에 따라 4개의 노드 모두에 최신 공급업체 저장소와 엔클로저 펌웨어 및 드라이버, 최신 공급업체 HBA 드라이버, 최신 공급업체 BIOS/UEFI 펌웨어, 최신 공급업체 네트워크 드라이버 및 최신 마더보드 칩셋 드라이버를 설치합니다. 필요에 따라 노드를 다시 시작합니다.  

    > [!NOTE]  
    > 공유 저장소 및 네트워킹 하드웨어 구성은 하드웨어 공급업체 설명서를 참조하세요.  

6.  서버의 BIOS/UEFI 설정이 고성능을 지원하는지 확인합니다(예: C-상태 사용 안 함, QPI 속도 설정, NUMA 사용, 가장 높은 메모리 주파수 설정 등). Windows Server의 전원 관리가 고성능으로 설정되었는지 확인합니다. 필요에 따라 다시 시작합니다.  

7.  다음과 같이 역할을 구성합니다.  

    -   **그래픽 사용**  

        1.  **ServerManager.exe**를 실행하고 모든 서버 노드를 추가하여 서버 그룹을 만듭니다.  

        2.  각 노드에 **파일 서버** 및 **저장소 복제본** 역할과 기능을 설치하고 다시 시작합니다.  

    -   **Windows PowerShell 메서드**  

        SR SRV04 또는 원격 관리 컴퓨터의 Windows PowerShell 콘솔에서 다음 명령을 실행하여 4개의 노드에 있는 확장 클러스터에 필요한 기능 및 역할을 설치하고 다시 시작합니다.  

        ```PowerShell
        $Servers = 'SR-SRV01','SR-SRV02','SR-SRV03','SR-SRV04'  

        $Servers | ForEach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,Failover-Clustering,FS-FileServer -IncludeManagementTools -restart }  
        ```  

        이러한 단계에 대한 자세한 내용은 [역할, 역할 서비스 또는 기능 설치 또는 제거](https://technet.microsoft.com/library/hh831809.aspx)를 참조하세요.  

9. 다음과 같이 저장소를 구성합니다.  

    > [!IMPORTANT]  
    > -   각 엔클로저에 두 개의 볼륨(데이터용 볼륨과 로그용 볼륨)을 만들어야 합니다.  
    > -   로그 및 데이터 디스크는 **MBR**이 아니라 **GPT**로 초기화되어야 합니다.  
    > -   두 개의 데이터 볼륨이 동일한 크기여야 합니다.  
    > -   두 개의 로그 볼륨이 동일한 크기여야 합니다.  
    > -   복제된 데이터 디스크의 섹터 크기가 모두 동일해야 합니다.  
    > -   로그 디스크의 섹터 크기가 모두 동일해야 합니다.  
    > -   로그 볼륨에서 SSD와 같은 플래시 기반 저장소를 사용해야 합니다.  로그 저장소는 데이터 저장소보다 더 빠른 것이 좋습니다. 로그 볼륨은 절대 다른 워크로드에 사용해서는 안 됩니다.
    > -   데이터 디스크에서는 HDD, SSD 또는 계층형 조합을 사용할 수 있으며, 미러링된 공간이나 패리티 공간 또는 RAID 1 또는 10, RAID 5 또는 RAID 50을 사용할 수 있습니다.  
    > -   로그 볼륨 기본적으로 8GB 이상 이어야 합니다 하 고 크거나 더 작은 로그 요구 사항에 따라 수 있습니다.
    > -   큼 표시를 NVME 또는 SSD 캐시를 사용 하 여 저장소 공간 다이렉트 (s2d) 사용할 때 보다 예상된 S2D 클러스터 간에 저장소 복제본 복제를 구성할 때 대기 시간이 증가 합니다. 대기 시간 변경 크기를 비례적으로 훨씬 보다 더 높은 성능 + 용량 구성은 HDD 계층 없음 용량 계층의 SSD 및 NVME를 사용 하는 경우 표시 합니다.

이 문제는 NVME 느린 미디어와 비교할 때 매우 짧은 대기 시간을 사용 하 여 결합 된 SR의 로그 메커니즘 내 아키텍처 제한으로 인해 발생 합니다. S2D 캐시를 사용할 때는 모든 최근 읽기/쓰기 응용 프로그램의 IO와 함께 모든 IO의 SR 로그 성능이 나 용량 계층 되지 캐시에 발생 합니다. 즉, 모든 SR 활동이 발생 같은 속도 미디어에는-이 구성은 권장 되지 지원 되지 않습니다 (참조 https://aka.ms/srfaq 로그 권장 사항에 대 한). 

Hdd를 사용 하 여 S2D를 사용 하는 경우에 사용 하지 않도록 설정 하거나 캐시를 방지할 수 없습니다. 대 안으로 SSD 및 NVME만을 사용 하는 경우, 성능과 용량 계층을 구성할 수 있습니다. 해당 구성을 사용 하 고 SR 로그는 용량 계층만 처리 하는 데이터 볼륨에만 성능 계층에 배치 하 여 위에서 설명한 높은 대기 시간 문제를 방지 합니다. 동일한 빠르고 느린 Ssd 및 NVME 없습니다 조합 하 여 수행할 수 있습니다.

이 해결 방법은 물론 이상적이 지 않습니다 및 일부 고객은 확인 하지 못할 수 있습니다 사용 합니다. SR 팀 최적화 및 발생 하는 이러한 인위적인 병목 상태를 줄이기 위해 미래에 대 한 업데이트 된 로그 메커니즘에서 작동 합니다. 이 위해 없습니다 ETA 이지만이 FAQ 테스트에 대 한 고객 탭을 사용 가능한 경우 업데이트 됩니다. 

    -   **JBOD 엔클로저:**  

        1.  각 클러스터에서 해당 사이트의 저장소 엔클로저만 볼 수 있는지, 그리고 SAS 연결이 제대로 구성되어 있는지 확인합니다.  

        2.  Windows PowerShell 또는 서버 관리자를 [사용하여 독립 실행형 서버에서 저장소 공간 배포에](https://technet.microsoft.com/library/jj822938.aspx) 제공된 **1~3단계에** 따라 저장소 공간을 사용하는 저장소를 프로비전합니다.  

    -   **Iscsi 대상 저장소:**  

        1.  각 클러스터에서 해당 사이트의 저장소 엔클로저만 볼 수 있는지 확인합니다. iSCSI를 사용하는 경우 둘 이상의 단일 네트워크 어댑터를 사용해야 합니다.  

        2.  공급업체 설명서를 사용하여 저장소를 프로비전합니다. Windows 기반 iSCSI 대상을 사용하는 경우 [iSCSI 대상 블록 저장소, 방법](https://technet.microsoft.com/library/hh848268.aspx)을 참조하세요.  

    -   **FC SAN 저장소:**  

        1.  각 서버에서 해당 사이트의 저장소 엔클로저만 볼 수 있는지, 그리고 호스트의 영역을 제대로 설정했는지 확인합니다.  

        2.  공급업체 설명서를 사용하여 저장소를 프로비전합니다.  

    -   **직접 저장소 공간:**  

        1.  저장소 공간 다이렉트를 배포하여 각 클러스터가 해당 사이트의 저장소 엔클로저만 볼 수 있게 합니다. (https://docs.microsoft.com/windows-server/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct) 

        2.  SR 로그 볼륨은 항상 가장 빠른 플래시 저장소에 있고, 데이터 볼륨은 더 느린 대용량 저장소에 있도록 합니다.

10. Windows PowerShell을 시작하고 `Test-SRTopology` cmdlet을 사용하여 모든 저장소 복제본 요구 사항을 충족하는지 확인합니다. 장기 실행 성능 평가 모드뿐만 아니라 빠른 테스트를 위해 요구 사항 전용 모드에서 cmdlet을 사용할 수 있습니다.  
예:  

   ```PowerShell
   MD c:\temp

   Test-SRTopology -SourceComputerName SR-SRV01 -SourceVolumeName f: -SourceLogVolumeName g: -DestinationComputerName SR-SRV03 -DestinationVolumeName f: -DestinationLogVolumeName g: -DurationInMinutes 30 -ResultPath c:\temp        
   ```

      > [!IMPORTANT]
      > 평가 기간 동안 지정된 원본 볼륨에 쓰기 IO 로드가 없는 테스트 서버를 사용하는 경우 워크로드를 추가하는 것이 좋습니다. 그렇지 않으면 유용한 보고서가 생성되지 않습니다. 실제 숫자와 권장 로그 크기를 확인하기 위해 프로덕션과 유사한 워크로드로 테스트해야 합니다. 또는 테스트하거나 다운로드하는 동안 일부 파일을 원본 볼륨에 복사하고 [DISKSPD](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223)를 실행하여 쓰기 IO를 생성합니다. 예를 들어 쓰기 IO 워크로드가 낮은 샘플로 D: 볼륨을 5분 동안 테스트하려면 다음을 실행합니다.  
      > `Diskspd.exe -c1g -d300 -W5 -C5 -b8k -t2 -o2 -r -w5 -h d:\test.dat`  

11. **TestSrTopologyReport.html** 보고서를 검사하여 저장소 복제본 요구 사항을 충족하는지 확인합니다.  

    ![복제 토폴로지 보고서 결과를 보여 주는 화면](./media/Cluster-to-Cluster-Storage-Replication/SRTestSRTopologyReport.png)      

## <a name="step-2-configure-two-scale-out-file-server-failover-clusters"></a>2단계: 스케일 아웃 파일 서버 장애 조치(Failover) 클러스터 구성  
이제 두 개의 정상적인 장애 조치(failover) 클러스터를 만듭니다. 구성, 유효성 검사 및 테스트 후 저장소 복제본을 사용하여 복제합니다. 아래의 모든 단계를 클러스터 노드에서 직접 수행하거나 Windows Server 2016 RSAT 관리 도구가 포함된 원격 관리 컴퓨터에서 수행할 수 있습니다.  

### <a name="graphical-method"></a>그래픽 사용  

1.  각 사이트의 노드에 대해 **cluadmin.msc**를 실행합니다.  

2.  제안된 클러스터의 유효성을 검사하고 결과를 분석하여 계속할 수 있는지 확인합니다. 아래에서 사용된 예는 **SR-SRVCLUSA** 및 **SR-SRVCLUSB**입니다.  

3.  두 개의 클러스터를 만듭니다. 클러스터 이름이 15자 이하인지 확인합니다.  

4.  파일 공유 감시 또는 클라우드 감시를 구성합니다.  

    > [!NOTE]  
    > 이제 Windows Server 2016에는 클라우드(Azure) 기반 감시 기능이 포함되어 있습니다. 파일 공유 감시 대신 이 쿼럼 옵션을 선택할 수 있습니다.  

    > [!WARNING]  
    > 쿼럼 구성에 대한 자세한 내용은 [Windows Server2012 장애 조치(failover) 클러스터에서 쿼럼 구성 및 관리](https://technet.microsoft.com/library/jj612870.aspx)에서 **감시 구성** 섹션을 참조하세요. `Set-ClusterQuorum` cmdlet에 대한 자세한 내용은 [Set-ClusterQuorum](https://technet.microsoft.com/library/hh847275.aspx)을 참조하세요.  

5.  **Redmond** 사이트의 디스크 하나를 클러스터 CSV에 추가합니다. 이렇게 하려면 **저장소** 섹션의 **디스크** 노드에서 원본 디스크를 마우스 오른쪽 단추로 클릭한 다음 **클러스터 공유 볼륨에 추가**를 클릭합니다.  

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

3.  각 클러스터에서 도메인 컨트롤러 또는 일부 다른 독립 서버에서 호스트되는 공유를 가리키는 파일 공유 감시 또는 클라우드(Azure) 감시를 구성합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

    ```PowerShell  
    Set-ClusterQuorum -FileShareWitness \\someserver\someshare  
    ```  

    > [!NOTE]  
    > 이제 Windows Server 2016에는 클라우드(Azure) 기반 감시 기능이 포함되어 있습니다. 파일 공유 감시 대신 이 쿼럼 옵션을 선택할 수 있습니다.  

    > [!WARNING]  
    > 쿼럼 구성에 대한 자세한 내용은 [Windows Server2012 장애 조치(failover) 클러스터에서 쿼럼 구성 및 관리](https://technet.microsoft.com/library/jj612870.aspx)에서 **감시 구성** 섹션을 참조하세요. `Set-ClusterQuorum` cmdlet에 대한 자세한 내용은 [Set-ClusterQuorum](https://technet.microsoft.com/library/hh847275.aspx)을 참조하세요.  

4.  [스케일 아웃 파일 서버 구성](https://technet.microsoft.com/library/hh831718.aspx)의 지침을 사용하여 두 클러스터 모두에서 클러스터된 스케일 아웃 파일 서버를 만듭니다.  

## <a name="step-3-set-up-cluster-to-cluster-replication-using-windows-powershell"></a>3단계: Windows PowerShell을 사용 하 여 클러스터 간 복제 설정  
이제 Windows PowerShell을 사용하여 클러스터 간 복제를 설정합니다. 아래의 모든 단계를 노드에서 직접 수행하거나 Windows Server 2016 RSAT 관리 도구가 포함된 원격 관리 컴퓨터에서 수행할 수 있습니다.  

1.  실행 하 여 다른 클러스터에 첫 번째 클러스터 전체 액세스 권한을 부여 합니다 **부여 SRAccess** 첫 번째 클러스터 노드의 cmdlet 또는 원격으로 합니다.  

    ```PowerShell
    Grant-SRAccess -ComputerName SR-SRV01 -Cluster SR-SRVCLUSB  
    ```  

2.  실행 하 여 다른 클러스터에 두 번째 클러스터 전체 액세스 권한을 부여 합니다 **부여 SRAccess** cmdlet은 두 번째 클러스터의 모든 노드에서 또는 원격으로.  

    ```PowerShell
    Grant-SRAccess -ComputerName SR-SRV03 -Cluster SR-SRVCLUSA  
    ```  

3.  원본 및 대상 디스크, 원본 및 대상 로그, 원본 및 대상 클러스터 이름, 로그 크기 등을 지정하여 클러스터 간 복제를 구성합니다. 서버에서 로컬로 이 명령을 수행하거나 원격 관리 컴퓨터를 사용하여 수행할 수 있습니다.  

    ```powershell  
    New-SRPartnership -SourceComputerName SR-SRVCLUSA -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\Volume2 -SourceLogVolumeName f: -DestinationComputerName SR-SRVCLUSB -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\Volume2 -DestinationLogVolumeName f:  
    ```  

    > [!WARNING]  
    > 기본 로그 크기는 8GB입니다. **Test-SRTopology** cmdlet의 결과에 따라 값이 더 높거나 낮은 **-LogSizeInBytes**를 사용할 수도 있습니다.  

4.  복제 원본 및 대상 상태를 가져오려면 다음과 같이 **Get-SRGroup** 및 **Get-SRPartnership**을 사용합니다.  

    ```powershell
    Get-SRGroup  
    Get-SRPartnership  
    (Get-SRGroup).replicas  
    ```  

5.  다음과 같이 복제 진행률을 확인합니다.  

    1.  원본 서버에서 다음 명령을 실행하고 5015, 5002, 5004, 1237, 5001 및 2200 이벤트를 확인합니다.
        
        ```PowerShell
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica -max 20
        ```
    2.  대상 서버에서 다음 명령을 실행하여 파트너 관계 생성을 표시하는 저장소 복제본 이벤트를 확인합니다. 이 이벤트는 복사한 바이트 수와 걸린 시간을 알려 줍니다. 예:  
        
        ```powershell
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | Where-Object {$_.ID -eq "1215"} | Format-List
        ```
        출력 예는 다음과 같습니다.
        
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
    3. 또는 복제본의 대상 서버 그룹은 복사할 남은 바이트 수를 알려 주며 PowerShell을 통해 쿼리할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

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

6. 대상 클러스터의 대상 서버에서 다음 명령을 실행하고 5009, 1237, 5001, 5015, 5005 및 2200 이벤트를 확인하여 처리 진행률을 이해합니다. 이 시퀀스에서는 오류 경고가 없어야 합니다. 여러 개의 1237 이벤트가 있습니다. 이는 진행률을 나타냅니다.  
    
   ```PowerShell
   Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | FL  
   ```
   > [!NOTE]  
        > 복제된 경우 대상 클러스터 디스크는 항상 **온라인(액세스 없음)** 으로 표시됩니다.  

## <a name="step-4-manage-replication"></a>4단계: 복제 관리

이제 클러스터 간 복제를 관리하고 운영합니다. 아래의 모든 단계를 클러스터 노드에서 직접 수행하거나 Windows Server 2016 RSAT 관리 도구가 포함된 원격 관리 컴퓨터에서 수행할 수 있습니다.  

1.  **Get-ClusterGroup** 또는 **장애 조치(Failover) 클러스터 관리자**를 사용하여 복제의 현재 원본과 대상 및 해당 상태를 확인합니다.  

2.  복제 성능을 측정하려면 원본 및 대상 노드 모두에서 **Get-Counter** cmdlet을 사용합니다. 카운터 이름은 다음과 같습니다.  

    -   \Storage Replica Partition I/O Statistics(*)\Number of times flush paused  

    -   \Storage Replica Partition I/O Statistics(*)\Number of pending flush I/O  

    -   \Storage Replica Partition I/O Statistics(*)\Number of requests for last log write  

    -   \Storage Replica Partition I/O Statistics(*)\Avg. Flush Queue Length  

    -   \Storage Replica Partition I/O Statistics(*)\Current Flush Queue Length  

    -   \Storage Replica Partition I/O Statistics(*)\Number of Application Write Requests  

    -   \Storage Replica Partition I/O Statistics(*)\Avg. Number of requests per log write  

    -   \Storage Replica Partition I/O Statistics(*)\Avg. App Write Latency  

    -   \Storage Replica Partition I/O Statistics(*)\Avg. App Read Latency  

    -   \Storage Replica Statistics(*)\Target RPO  

    -   \Storage Replica Statistics(*)\Current RPO  

    -   \Storage Replica Statistics(*)\Avg. Log Queue Length  

    -   \Storage Replica Statistics(*)\Current Log Queue Length  

    -   \Storage Replica Statistics(*)\Total Bytes Received  

    -   \Storage Replica Statistics(*)\Total Bytes Sent  

    -   \Storage Replica Statistics(*)\Avg. Network Send Latency  

    -   \Storage Replica Statistics(*)\Replication State  

    -   \Storage Replica Statistics(*)\Avg. Message Round Trip Latency  

    -   \Storage Replica Statistics(*)\Last Recovery Elapsed Time  

    -   \Storage Replica Statistics(*)\Number of Flushed Recovery Transactions  

    -   \Storage Replica Statistics(*)\Number of Recovery Transactions  

    -   \Storage Replica Statistics(*)\Number of Flushed Replication Transactions  

    -   \Storage Replica Statistics(*)\Number of Replication Transactions  

    -   \Storage Replica Statistics(*)\Max Log Sequence Number  

    -   \Storage Replica Statistics(*)\Number of Messages Received  

    -   \Storage Replica Statistics(*)\Number of Messages Sent  

    Windows PowerShell의 성능 카운터에 대한 자세한 내용은 [Get-Counter](https://technet.microsoft.com/library/hh849685.aspx)를 참조하세요.  

3.  하나의 사이트에서 복제 방향을 이동하려면 **Set-SRPartnership** cmdlet을 사용합니다.  

    ```PowerShell
    Set-SRPartnership -NewSourceComputerName SR-SRVCLUSB -SourceRGName rg02 -DestinationComputerName SR-SRVCLUSA -DestinationRGName rg01  
    ```  

    > [!NOTE]  
    > Windows Server 2016은 초기 동기화가 진행 중일 때 역할 전환을 방지하지 않습니다. 초기 복제를 완료할 수 있기 전에 전환하려고 하면 데이터가 손실될 수 있기 때문입니다. 초기 동기화가 완료될 때까지 방향을 강제로 전환하지 마세요.

    이벤트 로그에서 복제 방향이 변경되고 복구 모드가 발생했는지 확인한 다음 조정합니다. 그런 다음 쓰기 IO에서 새 원본 서버가 소유한 저장소에 쓸 수 있습니다. 복제 방향을 변경하면 이전 원본 컴퓨터에서 쓰기 IO가 차단됩니다.  

    > [!NOTE]  
    > 복제된 경우 대상 클러스터 디스크는 항상 **온라인(액세스 없음)** 으로 표시됩니다.  

4.  Windows Server 2016에서 로그 파일을 기본 8GB에서 변경하려면 원본 및 대상 저장소 복제본 그룹 모두에서 **Set-SRGroup**을 사용합니다.  

    > [!IMPORTANT]  
    > 기본 로그 크기는 8GB입니다. **Test-SRTopology** cmdlet의 결과에 따라 값이 더 높거나 낮은 -LogSizeInBytes를 사용할 수도 있습니다.  

5.  복제를 제거하려면 각 클러스터에서 **Get-SRGroup**, **Get-SRPartnership**, **Remove-SRGroup** 및 **Remove-SRPartnership**을 사용합니다.  

    ```powershell
    Get-SRPartnership | Remove-SRPartnership  
    Get-SRGroup | Remove-SRGroup  
    ```  

    > [!NOTE]  
    > 저장소 복제본이 대상 볼륨을 분리합니다. 이것은 의도적입니다.

## <a name="see-also"></a>참조

-   [저장소 복제본 개요](storage-replica-overview.md) 
-   [공유 저장소를 사용 하 여 확장 클러스터 복제](stretch-cluster-replication-using-shared-storage.md)  
-   [서버 간 저장소 복제](server-to-server-storage-replication.md)  
-   [저장소 복제본: 알려진된 문제](storage-replica-known-issues.md)  
-   [저장소 복제본: 질문과 대답](storage-replica-frequently-asked-questions.md)  
-   [Windows Server 2016의에서 저장소 공간 다이렉트](../storage-spaces/storage-spaces-direct-overview.md)  
