---
title: Windows Server 2019 게이트웨이 성능
description: ''
manager: dougkim
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: lizross
author: eross-msft
ms.date: 08/22/2018
ms.openlocfilehash: e8cdf4e100c65fae11637c681924746115444f71
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313019"
---
# <a name="windows-server-2019-gateway-performance"></a>Windows Server 2019 게이트웨이 성능

>적용 대상: Windows Server


Windows Server 2016에서는 고객의 관심사 중 하나가 최신 네트워크의 처리량 요구 사항을 충족할 수 있는 SDN 게이트웨이가 없습니다. IPsec 및 GRE 터널의 네트워크 처리량에는 IPsec 연결에 대 한 단일 연결 처리량에 약 300 Mbps 및 GRE 연결에 대 한 약 2.5 Gbps가 포함 됩니다.

Windows Server 2019에서는 Windows Server에서 크게 개선 되었으며, IPsec 및 GRE 연결에 대 한 숫자는 각각 1.8, soaring는 15gbps입니다. 이러한 모든 기능을 통해 CPU 사이클/바이트 단위로 상당한 비용을 절감할 수 있으므로 CPU 사용률이 훨씬 낮은 고성능 처리량이 제공 됩니다.

## <a name="enable-high-performance-with-gateways-in-windows-server-2019"></a>Windows Server 2019의 게이트웨이에서 높은 성능 사용

**GRE 연결**의 경우 게이트웨이 Vm에서 Windows Server 2019 빌드를 배포/업그레이드 하 고 나면 향상 된 성능을 자동으로 확인 해야 합니다. 수동 단계는 포함 되지 않습니다.

기본적으로 **IPsec 연결**의 경우 가상 네트워크에 대 한 연결을 만들 때 Windows Server 2016 데이터 경로 및 성능 번호를 가져옵니다. Windows Server 2019 데이터 경로를 사용 하도록 설정 하려면 다음을 수행 합니다.

   1. SDN 게이트웨이 VM에서 **서비스** 콘솔 (services.msc)로 이동 합니다.
   2. **Azure 게이트웨이 서비스**라는 서비스를 찾고 시작 유형을 **자동**으로 설정 합니다.
   3. 게이트웨이 VM을 다시 시작 합니다.
      이 게이트웨이의 활성 연결이 중복 게이트웨이 VM으로 장애 조치 (failover) 됩니다.
   4. 나머지 게이트웨이 Vm에 대해 이전 단계를 반복 합니다.

>[!TIP]
>최상의 성능 결과를 위해 IPsec 연결의 빠른 모드 설정에서 cipherTransformationConstant 및 authenticationTransformConstant가 **GCMAES256** 암호 그룹을 사용 하는지 확인 합니다.
>
>최대 성능을 위해 게이트웨이 호스트 하드웨어는 AES-NI 및 PCLMULQDQ CPU 명령 집합을 지원 해야 합니다. 이러한 기능은 AES-NI을 사용 하지 않도록 설정 된 모델을 제외 하 고 모든 Westmere (32nm) 이상 Intel CPU에서 사용할 수 있습니다. 하드웨어 공급 업체 설명서를 살펴보면 CPU에서 AES-NI 및 PCLMULQDQ CPU 명령 집합을 지원 하는지 확인할 수 있습니다.

다음은 최적의 보안 알고리즘을 사용한 IPsec 연결의 REST 샘플입니다.

```PowerShell
# NOTE: The virtual gateway must be created before creating the IPsec connection. More details here.
# Create a new object for Tenant Network IPsec Connection  
$nwConnectionProperties = New-Object Microsoft.Windows.NetworkController.NetworkConnectionProperties   

# Update the common object properties  
$nwConnectionProperties.ConnectionType = "IPSec"   
$nwConnectionProperties.OutboundKiloBitsPerSecond = 2000000   
$nwConnectionProperties.InboundKiloBitsPerSecond = 2000000  

# Update specific properties depending on the Connection Type  
$nwConnectionProperties.IpSecConfiguration = New-Object Microsoft.Windows.NetworkController.IpSecConfiguration   
$nwConnectionProperties.IpSecConfiguration.AuthenticationMethod = "PSK"   
$nwConnectionProperties.IpSecConfiguration.SharedSecret = "111_aaa"   

$nwConnectionProperties.IpSecConfiguration.QuickMode = New-Object Microsoft.Windows.NetworkController.QuickMode   
$nwConnectionProperties.IpSecConfiguration.QuickMode.PerfectForwardSecrecy = "PFS2048"   
$nwConnectionProperties.IpSecConfiguration.QuickMode.AuthenticationTransformationConstant = "GCMAES256"   
$nwConnectionProperties.IpSecConfiguration.QuickMode.CipherTransformationConstant = "GCMAES256"   
$nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeSeconds = 3600   
$nwConnectionProperties.IpSecConfiguration.QuickMode.IdleDisconnectSeconds = 500   
$nwConnectionProperties.IpSecConfiguration.QuickMode.SALifeTimeKiloBytes = 2000   

$nwConnectionProperties.IpSecConfiguration.MainMode = New-Object Microsoft.Windows.NetworkController.MainMode   
$nwConnectionProperties.IpSecConfiguration.MainMode.DiffieHellmanGroup = "Group2"   
$nwConnectionProperties.IpSecConfiguration.MainMode.IntegrityAlgorithm = "SHA256"   
$nwConnectionProperties.IpSecConfiguration.MainMode.EncryptionAlgorithm = "AES256"   
$nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeSeconds = 28800
$nwConnectionProperties.IpSecConfiguration.MainMode.SALifeTimeKiloBytes = 2000   

# L3 specific configuration (leave blank for IPSec)  
$nwConnectionProperties.IPAddresses = @()   
$nwConnectionProperties.PeerIPAddresses = @()   

# Update the IPv4 Routes that are reachable over the site-to-site VPN Tunnel  
$nwConnectionProperties.Routes = @()   
$ipv4Route = New-Object Microsoft.Windows.NetworkController.RouteInfo   
$ipv4Route.DestinationPrefix = "<<On premise subnet that must be reachable over the VPN tunnel. Ex: 10.0.0.0/24>>"   
$ipv4Route.metric = 10   
$nwConnectionProperties.Routes += $ipv4Route   

# Tunnel Destination (Remote Endpoint) Address  
$nwConnectionProperties.DestinationIPAddress = "<<Public IP address of the On-Premise VPN gateway. Ex: 192.168.3.4>>"   

# Add the new Network Connection for the tenant. Note that the virtual gateway must be created before creating the IPsec connection. $uri is the REST URI of your deployment and must be in the form of “https://<REST URI>”  
New-NetworkControllerVirtualGatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId $virtualGW.ResourceId -ResourceId "Contoso_IPSecGW" -Properties $nwConnectionProperties -Force
```

## <a name="testing-results"></a>테스트 결과

테스트 랩에서 SDN 게이트웨이에 대 한 광범위 한 성능 테스트를 완료 했습니다. 이 테스트에서는 SDN 시나리오 및 비 SDN 시나리오에서 Windows Server 2019와 게이트웨이 네트워크 성능을 비교 했습니다. [여기](https://blogs.technet.microsoft.com/networking/2018/08/15/high-performance-gateways/)의 블로그 문서에서 캡처된 결과와 테스트 정보를 확인할 수 있습니다.

---