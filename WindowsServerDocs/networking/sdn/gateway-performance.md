---
title: Windows Server 2019 게이트웨이 성능
description: ''
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/22/2018
ms.openlocfilehash: a6530b29ce7ffb0d18e0266e70cb2ca45188915c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845634"
---
# <a name="windows-server-2019-gateway-performance"></a>Windows Server 2019 게이트웨이 성능

>적용 대상: Windows Server


Windows Server 2016의 SDN 게이트웨이 최신 네트워크 처리량 요구 사항을 충족할 수 없이 된 고객의 관심사 중 하나입니다. IPsec 및 GRE 터널의 네트워크 처리량은 IPsec 연결에 대 한 300mbps 되 고 약 2.5 g b p s 되 GRE 연결에 대 한 단일 연결 처리량으로 제한 했습니다.

개선 했습니다 크게 Windows Server 2019에 각각 1.8 Gbps 15gbps IPsec 및 GRE 연결을 soaring 번호. 이 모든 것을 CPU 주기를 / 당 바이트, 초 고성능 처리량을 제공 하 여 훨씬 적은 cpu를 사용 하 여 중요 한 축소 합니다.

## <a name="enable-high-performance-with-gateways-in-windows-server-2019"></a>Windows Server 2019에 게이트웨이 사용 하 여 고성능을 사용 하도록 설정

에 대 한 **GRE 연결**, 향상 된 성능 면 있습니다 배포/업그레이드 하는 게이트웨이 Vm에 Windows Server 2019 빌드를 자동으로 표시 됩니다. 수동 단계 없이 포함 됩니다.

에 대 한 **IPsec 연결**, 기본적으로 가상 네트워크에 대 한 연결을 만들 때 얻게 Windows Server 2016 데이터 경로 및 성능 번호입니다. Windows Server 2019 데이터 경로 사용 하도록 설정 하려면 다음을 수행 합니다.

   1. 게이트웨이에서 SDN VM으로 이동 **Services** 콘솔 (services.msc).
   2. 명명 된 서비스를 찾는 **Azure 게이트웨이 서비스**, 시작 유형을 설정 하 고 **자동**합니다.
   3. 게이트웨이 VM을 다시 시작 합니다.
      중복 게이트웨이 VM에 대 한 게이트웨이 장애 조치에 대 한 활성 연결.
   4. 게이트웨이 Vm의 나머지 부분에 대 한 이전 단계를 반복 합니다.

>[!TIP]
>최상의 성능 결과 확인 하는 고 cipherTransformationConstant authenticationTransformConstant IPsec 연결 사용의 빠른 모드 설정에는 **GCMAES256** 암호 그룹입니다.
>
>최상의 성능을 위해 게이트웨이 호스트 하드웨어 AES-NI 및 PCLMULQDQ CPU 명령 집합을 지원 해야 합니다. 이러한 모든 Westmere (32nm) 및 AES-NI가 비활성화 된 모델에서 제외 하 고 이후 Intel CPU에 사용할 수 있습니다. CPU AES-NI 및 PCLMULQDQ CPU 명령 지원 하는지 하드웨어 공급 업체 설명서를 살펴볼 수 있습니다 설정 합니다.

다음은 최적의 보안 알고리즘을 사용 하 여 IPsec 연결의 REST 샘플이입니다.

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

광범위 한 성능 테스트에서 SDN 게이트웨이에 대 한 테스트를 수행한 합니다. 테스트에서 SDN 시나리오 및 SDN 아닌 시나리오에서 Windows Server 2019를 사용 하 여 게이트웨이 네트워크 성능을 비교 합니다. 결과 찾을 하 고 블로그 문서에서 캡처된 설정 세부 정보를 테스트할 수 있습니다 [여기](https://blogs.technet.microsoft.com/networking/2018/08/15/high-performance-gateways/)합니다.

---