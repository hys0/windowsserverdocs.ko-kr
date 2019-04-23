---
title: 테넌트 가상 네트워크에 컨테이너 끝점 연결
description: 이 항목에서는 살펴보겠습니다 SDN을 통해 만든 기존 테 넌 트 가상 네트워크에 컨테이너 끝점에 연결 하는 방법. l2bridge (및 필요에 따라 l2tunnel)를 사용 하면 네트워크 드라이버 컨테이너 네트워크를 만들려는 테 넌 트 VM에 Docker에 대 한 Windows libnetwork 플러그인을 사용 하 여 사용할 수 있습니다.
manager: ravirao
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7af1eb6-d035-4f74-a25b-d4b7e4ea9329
ms.author: pashort
author: jmesser81
ms.date: 08/24/2018
ms.openlocfilehash: 1968a4db9231459fe5858d9a0f3ba5e8f317ed1b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872744"
---
# <a name="connect-container-endpoints-to-a-tenant-virtual-network"></a>테넌트 가상 네트워크에 컨테이너 끝점 연결

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 살펴보겠습니다 SDN을 통해 만든 기존 테 넌 트 가상 네트워크에 컨테이너 끝점에 연결 하는 방법. 사용 된 *l2bridge* (및 필요에 따라 *l2tunnel*) 네트워크 드라이버 컨테이너 네트워크를 만들려는 테 넌 트 VM에 Docker에 대 한 Windows libnetwork 플러그인을 사용 하 여 사용할 수 있습니다.

에 [컨테이너 네트워크 드라이버](https://docs.microsoft.com/virtualization/windowscontainers/container-networking/network-drivers-topologies) 설명한 항목, 여러 네트워크 드라이버는 Windows에서 Docker를 통해 사용할 수 있습니다. SDN을 사용 합니다 *l2bridge* 하 고 *l2tunnel* 드라이버입니다. 두 드라이버 각 컨테이너 끝점은 컨테이너 (테 넌 트) 호스트 가상 컴퓨터와 동일한 가상 서브넷에 있습니다. 

네트워킹 서비스 HNS (호스트)에서 사설 클라우드 플러그 인을 통해 컨테이너 끝점에 대 한 IP 주소를 동적으로 할당합니다. 컨테이너 끝점을 고유 IP 주소가 있지만 계층 2 주소 변환으로 인해 컨테이너 (테 넌 트) 호스트 가상 컴퓨터의 같은 MAC 주소를 공유 합니다. 

네트워크 정책 (예: Acl, 간략화 및 QoS) 이러한 컨테이너 끝점에 대 한 네트워크 컨트롤러에서 받은 실제 Hyper-v 호스트에 적용 되며 상위 계층 관리 시스템에 정의 됩니다. 

차이 *l2bridge* 하 고 *l2tunnel* 드라이버:

| l2bridge | l2tunnel |
| --- | --- |
|에 있는 컨테이너 끝점: <ul><li>동일한 컨테이너 가상 머신 호스트 및 동일한 서브넷에는 모든 네트워크 트래픽은 Hyper-v 가상 스위치에서 브리지입니다. </li><li>다른 컨테이너 호스트 Vm 또는 서로 다른 서브넷에 실제 Hyper-v 호스트에 전달 하는 트래픽을 가집니다. </li></ul>물리적 호스트에 동일한 호스트와 동일한 서브넷 컨테이너 간에 네트워크 트래픽을 전달 되지 않습니다 이후 네트워크 정책이 적용 가져오기지 않습니다. 네트워크 정책에만 호스트 간 또는 서브넷 간 컨테이너 네트워크 트래픽에 적용 됩니다. | *모든* 두 컨테이너 끝점 간에 네트워크 트래픽을 호스트 또는 서브넷에 관계 없이 물리적 Hyper-v 호스트에 전달 됩니다. 네트워크 정책 서브넷 간 및 호스트 간 네트워크 트래픽 모두에 적용 됩니다. |
---

>[!NOTE]
>이러한 네트워킹 모드 Azure 공용 클라우드에서 테 넌 트 가상 네트워크에 연결 하는 windows 컨테이너 끝점이 작동 하지 않습니다.


## <a name="prerequisites"></a>사전 요구 사항
-  네트워크 컨트롤러를 사용 하 여 배포 된 SDN 인프라입니다.
-  테 넌 트 가상 네트워크를 만들었습니다.
-  Docker 설치 및 Hyper-v 기능을 사용할 수 Windows 컨테이너 기능을 사용 하 여 배포 된 테 넌 트 가상 머신을 사용 합니다. Hyper-v 기능은 l2bridge 및 l2tunnel 네트워크에 대 한 몇 가지 바이너리를 설치 해야 합니다.

   ```powershell
   # To install HyperV feature without checks for nested virtualization
   dism /Online /Enable-Feature /FeatureName:Microsoft-Hyper-V /All 
   ```

>[!Note]
>[중첩 된 가상화](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/nesting) 가상화 확장을 노출 하지 않는 필수 Hyper-v 컨테이너를 사용 하 고 있습니다. 


## <a name="workflow"></a>워크플로

[1. 네트워크 컨트롤러 (Hyper-v 호스트)를 통해 기존 VM NIC 리소스에 여러 IP 구성 추가](#1-add-multiple-ip-configurations)
[2입니다. 컨테이너 끝점 (Hyper-v 호스트)에 대 한 CA IP 주소를 할당 하려면 호스트에서 네트워크 프록시를 사용 ](#2-enable-the-network-proxy) 
 [3입니다. 사설 클라우드 (컨테이너 호스트 VM) 컨테이너 끝점 CA IP 주소를 할당 하는 플러그 인 설치 ](#3-install-the-private-cloud-plug-in) 
 [4입니다. 만들기는 *l2bridge* 하거나 *l2tunnel* docker (컨테이너 호스트 VM)를 사용 하 여 네트워크 ](#4-create-an-l2bridge-container-network)
 
>[!NOTE]
>System Center Virtual Machine Manager를 통해 만든 VM NIC 리소스에 대해 여러 IP 구성이 지원 되지 않습니다. 것이 좋습니다 이러한 배포 유형에 대 한 네트워크 컨트롤러 PowerShell을 사용 하 여 대역 외에서 VM NIC 리소스를 만들어야 합니다.

### <a name="1-add-multiple-ip-configurations"></a>1. 여러 IP 구성 추가
이 단계에서는 테 넌 트 가상 컴퓨터의 VM NIC 192.168.1.9 IP 주소로 IP 구성이 하나만 있고 192.168.1.0/24 IP 서브넷의 VNet 리소스 ID 'VNet1' 및 'Subnet1'의 VM 서브넷 리소스에 연결 되어 가정 합니다. 192.168.1.101-에서 컨테이너에 대 한 10 개의 IP 주소 추가 합니다 192.168.1.110 합니다.

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
이 단계에서는 컨테이너 호스트 가상 머신의 여러 IP 주소를 할당할 네트워크 프록시를 사용 합니다. 

네트워크 프록시를 사용 하도록 설정 하려면 실행 합니다 [ConfigureMCNP.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/ConfigureMCNP.ps1) 의 스크립트를 **Hyper-v 호스트** 컨테이너 (테 넌 트) 호스트 가상 컴퓨터를 호스트 합니다.

```powershell
PS C:\> ConfigureMCNP.ps1
```

### <a name="3-install-the-private-cloud-plug-in"></a>3. 사설 클라우드 플러그 인 설치
이 단계는 HNS에서 Hyper-v 호스트의 네트워크 프록시와 통신할 수 있도록 플러그 인 설치 합니다.

플러그 인을 설치 하려면 다음을 실행 합니다 [InstallPrivateCloudPlugin.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/InstallPrivateCloudPlugin.ps1) 내에서 스크립트를 **컨테이너 (테 넌 트) 호스트 가상 머신**.


```powershell
PS C:\> InstallPrivateCloudPlugin.ps1
```

### <a name="4-create-an-l2bridge-container-network"></a>4. 만들기는 *l2bridge* 컨테이너 네트워크
이 단계에서는 사용 하 여 합니다 `docker network create` 명령을 합니다 **컨테이너 (테 넌 트) 호스트 가상 머신** l2bridge 네트워크를 만들려면. 

```powershell
# Create the container network
C:\> docker network create -d l2bridge --subnet="192.168.1.0/24" --gateway="192.168.1.1" MyContainerOverlayNetwork

# Attach a container to the MyContainerOverlayNetwork 
C:\> docker run -it --network=MyContainerOverlayNetwork <image> <cmd>
```

>[!NOTE]
>고정 IP 할당은 지원 되지 않습니다 *l2bridge* 또는 *l2tunnel* 컨테이너 네트워크 Microsoft SDN 스택을 사용 하는 경우.

## <a name="more-information"></a>자세한 정보
SDN 인프라를 배포 하는 방법에 대 한 자세한 내용은 참조 하세요. [소프트웨어 정의 네트워크 인프라 배포](https://docs.microsoft.com/windows-server/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure)합니다.

