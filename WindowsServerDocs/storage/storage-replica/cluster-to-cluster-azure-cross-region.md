---
title: Azure의 교차 지역 클러스터 간 저장소 복제
description: 클러스터 간 저장소 복제는 Azure의 지역 간
keywords: 저장소 복제본, 서버 관리자, Windows Server, Azure 지역에서 다른 지역 간 클러스터
author: arduppal
ms.author: arduppal
ms.date: 12/19/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-replica
manager: mchad
ms.openlocfilehash: d9999f786639ff4aa303ed34ade14849cda8feec
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475909"
---
# <a name="cluster-to-cluster-storage-replica-cross-region-in-azure"></a>Azure의 교차 지역 클러스터 간 저장소 복제

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널)

Azure에서 응용 프로그램의 지역 간 클러스터 간 저장소 복제를 구성할 수 있습니다. 아래 예제에서 두 노드 클러스터를 사용 하지만 클러스터 간 저장소 복제본 2 개 노드 클러스터로 제한 되지 않습니다. 아래 그림은 서로 통신할 수 있습니다, 같은 도메인에 있으며이 지역 간 2 노드 저장소 공간 다이렉트 클러스터.

프로세스의 전체 연습에 대 한 아래 비디오를 시청 하세요.
> [!video https://www.microsoft.com/en-us/videoplayer/embed/RE26xeW]

![아키텍처 다이어그램 들 C2C SR Azure 내에서 동일한 지역입니다.](media\Cluster-to-cluster-azure-cross-region\architecture.png)
> [!IMPORTANT]
> 모든 참조 된 예제는 위 그림와 관련이 있습니다.


1. Azure portal에서 만들 [리소스 그룹](https://ms.portal.azure.com/#create/Microsoft.ResourceGroup) 서로 다른 두 지역에서입니다.

    예를 들어 **SR AZ2AZ** 에서 **미국 서 부 2** 및 **SR AZCROSS** 에서 **미국 중서부**위와 같이 합니다.

2. 2 개를 만든 [가용성 집합](https://ms.portal.azure.com/#create/Microsoft.AvailabilitySet-ARM), 각 클러스터에 대 한 각 리소스 그룹의 하나입니다.
    - 가용성 집합 (**az2azAS1**)에서 (**SR-AZ2AZ**)
    - 가용성 집합 (**azcross-AS**)에서 (**SR-AZCROSS**)

3. 두 가상 네트워크 만들기
   - 만들기는 [가상 네트워크](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**az2az Vnet**)의 첫 번째 리소스 그룹 (**SR AZ2AZ**), 하나의 서브넷 및 하나의 게이트웨이 서브넷입니다.
   - 만들기는 [가상 네트워크](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM) (**azcross VNET**)의 두 번째 리소스 그룹 (**SR AZCROSS**), 하나의 서브넷 및 하나의 게이트웨이 서브넷입니다.

4. 두 네트워크 보안 그룹 만들기
   - 만들기는 [네트워크 보안 그룹](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**az2az NSG**)의 첫 번째 리소스 그룹 (**SR AZ2AZ**).
   - 만들기는 [네트워크 보안 그룹](https://ms.portal.azure.com/#create/Microsoft.NetworkSecurityGroup-ARM) (**azcross NSG**)의 두 번째 리소스 그룹 (**SR AZCROSS**).

   네트워크 보안 그룹 모두에 RDP:3389에 대 한 인바운드 보안 규칙을 추가 합니다. 설치를 마친 후이 규칙을 제거 하도록 선택할 수 있습니다.

5. Windows Server를 만듭니다 [가상 머신](https://ms.portal.azure.com/#create/Microsoft.WindowsServer2016Datacenter-ARM) 이전에 만든된 리소스 그룹의 합니다.

   도메인 컨트롤러 (**az2azDC**). 도메인 컨트롤러에 대 한 타사 가용성 집합을 만들거나 두 개의 가용성 집합 중 하나에서 도메인 컨트롤러를 추가 하도록 선택할 수 있습니다. 경우에 추가 하는이 두 클러스터에 대해 만든 가용성 집합에 할당할 표준 공용 IP 주소를 VM 생성 중.
      - Active Directory 도메인 서비스를 설치 합니다.
      - (Contoso.com) 도메인 만들기
      - 관리자 권한 (contosoadmin)를 사용 하 여 사용자 만들기

   두 개의 가상 머신을 만듭니다 (**az2az1**를 **az2az2**)의 리소스 그룹 (**SR AZ2AZ**) 가상 네트워크를 사용 하 여 (**az2az Vnet**) 및 네트워크 보안 그룹 (**az2az-NSG**) 가용성 집합 (**az2azAS1**). 자체를 만드는 동안 각 가상 머신에 표준 공용 IP 주소를 할당 합니다.
      - 각 컴퓨터에 최소 두 개의 관리 디스크 추가
      - 장애 조치 클러스터링 및 저장소 복제본 기능 설치

   두 개의 가상 머신을 만듭니다 (**azcross1**를 **azcross2**)의 리소스 그룹 (**SR AZCROSS**) 가상 네트워크를 사용 하 여 (**azcross-VNET**) 및 네트워크 보안 그룹 (**azcross NSG**) 가용성 집합 (**azcross-AS**). 자체를 만드는 동안 각 가상 머신에 표준 공용 IP 주소 할당
      - 각 컴퓨터에 두 개 이상의 관리 되는 디스크를 추가 합니다.
      - 장애 조치 클러스터링 및 저장소 복제본 기능 설치

   도메인에 모든 노드를 연결 하 고 이전에 만든된 사용자에 게 관리자 권한을 제공 합니다.

   도메인 컨트롤러 개인 IP 주소를 가상 네트워크의 DNS 서버를 변경 합니다.
   - 예제에서는 도메인 컨트롤러 **az2azDC** 개인 IP 주소가 (10.3.0.8이). 가상 네트워크에 (**az2az Vnet** 하 고 **azcross VNET**) 10.3.0.8이 DNS 서버를 변경 합니다. 

    예제에서는 "contoso.com"에 모든 노드를 연결 하 고 "contosoadmin"에 대 한 관리자 권한을 제공 합니다.
   - 모든 노드에서 contosoadmin로 로그인 합니다. 
 
6. 클러스터를 만들려면 (**SRAZC1**하십시오 **SRAZCross**).

   다음은 예제에 대 한 PowerShell 명령
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
   > 각 클러스터에 대 한 가상 디스크 및 볼륨을 만듭니다. 데이터 및 로그에 대 한 다른 하나입니다.

8. 내부 표준 SKU를 만드는 [부하 분산 장치](https://ms.portal.azure.com/#create/Microsoft.LoadBalancer-ARM) 각 클러스터에 대 한 (**azlbr1**하십시오 **azlbazcross**).

   부하 분산 장치에 대 한 정적 개인 IP 주소로 클러스터 IP 주소를 제공 합니다.
      - azlbr1 => Frontend IP: 10.3.0.100 (가상 네트워크에서 사용 되지 않는 IP 주소 선택 (**az2az Vnet**) 서브넷)
      - 각 부하 분산 장치에 대 한 백 엔드 풀을 만듭니다. 연결 된 클러스터 노드를 추가 합니다.
      - 포트 59999 상태 프로브를 만듭니다.
      - 부하 분산 규칙을 만듭니다. 설정 된 부동 IP를 사용 하 여 HA 포트를 허용 합니다.

   부하 분산 장치에 대 한 정적 개인 IP 주소로 클러스터 IP 주소를 제공 합니다. 
      - azlbazcross => Frontend IP: 10.0.0.10 (가상 네트워크에서 사용 되지 않는 IP 주소 선택 (**azcross VNET**) 서브넷)
      - 각 부하 분산 장치에 대 한 백 엔드 풀을 만듭니다. 연결 된 클러스터 노드를 추가 합니다.
      - 포트 59999 상태 프로브를 만듭니다.
      - 부하 분산 규칙을 만듭니다. 설정 된 부동 IP를 사용 하 여 HA 포트를 허용 합니다. 

9. 만들 [가상 네트워크 게이트웨이](https://ms.portal.azure.com/#create/Microsoft.VirtualNetworkGateway-ARM) Vnet 대 Vnet 연결 합니다.

 - 첫 번째 가상 네트워크 게이트웨이 만듭니다 (**az2az VNetGateway**)의 첫 번째 리소스 그룹 (**SR-AZ2AZ**)
 - 게이트웨이 유형 = VPN 및 VPN 형식 = 경로 기반

 - 두 번째 가상 네트워크 게이트웨이 만듭니다 (**azcross VNetGateway**)의 두 번째 리소스 그룹 (**SR-AZCROSS**)
 - 게이트웨이 유형 = VPN 및 VPN 형식 = 경로 기반

 - 첫 번째 가상 네트워크 게이트웨이에서 가상 네트워크 게이트웨이 두 번째 Vnet 대 Vnet 연결을 만듭니다. 공유 키를 제공 합니다.

 - 첫 번째 가상 네트워크 게이트웨이를 두 번째 가상 네트워크 게이트웨이에서 Vnet 대 Vnet 연결을 만듭니다. 위의 단계에서 제공 된 동일한 공유 키를 제공 합니다. 

10. 각 클러스터 노드에서 포트 59999 (상태 프로브)을 엽니다.

   각 노드에서 다음 명령을 실행 합니다.

   ```powershell
      netsh advfirewall firewall add rule name=PROBEPORT dir=in protocol=tcp action=allow localport=59999 remoteip=any profile=any 
   ```

11. 클러스터 포트 59999에서 상태 프로브 메시지를 수신 하 고 현재이 리소스를 소유 하는 노드에서 응답을 지시 합니다.

   한 번 실행 한 각 클러스터에 대 한 클러스터의 노드에서 합니다. 
    
   예제에서는 "ILBIP" 구성 값에 따라 변경 해야 합니다. 다음 명령을 실행 하는 모든 노드에서 **az2az1**/**az2az2**

   ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.3.0.100" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
   ```

12. 다음 명령을 실행 하는 모든 노드에서 **azcross1**/**azcross2**
   ```PowerShell
     $ClusterNetworkName = "Cluster Network 1" # Cluster network name (Use Get-ClusterNetwork on Windows Server 2012 or higher to find the name. And use Get-ClusterResource to find the IPResourceName).
     $IPResourceName = "Cluster IP Address" # IP Address cluster resource name.
     $ILBIP = "10.0.0.10" # IP Address in Internal Load Balancer (ILB) - The static IP address for the load balancer configured in the Azure portal.
     [int]$ProbePort = 59999
     Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";”ProbeFailureThreshold”=5;"EnableDhcp"=0}  
   ```

   두 클러스터를 연결 / 서로 통신할 수 있는지 확인 합니다.

   하거나 장애 조치 클러스터 관리자에서 "클러스터에 연결" 기능을 사용 하 여 다른 클러스터에 연결 하거나 현재 클러스터의 노드 중 하나에서 다른 클러스터의 응답을 확인 합니다.

   예제에서를 사용해 왔습니다.
   ```powershell
      Get-Cluster -Name SRAZC1 (ran from azcross1)
   ```
   ```powershell
      Get-Cluster -Name SRAZCross (ran from az2az1) 
   ```

13. 두 클러스터 모두에 대 한 클라우드 감시를 만듭니다. 2 개를 만든 [저장소 계정](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) (**az2azcw**를**azcrosssa**) 각 리소스 그룹의 각 클러스터에 대 한 Azure에서 (**SR AZ2AZ**합니다  **SR-AZCROSS**).
   
   - "액세스 키"에서 저장소 계정 이름과 키를 복사 합니다.
   - 클라우드 감시 "장애 조치 클러스터 관리자"를에서 만들고 만들려면 위의 계정 이름과 키를 사용 합니다. 

14. 실행할 [클러스터 유효성 검사 테스트](../../failover-clustering/create-failover-cluster.md#validate-the-configuration) 다음 단계로 넘어가기 전에

15. Windows PowerShell을 시작하고 [Test-SRTopology](https://docs.microsoft.com/powershell/module/storagereplica/test-srtopology?view=win10-ps) cmdlet을 사용하여 모든 저장소 복제본 요구 사항을 충족하는지 확인합니다. 장기 실행 성능 평가 모드뿐만 아니라 빠른 테스트를 위해 요구 사항 전용 모드에서 cmdlet을 사용할 수 있습니다.
 
16. 클러스터 간 저장소 복제본을 구성 합니다.
양쪽 방향에서 다른 클러스터에 하나의 클러스터에서 액세스를 부여 합니다.

   예:
   ```powershell
     Grant-SRAccess -ComputerName az2az1 -Cluster SRAZCross
   ```
Windows Server 2016을 사용 하는 경우 다음도이 명령을 실행 합니다.

   ```powershell
     Grant-SRAccess -ComputerName azcross1 -Cluster SRAZC1
   ```

17. 두 클러스터에 대 한 SR-파트너 관계를 만듭니다.</ol>

   - 클러스터에 대 한 **SRAZC1**
      - 볼륨 위치:-c:\ClusterStorage\DataDisk1
      - 로그 위치:-g:
   - 클러스터에 대 한 **SRAZCross**
      - 볼륨 위치:-c:\ClusterStorage\DataDiskCross
      - 로그 위치:-g:

명령을 실행 합니다.

```powershell
PowerShell

New-SRPartnership -SourceComputerName SRAZC1 -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\DataDisk1 -SourceLogVolumeName  g: -DestinationComputerName SRAZCross -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\DataDiskCross -DestinationLogVolumeName  g:
```