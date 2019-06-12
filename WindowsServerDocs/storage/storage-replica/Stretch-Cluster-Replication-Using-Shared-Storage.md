---
title: 공유 저장소를 사용하여 확장 클러스터 복제
ms.prod: windows-server-threshold
manager: eldenc
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 04/26/2019
ms.assetid: 6c5b9431-ede3-4438-8cf5-a0091a8633b0
ms.openlocfilehash: 9cfe587983ccce2c9f8ae0f029cf18ade7451465
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447646"
---
# <a name="stretch-cluster-replication-using-shared-storage"></a>공유 저장소를 사용하여 확장 클러스터 복제

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널)

이 평가 예제에서는 이러한 컴퓨터와 해당 저장소를 단일 확장 클러스터에서 구성합니다. 이 클러스터에서는 두 노드가 하나의 저장소 집합과 또 다른 저장소 집합을 공유한 다음 즉각적인 장애 조치(failover)가 가능하도록 복제에서 미러된 두 저장소 집합을 모두 클러스터에 유지합니다. 필수 사항은 아니지만 이러한 노드와 해당 저장소는 별도의 실제 사이트에 있어야 합니다. Hyper-V 및 파일 서버 클러스터를 샘플 시나리오로 만들기 위한 별도의 단계가 있습니다.  

> [!IMPORTANT]  
> 이 평가에서는 서로 다른 사이트의 서버가 네트워크를 통해 다른 서버와 통신할 수 있어야 하지만 다른 사이트의 공유 저장소에 실제로 연결되어 있을 필요는 없습니다. 이 시나리오에서는 저장소 공간 다이렉트를 사용하지 않습니다.  

## <a name="terms"></a>용어  
이 연습에서는 다음 환경을 예로 사용합니다.  

-   **SR-SRVCLUS**라는 단일 클러스터로 구성된 **SR-SRV01**, **SR-SRV02**, **SR-SRV03** 및 **SR-SRV04**라는 서버 4개  

-   각각 **Redmond**와 **Bellevue**라는 두 개의 데이터 센터를 나타내는 논리적 "사이트" 쌍  

> [!NOTE]  
> 각 사이트에 노드 하나씩 두 개의 노드만 사용할 수 있습니다. 그러나 두 개의 서버만으로는 사이트 간 장애 조치(failover)를 수행할 수 없습니다. 최대 64개의 노드를 사용할 수 있습니다.

![Bellevue 사이트에 있는 동일한 클러스터의 2개 노드로 복제하는 Redmond의 2개 사이트를 보여 주는 다이어그램](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_StretchClusterExample.png)  

**그림 1:  확장 클러스터의 저장소 복제**  

## <a name="prerequisites"></a>사전 요구 사항  
-   Active Directory 도메인 서비스 포리스트(Windows Server 2016을 실행하지 않아도 됨).  
-   Windows Server 2019 또는 Windows Server 2016 Datacenter Edition을 실행 하는 2-64 서버. Windows Server 2019를 실행 하는 경우 대신 사용할 수 있습니다 Standard Edition 단일 볼륨에만 복제 확인 하는 경우 최대 2TB의 크기입니다. 
-   SAS JBOD(저장소 공간 등), 파이버 채널 SAN, 공유 VHDX 또는 iSCSI 대상을 사용하는 공유 저장소 집합 2개. 저장소는 HDD 및 SSD 미디어가 혼합되고 영구 예약을 지원해야 합니다. 각 저장소 집합을 두 개의 서버에만 사용할 수 있도록 설정합니다(비대칭).  
-   각 저장소 집합에서 복제된 데이터용과 로그용으로 둘 이상의 가상 디스크를 만들 수 있어야 합니다. 실제 저장소의 섹터 크기는 모든 데이터 디스크의 섹터 크기와 동일해야 합니다. 실제 저장소의 섹터 크기는 모든 로그 디스크의 섹터 크기와 동일해야 합니다.  
-   각 서버에 하나 이상의 동기 복제용 1GbE 연결(RDMA 권장)   
-   최소 2GB의 RAM과 서버당 두 개의 코어. 더 많은 가상 컴퓨터에는 추가 메모리와 코어가 필요합니다.  
-   모든 노드 간에 ICMP, SMB(포트 445 및 SMB 다이렉트용 5445) 및 WS-MAN(포트 5985) 양방향 트래픽을 허용하는 적절한 방화벽 및 라우터 규칙  
-   동기 복제를 위해 IO 쓰기 워크로드가 포함된 충분한 대역폭 및 평균 5ms 왕복 대기 시간을 지원하는 서버 간의 네트워크. 비동기 복제에는 권장 대기 시간이 없습니다.  
-   복제된 저장소는 Windows 운영 체제 폴더가 포함된 드라이브에 있을 수 없습니다.

이러한 요구 사항은 대부분 `Test-SRTopology` cmdlet을 사용하여 확인할 수 있습니다. 하나 이상의 서버에 저장소 복제본 또는 저장소 복제 관리 도구 기능을 설치한 경우 이 도구에 액세스할 수 있습니다. 이 도구를 사용하기 위해 저장소 복제본을 구성할 필요는 없으며 cmdlet을 설치하기만 하면 됩니다. 자세한 내용은 다음 단계에 포함되어 있습니다.  

## <a name="provision-operating-system-features-roles-storage-and-network"></a>운영 체제, 기능, 역할, 저장소 및 네트워크 프로비전  

1.  데스크톱 환경 설치 옵션을 사용 하 여 Server Core 또는 서버를 사용 하 여 모든 서버 노드에 Windows Server를 설치 합니다.  
    > [!IMPORTANT]
    > 이 시점부터는 항상 모든 서버에서 기본 제공 관리자 그룹의 구성원인 도메인 사용자로 로그온합니다. 그래픽 서버 설치 또는 Windows 10 컴퓨터에서 실행할 때는 항상 PowerShell 및 명령줄 프롬프트를 관리자 권한으로 사용해야 합니다.

2.  네트워크 정보를 추가하고 노드를 도메인에 가입한 다음 다시 시작합니다.  
    > [!NOTE]
    > 이제 가이드에서는 확장 클러스터에서 사용할 두 쌍의 서버가 있다고 가정합니다. WAN 또는 LAN 네트워크는 실제 또는 논리 사이트에 속한 서버를 구분합니다. 이 가이드에서는 **SR-SRV01** 및 **SR-SRV02**는 Redmond 사이트에 있고 **SR-SRV03** 및 **SR-SRV04**는 **Bellevue** 사이트에 있는 것으로 간주합니다.  

3.  첫 번째 공유 JBOD 저장소 엔클로저, 공유 VHDX, iSCSI 대상 또는 FC SAN 집합을 **Redmond** 사이트에 연결합니다.  

4.  두 번째 저장소 집합을 **Bellevue** 사이트의 서버에 연결합니다.  

5.  필요에 따라 4개의 노드 모두에 최신 공급업체 저장소와 엔클로저 펌웨어 및 드라이버, 최신 공급업체 HBA 드라이버, 최신 공급업체 BIOS/UEFI 펌웨어, 최신 공급업체 네트워크 드라이버 및 최신 마더보드 칩셋 드라이버를 설치합니다. 필요에 따라 노드를 다시 시작합니다.  

    > [!NOTE]
    > 공유 저장소 및 네트워킹 하드웨어 구성은 하드웨어 공급업체 설명서를 참조하세요.  

6.  서버의 BIOS/UEFI 설정이 고성능을 지원하는지 확인합니다(예: C-상태 사용 안 함, QPI 속도 설정, NUMA 사용, 가장 높은 메모리 주파수 설정 등). Windows Server의 전원 관리가 고성능으로 설정되었는지 확인합니다. 필요에 따라 다시 시작합니다.  

7.  다음과 같이 역할을 구성합니다.  

    -   **그래픽 사용**  

        **ServerManager.exe**를 실행하고 **관리** 및 **서버 추가**를 클릭하여 모든 서버 노드를 추가합니다.  

        > [!IMPORTANT]
        > 각 노드에 **장애 조치(failover) 클러스터링** 및 **저장소 복제본** 역할 및 기능을 설치하고 다시 시작합니다. Hyper-V, 파일 서버 등의 다른 역할을 사용하려는 경우 이러한 역할도 지금 설치할 수 있습니다.  

    -   **Windows PowerShell 메서드를 사용 하 여**  

        **SR SRV04** 또는 원격 관리 컴퓨터의 Windows PowerShell 콘솔에서 다음 명령을 실행하여 4개의 노드에 있는 확장 클러스터에 필요한 기능 및 역할을 설치하고 다시 시작합니다.  

        ```PowerShell  
        $Servers = 'SR-SRV01','SR-SRV02','SR-SRV03','SR-SRV04'  

        $Servers | foreach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,Failover-Clustering,FS-FileServer -IncludeManagementTools -restart }  

        ```  

        이러한 단계에 대한 자세한 내용은 [역할, 역할 서비스 또는 기능 설치 또는 제거](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md)를 참조하세요.  


8. 다음과 같이 저장소를 구성합니다.  

    > [!IMPORTANT]  
    > -   각 엔클로저에 두 개의 볼륨(데이터용 볼륨과 로그용 볼륨)을 만들어야 합니다.  
    > -   로그 및 데이터 디스크는 MBR이 아니라 GPT로 초기화되어야 합니다.  
    > -   두 개의 데이터 볼륨이 동일한 크기여야 합니다.  
    > -   두 개의 로그 볼륨이 동일한 크기여야 합니다.  
    > -   복제된 데이터 디스크의 섹터 크기가 모두 동일해야 합니다.  
    > -   로그 디스크의 섹터 크기가 모두 동일해야 합니다.  
    > -   로그 볼륨은 플래시 기반 저장소 및 고성능 복원력 설정을 사용해야 합니다. 로그 저장소는 데이터 저장소보다 더 빠른 것이 좋습니다. 로그 볼륨은 절대 다른 워크로드에 사용해서는 안 됩니다. 
    > -   데이터 디스크에서는 HDD, SSD 또는 계층형 조합을 사용할 수 있으며, 미러링된 공간이나 패리티 공간 또는 RAID 1 또는 10, RAID 5 또는 RAID 50을 사용할 수 있습니다.  
    > -  로그 볼륨은 기본적으로 9GB 이상이어야 하며, 로그 요구 사항에 따라 더 크거나 작아야 할 수도 있습니다.  
    > - 볼륨은 NTFS 또는 ReFS로 포맷되어야 합니다.
    > - 파일 서버 역할은 테스트에 필요한 방화벽 포트를 여는 Test-SRTopology를 작동하는 데에만 필요합니다.  

    -   **JBOD 엔클로저:**  

        1.  각 쌍을 이루는 서버 노드 집합에서 해당 사이트의 저장소 엔클로저만(즉, 비대칭 저장소) 볼 수 있는지, 그리고 SAS 연결이 제대로 구성되어 있는지 확인합니다.  

        2.  Windows PowerShell 또는 서버 관리자를 [사용하여 독립 실행형 서버에서 저장소 공간 배포에](../storage-spaces/deploy-standalone-storage-spaces.md) 제공된 **1~3단계에** 따라 저장소 공간을 사용하는 저장소를 프로비전합니다.  

    -   **ISCSI 저장소:**  

        1.  각 쌍을 이루는 서버 노드 집합에서 해당 사이트의 저장소 엔클로저만(즉, 비대칭 저장소) 볼 수 있는지 확인합니다. iSCSI를 사용하는 경우 둘 이상의 단일 네트워크 어댑터를 사용해야 합니다.  

        2.  공급업체 설명서를 사용하여 저장소를 프로비전합니다. Windows 기반 iSCSI 대상을 사용하는 경우 [iSCSI 대상 블록 저장소, 방법](../iscsi/iscsi-target-server.md)을 참조하세요.  

    -   **FC SAN 저장소:**  

        1.  각 쌍을 이루는 서버 노드 집합에서 해당 사이트의 저장소 엔클로저만(즉, 비대칭 저장소) 볼 수 있는지, 그리고 호스트의 영역을 올바르게 설정했는지 확인합니다.  

        2.  공급업체 설명서를 사용하여 저장소를 프로비전합니다.  

## <a name="configure-a-hyper-v-failover-cluster-or-a-file-server-for-a-general-use-cluster"></a>Hyper-V 장애 조치(failover) 클러스터 또는 범용 파일 서버 클러스터 구성

서버 노드를 설정한 후에는 다음 클러스터 유형 중 하나를 만들어야 합니다.  
*  [Hyper-v 장애 조치 클러스터](#BKMK_HyperV)  
*  [범용 클러스터에 대 한 파일 서버](#BKMK_FileServer)  

### <a name="BKMK_HyperV"></a> Hyper-v 장애 조치 클러스터 구성  

>[!NOTE]
> Hyper-V 클러스터가 아니라 파일 서버 클러스터를 만들려면 이 섹션을 건너뛰고 [범용 파일 서버 클러스터 구성](#BKMK_FileServer) 섹션으로 이동하세요.  

이제 일반적인 장애 조치(failover) 클러스터를 만듭니다. 구성, 유효성 검사 및 테스트 후 저장소 복제본을 사용하여 확장합니다. 클러스터 노드에서 직접 또는 Windows Server 원격 서버 관리 도구를 포함 하는 원격 관리 컴퓨터에서 아래 단계를 모두 수행할 수 있습니다.  

#### <a name="graphical-method"></a>그래픽 사용  

1. **cluadmin.msc**를 실행합니다.  

2. 제안된 클러스터의 유효성을 검사하고 결과를 분석하여 계속할 수 있는지 확인합니다.  

   > [!NOTE]  
   > 비대칭 저장소의 사용으로 인해 클러스터 유효성 검사에서 저장소 오류가 발생합니다.  

3. Hyper-V 계산 클러스터를 만듭니다. 클러스터 이름이 15자 이하인지 확인합니다. 아래에서 사용된 예는 SR-SRVCLUS입니다. 노드가 다른 서브넷에, 하려고 하는 경우 각 서브넷에 대 한 클러스터 이름에 대 한 IP 주소 만들기 하며 "또는" 종속성을 사용 합니다.  자세한 정보를 찾을 수 있습니다 [IP 주소 구성 및 제 3 부-다중 서브넷 클러스터에 대 한 종속성](https://techcommunity.microsoft.com/t5/Failover-Clustering/Configuring-IP-Addresses-and-Dependencies-for-Multi-Subnet/ba-p/371698)합니다.  

4. 사이트 손실 시 쿼럼을 제공하도록 파일 공유 감시 또는 클라우드 감시를 구성합니다.  

   > [!NOTE]  
   > 이제 WIndows Server 클라우드 (Azure)에 대 한 옵션을 포함-미러링 모니터 서버를 기반으로 합니다. 파일 공유 감시 대신 이 쿼럼 옵션을 선택할 수 있습니다.  

   > [!WARNING]  
   > 쿼럼 구성에 대한 자세한 내용은 [Windows Server2012 장애 조치(failover) 클러스터에서 쿼럼 구성 및 관리 가이드의 감시 구성](https://technet.microsoft.com/library/jj612870.aspx)을 참조하세요. `Set-ClusterQuorum` cmdlet에 대한 자세한 내용은 [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum)을 참조하세요.  

5. [Windows Server 2012의 Hyper-V 클러스터에 대한 네트워크 권장 사항](https://technet.microsoft.com/library/dn550728.aspx)을 검토하여 클러스터 네트워킹을 가장 적절하게 구성했는지 확인합니다.  

6. Redmond 사이트의 디스크 하나를 클러스터 CSV에 추가합니다. 이렇게 하려면 **저장소** 섹션의 **디스크** 노드에서 원본 디스크를 마우스 오른쪽 단추로 클릭한 다음 **클러스터 공유 볼륨에 추가**를 클릭합니다.  

7. 클러스터가 첫 번째 테스트 사이트의 저장소를 공유하는 두 노드 내에서 정상적으로 작동하는지 확인하기 위해 [Hyper-V 클러스터 배포](https://technet.microsoft.com/library/jj863389.aspx) 가이드를 사용하여 **Redmond** 사이트 내에서 7~10단계에 따라 테스트 가상 컴퓨터만 만듭니다.  

8. 2-노드 확장 클러스터를 만드는 경우 먼저 모든 저장소를 추가해야 합니다. 이렇게 하려면 클러스터 노드에서 관리자 권한으로 PowerShell 세션을 열고 다음 명령을 실행합니다. `Get-ClusterAvailableDisk -All | Add-ClusterDisk`

   이것은 Windows Server 2016의 기본 동작입니다.

9. Windows PowerShell을 시작하고 `Test-SRTopology` cmdlet을 사용하여 모든 저장소 복제본 요구 사항을 충족하는지 확인합니다.  

    예를 들어 각각 **D:** 및 **E:** 볼륨이 있는 제안된 확장 클러스터 노드 중 2개의 유효성을 검사하고 30분 동안 테스트를 실행하려면 다음 작업을 수행합니다.
   1. 사용 가능한 모든 저장소를 **SR-SRV01**로 이동합니다.
   2. 장애 조치(Failover) 클러스터 관리자의 **역할** 섹션에서 **빈 역할 만들기**를 클릭합니다.
   3. **새 역할**이라는 빈 역할에 온라인 저장소를 추가합니다.
   4. 사용 가능한 모든 저장소를 **SR-SRV03**으로 이동합니다.
   5. 장애 조치(Failover) 클러스터 관리자의 **역할** 섹션에서 **빈 역할 만들기**를 클릭합니다.
   6. 빈 **새 역할(2)** 을 **SR-SRV03**으로 이동합니다.
   7. **새 역할(2)** 이라는 빈 역할에 온라인 저장소를 추가합니다.
   8. 드라이브 문자가 있는 모든 저장소를 탑재했으므로 이제 `Test-SRTopology`를 사용하여 클러스터를 평가할 수 있습니다.

       예를 들어 다음과 같은 가치를 제공해야 합니다.

           MD c:\temp  

           Test-SRTopology -SourceComputerName SR-SRV01 -SourceVolumeName D: -SourceLogVolumeName E: -DestinationComputerName SR-SRV03 -DestinationVolumeName D: -DestinationLogVolumeName E: -DurationInMinutes 30 -ResultPath c:\temp        

      > [!IMPORTANT]
      > 평가 기간 동안 지정된 원본 볼륨에 쓰기 IO 로드가 없는 테스트 서버를 사용하는 경우 워크로드를 추가하는 것이 좋습니다. 그렇지 않으면 Test-SRTopology에서 유용한 보고서를 생성하지 않습니다. 실제 숫자와 권장 로그 크기를 확인하기 위해 프로덕션과 유사한 워크로드로 테스트해야 합니다. 또는 테스트하거나 다운로드하는 동안 일부 파일을 원본 볼륨에 복사하고 DISKSPD를 실행하여 쓰기 IO를 생성합니다. 예를 들어 쓰기 IO 워크로드가 낮은 샘플로 D: 볼륨을 10분 동안 테스트하려면 다음을 실행합니다.   
       `Diskspd.exe -c1g -d600 -W5 -C5 -b4k -t2 -o2 -r -w5 -i100 d:\test.dat`  

10. **TestSrTopologyReport-&lt; date &gt;.html** 보고서를 검사하여 저장소 복제본 요구 사항을 충족하는지 확인하고 초기 동기화 시간 예측 및 로그 권장 사항에 주의합니다.  

      ![복제 보고서를 보여 주는 화면](./media/Stretch-Cluster-Replication-Using-Shared-Storage/SRTestSRTopologyReport.png)

11. 디스크를 사용 가능한 저장소로 되돌리고 임시 빈 역할을 제거합니다.

12. 충족되면 테스트 가상 컴퓨터를 제거합니다. 추가 평가에 필요한 모든 실제 테스트 가상 컴퓨터를 제안된 원본 노드에 추가합니다.  

13. **SR-SRV01** 및 **SR-SRV02** 서버가 **Redmond** 사이트에 있고, **SR-SRV03** 및 **SR-SRV04** 서버가 **Bellevue**에 있으며, **Redmond**가 원본 저장소 및 VM의 노드 소유권에 대한 기본 설정이 되도록 확장 클러스터 사이트 인식을 구성합니다.  

    ```PowerShell
    New-ClusterFaultDomain -Name Seattle -Type Site -Description "Primary" -Location "Seattle Datacenter"  
   
    New-ClusterFaultDomain -Name Bellevue -Type Site -Description "Secondary" -Location "Bellevue Datacenter"  
   
    Set-ClusterFaultDomain -Name sr-srv01 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv02 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv03 -Parent Bellevue  
    Set-ClusterFaultDomain -Name sr-srv04 -Parent Bellevue  

    (Get-Cluster).PreferredSite="Seattle"
    ```

    > [!NOTE]
    > Windows Server 2016에는 장애 조치(Failover) 클러스터 관리자를 사용하여 사이트 인식을 구성하는 옵션은 없습니다.  

14. **(선택 사항)** 보다 빠른 DNS 사이트 장애 조치(failover)를 위해 클러스터 네트워킹 및 Active Directory를 구성합니다. Hyper-V 소프트웨어 정의 네트워킹, 확장된 VLAN, 네트워크 추상화 장치, 낮은 DNS TTL 및 기타 일반적인 기술을 활용할 수 있습니다.

    자세한 내용은 Microsoft Ignite 세션을 검토 합니다. [Windows Server vNext에서 장애 조치 클러스터 및 저장소 복제본 사용 늘이기](http://channel9.msdn.com/Events/Ignite/2015/BRK3487) 하며 [-사이트 간에 변경 알림 사용 방법과 이유?](http://blogs.technet.com/b/qzaidi/archive/2010/09/23/enable-change-notifications-between-sites-how-and-why.aspx) 블로그 게시물.  

15. **(선택 사항)** 노드 장애 중 게스트가 장시간 일시 중지하지 않도록 VM 복원력을 구성합니다. 대신, 게스트는 10초 이내에 새 복제 원본 저장소로 장애 조치(failover)됩니다.  

    ```PowerShell  
    (Get-Cluster).ResiliencyDefaultPeriod=10  
    ```  

    > [!NOTE]
    >  Windows Server 2016에는 장애 조치(Failover) 클러스터 관리자를 사용하여 VM 복원력을 구성하는 옵션은 없습니다.  

#### <a name="windows-powershell-method"></a>Windows PowerShell 사용  

1. 제안된 클러스터를 테스트하고 결과를 분석하여 계속할 수 있는지 확인합니다.  

   ```PowerShell  
   Test-Cluster SR-SRV01, SR-SRV02, SR-SRV03, SR-SRV04  
   ```  

   > [!NOTE]
   >  비대칭 저장소의 사용으로 인해 클러스터 유효성 검사에서 저장소 오류가 발생합니다.  

2. Hyper-V 계산 클러스터를 만듭니다(클러스터에서 사용할 고유한 고정 IP 주소를 지정해야 함). 클러스터 이름이 15자 이하인지 확인합니다.  노드를 서로 다른 서브넷에 있는 경우 추가 사이트에 대 한 IP 주소 보다 만들어야 "OR" 종속성을 사용 합니다. 자세한 정보를 찾을 수 있습니다 [IP 주소 구성 및 제 3 부-다중 서브넷 클러스터에 대 한 종속성](https://techcommunity.microsoft.com/t5/Failover-Clustering/Configuring-IP-Addresses-and-Dependencies-for-Multi-Subnet/ba-p/371698)합니다.
   ```PowerShell  
   New-Cluster -Name SR-SRVCLUS -Node SR-SRV01, SR-SRV02, SR-SRV03, SR-SRV04 -StaticAddress <your IP here>  
   Add-ClusterResource -Name NewIPAddress -ResourceType “IP Address” -Group “Cluster Group”
   Set-ClusterResourceDependency -Resource “Cluster Name” -Dependency “[Cluster IP Address] or [NewIPAddress]”
   ```  

3. 클러스터에서 도메인 컨트롤러 또는 일부 다른 독립 서버에서 호스트되는 공유를 가리키는 파일 공유 감시 또는 클라우드(Azure) 감시를 구성합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

   ```PowerShell  
   Set-ClusterQuorum -FileShareWitness \\someserver\someshare  
   ```  

   > [!NOTE]
   > 이제 WIndows Server 클라우드 (Azure)에 대 한 옵션을 포함-미러링 모니터 서버를 기반으로 합니다. 파일 공유 감시 대신 이 쿼럼 옵션을 선택할 수 있습니다.  
    
   쿼럼 구성에 대한 자세한 내용은 [Windows Server2012 장애 조치(failover) 클러스터에서 쿼럼 구성 및 관리 가이드의 감시 구성](https://technet.microsoft.com/library/jj612870.aspx)을 참조하세요. `Set-ClusterQuorum` cmdlet에 대한 자세한 내용은 [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum)을 참조하세요.  

4. [Windows Server 2012의 Hyper-V 클러스터에 대한 네트워크 권장 사항](https://technet.microsoft.com/library/dn550728.aspx)을 검토하여 클러스터 네트워킹을 가장 적절하게 구성했는지 확인합니다.  

5. 2-노드 확장 클러스터를 만드는 경우 먼저 모든 저장소를 추가해야 합니다. 이렇게 하려면 클러스터 노드에서 관리자 권한으로 PowerShell 세션을 열고 다음 명령을 실행합니다. `Get-ClusterAvailableDisk -All | Add-ClusterDisk`

   이것은 Windows Server 2016의 기본 동작입니다.

6. 클러스터가 첫 번째 테스트 사이트의 저장소를 공유하는 두 노드 내에서 정상적으로 작동하는지 확인하기 위해 [Hyper-V 클러스터 배포](https://technet.microsoft.com/library/jj863389.aspx) 가이드를 사용하여 **Redmond** 사이트 내에서 7~10단계에 따라 테스트 가상 컴퓨터만 만듭니다.  

7. 충족되면 테스트 VM을 제거합니다. 추가 평가에 필요한 모든 실제 테스트 가상 컴퓨터를 제안된 원본 노드에 추가합니다.  

8. **SR-SRV01** 및 **SR-SRV02** 서버가 **Redmond** 사이트에 있고, **SR-SRV03** 및 **SR-SRV04** 서버가 **Bellevue**에 있으며, **Redmond**가 원본 저장소 및 가상 컴퓨터의 노드 소유권에 대한 기본 설정이 되도록 확장 클러스터 사이트 인식을 구성합니다.  

   ```PowerShell  
   New-ClusterFaultDomain -Name Seattle -Type Site -Description "Primary" -Location "Seattle Datacenter"  

   New-ClusterFaultDomain -Name Bellevue -Type Site -Description "Secondary" -Location "Bellevue Datacenter"  

   Set-ClusterFaultDomain -Name sr-srv01 -Parent Seattle  
   Set-ClusterFaultDomain -Name sr-srv02 -Parent Seattle  
   Set-ClusterFaultDomain -Name sr-srv03 -Parent Bellevue  
   Set-ClusterFaultDomain -Name sr-srv04 -Parent Bellevue  

   (Get-Cluster).PreferredSite="Seattle"  
   ```  

9. **(선택 사항)** 보다 빠른 DNS 사이트 장애 조치(failover)를 위해 클러스터 네트워킹 및 Active Directory를 구성합니다. Hyper-V 소프트웨어 정의 네트워킹, 확장된 VLAN, 네트워크 추상화 장치, 낮은 DNS TTL 및 기타 일반적인 기술을 활용할 수 있습니다.  

   자세한 내용은 Microsoft Ignite 세션을 검토 합니다. [Windows Server vNext에서 장애 조치 클러스터 및 저장소 복제본 사용 늘이기](http://channel9.msdn.com/Events/Ignite/2015/BRK3487) 하 고 [-사이트 간에 변경 알림 사용 방법과 이유](http://blogs.technet.com/b/qzaidi/archive/2010/09/23/enable-change-notifications-between-sites-how-and-why.aspx)합니다.  

10. **(선택 사항)** 노드 장애 중 게스트가 장시간 일시 중지하지 않도록 VM 복원력을 구성합니다. 대신, 게스트는 10초 이내에 새 복제 원본 저장소로 장애 조치(failover)됩니다.  

    ```PowerShell  
    (Get-Cluster).ResiliencyDefaultPeriod=10  
    ```  

    > [!NOTE]  
    > Windows Server 2016에는 장애 조치(Failover) 클러스터 관리자를 사용하여 VM 복원력을 구성하는 옵션은 없습니다.  



### <a name="BKMK_FileServer"></a> 파일 서버를 일반 클러스터 구성  

>[!NOTE]
> [Hyper-V 장애 조치(failover) 클러스터 구성](#BKMK_HyperV)에 설명된 대로 Hyper-V 장애 조치(failover) 클러스터를 이미 구성한 경우에는 이 섹션을 건너뜁니다.  

이제 일반적인 장애 조치(failover) 클러스터를 만듭니다. 구성, 유효성 검사 및 테스트 후 저장소 복제본을 사용하여 확장합니다. 클러스터 노드에서 직접 또는 Windows Server 원격 서버 관리 도구를 포함 하는 원격 관리 컴퓨터에서 아래 단계를 모두 수행할 수 있습니다.  

#### <a name="graphical-method"></a>그래픽 사용  

1. cluadmin.msc를 실행합니다.  

2. 제안된 클러스터의 유효성을 검사하고 결과를 분석하여 계속할 수 있는지 확인합니다.  
   >[!NOTE]
   >비대칭 저장소의 사용으로 인해 클러스터 유효성 검사에서 저장소 오류가 발생합니다.   
3. 범용 파일 서버 저장소 클러스터를 만듭니다. 클러스터 이름이 15자 이하인지 확인합니다. 아래에서 사용된 예는 SR-SRVCLUS입니다.  노드가 다른 서브넷에, 하려고 하는 경우 각 서브넷에 대 한 클러스터 이름에 대 한 IP 주소 만들기 하며 "또는" 종속성을 사용 합니다.  자세한 정보를 찾을 수 있습니다 [IP 주소 구성 및 제 3 부-다중 서브넷 클러스터에 대 한 종속성](https://techcommunity.microsoft.com/t5/Failover-Clustering/Configuring-IP-Addresses-and-Dependencies-for-Multi-Subnet/ba-p/371698)합니다.  

4. 사이트 손실 시 쿼럼을 제공하도록 파일 공유 감시 또는 클라우드 감시를 구성합니다.  
   >[!NOTE]
   > 이제 WIndows Server 클라우드 (Azure)에 대 한 옵션을 포함-미러링 모니터 서버를 기반으로 합니다. 파일 공유 감시 대신 이 쿼럼 옵션을 선택할 수 있습니다.                                                                                                                                                                             
   >[!NOTE]
   >  쿼럼 구성에 대한 자세한 내용은 [Windows Server2012 장애 조치(failover) 클러스터에서 쿼럼 구성 및 관리 가이드의 감시 구성](https://technet.microsoft.com/library/jj612870.aspx)을 참조하세요. Set-ClusterQuorum cmdlet에 대한 자세한 내용은 [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum)을 참조하세요. 

5. 2-노드 확장 클러스터를 만드는 경우 먼저 모든 저장소를 추가해야 합니다. 이렇게 하려면 클러스터 노드에서 관리자 권한으로 PowerShell 세션을 열고 다음 명령을 실행합니다. `Get-ClusterAvailableDisk -All | Add-ClusterDisk`

   이것은 Windows Server 2016의 기본 동작입니다.

6. 클러스터 네트워킹을 가장 적절하게 구성했는지 확인합니다.  
    >[!NOTE]
    > 다음 단계를 계속 진행하기 전에 모든 노드에서 파일 서버 역할을 설치해야 합니다.   |  

7. **역할** 아래에서 **역할 구성**을 클릭합니다. **시작하기 전**을 검토하고 **다음**을 클릭합니다.  

8. **파일 서버**를 선택하고 **다음**을 클릭합니다.  

9. **범용 파일 서버**를 선택된 상태로 두고 **다음**을 클릭합니다.  

10. **클라이언트 액세스 지점** 이름(15자 이하)을 입력하고 **다음**을 클릭합니다.  

11. 데이터 볼륨으로 사용할 디스크를 선택하고 **다음**을 클릭합니다.  

12. 설정을 검토하고 **다음**을 클릭합니다. **마침**을 클릭합니다.  

13. 새 파일 서버 역할을 마우스 오른쪽 단추로 클릭한 다음 **파일 공유 추가**를 클릭합니다. 계속해서 마법사를 통해 공유를 구성합니다.  

14. 선택 사항: 이 사이트에서 다른 저장소를 사용 하는 다른 파일 서버 역할을 추가 합니다.  

15. SR-SRV01 및 SR-SRV02 서버가 Redmond 사이트에 있고, SR-SRV03 및 SR-SRV04 서버가 Bellevue에 있으며, Redmond가 원본 저장소 및 VM의 노드 소유권에 대한 기본 설정이 되도록 확장 클러스터 사이트 인식을 구성합니다.  

    ```PowerShell  
    New-ClusterFaultDomain -Name Seattle -Type Site -Description "Primary" -Location "Seattle Datacenter"  

    New-ClusterFaultDomain -Name Bellevue -Type Site -Description "Secondary" -Location "Bellevue Datacenter"  

    Set-ClusterFaultDomain -Name sr-srv01 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv02 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv03 -Parent Bellevue  
    Set-ClusterFaultDomain -Name sr-srv04 -Parent Bellevue  

    (Get-Cluster).PreferredSite="Seattle"  
    ```  

      >[!NOTE]
      > Windows Server 2016에는 장애 조치(Failover) 클러스터 관리자를 사용하여 사이트 인식을 구성하는 옵션은 없습니다.  

16. (선택 사항) 보다 빠른 DNS 사이트 장애 조치(failover)를 위해 클러스터 네트워킹 및 Active Directory를 구성합니다. 확장된 VLAN, 네트워크 추상화 장치, 낮은 DNS TTL 및 기타 일반적인 기술을 활용할 수 있습니다.  

자세한 내용은 Microsoft Ignite 세션 [Windows Server vNext에서 장애 조치(Failover) 클러스터 확장 및 저장소 복제본 사용](http://channel9.msdn.com/events/ignite/2015/brk3487) 및 블로그 게시물 [사이트 간에 변경 알림 사용 - 방법과 이유](http://blogs.technet.com/b/qzaidi/archive/2010/09/23/enable-change-notifications-between-sites-how-and-why.aspx)를 참조하세요.    

#### <a name="powershell-method"></a>PowerShell 사용

1. 제안된 클러스터를 테스트하고 결과를 분석하여 계속할 수 있는지 확인합니다.    

    ```PowerShell
    Test-Cluster SR-SRV01, SR-SRV02, SR-SRV03, SR-SRV04
    ```

    > [!NOTE]
    >  비대칭 저장소의 사용으로 인해 클러스터 유효성 검사에서 저장소 오류가 발생합니다.   

2.  Hyper-V 계산 클러스터를 만듭니다(클러스터에서 사용할 고유한 고정 IP 주소를 지정해야 함). 클러스터 이름이 15자 이하인지 확인합니다.  노드를 서로 다른 서브넷에 있는 경우 추가 사이트에 대 한 IP 주소 보다 만들어야 "OR" 종속성을 사용 합니다. 자세한 정보를 찾을 수 있습니다 [IP 주소 구성 및 제 3 부-다중 서브넷 클러스터에 대 한 종속성](https://techcommunity.microsoft.com/t5/Failover-Clustering/Configuring-IP-Addresses-and-Dependencies-for-Multi-Subnet/ba-p/371698)합니다.  

    ```PowerShell
    New-Cluster -Name SR-SRVCLUS -Node SR-SRV01, SR-SRV02, SR-SRV03, SR-SRV04 -StaticAddress <your IP here> 

    Add-ClusterResource -Name NewIPAddress -ResourceType “IP Address” -Group “Cluster Group”

    Set-ClusterResourceDependency -Resource “Cluster Name” -Dependency “[Cluster IP Address] or [NewIPAddress]”
    ```


3. 클러스터에서 도메인 컨트롤러 또는 일부 다른 독립 서버에서 호스트되는 공유를 가리키는 파일 공유 감시 또는 클라우드(Azure) 감시를 구성합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

    ```PowerShell
    Set-ClusterQuorum -FileShareWitness \\someserver\someshare
    ```

    >[!NOTE]
    > Windows Server는 이제 Azure를 사용 하 여 클라우드 감시에 대 한 옵션을 포함 합니다. 파일 공유 감시 대신 이 쿼럼 옵션을 선택할 수 있습니다.  

   쿼럼 구성에 대 한 자세한 내용은 참조는 [이해 클러스터 및 풀 쿼럼을](../storage-spaces/understand-quorum.md)합니다. Set-ClusterQuorum cmdlet에 대한 자세한 내용은 [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum)을 참조하세요.

4.  2-노드 확장 클러스터를 만드는 경우 먼저 모든 저장소를 추가해야 합니다. 이렇게 하려면 클러스터 노드에서 관리자 권한으로 PowerShell 세션을 열고 다음 명령을 실행합니다. `Get-ClusterAvailableDisk -All | Add-ClusterDisk`

    이것은 Windows Server 2016의 기본 동작입니다.

5. 클러스터 네트워킹을 가장 적절하게 구성했는지 확인합니다.  

6.  파일 서버 역할을 구성합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

    ```PowerShell  
    Get-ClusterResource  
    Add-ClusterFileServerRole -Name SR-CLU-FS2 -Storage "Cluster Disk 4"  

    MD e:\share01  

    New-SmbShare -Name Share01 -Path f:\share01 -ContinuouslyAvailable $false  
    ```

7. SR-SRV01 및 SR-SRV02 서버가 Redmond 사이트에 있고, SR-SRV03 및 SR-SRV04 서버가 Bellevue에 있으며, Redmond가 원본 저장소 및 가상 컴퓨터의 노드 소유권에 대한 기본 설정이 되도록 확장 클러스터 사이트 인식을 구성합니다.  

    ```PowerShell
    New-ClusterFaultDomain -Name Seattle -Type Site -Description "Primary" -Location "Seattle Datacenter"  

    New-ClusterFaultDomain -Name Bellevue -Type Site -Description "Secondary" -Location "Bellevue Datacenter"  

    Set-ClusterFaultDomain -Name sr-srv01 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv02 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv03 -Parent Bellevue  
    Set-ClusterFaultDomain -Name sr-srv04 -Parent Bellevue  

    (Get-Cluster).PreferredSite="Seattle"  
    ```

8.  (선택 사항) 보다 빠른 DNS 사이트 장애 조치(failover)를 위해 클러스터 네트워킹 및 Active Directory를 구성합니다. 확장된 VLAN, 네트워크 추상화 장치, 낮은 DNS TTL 및 기타 일반적인 기술을 활용할 수 있습니다.  
    
    자세한 내용은 Microsoft Ignite 세션 [Windows Server vNext에서 장애 조치(Failover) 클러스터 확장 및 저장소 복제본 사용](http://channel9.msdn.com/events/ignite/2015/brk3487) 및 블로그 게시물 [사이트 간에 변경 알림 사용 - 방법과 이유](http://blogs.technet.com/b/qzaidi/archive/2010/09/23/enable-change-notifications-between-sites-how-and-why.aspx)를 참조하세요.

### <a name="configure-a-stretch-cluster"></a>확장 클러스터를 구성합니다.  
이제 장애 조치(Failover) 클러스터 관리자 또는 Windows PowerShell을 사용하여 확장 클러스터를 구성합니다. 클러스터 노드에서 직접 또는 Windows Server 원격 서버 관리 도구를 포함 하는 원격 관리 컴퓨터에서 아래 단계를 모두 수행할 수 있습니다.  

#### <a name="failover-cluster-manager-method"></a>장애 조치(failover) 클러스터 관리자 사용  

1.  Hyper-V 워크로드의 경우 복제할 데이터가 있는 하나의 노드에서 사용 가능한 디스크의 원본 데이터 디스크를 클러스터 공유 볼륨에 추가합니다(아직 구성하지 않은 경우). 모든 디스크를 추가해서는 안 됩니다. 단일 디스크만 추가하세요. 이는 비대칭 저장소이므로 이 시점부터는 절반의 디스크가 오프라인 상태로 표시됩니다.  
범용 파일 서버와 같은 PDR(실제 디스크 리소스) 워크로드를 복제하는 경우 역할 연결 디스크가 이미 준비되어 있습니다.  

    ![장애 조치(Failover) 클러스터 관리자를 보여 주는 화면](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_OnlineDisks2.png)  

2.  CSV 디스크 또는 역할 연결 디스크를 마우스 오른쪽 단추로 클릭하고 **복제**를 클릭한 다음 **사용**을 클릭합니다.  

3.  적절한 대상 데이터 볼륨을 선택하고 **다음**을 클릭합니다. 표시되는 대상 디스크에 선택한 원본 디스크와 같은 크기의 볼륨이 생성됩니다. 이러한 마법사 대화 상자 간에 이동할 때 사용 가능한 저장소가 자동으로 이동하며 필요에 따라 백그라운드에서 온라인 상태로 전환됩니다.  

    ![저장소 복제본 구성 마법사의 대상 디스크 선택 페이지를 보여 주는 화면](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_SelectDestinationDataDisk2.png)  

4.  적절한 원본 로그 디스크를 선택하고 **다음**을 클릭합니다. 원본 로그 볼륨은 회전 디스크가 아니라 SSD 또는 유사한 속도의 미디어를 사용하는 디스크에 있어야 합니다.  

5.  적절한 대상 로그 볼륨을 선택하고 다음을 클릭합니다. 표시되는 대상 로그 디스크에 선택한 원본 로그 디스크 볼륨과 같은 크기의 볼륨이 생성됩니다.  

6.  원본 서버의 이전 데이터 복사본이 대상 볼륨에 없는 경우 **대상 볼륨 덮어쓰기**에서 **볼륨 덮어쓰기** 값을 그대로 둡니다. 대상에 유사한 데이터가 없는 경우 최근 백업 또는 이전 복제에서 **시드된 대상 디스크**를 선택하고 **다음**을 클릭합니다.  

7.  RPO가 0인 복제를 사용하려는 경우 **동기 복제**에서 **복제 모드** 값을 그대로 둡니다. 대기 시간이 더 높은 네트워크로 클러스터를 확장할 계획이거나 기본 사이트 노드에 더 낮은 IO 대기 시간이 필요한 경우 **비동기 복제**로 변경합니다.  
8.  나중에 복제 그룹의 추가 디스크 쌍에서 쓰기 순서 지정을 사용하지 않으려는 경우 **최고 성능**에서 **일관성 그룹** 값을 그대로 둡니다. 이 복제 그룹에 디스크를 더 추가할 계획이고 보장된 쓰기 순서 지정이 필요한 경우 **쓰기 순서 지정 사용**을 선택하고 **다음**을 클릭합니다.  

9.  **다음**을 클릭하여 복제 및 확장 클러스터 형성을 구성합니다.  

    ![저장소 복제본 구성 마법사의 확인 선택 페이지를 보여 주는 화면](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_ConfigureSR2.png)  

10. 요약 화면에서 완료 대화 상자 결과를 확인합니다. 웹 브라우저에서 보고서를 볼 수 있습니다.  

11. 이제 절반의 두 클러스터 간에 저장소 복제본 파트너 관계를 구성했지만 복제는 계속 진행 중입니다. 그래픽 도구를 통해 복제 상태를 볼 수 있는 여러 가지 방법이 있습니다.  

    1.  **복제 역할** 열 및 **복제** 탭을 사용합니다. 초기 동기화를 마치면 원본 및 대상 디스크의 복제 상태가 **지속적으로 복제 중**으로 전환됩니다.   

        ![장애 조치(Failover) 클러스터 관리자에서 디스크의 복제 탭을 보여 주는 화면](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_ReplicationDetails2.png)  

    2.  **eventvwr.exe**를 시작합니다.  

        1.  원본 서버에서 **응용 프로그램 및 서비스\Microsoft\Windows\저장소 복제본\관리**로 이동하여 이벤트 5015, 5002, 5004, 1237, 5001 및 2200을 검토합니다.  

        2.  대상 서버에서 **응용 프로그램 및 서비스\Microsoft\Windows\저장소 복제본\운영**으로 이동하여 이벤트 1215를 기다립니다. 이 이벤트는 복사한 바이트 수와 걸린 시간을 알려 줍니다. 예:  

            ```  
            Log Name:      Microsoft-Windows-StorageReplica/Operational  
            Source:        Microsoft-Windows-StorageReplica  
            Date:          4/6/2016 4:52:23 PM  
            Event ID:      1215  
            Task Category: (1)  
            Level:         Information  
            Keywords:      (1)  
            User:          SYSTEM  
            Computer:      SR-SRV03.Threshold.nttest.microsoft.com  
            Description:  
            Block copy completed for replica.  

            ReplicationGroupName: Replication 2  
            ReplicationGroupId: {c6683340-0eea-4abc-ab95-c7d0026bc054}  
            ReplicaName: \\?\Volume{43a5aa94-317f-47cb-a335-2a5d543ad536}\  
            ReplicaId: {00000000-0000-0000-0000-000000000000}  
            End LSN in bitmap:   
            LogGeneration: {00000000-0000-0000-0000-000000000000}  
            LogFileId: 0  
            CLSFLsn: 0xFFFFFFFF  
            Number of Bytes Recovered: 68583161856  
            Elapsed Time (ms): 140  
            ```  

        3.  대상 서버에서 **응용 프로그램 및 서비스\Microsoft\Windows\저장소 복제본\관리**로 이동하여 이벤트 5009, 1237, 5001, 5015, 5005 및 2200을 통해 진행 상황을 파악합니다. 이 시퀀스에서는 오류 경고가 없어야 합니다. 여러 개의 1237 이벤트가 있습니다. 이는 진행률을 나타냅니다.  

            > [!WARNING]
            > 초기 동기화가 완료될 때까지 CPU 및 메모리 사용량이 평소보다 높을 수 있습니다.  

#### <a name="windows-powershell-method"></a>Windows PowerShell 사용  

1.  Powershell 콘솔이 관리자 권한이 있는 관리자 계정으로 실행되고 있는지 확인합니다.  
2.  원본 데이터 저장소만 클러스터에 CSV로 추가합니다. 사용 가능한 디스크의 크기, 파티션 및 볼륨 레이아웃을 가져오려면 다음 명령을 사용합니다.  

    ```PowerShell  
    Move-ClusterGroup -Name "available storage" -Node sr-srv01  

    $DiskResources = Get-ClusterResource | Where-Object { $_.ResourceType -eq 'Physical Disk' -and $_.State -eq 'Online' }  
    $DiskResources | foreach {  
        $resource = $_  
        $DiskGuidValue = $resource | Get-ClusterParameter DiskIdGuid  

        Get-Disk | where { $_.Guid -eq $DiskGuidValue.Value } | Get-Partition | Get-Volume |  
            Select @{N="Name"; E={$resource.Name}}, @{N="Status"; E={$resource.State}}, DriveLetter, FileSystemLabel, Size, SizeRemaining  
    } | FT -AutoSize  

    Move-ClusterGroup -Name "available storage" -Node sr-srv03  

    $DiskResources = Get-ClusterResource | Where-Object { $_.ResourceType -eq 'Physical Disk' -and $_.State -eq 'Online' }  
    $DiskResources | foreach {  
        $resource = $_  
        $DiskGuidValue = $resource | Get-ClusterParameter DiskIdGuid  

        Get-Disk | where { $_.Guid -eq $DiskGuidValue.Value } | Get-Partition | Get-Volume |  
            Select @{N="Name"; E={$resource.Name}}, @{N="Status"; E={$resource.State}}, DriveLetter, FileSystemLabel, Size, SizeRemaining  
    } | FT -AutoSize  
    ```  

4.  다음을 사용하여 올바른 디스크를 CSV로 설정합니다.  

    ```PowerShell  
    Add-ClusterSharedVolume -Name "Cluster Disk 4"  
    Get-ClusterSharedVolume  
    Move-ClusterSharedVolume -Name "Cluster Disk 4" -Node sr-srv01  
    ```  

5.  다음을 지정하여 확장 클러스터를 구성합니다.  

    -   원본 및 대상 노드(원본 데이터만 CSV 디스크이고 다른 모든 디스크는 CSV 디스크가 아님)  

    -   원본 및 대상 복제 그룹 이름  

    -   원본 및 대상 디스크(파티션 크기가 일치함)  

    -   원본 및 대상 로그 볼륨(두 디스크 모두에 로그 크기를 수용할 수 있는 충분한 여유 공간이 있고 저장소가 SSD 또는 이와 유사한 속도의 미디어임)  

    -   원본 및 대상 로그 볼륨(두 디스크 모두에 로그 크기를 수용할 수 있는 충분한 여유 공간이 있고 저장소가 SSD 또는 이와 유사한 속도의 미디어임)  

    -   로그 크기  

    -   원본 로그 볼륨은 회전 디스크가 아니라 SSD 또는 유사한 속도의 미디어를 사용하는 디스크에 있어야 합니다.  

    ```PowerShell  
    New-SRPartnership -SourceComputerName sr-srv01 -SourceRGName rg01 -SourceVolumeName "C:\ClusterStorage\Volume1" -SourceLogVolumeName e: -DestinationComputerName sr-srv03 -DestinationRGName rg02 -DestinationVolumeName d: -DestinationLogVolumeName e:  
    ```  

    > [!NOTE]  
    > 한 번에 모두 만드는 대신 각 사이트의 한 노드에서 `New-SRGroup` 및 `New-SRPartnership`을 사용하여 단계별로 복제를 만들 수도 있습니다.  

6.  복제 진행률을 확인합니다.  

    1.  원본 서버에서 다음 명령을 실행하고 5015, 5002, 5004, 1237, 5001 및 2200 이벤트를 확인합니다.  

        ```PowerShell  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica -max 20  
        ```  

    2.  대상 서버에서 다음 명령을 실행하여 파트너 관계 생성을 표시하는 저장소 복제본 이벤트를 확인합니다. 이 이벤트는 복사한 바이트 수와 걸린 시간을 알려 줍니다. 예:  

            Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | Where-Object {$_.ID -eq "1215"} | fl  

            TimeCreated  : 4/6/2016 4:52:23 PM  
            ProviderName : Microsoft-Windows-StorageReplica  
            Id           : 1215  
            Message      : Block copy completed for replica.  

               ReplicationGroupName: Replication 2  
               ReplicationGroupId: {c6683340-0eea-4abc-ab95-c7d0026bc054}  
               ReplicaName: ?Volume{43a5aa94-317f-47cb-a335-2a5d543ad536}  
               ReplicaId: {00000000-0000-0000-0000-000000000000}  
               End LSN in bitmap:   
               LogGeneration: {00000000-0000-0000-0000-000000000000}  
               LogFileId: 0  
               CLSFLsn: 0xFFFFFFFF  
               Number of Bytes Recovered: 68583161856  
               Elapsed Time (ms): 140  

    3.  대상 서버에서 다음 명령을 실행하고 5009, 1237, 5001, 5015, 5005 및 2200 이벤트를 확인하여 처리 진행률을 이해합니다. 이 시퀀스에서는 오류 경고가 없어야 합니다. 여러 개의 1237 이벤트가 있습니다. 이는 진행률을 나타냅니다.  

        ```PowerShell  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | FL  
        ```  

    4.  또는 복제본의 대상 서버 그룹은 복사할 남은 바이트 수를 알려 주며 PowerShell을 통해 쿼리할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

        ```PowerShell  
        (Get-SRGroup).Replicas | Select-Object numofbytesremaining  
        ```  

        진행률 샘플(종료되지 않음):  

        ```PowerShell  
        while($true) {  

         $v = (Get-SRGroup -Name "Replication 2").replicas | Select-Object numofbytesremaining  
         [System.Console]::Write("Number of bytes remaining: {0}`r", $v.numofbytesremaining)  
         Start-Sleep -s 5  
        }  
        ```  

7.  확장 클러스터 내에서 복제 원본 및 대상 상태를 가져오려면 `Get-SRGroup` 및 `Get-SRPartnership`을 사용하여 확장 클러스터에서 구성된 복제 상태를 확인합니다.  

    ```PowerShell  
    Get-SRGroup  
    Get-SRPartnership  
    (Get-SRGroup).replicas  
    ```  

### <a name="manage-stretched-cluster-replication"></a>확장 클러스터 복제 관리  
이제 확장 클러스터를 관리하고 운영합니다. 클러스터 노드에서 직접 또는 Windows Server 원격 서버 관리 도구를 포함 하는 원격 관리 컴퓨터에서 아래 단계를 모두 수행할 수 있습니다.  

#### <a name="graphical-tools-method"></a>그래픽 도구 사용  

1.  장애 조치(Failover) 클러스터 관리자를 사용하여 복제의 현재 원본과 대상 및 해당 상태를 확인합니다.  

2.  복제 성능을 측정하려면 원본 및 대상 노드 모두에서 **Perfmon.exe**를 실행합니다.  

    1.  대상 노드에서 다음을 수행합니다.  

        1.  데이터 볼륨에 대한 모든 성능 카운터가 포함된 **저장소 복제본 통계** 개체를 추가합니다.  

        2.  결과를 확인합니다.  

    2.  원본 노드에서 다음을 수행합니다.  

        1.  데이터 볼륨에 대한 모든 성능 카운터가 포함된 **저장소 복제본 통계** 및 **저장소 복제본 파티션 I/O 통계** 개체를 추가합니다(후자는 현재 원본 서버의 데이터에만 사용할 수 있음).  

        2.  결과를 확인합니다.  

3.  확장 클러스터 내에서 복제 원본 및 대상을 변경하려면 다음 방법을 사용합니다.  

    1.  동일한 사이트의 노드 간에 원본 복제를 이동하려면 원본 CSV를 마우스 오른쪽 단추로 클릭하고 **저장소 이동**, **노드 선택**을 차례로 클릭한 다음 동일한 사이트에 있는 노드를 선택합니다. 역할 할당 디스크에 CSV가 아닌 저장소를 사용하는 경우 역할을 이동합니다.  

    2.  사이트 간에 원본 복제를 이동하려면 원본 CSV를 마우스 오른쪽 단추로 클릭하고 **저장소 이동**, **노드 선택**을 차례로 클릭한 다음 다른 사이트에 있는 노드를 선택합니다. 기본 설정 사이트를 구성한 경우 가장 적합한 노드를 사용하여 언제든지 원본 저장소를 기본 설정 사이트의 노드로 이동할 수 있습니다. 역할 할당 디스크에 CSV가 아닌 저장소를 사용하는 경우 역할을 이동합니다.  

    3.  사이트 간에 계획된 복제 방향 장애 조치(failover)를 수행하려면 **ServerManager.exe** 또는 **SConfig**를 사용하여 하나의 사이트에서 두 노드를 모두 종료합니다.  

    4.  사이트 간에 계획되지 않은 복제 방향 장애 조치(failover)를 수행하려면 하나의 사이트에서 두 노드 모두에 대한 전원을 차단합니다.  

        > [!NOTE]
        > Windows Server 2016에서는 노드가 온라인 상태로 다시 전환된 후 장애 조치(Failover) 클러스터 관리자 또는 Move-ClusterGroup을 사용하여 대상 디스크를 다른 사이트로 수동으로 이동해야 할 수도 있습니다.  

        > [!NOTE]
        > 저장소 복제본이 대상 볼륨을 분리합니다. 이것은 의도적입니다.  

4.  로그 크기를 기본 8GB에서에서 변경, 원본 및 대상 로그 디스크를 마우스 오른쪽 단추로 클릭 한 다음 클릭 하 여 **복제 로그** 탭을 선택한 후에 맞게 두 디스크의 크기를 변경 합니다.  

    > [!NOTE]  
    > 기본 로그 크기는 8GB입니다. `Test-SRTopology` cmdlet의 결과에 따라 값이 더 높거나 낮은 `-LogSizeInBytes`를 사용할 수도 있습니다.  

5.  또 다른 쌍의 복제된 디스크를 기존 복제 그룹에 추가하려면 사용 가능한 저장소에 하나 이상의 추가 디스크가 있는지 확인해야 합니다. 그런 다음 원본 디스크를 마우스 오른쪽 단추로 클릭하고 **복제 파트너 관계 추가**를 선택할 수 있습니다.  
    > [!NOTE]  
    > 사용 가능한 저장소에 추가 '더미' 디스크가 필요한 이유는 회귀 때문이며 의도적인 것이 아닙니다. 장애 조치(Failover) 클러스터 관리자는 이전에 디스크 추가를 정상적으로 지원했으며, 이후 릴리스에서도 지원할 예정입니다.  


6.  기존 복제를 제거하려면 다음을 수행합니다.  

    1.  **cluadmin.msc**를 시작합니다.  

    2.  원본 CSV 디스크를 마우스 오른쪽 단추로 클릭하고 **복제**를 클릭한 다음 **제거**를 클릭합니다. 경고 메시지를 수락합니다.  

    3.  필요에 따라 추가 테스트를 위해 CSV에서 저장소를 제거하고 사용 가능한 저장소로 반환합니다.  

        > [!NOTE]  
        > 사용 가능한 저장소로 반환한 후 **DiskMgmt.msc** 또는 **ServerManager.exe**를 사용하여 볼륨에 드라이브 문자를 다시 추가해야 할 수도 있습니다.  

#### <a name="windows-powershell-method"></a>Windows PowerShell 사용  

1.  **Get-SRGroup** 및 **(Get-SRGroup).Replicas**를 사용하여 복제의 현재 원본과 대상 및 해당 상태를 확인합니다.  

2.  복제 성능을 측정하려면 원본 및 대상 노드 모두에서 `Get-Counter` cmdlet을 사용합니다. 카운터 이름은 다음과 같습니다.  

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

    Windows PowerShell의 성능 카운터에 대한 자세한 내용은 [Get-Counter](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Diagnostics/Get-Counter)를 참조하세요.  

3.  확장 클러스터 내에서 복제 원본 및 대상을 변경하려면 다음 방법을 사용합니다.  

    1.  **Redmond** 사이트에서 노드 간에 복제 원본을 이동하려면 Move-ClusterSharedVolume cmdlet을 사용하여 CSV 리소스를 이동합니다.  

        ```PowerShell  
        Get-ClusterSharedVolume | fl *  
        Move-ClusterSharedVolume -Name "cluster disk 4" -Node sr-srv02  
        ```  

    2.  "계획된" 대로 사이트 간에 복제 방향을 이동하려면 **Move-ClusterSharedVolume** cmdlet을 사용하여 CSV 리소스를 이동합니다.  

        ```PowerShell 
        Get-ClusterSharedVolume | fl *  
        Move-ClusterSharedVolume -Name "cluster disk 4" -Node sr-srv04  
        ```  

        다른 사이트 및 노드에 적절하게 로그 및 데이터도 함께 이동합니다.  

    3.  사이트 간에 계획되지 않은 복제 방향 장애 조치(failover)를 수행하려면 하나의 사이트에서 두 노드 모두에 대한 전원을 차단합니다.  

        > [!NOTE]  
        > 저장소 복제본이 대상 볼륨을 분리합니다. 이것은 의도적입니다.  

4.  로그 크기를 기본 8GB에서에서 변경 하려면 사용 하세요 **Set-srgroup** 원본 및 대상 저장소 복제본 그룹에서 합니다.   예를 들어 모든 로그를 2GB로 설정하려면 다음을 수행합니다.  

    ```PowerShell  
    Get-SRGroup | Set-SRGroup -LogSizeInBytes 2GB  
    Get-SRGroup  
    ```  

5.  또 다른 쌍의 복제된 디스크를 기존 복제 그룹에 추가하려면 사용 가능한 저장소에 하나 이상의 추가 디스크가 있는지 확인해야 합니다. 그런 다음 원본 디스크를 마우스 오른쪽 단추로 클릭하고 복제 파트너 관계 추가를 선택할 수 있습니다.  
       >[!NOTE]
       >사용 가능한 저장소에 추가 '더미' 디스크가 필요한 이유는 회귀 때문이며 의도적인 것이 아닙니다. 장애 조치(Failover) 클러스터 관리자는 이전에 디스크 추가를 정상적으로 지원했으며, 이후 릴리스에서도 지원할 예정입니다.  

    **-SourceAddVolumePartnership** 및 **-DestinationAddVolumePartnership** 매개 변수와 함께 **Set-SRPartnership** cmdlet을 사용합니다.  
6.  복제를 제거하려면 임의의 노드에서 `Get-SRGroup`, Get-`SRPartnership`, `Remove-SRGroup` 및 `Remove-SRPartnership`을 사용합니다.  

    ```PowerShell  
    Get-SRPartnership | Remove-SRPartnership  
    Get-SRGroup | Remove-SRGroup  
    ```  

    > [!NOTE]
    > 원격 관리 컴퓨터를 사용하는 경우 이러한 cmdlet에 클러스터 이름을 지정하고 두 개의 RG 이름을 제공해야 합니다.  

### <a name="related-topics"></a>관련 항목  
- [저장소 복제본 개요](storage-replica-overview.md)  
- [서버 간 저장소 복제](server-to-server-storage-replication.md)  
- [클러스터 간 저장소 복제](cluster-to-cluster-storage-replication.md)  
- [스토리지 복제본: 알려진된 문제](storage-replica-known-issues.md) 
- [스토리지 복제본: 질문과 대답](storage-replica-frequently-asked-questions.md)  

## <a name="see-also"></a>관련 항목  
- [Windows Server 2016](../../get-started/windows-server-2016.md)  
- [Windows Server 2016의에서 저장소 공간 다이렉트](../storage-spaces/storage-spaces-direct-overview.md)
