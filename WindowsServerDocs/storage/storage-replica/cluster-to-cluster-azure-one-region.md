---
title: Azure의 동일한 지역 내에서 클러스터에서 저장소 복제본으로 클러스터
description: Azure의 동일한 지역 내에서 클러스터 간 저장소 복제
keywords: 저장소 복제본, 서버 관리자, Windows Server, Azure, 클러스터, 동일한 지역
author: arduppal
ms.author: arduppal
ms.date: 04/26/2019
ms.topic: article
ms.prod: windows-server
ms.technology: storage-replica
manager: mchad
ms.openlocfilehash: 55d9c600c86b6b64efdb5c7d4437697539f887ae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402942"
---
# <a name="cluster-to-cluster-storage-replica-within-the-same-region-in-azure"></a>Azure의 동일한 지역 내에서 클러스터에서 저장소 복제본으로 클러스터

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

Azure의 동일한 지역 내에서 클러스터를 클러스터로 구성할 수 있습니다. 아래 예제에서는 2 개 노드 클러스터를 사용 하지만 클러스터에서 클러스터로의 저장소 복제본은 2 개 노드 클러스터로 제한 되지 않습니다. 아래 그림은 서로 통신 하 고, 동일한 도메인에 있고, 동일한 지역 내에 있는 2 노드 저장소 공간 다이렉트 클러스터입니다.

프로세스에 대 한 전체 연습을 보려면 아래 비디오를 시청 하세요.

1 부
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE26f2Y]

2 부
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE269Pq]

![아키텍처 다이어그램은 동일한 지역 내의 Azure에서 클러스터 간 저장소 복제본을 보여주는 합니다.](media/Cluster-to-cluster-azure-one-region/architecture.png)
> [!IMPORTANT]
> 참조 되는 모든 예제는 위의 그림에만 적용 됩니다.

1. 지역 ( **미국 서 부 2**의**AZ2AZ** )에 [리소스 Azure Portal 그룹](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup) 을 만듭니다. 
2. 각 클러스터에 대해 하나씩, 위에서 만든 리소스 그룹 (**AZ2AZ**)에 두 개의 [가용성 집합](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM) 을 만듭니다. 
    a. 가용성 집합 (**az2azAS1**) b. 가용성 집합 (**az2azAS2**)
3. 하나 이상의 서브넷이 있는 이전에 만든 리소스 그룹 (**az2az**)에 [가상 네트워크](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**az2az**)를 만듭니다. 
4. [네트워크 보안 그룹](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**az2az**)을 만들고 RDP: 3389에 대 한 인바운드 보안 규칙을 추가 합니다. 설치가 완료 되 면이 규칙을 제거 하도록 선택할 수 있습니다. 
5. 이전에 만든 리소스 그룹 (**AZ2AZ**)에서 Windows Server [가상 컴퓨터](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM) 를 만듭니다. 이전에 만든 가상 네트워크 (**az2az**) 및 네트워크 보안 그룹 (**az2az**)을 사용 합니다. 
   
   도메인 컨트롤러 (**az2azDC**). 도메인 컨트롤러에 대 한 세 번째 가용성 집합을 만들도록 선택 하거나 두 가용성 집합 중 하나에 도메인 컨트롤러를 추가할 수 있습니다. 두 클러스터에 대해 만든 가용성 집합에이를 추가 하는 경우 VM을 만드는 동안 표준 공용 IP 주소를 할당 합니다. 
   - Active Directory 도메인 서비스를 설치 합니다.
   - 도메인 만들기 (Contoso.com)
   - 관리자 권한으로 사용자 만들기 (contosoadmin) 
   - 첫 번째 가용성 집합 (**az2azAS1**)에 두 개의 가상 머신 (**az2az1**, **az2az2**)를 만듭니다. 생성 하는 동안 각 가상 머신에 표준 공용 IP 주소를 할당 합니다.
   - 각 컴퓨터에 2 개 이상의 관리 디스크 추가
   - 장애 조치 (Failover) 클러스터링 및 저장소 복제본 기능 설치
   - 두 번째 가용성 집합 (**az2azAS2**)에 두 개의 가상 머신 (**az2az3**, **az2az4**)를 만듭니다. 생성 하는 동안 각 가상 머신에 표준 공용 IP 주소를 할당 합니다. 
   - 각 컴퓨터에 최소 2 개의 관리 디스크를 추가 합니다. 
   - 장애 조치 (Failover) 클러스터링 및 저장소 복제본 기능을 설치 합니다. 
   
6. 모든 노드를 도메인에 연결 하 고 이전에 만든 사용자에 게 관리자 권한을 제공 합니다. 

7. 가상 네트워크의 DNS 서버를 도메인 컨트롤러 개인 IP 주소로 변경 합니다. 
8. 이 예제에서 도메인 컨트롤러 **az2azDC** 에는 개인 IP 주소 (10.3.0.8)가 있습니다. Virtual Network (**az2az**)에서 DNS 서버 10.3.0.8를 변경 합니다. 모든 노드를 "Contoso.com"에 연결 하 고 "contosoadmin"에 관리자 권한을 제공 합니다.
   - 모든 노드에서 contosoadmin로 로그인 합니다. 
    
9. 클러스터 (**SRAZC1**, **SRAZC2**)를 만듭니다. 
   다음은 예제에 대 한 PowerShell 명령입니다.
   ```PowerShell
    New-Cluster -Name SRAZC1 -Node az2az1,az2az2 –StaticAddress 10.3.0.100
   ```
   ```PowerShell
    New-Cluster -Name SRAZC2 -Node az2az3,az2az4 –StaticAddress 10.3.0.101
   ```
10. 저장소 공간 다이렉트 사용
    ```PowerShell
    Enable-clusterS2D
    ```   
   
    각 클러스터에 대해 가상 디스크 및 볼륨을 만듭니다. 하나는 데이터를 위한 것이 고 다른 하나는 로그에 대 한 것입니다. 
   
11. 각 클러스터에 대 한 내부 표준 SKU [Load Balancer](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM) (**azlbr1**,**azlbr2**)를 만듭니다. 
   
    부하 분산 장치에 대 한 정적 개인 IP 주소로 클러스터 IP 주소를 제공 합니다.
    - azlbr1 = > 프런트 엔드 IP: 10.3.0.100 (가상 네트워크 (**az2az**) 서브넷에서 사용 하지 않는 IP 주소 선택)
    - 각 부하 분산 장치에 대 한 백 엔드 풀을 만듭니다. 연결 된 클러스터 노드를 추가 합니다.
    - 상태 프로브 만들기: 포트 59999
    - 부하 분산 규칙 만들기: 사용 되는 부동 IP를 사용 하는 HA 포트를 허용 합니다. 
   
    부하 분산 장치에 대 한 정적 개인 IP 주소로 클러스터 IP 주소를 제공 합니다.
    - azlbr2 = > 프런트 엔드 IP: 10.3.0.101 (가상 네트워크 (**az2az**) 서브넷에서 사용 하지 않는 IP 주소 선택)
    - 각 부하 분산 장치에 대 한 백 엔드 풀을 만듭니다. 연결 된 클러스터 노드를 추가 합니다.
    - 상태 프로브 만들기: 포트 59999
    - 부하 분산 규칙 만들기: 사용 되는 부동 IP를 사용 하는 HA 포트를 허용 합니다. 
   
12. 각 클러스터 노드에서 포트 59999 (상태 프로브)을 엽니다. 
   
    각 노드에서 다음 명령을 실행 합니다.
    ```PowerShell
    netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any 
    ```   
13. 클러스터에서 포트 59999에 대 한 상태 프로브 메시지를 수신 대기 하 고 현재이 리소스를 소유 하 고 있는 노드에서 응답 하도록 지시 합니다. 
    각 클러스터에 대해 클러스터의 한 노드에서 한 번 실행 합니다. 
    
    이 예제에서는 구성 값에 따라 "ILBIP"를 변경 해야 합니다. **Az2az1**/**az2az2**한 노드에서 다음 명령을 실행 합니다.

    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}
    ```

14. **Az2az3**/**az2az4**한 노드에서 다음 명령을 실행 합니다. 

    ```PowerShell
    $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
    $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
    $ILBIP = "10.3.0.101" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
    [int]$ProbePort = 59999
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
    ```   
    두 클러스터 모두 서로 연결/통신할 수 있는지 확인 합니다. 

    장애 조치 (Failover) 클러스터 관리자의 "클러스터에 연결" 기능을 사용 하 여 다른 클러스터에 연결 하거나 현재 클러스터 노드 중 하나에서 다른 클러스터가 응답 하는지 확인 합니다.  
   
    ```PowerShell
     Get-Cluster -Name SRAZC1 (ran from az2az3)
    ```
    ```PowerShell
     Get-Cluster -Name SRAZC2 (ran from az2az1)
    ```   

15. 두 클러스터에 대 한 cloud 미러링 모니터 서버를 만듭니다. 동일한 리소스 그룹 (az2azcw)의 각 클러스터에 대해 azure에서 [저장소 계정](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) (, **az2azcw2** **)을**두 개 만듭니다.

    - "액세스 키"에서 저장소 계정 이름 및 키를 복사 합니다.
    - "장애 조치 (failover) 클러스터 관리자"에서 클라우드 감시를 만들고 위의 계정 이름 및 키를 사용 하 여 만듭니다.

16. 다음 단계로 이동 하기 전에 [클러스터 유효성 검사 테스트](../../failover-clustering/create-failover-cluster.md#validate-the-configuration) 를 실행 합니다.

17. Windows PowerShell을 시작하고 [Test-SRTopology](https://docs.microsoft.com/powershell/module/storagereplica/test-srtopology?view=win10-ps) cmdlet을 사용하여 모든 저장소 복제본 요구 사항을 충족하는지 확인합니다. 장기 실행 성능 평가 모드 뿐만 아니라 빠른 테스트에 대 한 요구 사항 전용 모드에서 cmdlet을 사용할 수 있습니다.

18. 클러스터 간 저장소 복제본을 구성 합니다.
   
    두 방향으로 한 클러스터에서 다른 클러스터로의 액세스 권한 부여:

    예제:

    ```PowerShell
      Grant-SRAccess -ComputerName az2az1 -Cluster SRAZC2
    ```
    Windows Server 2016를 사용 하는 경우에도 다음 명령을 실행 합니다.

    ```PowerShell
      Grant-SRAccess -ComputerName az2az3 -Cluster SRAZC1
    ```   
   
19. 클러스터에 대해 SRPartnership 관계 만들기:</ol>

    - 클러스터 **SRAZC1**.
    - 볼륨 위치:-c:\ClusterStorage\DataDisk1
    - 로그 위치:-g:
    - 클러스터 **SRAZC2**
    - 볼륨 위치:-c:\ClusterStorage\DataDisk2
    - 로그 위치:-g:

다음 명령을 실행합니다.

```PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName **SRAZC2** -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDisk2 -DestinationLogVolumeName  g:
```