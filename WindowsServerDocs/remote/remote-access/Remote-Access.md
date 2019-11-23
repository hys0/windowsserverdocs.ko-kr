---
title: 원격 액세스
description: 이 항목에서는 Windows Server 2016의 원격 액세스 서버 역할에 대 한 개요를 제공 합니다.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 05/18/2018
ms.openlocfilehash: d2fa9c82c4cab05b2a60916fee3f09c1ea48a472
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388912"
---
# <a name="remote-access"></a>원격 액세스

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

원격 액세스 가이드에서는 Windows Server 2016의 원격 액세스 서버 역할에 대 한 개요를 제공 하 고 다음 주제를 다룹니다.

- [Always On VPN 배포 가이드](vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)
- [BGP &#40;Border Gateway Protocol&#41;](bgp/Border-Gateway-Protocol-BGP.md)
- [RAS 게이트웨이](ras-gateway/RAS-Gateway.md) 
- [원격 액세스 서버 역할 설명서](ras/Remote-Access-Server-Role-Documentation.md)
- [SDN용 RAS 게이트웨이](../../networking/sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)
- [VPN(가상 사설망)](vpn/vpn-top.md)
 
다른 네트워킹 기술에 대 한 자세한 내용은 [Windows Server 2016의 네트워킹](https://docs.microsoft.com/windows-server/networking/networking)을 참조 하세요.

원격 액세스 서버 역할은 [원격 액세스 서비스 (RAS)](#bkmk_da), [라우팅](#bkmk_rras)및 [웹 응용 프로그램 프록시](#bkmk_proxy)와 같은 관련 네트워크 액세스 기술의 논리적 그룹화입니다. 이러한 기술은 원격 액세스 서버 역할의 *역할 서비스* 입니다. **역할 및 기능 추가 마법사** 또는 Windows PowerShell을 사용 하 여 원격 액세스 서버 역할을 설치 하는 경우이 세 가지 역할 서비스 중 하나 이상을 설치할 수 있습니다.

>[!IMPORTANT]
>Microsoft Azure에서 VM\) \(가상 컴퓨터에 원격 액세스를 배포 하지 마십시오. Microsoft Azure에서 원격 액세스를 사용 하는 것은 지원 되지 않습니다. Azure VM에서 원격 액세스를 사용 하 여 Windows server 2016 또는 이전 버전의 Windows Server에서 VPN, DirectAccess 또는 기타 원격 액세스 기능을 배포할 수 없습니다. 자세한 내용은 [Microsoft Azure 가상 컴퓨터에 대 한 Microsoft 서버 소프트웨어 지원](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)을 참조 하세요.

## <a name="bkmk_da"></a>RAS\) 원격 액세스 서비스 \(-RAS 게이트웨이

**DirectAccess 및 VPN (ras)** 역할 서비스를 설치할 때 **ras Gateway**\)\(원격 액세스 서비스 게이트웨이를 배포 하 게 됩니다. RAS 게이트웨이는 단일 테 넌 트 RAS 게이트웨이 가상 사설망 \(VPN\) 서버, 다중 테 넌 트 RAS 게이트웨이 VPN 서버 및 DirectAccess 서버로 배포할 수 있습니다.

- **RAS 게이트웨이-단일 테 넌 트**. RAS Gateway를 사용 하 여 VPN 연결을 배포 하 여 최종 사용자에 게 조직의 네트워크 및 리소스에 대 한 원격 액세스를 제공할 수 있습니다. 클라이언트에서 Windows 10을 실행 하는 경우 원격 컴퓨터가 인터넷에 연결 될 때마다 클라이언트와 조직 네트워크 간에 영구 연결을 유지 하는 Always On VPN을 배포할 수 있습니다. RAS Gateway를 사용 하 여 기본 사무실과 지사 사이에서 서로 다른 위치에 있는 두 서버 간에 사이트 간 VPN 연결을 만들 수도 있습니다. 네트워크 내의 사용자가 인터넷과 같은 외부 리소스에 액세스할 수 있도록 NAT\) \(네트워크 주소 변환을 사용할 수도 있습니다. 또한 RAS 게이트웨이는 원격 사무실 위치에 BGP를 지 원하는에 지 게이트웨이가 있는 경우 동적 라우팅 서비스를 제공 하는 BGP (Border Gateway Protocol)를 지원 합니다.

- **RAS 게이트웨이-다중 테 넌 트**. \-Hyper-v 네트워크 가상화를 사용 하는 경우 또는 Vlan\)virtual Local Area \(Network를 사용 하 여 배포 된 VM 네트워크를 사용 하는 경우 RAS 게이트웨이를 다중 테 넌 트, 소프트웨어 기반 edge 게이트웨이 및 라우터로 배포할 수 있습니다. RAS 게이트웨이를 사용 하면 클라우드 서비스 공급자 \(Csp\) 및 기업은 인터넷을 포함 하 여 가상 네트워크와 실제 네트워크 간에 데이터 센터 및 클라우드 네트워크 트래픽 라우팅을 사용할 수 있습니다. RAS 게이트웨이를 사용 하 여 테 넌 트는 지점 및 사이트 간 VPN 연결을 사용 하 여 어디서 나 데이터 센터의 VM 네트워크 리소스에 액세스할 수 있습니다. 원격 사이트와 CSP 데이터 센터 간에 사이트 간 VPN 연결을 사용 하 여 테 넌 트를 제공할 수도 있습니다. 또한 동적 라우팅을 위해 BGP를 사용 하 여 RAS 게이트웨이를 구성할 수 있으며 NAT\) \(네트워크 주소 변환을 사용 하도록 설정 하 여 VM 네트워크의 Vm에 대 한 인터넷 액세스를 제공할 수 있습니다.

>[!IMPORTANT]
> 다중 테 넌 트 기능을 포함 하는 RAS 게이트웨이는 Windows Server 2012 r 2 에서도 사용할 수 있습니다.

- **VPN을 Always On**합니다. Always On VPN을 사용 하면 원격 사용자가 VPN에 연결 하지 않고도 내부 네트워크의 공유 리소스, 인트라넷 웹 사이트 및 응용 프로그램에 안전 하 게 액세스할 수 있습니다. 

자세한 내용은 [RAS Gateway](ras-gateway/RAS-Gateway.md) and [Border Gateway Protocol (BGP)](bgp/Border-Gateway-Protocol-BGP.md)를 참조 하세요.

## <a name="bkmk_rras"></a>라우팅이

원격 액세스를 사용 하 여 로컬 영역 네트워크의 서브넷 간에 네트워크 트래픽을 라우팅할 수 있습니다. 라우팅은 NAT (네트워크 주소 변환) 라우터, BGP를 실행 하는 LAN 라우터, RIP (Routing Information Protocol) 및 IGMP (Internet Group Management Protocol)를 사용 하는 멀티 캐스트 가능 라우터를 지원 합니다. 모든 기능을 갖춘 라우터는 Hyper-v를 실행 하는 컴퓨터에서 서버 컴퓨터 또는 VM (가상 컴퓨터)으로 RAS를 배포할 수 있습니다.

원격 액세스를 LAN 라우터로 설치 하려면 서버 관리자에서 역할 및 기능 추가 마법사를 사용 하 여 **원격 액세스** 서버 역할 및 **라우팅** 역할 서비스를 선택 합니다. 또는 Windows PowerShell 프롬프트에서 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.

```  
Install-RemoteAccess -VpnType RoutingOnly
```  

## <a name="bkmk_proxy"></a>웹 응용 프로그램 프록시

웹 응용 프로그램 프록시는 Windows Server 2016의 원격 액세스 역할 서비스입니다. 웹 응용 프로그램 프록시는 회사 네트워크 내부의 웹 응용 프로그램에 역방향 프록시 기능을 제공하여 모든 장치의 사용자가 회사 네트워크 권역을 벗어나서도 해당 네트워크에 액세스할 수 있습니다. 웹 응용 프로그램 프록시는 Active Directory Federation Services (AD FS)를 사용 하 여 웹 응용 프로그램에 대 한 액세스를 사전 인증 하며, AD FS 프록시로도 작동 합니다.

원격 액세스를 웹 응용 프로그램 프록시로 설치 하려면 서버 관리자에서 역할 및 기능 추가 마법사를 사용 하 여 **원격 액세스** 서버 역할 및 **웹 응용 프로그램 프록시** 역할 서비스를 선택 합니다. 또는 Windows PowerShell 프롬프트에서 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.  

```  
Install-RemoteAccess -VpnType SstpProxy  
```  

자세한 내용은 [웹 응용 프로그램 프록시](https://technet.microsoft.com/windows-server-docs/identity/web-application-proxy/web-application-proxy-windows-server)를 참조 하세요.


---