---
title: Azure의 교차 지역 클러스터 간 저장소 복제
description: Azure에서 클러스터 간 저장소 복제 교차 지역
keywords: 저장소 복제본, 서버 관리자, Windows Server, Azure, 클러스터, 지역 간, 다른 지역
author: arduppal
ms.author: arduppal
ms.date: 12/19/2018
ms.topic: article
ms.prod: windows-server
ms.technology: storage-replica
manager: mchad
ms.openlocfilehash: 26eba76c836d1157f4d4c10d7a989a3a7dcc1538
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393831"
---
# <a name="cluster-to-cluster-storage-replica-cross-region-in-azure"></a>Azure의 교차 지역 클러스터 간 저장소 복제

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

Azure에서 지역 간 응용 프로그램에 대 한 저장소 복제본을 클러스터로 구성할 수 있습니다. 아래 예제에서는 2 개 노드 클러스터를 사용 하지만 클러스터에서 클러스터로의 저장소 복제본은 2 개 노드 클러스터로 제한 되지 않습니다. 아래 그림은 서로 통신할 수 있고, 동일한 도메인에 있고, 지역 간 인 2 노드 저장소 공간 다이렉트 클러스터입니다.

프로세스에 대 한 전체 연습을 보려면 아래 비디오를 시청 하세요.
> [!video https://www.microsoft.com/en-us/videoplayer/embed/RE26xeW]

![아키텍처 다이어그램 보여주는 C2C SR in Azure 트 내의 동일한 지역.](media/Cluster-to-cluster-azure-cross-region/architecture.png)
> [!IMPORTANT]
> 참조 되는 모든 예제는 위의 그림에만 적용 됩니다.


1. Azure Portal에서 두 개의 다른 지역에 [리소스 그룹](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup) 을 만듭니다.

    예를 들어 위에 나와 있는 것 처럼 미국 서 부 **2** 및 **AZCROSS** 의AZ2AZ에 대 한 **sr-iov** 가 있습니다.

2. 각 클러스터에 대 한 각 리소스 그룹에 하나씩 두 개의 [가용성 집합](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM)을 만듭니다.
    - 가용성 집합 (**az2azAS1**) (**AZ2AZ**)
    - 가용성 집합 (**azcross**) IN (**azcross**)

3. 두 개의 가상 네트워크 만들기
   - 하나의 서브넷과 하나의 게이트웨이 서브넷이 있는 첫 번째 리소스 그룹 (**az2az**)에 [가상 네트워크](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**az2az**)를 만듭니다.
   - 하나의 서브넷과 하나의 게이트웨이 서브넷이 있는 두 번째 리소스 그룹 (**azcross**)에 [가상 네트워크](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**azcross**)를 만듭니다.

4. 네트워크 보안 그룹 두 개를 만듭니다.
   - 첫 번째 리소스 그룹 (**az2az**)에 [네트워크 보안 그룹](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**az2az**)을 만듭니다.
   - 두 번째 리소스 그룹 (**azcross**)에서 [네트워크 보안 그룹](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**azcross**)을 만듭니다.

   RDP: 3389에 대 한 인바운드 보안 규칙 하나를 두 네트워크 보안 그룹에 추가 합니다. 설치가 완료 되 면이 규칙을 제거 하도록 선택할 수 있습니다.

5. 이전에 만든 리소스 그룹에서 Windows Server [가상 컴퓨터](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM) 를 만듭니다.

   도메인 컨트롤러 (**az2azDC**). 도메인 컨트롤러에 대 한 세 번째 가용성 집합을 만들도록 선택 하거나 두 가용성 집합 중 하나에 도메인 컨트롤러를 추가할 수 있습니다. 두 클러스터에 대해 만든 가용성 집합에이를 추가 하는 경우 VM을 만드는 동안 표준 공용 IP 주소를 할당 합니다.
      - Active Directory 도메인 서비스를 설치 합니다.
      - 도메인 만들기 (contoso.com)
      - 관리자 권한으로 사용자 만들기 (contosoadmin)

   가용성 집합 (**AZ2AZ**)에서 가상 네트워크 (**AZ2AZ**) 및 네트워크 보안 그룹 (**az2azAS1**)을 사용 하 여 리소스 그룹 (**az2az1**, **az2az2**)에 두 개의 가상 컴퓨터 (**AZ2AZ**)를 만듭니다. 생성 하는 동안 각 가상 머신에 표준 공용 IP 주소를 할당 합니다.
      - 각 컴퓨터에 두 개 이상의 관리 디스크 추가
      - 장애 조치 (Failover) 클러스터링 및 저장소 복제본 기능 설치

   가용성 집합 (**AZCROSS**)에서 가상 네트워크 (**AZCROSS**) 및 네트워크 보안 그룹 (**AZCROSS-nsg**)을 사용 하 여 리소스 그룹 (**azcross1**, **azcross2**)에 두 개의 가상 컴퓨터 (**AZCROSS**)를 만듭니다. . 생성 하는 동안 각 가상 머신에 표준 공용 IP 주소 할당
      - 각 컴퓨터에 두 개 이상의 관리 디스크 추가
      - 장애 조치 (Failover) 클러스터링 및 저장소 복제본 기능 설치

   모든 노드를 도메인에 연결 하 고 이전에 만든 사용자에 게 관리자 권한을 제공 합니다.

   가상 네트워크의 DNS 서버를 도메인 컨트롤러 개인 IP 주소로 변경 합니다.
   - 이 예에서 도메인 컨트롤러 **az2azDC** 에는 개인 IP 주소 (10.3.0.8)가 있습니다. Virtual Network (**az2az** 및 **AZCROSS**)에서 DNS 서버 10.3.0.8를 변경 합니다. 

     이 예에서는 모든 노드를 "contoso.com"에 연결 하 고 "contosoadmin"에 관리자 권한을 제공 합니다.
   - 모든 노드에서 contosoadmin로 로그인 합니다. 
 
6. 클러스터를 만듭니다 (**SRAZC1**, **srazcross**).

   예제에 대 한 PowerShell 명령은 다음과 같습니다.
   ```powershell
      New-Cluster -Name SRAZC1 -Node az2az1,az2az2 –StaticAddress 10.3.0.100
   ```
   ```powershell
      New-Cluster -Name SRAZCross -Node azcross1,azcross2 –StaticAddress 10.0.0.10
   ```

7. 저장소 공간 다이렉트를 사용 하도록 설정 합니다.

   ```powershell
      Enable-clusterS2D
   ```

   > [!NOTE]
   > 각 클러스터에 대해 가상 디스크 및 볼륨을 만듭니다. 하나는 데이터를 위한 것이 고 다른 하나는 로그에 대 한 것입니다.

8. 각 클러스터에 대 한 내부 표준 SKU [Load Balancer](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM) (**azlbr1**, **azlbazcross**)를 만듭니다.

   부하 분산 장치에 대 한 정적 개인 IP 주소로 클러스터 IP 주소를 제공 합니다.
      - azlbr1 = > 프런트 엔드 IP: 10.3.0.100 (가상 네트워크 (**az2az**) 서브넷에서 사용 하지 않는 IP 주소 선택)
      - 각 부하 분산 장치에 대 한 백 엔드 풀을 만듭니다. 연결 된 클러스터 노드를 추가 합니다.
      - 상태 프로브 만들기: 포트 59999
      - 부하 분산 규칙 만들기: 사용 되는 부동 IP를 사용 하는 HA 포트를 허용 합니다.

   부하 분산 장치에 대 한 정적 개인 IP 주소로 클러스터 IP 주소를 제공 합니다. 
      - azlbazcross = > 프런트 엔드 IP: 10.0.0.10 (가상 네트워크 (**azcross**) 서브넷에서 사용 하지 않는 IP 주소 선택)
      - 각 부하 분산 장치에 대 한 백 엔드 풀을 만듭니다. 연결 된 클러스터 노드를 추가 합니다.
      - 상태 프로브 만들기: 포트 59999
      - 부하 분산 규칙 만들기: 사용 되는 부동 IP를 사용 하는 HA 포트를 허용 합니다. 

9. Vnet 간 연결에 대 한 [가상 네트워크 게이트웨이](https://ms.portal.azure.com/#create/Microsoft.VirtualNetworkGateway-ARM) 를 만듭니다.

   - 첫 번째 리소스 그룹 (**az2az**)에서 첫 번째 가상 네트워크 게이트웨이 (**Az2az-vnetgateway**) 만들기
   - 게이트웨이 유형 = VPN 및 VPN 유형 = 경로 기반

   - 두 번째 리소스 그룹 (**azcross**)에서 두 번째 가상 네트워크 게이트웨이 (**Azcross-vnetgateway**) 만들기
   - 게이트웨이 유형 = VPN 및 VPN 유형 = 경로 기반

   - 첫 번째 가상 네트워크 게이트웨이에서 두 번째 가상 네트워크 게이트웨이로 Vnet 간 연결을 만듭니다. 공유 키 제공

   - 두 번째 가상 네트워크 게이트웨이에서 첫 번째 가상 네트워크 게이트웨이로 Vnet 간 연결을 만듭니다. 위의 단계에서 제공 하는 것과 동일한 공유 키를 제공 합니다. 

10. 각 클러스터 노드에서 포트 59999 (상태 프로브)을 엽니다.

    각 노드에서 다음 명령을 실행 합니다.

    ```powershell
      netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any 
    ```

11. 클러스터에서 포트 59999에 대 한 상태 프로브 메시지를 수신 대기 하 고 현재이 리소스를 소유 하 고 있는 노드에서 응답 하도록 지시 합니다.

    각 클러스터에 대해 클러스터의 한 노드에서 한 번 실행 합니다. 
    
    이 예제에서는 구성 값에 따라 "ILBIP"를 변경 해야 합니다. **Az2az1**/**az2az2** 한 노드에서 다음 명령을 실행 합니다.

    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
    ```

12. **Azcross1**/**azcross2** 한 노드에서 다음 명령을 실행 합니다.
    ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.0.0.10" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
    ```

    두 클러스터 모두 서로 연결/통신할 수 있는지 확인 합니다.

    장애 조치 (Failover) 클러스터 관리자의 "클러스터에 연결" 기능을 사용 하 여 다른 클러스터에 연결 하거나 현재 클러스터 노드 중 하나에서 다른 클러스터가 응답 하는지 확인 합니다.

    사용 중인 예제에서 다음을 수행 합니다.
    ```powershell
      Get-Cluster -Name SRAZC1 (ran from azcross1)
    ```
    ```powershell
      Get-Cluster -Name SRAZCross (ran from az2az1) 
    ```

13. 두 클러스터에 대 한 클라우드 감시를 만듭니다. Azure에서 두 개의 [저장소 계정](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) (**az2azcw**,**azcrosssa**)을 만듭니다. 각 리소스 그룹의 각 클러스터에 대해 하나씩 (**AZ2AZ**, **AZCROSS**).
   
    - "액세스 키"에서 저장소 계정 이름 및 키를 복사 합니다.
    - "장애 조치 (failover) 클러스터 관리자"에서 클라우드 감시를 만들고 위의 계정 이름 및 키를 사용 하 여 만듭니다. 

14. 다음 단계로 이동 하기 전에 [클러스터 유효성 검사 테스트](../../failover-clustering/create-failover-cluster.md#validate-the-configuration) 를 실행 합니다.

15. Windows PowerShell을 시작하고 [Test-SRTopology](https://docs.microsoft.com/powershell/module/storagereplica/test-srtopology?view=win10-ps) cmdlet을 사용하여 모든 저장소 복제본 요구 사항을 충족하는지 확인합니다. 장기 실행 성능 평가 모드뿐만 아니라 빠른 테스트를 위해 요구 사항 전용 모드에서 cmdlet을 사용할 수 있습니다.
 
16. 클러스터 간 저장소 복제본을 구성 합니다.
    두 방향으로 한 클러스터에서 다른 클러스터로의 액세스 권한 부여:

    예제:
    ```powershell
     Grant-SRAccess -ComputerName az2az1 -Cluster SRAZCross
    ```
    Windows Server 2016를 사용 하는 경우 다음 명령을 실행 합니다.

    ```powershell
     Grant-SRAccess -ComputerName azcross1 -Cluster SRAZC1
    ```

17. 두 클러스터에 대 한 SR-IOV를 만듭니다.</ol>

    - 클러스터 **SRAZC1**
      - 볼륨 위치:-c:\ClusterStorage\DataDisk1
      - 로그 위치:-g:
    - Cluster **Srazcross**
      - 볼륨 위치:-c:\ClusterStorage\DataDiskCross
      - 로그 위치:-g:

다음 명령을 실행 합니다.

```powershell
PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName SRAZCross -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDiskCross -DestinationLogVolumeName  g:
```