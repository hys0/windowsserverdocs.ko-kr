---
title: 테넌트 가상 네트워크에 컨테이너 끝점 연결
description: 이 항목에서는 SDN을 통해 만든 기존 테 넌 트 가상 네트워크에 컨테이너 끝점을 연결 하는 방법을 보여 줍니다. Docker 용 Windows l2bridge (및 선택적으로 l2tunnel) 네트워크 드라이버를 사용 하 여 테 넌 트 VM에 컨테이너 네트워크를 만들 수 있습니다.
manager: ravirao
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7af1eb6-d035-4f74-a25b-d4b7e4ea9329
ms.author: pashort
author: jmesser81
ms.date: 08/24/2018
ms.openlocfilehash: 83996f7ffb82d01c9f36945efa022f0dd0b9825b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355823"
---
# <a name="connect-container-endpoints-to-a-tenant-virtual-network"></a>테넌트 가상 네트워크에 컨테이너 끝점 연결

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 SDN을 통해 만든 기존 테 넌 트 가상 네트워크에 컨테이너 끝점을 연결 하는 방법을 보여 줍니다. Docker 용 Windows *l2bridge* (및 선택적으로 *l2tunnel*) 네트워크 드라이버를 사용 하 여 테 넌 트 VM에 컨테이너 네트워크를 만들 수 있습니다.

[컨테이너 네트워크 드라이버](https://docs.microsoft.com/virtualization/windowscontainers/container-networking/network-drivers-topologies) 항목에서는 Windows에서 Docker를 통해 사용할 수 있는 여러 네트워크 드라이버에 대해 설명 했습니다. SDN의 경우 *l2bridge* 및 *l2tunnel* 드라이버를 사용 합니다. 두 드라이버 각 컨테이너 끝점은 컨테이너 (테 넌 트) 호스트 가상 컴퓨터와 동일한 가상 서브넷에 있습니다. 

사설 클라우드 플러그 인을 통해 HNS (호스트 네트워킹 서비스)는 컨테이너 끝점의 IP 주소를 동적으로 할당 합니다. 컨테이너 끝점을 고유 IP 주소가 있지만 계층 2 주소 변환으로 인해 컨테이너 (테 넌 트) 호스트 가상 컴퓨터의 같은 MAC 주소를 공유 합니다. 

이러한 컨테이너 끝점에 대 한 네트워크 정책 (Acl, 캡슐화 및 QoS)은 네트워크 컨트롤러에서 받아서 상위 계층 관리 시스템에 정의 된 실제 Hyper-v 호스트에 적용 됩니다. 

*L2bridge* 및 *l2tunnel* 드라이버의 차이점은 다음과 같습니다.


|                                                                                                                                                                                                                                                                            l2bridge                                                                                                                                                                                                                                                                            |                                                                                                 l2tunnel                                                                                                  |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 다음 위치에 있는 컨테이너 끝점: <ul><li>동일한 서브넷의 컨테이너 호스트 가상 머신과 동일한 서브넷에는 모두 Hyper-v 가상 스위치 내에서 브리지 된 모든 네트워크 트래픽이 있습니다. </li><li>다른 컨테이너 호스트 Vm 또는 다른 서브넷의 트래픽은 실제 Hyper-v 호스트에 전달 됩니다. </li></ul>동일한 호스트와 동일한 서브넷에 있는 컨테이너 간의 네트워크 트래픽이 실제 호스트로 전달 되지 않기 때문에 네트워크 정책이 적용 되지 않습니다. 네트워크 정책은 호스트 간 또는 서브넷 간 컨테이너 네트워크 트래픽에만 적용 됩니다. | 두 컨테이너 끝점 간의 *모든* 네트워크 트래픽은 호스트 또는 서브넷에 관계 없이 실제 hyper-v 호스트에 전달 됩니다. 네트워크 정책은 서브넷 간 및 크로스 호스트 네트워크 트래픽에 모두 적용 됩니다. |

---

>[!NOTE]
>이러한 네트워킹 모드는 Azure 공용 클라우드의 테 넌 트 가상 네트워크에 windows 컨테이너 끝점을 연결 하는 데 작동 하지 않습니다.


## <a name="prerequisites"></a>필수 구성 요소
-  네트워크 컨트롤러를 사용 하 여 배포 된 SDN 인프라
-  테 넌 트 가상 네트워크를 만들었습니다.
-  Windows 컨테이너 기능이 사용 하도록 설정 되 고 Docker가 설치 되었으며 Hyper-v 기능이 활성화 된 배포 된 테 넌 트 가상 컴퓨터입니다. L2bridge 및 l2tunnel 네트워크용 이진 파일을 여러 개 설치 하려면 Hyper-v 기능이 필요 합니다.

   ```powershell
   # To install HyperV feature without checks for nested virtualization
   dism /Online /Enable-Feature /FeatureName:Microsoft-Hyper-V /All 
   ```

>[!Note]
>Hyper-v 컨테이너를 사용 하지 않는 한 [중첩 된 가상화](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/nesting) 및 가상화 확장 노출은 필요 하지 않습니다. 


## <a name="workflow"></a>워크플로

[1. 네트워크 컨트롤러 (Hyper-v 호스트)
2를 통해 기존 VM NIC 리소스에 여러 IP 구성을 추가 합니다.](#1-add-multiple-ip-configurations) [ 호스트에서 네트워크 프록시를 사용 하도록 설정 하 여 컨테이너 끝점 (Hyper-v 호스트)
3에 대 한 CA IP 주소를 할당](#2-enable-the-network-proxy) 합니다 [. 컨테이너 끝점 (컨테이너 호스트 VM)에 CA IP 주소를 할당 하려면 사설 클라우드 플러그](#3-install-the-private-cloud-plug-in) 인
4를 설치 [합니다. Docker를 사용 하 여 *l2bridge* 또는 *l2tunnel* 네트워크 만들기 (컨테이너 호스트 VM)](#4-create-an-l2bridge-container-network)

>[!NOTE]
>System Center Virtual Machine Manager를 통해 만든 VM NIC 리소스에 대해 여러 IP 구성이 지원 되지 않습니다. 것이 좋습니다 이러한 배포 유형에 대 한 네트워크 컨트롤러 PowerShell을 사용 하 여 대역 외에서 VM NIC 리소스를 만들어야 합니다.

### <a name="1-add-multiple-ip-configurations"></a>1. 여러 IP 구성 추가
이 단계에서는 테 넌 트 가상 컴퓨터의 VM NIC에 IP 주소가 192.168.1.9 인 ip 구성이 하나 있고, 192.168.1.0/24 IP 서브넷에서 ' VNet1 '의 VNet 리소스 ID와 ' Subnet1 '의 VM 서브넷 리소스에 연결 되어 있다고 가정 합니다. 192.168.1.101-192.168.1.110에서 컨테이너에 대 한 10 개의 IP 주소를 추가 합니다.

```powershell
Import-Module NetworkController

# Specify Network Controller REST IP or FQDN
$uri = "<NC REST IP or FQDN>"
$vnetResourceId = "VNet1"
$vsubnetResourceId = "Subnet1"

$vmnic= Get-NetworkControllerNetworkInterface -ConnectionUri $uri | where {$_.properties.IpConfigurations.Properties.PrivateIPAddress -eq "192.168.1.9" }
$vmsubnet = Get-NetworkControllerVirtualSubnet -VirtualNetworkId $vnetResourceId -ResourceId $vsubnetResourceId -ConnectionUri $uri

# For this demo, we will assume an ACL has already been defined; any ACL can be applied here
$allowallacl = Get-NetworkControllerAccessControlList -ConnectionUri $uri -ResourceId "AllowAll"


foreach ($i in 1..10)
{
    $newipconfig = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfiguration
    $props = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfigurationProperties

    $resourceid = "IP_192_168_1_1"
    if ($i -eq 10) 
    {
        $resourceid += "10"
        $ipstr = "192.168.1.110"
    }
    else
    {
        $resourceid += "0$i"
        $ipstr = "192.168.1.10$i"
    }

    $newipconfig.ResourceId = $resourceid
    $props.PrivateIPAddress = $ipstr    

    $props.PrivateIPAllocationMethod = "Static"
    $props.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $props.Subnet.ResourceRef = $vmsubnet.ResourceRef
    $props.AccessControlList = new-object Microsoft.Windows.NetworkController.AccessControlList
    $props.AccessControlList.ResourceRef = $allowallacl.ResourceRef

    $newipconfig.Properties = $props
    $vmnic.Properties.IpConfigurations += $newipconfig
}

New-NetworkControllerNetworkInterface -ResourceId $vmnic.ResourceId -Properties $vmnic.Properties -ConnectionUri $uri
```

### <a name="2-enable-the-network-proxy"></a>2. 네트워크 프록시를 사용 하도록 설정
이 단계에서는 네트워크 프록시가 컨테이너 호스트 가상 컴퓨터에 대해 여러 IP 주소를 할당 하도록 설정 합니다. 

네트워크 프록시를 사용 하도록 설정 하려면 컨테이너 호스트 (테 넌 트) 가상 머신을 호스트 하는 **Hyper-v 호스트** 에서 [ConfigureMCNP](https://github.com/Microsoft/SDN/blob/master/Containers/ConfigureMCNP.ps1) 스크립트를 실행 합니다.

```powershell
PS C:\> ConfigureMCNP.ps1
```

### <a name="3-install-the-private-cloud-plug-in"></a>3. 사설 클라우드 플러그 인을 설치 합니다.
이 단계에서는 HNS가 Hyper-v 호스트의 네트워크 프록시와 통신할 수 있도록 플러그 인을 설치 합니다.

플러그 인을 설치 하려면 **컨테이너 호스트 (테 넌 트) 가상 머신**내에서 [InstallPrivateCloudPlugin](https://github.com/Microsoft/SDN/blob/master/Containers/InstallPrivateCloudPlugin.ps1) 스크립트를 실행 합니다.


```powershell
PS C:\> InstallPrivateCloudPlugin.ps1
```

### <a name="4-create-an-l2bridge-container-network"></a>4. *l2bridge* Container Network 만들기
이 단계에서는 **컨테이너 호스트 (테 넌 트) 가상 컴퓨터** 의 `docker network create` 명령을 사용 하 여 l2bridge 네트워크를 만듭니다. 

```powershell
# Create the container network
C:\> docker network create -d l2bridge --subnet="192.168.1.0/24" --gateway="192.168.1.1" MyContainerOverlayNetwork

# Attach a container to the MyContainerOverlayNetwork 
C:\> docker run -it --network=MyContainerOverlayNetwork <image> <cmd>
```

>[!NOTE]
>고정 IP 할당은 지원 되지 않습니다 *l2bridge* 또는 *l2tunnel* 컨테이너 네트워크 Microsoft SDN 스택을 사용 하는 경우.

## <a name="more-information"></a>자세한 정보
SDN 인프라 배포에 대 한 자세한 내용은 [소프트웨어 정의 네트워크 인프라 배포](https://docs.microsoft.com/windows-server/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure)를 참조 하세요.

