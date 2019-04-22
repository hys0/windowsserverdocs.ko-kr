---
title: 원격 액세스
description: 이 항목에서는 Windows Server 2016에서 원격 액세스 서버 역할의 개요를 제공합니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 05/18/2018
ms.openlocfilehash: faf12ad22678fa58ea933613759e3e8414966bca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818364"
---
# <a name="remote-access"></a>원격 액세스

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

원격 액세스 가이드 Windows Server 2016에서 원격 액세스 서버 역할의 개요를 제공 하 고 다음 주제를 다룹니다.

- [Always On VPN 배포 가이드](vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)
- [경계 게이트웨이 프로토콜 &#40;BGP&#41;](bgp/Border-Gateway-Protocol-BGP.md)
- [RAS Gateway](ras-gateway/RAS-Gateway.md) 
- [원격 액세스 서버 역할 설명서](ras/Remote-Access-Server-Role-Documentation.md)
- [SDN 용 RAS 게이트웨이](../../networking/sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)
- [가상 사설망 (VPN)](vpn/vpn-top.md)
 
다른 네트워킹 기술에 대 한 자세한 내용은 참조 하세요. [Windows Server 2016에서 네트워킹](https://docs.microsoft.com/windows-server/networking/networking)합니다.

원격 액세스 서버 역할은 이러한 관련된 네트워크 액세스 기술의 논리적 그룹화: [원격 액세스 서비스 (RAS)](#bkmk_da)하십시오 [라우팅](#bkmk_rras), 및 [웹 응용 프로그램 프록시](#bkmk_proxy)합니다. 이러한 기술은 원격 액세스 서버 역할의 *역할 서비스* 입니다. 사용 하 여 원격 액세스 서버 역할을 설치 하는 경우는 **역할 및 추가 기능 마법사** 하거나 Windows PowerShell에서 이러한 세 가지 역할 서비스 중 하나 이상을 설치할 수 있습니다.

>[!IMPORTANT]
>가상 컴퓨터에서 원격 액세스를 배포 하지 마세요 \(VM\) Microsoft Azure에서. 원격 액세스를 사용 하 여 Microsoft Azure에서 지원 되지 않습니다. VPN, DirectAccess, 또는 Windows Server 2016 또는 이전 버전의 Windows Server의 다른 모든 원격 액세스 기능을 배포 하려면 Azure VM에서 원격 액세스를 사용할 수 없습니다. 자세한 내용은 [Microsoft Azure virtual machines에 대 한 Microsoft 서버 소프트웨어 지원](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)합니다.

## <a name="bkmk_da"></a>원격 액세스 서비스 \(RAS\) -RAS 게이트웨이

설치 하는 경우는 **DirectAccess 및 VPN (RAS)** 역할 서비스를 원격 액세스 서비스 게이트웨이 배포 하는 \( **RAS 게이트웨이**\)합니다. RAS 게이트웨이 단일 테 넌 트 RAS 게이트웨이 가상 개인 네트워크를 배포할 수 있습니다 \(VPN\) 서버, 다중 테 넌 트 RAS 게이트웨이 VPN 서버와 DirectAccess 서버.

- **단일 테 넌 트 RAS 게이트웨이-** 합니다. RAS 게이트웨이 사용 하 여 VPN 연결을 통해 조직의 네트워크와 리소스에 대 한 원격 액세스를 사용 하 여 최종 사용자에 게 배포할 수 있습니다. 클라이언트는 Windows 10을 실행 하는 경우 Always On VPN, 원격 컴퓨터가 인터넷에 연결 되어 때마다 클라이언트와 조직 네트워크에 영구 연결을 유지 관리 하는 배포할 수 있습니다. RAS 게이트웨이 사용 하 여 있습니다도 다른 위치에 있는 두 서버 간에 사이트 간 VPN 연결을 같은 주 사무실 및 지점 간 만들고 사용할 수 있는 Network Address Translation \(NAT\) 있도록 내에서 사용자는 네트워크에는 인터넷과 같은 외부 리소스에 액세스할 수 있습니다. 또한 RAS 게이트웨이 프로토콜 BGP (경계 게이트웨이), 원격 사무실 위치에 있어야 edge 게이트웨이에 BGP를 지 원하는 경우 동적 라우팅 서비스를 제공 하는 지원 합니다.

- **RAS 게이트웨이-다중 테 넌 트**합니다. 하이퍼를 사용 하는 경우 다중 테 넌 트, 소프트웨어 기반 edge 게이트웨이 및 라우터로 RAS 게이트웨이 배포할 수 있습니다\-V 네트워크 가상화 또는 사용자가 가상 로컬 영역 네트워크를 사용 하 여 배포 된 VM 네트워크가 \(Vlan\)합니다. RAS 게이트웨이 클라우드 서비스 공급자를 사용 하 여 \(Csp\) 기업 데이터 센터를 사용 하도록 설정 하 고 인터넷을 포함 하 여, 가상 및 실제 네트워크 간의 네트워크 트래픽 라우팅을 클라우드 수 있습니다. RAS 게이트웨이 사용 하 여 테 넌 트 어디에서 나 데이터 센터에서 해당 VM 네트워크 리소스에 액세스 하려면 지점 하므로 사이트 간 VPN 연결을 사용할 수 있습니다. 또한 해당 원격 사이트와 CSP 데이터 센터 간의 사이트 간 VPN 연결을 사용 하 여 테 넌 트에 제공할 수 있습니다. 또한 동적 라우팅을 위해 BGP를 사용 하 여 RAS 게이트웨이 구성할 수 있습니다 및 설정할 수 있습니다. Network Address Translation \(NAT\) VM 네트워크에서 Vm에 대해 인터넷 액세스를 제공 합니다.

>[!IMPORTANT]
> RAS 게이트웨이 다중 테 넌 트 기능을 사용 하 여 Windows Server 2012 R2에서 제공 됩니다.

- **VPN에 항상**합니다. Always On VPN 원격 사용자가 VPN에 연결 하지 않고 공유 리소스, 웹 사이트, 인트라넷 및 내부 네트워크에서 응용 프로그램을 안전 하 게 액세스할 수 있습니다. 

자세한 내용은 [RAS 게이트웨이](ras-gateway/RAS-Gateway.md) 하 고 [프로토콜 BGP (경계 게이트웨이)](bgp/Border-Gateway-Protocol-BGP.md)합니다.

## <a name="bkmk_rras"></a>라우팅

원격 액세스를 사용 하 여 로컬 영역 네트워크에서 서브넷 간에 네트워크 트래픽을 라우팅할 수 있습니다. 라우팅은 네트워크 주소 변환 (NAT) 라우터에, BGP, 라우팅 RIP (Information Protocol), 및 그룹 관리 IGMP (Internet Protocol)를 사용 하 여 멀티 캐스트 가능 라우터를 실행 하는 LAN 라우터에 대 한 지원을 제공 합니다. Hyper-v를 실행 하는 컴퓨터에서 가상 머신 (VM) 또는 서버 컴퓨터에서 모든 기능을 갖춘 라우터, RAS를 배포할 수 있습니다.

LAN 라우터 원격 액세스를 설치 하려면 서버 관리자에서 추가 역할 및 기능 마법사를 사용 하거나 및이 선택 합니다 **원격 액세스** 서버 역할 및 **라우팅** 역할 서비스 또는 다음 형식 Windows PowerShell 프롬프트에서 명령을 클릭 한 다음 ENTER를 누릅니다.

```  
Install-RemoteAccess -VpnType RoutingOnly
```  

## <a name="bkmk_proxy"></a>웹 응용 프로그램 프록시

웹 응용 프로그램 프록시는 Windows Server 2016에서 원격 액세스 역할 서비스. 웹 응용 프로그램 프록시는 회사 네트워크 내부의 웹 응용 프로그램에 역방향 프록시 기능을 제공하여 모든 장치의 사용자가 회사 네트워크 권역을 벗어나서도 해당 네트워크에 액세스할 수 있습니다. 웹 응용 프로그램 프록시 사전 Active Directory Federation Services (AD FS)를 사용 하 여 웹 응용 프로그램에 대 한 액세스를 인증 하 고 AD FS 프록시로 작동 합니다.

원격 액세스는 웹 응용 프로그램 프록시를 설치 하려면 서버 관리자에서 추가 역할 및 기능 마법사를 사용 하거나 및이 선택 합니다 **원격 액세스** 서버 역할 및 **웹 응용 프로그램 프록시** 역할 서비스 또는 Windows PowerShell 프롬프트에서 다음 명령을 입력 하 고 enter 키를 누릅니다.  

```  
Install-RemoteAccess -VpnType SstpProxy  
```  

자세한 내용은 [웹 응용 프로그램 프록시](https://technet.microsoft.com/windows-server-docs/identity/web-application-proxy/web-application-proxy-windows-server)합니다.


---