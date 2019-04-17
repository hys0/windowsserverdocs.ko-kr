---
title: 컨테이너 가상 네트워크에 연결
description: 이 항목은 관리 테 작업 및 Windows Server 2016에 가상 네트워크 방법에 대해 소프트웨어 네트워킹 정의 가이드 일부입니다.
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
ms.openlocfilehash: 801cf4b8f71935eb72d820d47e523a310fa64562
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="connect-container-endpoints-to-a-tenant-virtual-network"></a>컨테이너 끝점 테 가상 네트워크에 연결

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목에서는 컨테이너 끝점 Microsoft 소프트웨어 정의 네트워킹 (SDN) 스택 통해 생성 기존 테 가상 네트워크에 연결 하는 방법을 보여 줍니다. 사용 합니다는 *l2bridge* (고 필요에 따라 *l2tunnel*) 네트워크 드라이버와 컨테이너 네트워크 컨테이너 호스트 (테) 가상 컴퓨터에서 만들려는 Docker에 대 한 Windows libnetwork 플러그 인 사용할 수 있습니다.

에 명시 된 대로 [컨테이너 네트워킹](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/management/container_networking) MSDN 항목이, 여러 네트워크 드라이버는 Windows에서 Docker 시까지 제공 됩니다. SDN에 가장 적합 한 드라이버를 *l2bridge* 및 *l2tunnel*합니다. 두 드라이버에 대 한 각 컨테이너 끝점 컨테이너 호스트 (테) 가상 컴퓨터와 동일한 가상 서브넷 중인 합니다. 여는 호스트 네트워킹 서비스 (HNS) 개인 클라우드 플러그 인을 통해의 IP 주소를 컨테이너 끝점 동적으로 지정 됩니다. 컨테이너 끝점 고유한 IP 주소가 있지만 2 계층 주소 변환 인해 컨테이너 호스트 (테) 가상 컴퓨터의 같은 MAC 주소를 공유 합니다. 네트워크 정책 (예: Acl, 간략화 및 QoS)이 컨테이너 끝점 네트워크 컨트롤러에서 수신 실제 Hyper-v 호스트에 적용 되며 상위 계층 관리 시스템에 정의 된에 대 한 합니다. 약간의 차이가 *l2bridge* 및 *l2tunnel* 아래에 설명 된 드라이버 합니다.

- **L 2 다리** -동일한 컨테이너 호스트 가상 컴퓨터에 있는 같은 서브넷 되 고 있는 컨테이너 끝점은 Hyper-v의 가상 스위치 내 브리지 모든 네트워크 교통 합니다. 컨테이너 끝점 서로 다른 서브넷은는 하거나 다른 컨테이너 호스트 Vm에 존재 하는 물리적 Hyper-v 호스트 전달 트래픽을 합니다. 컨테이너 같은 서브넷와 같은 호스트에서 간에 네트워크 교통 물리적 호스트 이동 하지 않는, 이후 없는 네트워크 정책이 적용 됩니다. 정책 간 호스트 또는 간 서브넷 컨테이너 네트워크 교통에만 적용 됩니다.  
 
- **L 2 터널** - *모든* 실제 Hyper-v 호스트 호스트 또는 서브넷 관계 없이 네트워크 교통 두 컨테이너 끝점 간의 전달 됩니다. 크로스 서브넷 및 간 호스트 네트워크 교통량 네트워크 정책이 적용 됩니다.   

>[!NOTE]
>이러한 네트워킹 모드 연결 windows 컨테이너 끝점 공개 Azure 클라우드 테 가상 네트워크에 대해 작동 하지 않습니다.

## <a name="prerequistes"></a>필수 구성 요소
 * 네트워크 컨트롤러와 SDN 인프라 배포한
 * 테 가상 네트워크를 만들었는지
 * 테 가상 컴퓨터 Windows 컨테이너 기능을 사용 하면, Docker 설치 및 Hyper-v 기능을 사용 하면 배포한

>[!Note]
>[중첩된 가상화](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/nesting) virtualization 확장 노출 필요 없는 아니면 l2bridge 및 l2tunnel 네트워크에 대 한 몇 가지 바이너리를 설치 하는 데 필요한 Hyper-v 컨테이너 The HyperV 기능을 사용 하 고

```powershell
# To install HyperV feature without checks for nested virtualization
dism /Online /Enable-Feature /FeatureName:Microsoft-Hyper-V /All 
```

 

## <a name="workflow"></a>워크플로

1. [네트워크 컨트롤러를 통해 기존 VM NIC 리소스에 여러 IP 구성을 추가](#Add) (Hyper-v 호스트)
2. [호스트 IP 주소 캘리포니아 컨테이너 끝점에 할당에서 네트워크 프록시 설정](#Enable) (Hyper-v 호스트) 
3. [플러그 인을 컨테이너 끝점 캘리포니아 IP 주소를 지정 하려면 개인 클라우드 설치](#Install) (컨테이너 호스트 VM) 
4. [만들기는 *l2bridge* 또는 *l2tunnel* docker를 사용 하 여 네트워크](#Create) (컨테이너 호스트 VM) 
 
>[!NOTE]
>System Center 가상 컴퓨터 Manager 만든 VM NIC 리소스에는 여러 IP 구성은 지원 되지 않습니다. 것이 좋습니다 이러한 배포 유형에 네트워크 컨트롤러 PowerShell를 사용 하 여 대역 VM NIC 리소스를 만들 수 있습니다.

### <a name="Add"></a>1. 여러 IP 구성 추가

예를이 들어가 했습니다 가정 테 가상 컴퓨터의 VM NIC 이미 192.168.1.9의 IP 주소와 한 IP 구성이 192.168.1.0 월 24 IP 서브넷에서 'VNet1' VNet 리소스 ID 및 'Subnet1'의 VM 서브넷 리소스에 연결 합니다. 컨테이너 10 IP 주소에서 192.168.1.101-192.168.1.110 추가 될 것입니다.

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

### <a name="Enable"></a>2. 네트워크 프록시 설정

[ConfigureMCNP.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/ConfigureMCNP.ps1>)

이 스크립트를 실행할는 **Hyper-v 호스트** 네트워크 프록시 컨테이너 호스트 가상 컴퓨터에 대 한 여러 IP 주소를 할당를 사용 하도록 설정 하려면 컨테이너 호스트 (테) 가상 컴퓨터 호스팅하고 합니다.

```powershell
PS C:\> ConfigureMCNP.ps1
```

### <a name="Install"></a>3. 개인 클라우드 플러그 인을 설치 합니다.

[InstallPrivateCloudPlugin.ps1](https://github.com/Microsoft/SDN/blob/master/Containers/InstallPrivateCloudPlugin.ps1)

내이 스크립트를 실행할는 **컨테이너 호스트 (테) 가상 컴퓨터** Hyper-v 호스트 네트워크 프록시와 통신 하도록 호스트 네트워킹 서비스 (HNS) 수 있도록 합니다.

```powershell
PS C:\> InstallPrivateCloudPlugin.ps1
```

### <a name="Create"></a>4. 작성 된 *l2bridge* 컨테이너 네트워크

에 **컨테이너 호스트 (테) 가상 컴퓨터** 사용는 `docker network create`명령을 l2bridge 네트워크를 만들려면

```powershell
# Create the container network
C:\> docker network create -d l2bridge --subnet="192.168.1.0/24" --gateway="192.168.1.1" MyContainerOverlayNetwork

# Attach a container to the MyContainerOverlayNetwork 
C:\> docker run -it --network=MyContainerOverlayNetwork <image> <cmd>
```

>[!NOTE]
>고정 IP 할당 지원 되지 않습니다 *l2bridge* 또는 *l2tunnel* 컨테이너 Microsoft SDN 스택와 함께 사용할 경우 네트워크입니다.

## <a name="more-information"></a>자세한 내용
배포 SDN 인프라에 대해 더 많은 infortation 참조 [소프트웨어 정의 네트워크 인프라 배포](https://technet.microsoft.com/en-us/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure)합니다.

