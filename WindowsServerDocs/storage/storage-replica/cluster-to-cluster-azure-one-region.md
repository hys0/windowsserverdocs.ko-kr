---
title: Azure의 동일 지역 내 클러스터 간 저장소 복제
description: Azure에서 동일한 지역 내에서 클러스터 간 저장소 복제
keywords: 저장소 복제본, 서버 관리자, Windows Server, Azure, 클러스터, 동일한 지역
author: arduppal
ms.author: arduppal
ms.date: 12/19/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-replica
manager: mchad
ms.openlocfilehash: 8dbfab96404f5c98b9861476c0bc654af1bda775
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829144"
---
# <a name="cluster-to-cluster-storage-replica-within-the-same-region-in-azure"></a>Azure의 동일 지역 내 클러스터 간 저장소 복제
Azure에서 동일한 지역 내에서 클러스터 간 저장소 복제를 구성할 수 있습니다. 아래 예제에서 두 노드 클러스터를 사용 하지만 클러스터 간 저장소 복제본 2 개 노드 클러스터로 제한 되지 않습니다. 아래 그림은 서로 통신할 수 있는 2 노드 저장소 공간 다이렉트 클러스터는 동일한 지역 내의 동일한 도메인에 있습니다.

프로세스의 전체 연습에 대 한 아래 비디오를 시청 하세요.

1 부
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE26f2Y]

2 부
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE269Pq]

![동일한 지역 내에서 Azure의 클러스터 간 저장소 복제본을 표시 하는 아키텍처 다이어그램.](media\Cluster-to-cluster-azure-one-region\architecture.png)
> [!IMPORTANT]
> 모든 참조 된 예제는 위 그림와 관련이 있습니다.

1. 만들기는 [리소스 그룹](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup) 지역에 Azure portal에서 (**SR-AZ2AZ** 에서 **미국 서 부 2**). 
2. 2 개를 만든 [가용성 집합](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM) 리소스 그룹에서 (**SR-AZ2AZ**) 각 클러스터에 대해 위에서 만든된 것입니다. 
    a. 가용성 집합 (**az2azAS1**) b. 가용성 집합 (**az2azAS2**)
3. 만들기는 [가상 네트워크](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**az2az Vnet**) 이전에 만든된 리소스 그룹에서 (**SR AZ2AZ**), 서브넷 1 개 이상 필요 합니다. 
4. 만들기는 [네트워크 보안 그룹](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**az2az NSG**), RDP:3389에 대 한 인바운드 보안 규칙을 추가 합니다. 설치를 마친 후이 규칙을 제거 하도록 선택할 수 있습니다. 
5. Windows Server를 만듭니다 [virtual machines](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM) 이전에 만든된 리소스 그룹에서 (**SR-AZ2AZ**). 이전에 만든된 가상 네트워크를 사용 하 여 (**az2az Vnet**) 및 네트워크 보안 그룹 (**az2az NSG**). 
   
   도메인 컨트롤러 (**az2azDC**). 도메인 컨트롤러에 대 한 세 번째 가용성 집합을 만들거나 두 개의 가용성 집합 중 하나에서 도메인 컨트롤러를 추가 하도록 선택할 수 있습니다. 경우에 추가 하는이 두 클러스터에 대해 만든 가용성 집합에 할당할 표준 공용 IP 주소를 VM 생성 중. 
   - Active Directory 도메인 서비스를 설치 합니다.
   - (Contoso.com) 도메인 만들기
   - 관리자 권한 (contosoadmin)를 사용 하 여 사용자 만들기 
   - 두 개의 가상 머신을 만듭니다 (**az2az1**하십시오 **az2az2**) 첫 번째 가용성 집합 (**az2azAS1**). 자체를 만드는 동안 각 가상 머신에 표준 공용 IP 주소를 할당 합니다.
   - 각 컴퓨터에 최소 2 개의 관리 디스크 추가
   - 장애 조치 클러스터링 및 저장소 복제본 기능 설치
   - 두 개의 가상 머신을 만듭니다 (**az2az3**하십시오 **az2az4**) 두 번째 가용성 집합 (**az2azAS2**). 자체를 만드는 동안 각 가상 머신에 표준 공용 IP 주소를 할당 합니다. 
   - 각 컴퓨터에 최소 2 개의 관리 디스크를 추가 합니다. 
   - 장애 조치 클러스터링 및 저장소 복제본 기능을 설치 합니다. 
   
6. 도메인에 모든 노드를 연결 하 고 이전에 만든된 사용자에 게 관리자 권한을 제공 합니다. 

7. 도메인 컨트롤러 개인 IP 주소를 가상 네트워크의 DNS 서버를 변경 합니다. 
8. 예제에서는 도메인 컨트롤러 **az2azDC** 개인 IP 주소가 (10.3.0.8이). 가상 네트워크에 (**az2az Vnet**) 10.3.0.8이 DNS 서버를 변경 합니다. "Contoso.com"에 모든 노드를 연결 하 고 "contosoadmin"에 대 한 관리자 권한을 제공 합니다.
   - 모든 노드에서 contosoadmin로 로그인 합니다. 
    
9. 클러스터를 만들려면 (**SRAZC1**하십시오 **SRAZC2**). 다음은 예제에 대 한 PowerShell 명령
```PowerShell
    New-Cluster -Name SRAZC1 -Node az2az1,az2az2 – StaticAddress 10.3.0.100
```
```PowerShell
    New-Cluster -Name SRAZC2 -Node az2az3,az2az4 – StaticAddress 10.3.0.101
```
10. 저장소 공간 다이렉트를 사용 하도록 설정
```PowerShell
    Enable-clusterS2D
```   
   
   각 클러스터에 대 한 가상 디스크 및 볼륨을 만듭니다. 데이터 및 로그에 대 한 다른 하나입니다. 
   
11. 내부 표준 SKU를 만드는 [부하 분산 장치](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM) 각 클러스터에 대 한 (**azlbr1**하십시오**azlbr2**). 
   
   부하 분산 장치에 대 한 정적 개인 IP 주소로 클러스터 IP 주소를 제공 합니다.
   - azlbr1 => Frontend IP: 10.3.0.100 (가상 네트워크에서 사용 되지 않는 IP 주소 선택 (**az2az Vnet**) 서브넷)
   - 각 부하 분산 장치에 대 한 백 엔드 풀을 만듭니다. 연결 된 클러스터 노드를 추가 합니다.
   - 포트 59999 상태 프로브를 만듭니다.
   - 부하 분산 규칙을 만듭니다. 설정 된 부동 IP를 사용 하 여 HA 포트를 허용 합니다. 
   
   부하 분산 장치에 대 한 정적 개인 IP 주소로 클러스터 IP 주소를 제공 합니다.
   - azlbr2 => Frontend IP: 10.3.0.101 (가상 네트워크에서 사용 되지 않는 IP 주소 선택 (**az2az Vnet**) 서브넷)
   - 각 부하 분산 장치에 대 한 백 엔드 풀을 만듭니다. 연결 된 클러스터 노드를 추가 합니다.
   - 포트 59999 상태 프로브를 만듭니다.
   - 부하 분산 규칙을 만듭니다. 설정 된 부동 IP를 사용 하 여 HA 포트를 허용 합니다. 
   
12. 각 클러스터 노드에서 포트 59999 (상태 프로브)을 엽니다. 
   
    각 노드에서 다음 명령을 실행 합니다.
```PowerShell
netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any 
```   
13. 클러스터 포트 59999에서 상태 프로브 메시지를 수신 하 고 현재이 리소스를 소유 하는 노드에서 응답을 지시 합니다. 한 번 실행 한 각 클러스터에 대 한 클러스터의 노드에서 합니다. 
    
    예제에서는 "ILBIP" 구성 값에 따라 변경 해야 합니다. 다음 명령을 실행 하는 모든 노드에서 **az2az1**/**az2az2**:

    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}
    ```

14. 다음 명령을 실행 하는 모든 노드에서 **az2az3**/**az2az4**합니다. 

    ```PowerShell
    $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
    $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
    $ILBIP = "10.3.0.101" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
    [int]$ProbePort = 59999
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
    ```   
   두 클러스터를 연결 / 서로 통신할 수 있는지 확인 합니다. 

   하거나 장애 조치 클러스터 관리자에서 "클러스터에 연결" 기능을 사용 하 여 다른 클러스터에 연결 하거나 현재 클러스터의 노드 중 하나에서 다른 클러스터의 응답을 확인 합니다.  
   
   ```PowerShell
     Get-Cluster -Name SRAZC1 (ran from az2az3)
   ```
   ```PowerShell
     Get-Cluster -Name SRAZC2 (ran from az2az1)
   ```   

15. 두 클러스터 모두에 대 한 클라우드 미러링 모니터 서버를 만듭니다. 2 개를 만든 [저장소 계정](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) (**az2azcw**를 **az2azcw2**)는 동일한 리소스 그룹의 각 클러스터에 대 한 azure에서 (**SR AZ2AZ**).

    - "액세스 키"에서 저장소 계정 이름과 키를 복사 합니다.
    - 클라우드 감시 "장애 조치 클러스터 관리자"를에서 만들고 만들려면 위의 계정 이름과 키를 사용 합니다.

16. 실행할 [클러스터 유효성 검사 테스트](../../failover-clustering/create-failover-cluster.md#validate-the-configuration) 다음 단계로 넘어가기 전에 합니다.

17. Windows PowerShell을 시작하고 [Test-SRTopology](https://docs.microsoft.com/powershell/module/storagereplica/test-srtopology?view=win10-ps) cmdlet을 사용하여 모든 저장소 복제본 요구 사항을 충족하는지 확인합니다. 장기 실행 성능 평가 모드 뿐만 아니라 빠른 테스트에 대 한 요구 사항 전용 모드에서 cmdlet을 사용할 수 있습니다.

18. 클러스터 간 저장소 복제본을 구성 합니다.
   
   양쪽 방향에서 다른 클러스터에 하나의 클러스터에서 액세스를 부여 합니다.

   예제:

   ```PowerShell
      Grant-SRAccess -ComputerName az2az1 -Cluster SRAZC2
   ```
또한이 명령을 실행 하는 Windows Server 2016 사용 하는 경우:

   ```PowerShell
      Grant-SRAccess -ComputerName az2az3 -Cluster SRAZC1
   ```   
   
19. 클러스터에 대해 SRPartnership를 만듭니다.</ol>

 - 클러스터에 대 한 **SRAZC1**합니다.
   - 볼륨 위치:-c:\ClusterStorage\DataDisk1
   - 로그 위치:-g:
 - 클러스터에 대 한 **SRAZC2**
    - 볼륨 위치:-c:\ClusterStorage\DataDisk2
    - 로그 위치:-g:

다음 명령을 실행합니다.

```PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName **SRAZC2** -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDisk2 -DestinationLogVolumeName  g:
```