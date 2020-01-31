---
title: 1 단계 고급 DirectAccess 인프라 계획
description: 이 항목은 Windows Server 2016에 대 한 고급 설정을 사용 하 여 단일 DirectAccess 서버 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aa3174f3-42af-4511-ac2d-d8968b66da87
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bb8bb6dda6eab27413b462a4c7f17176fbed85a1
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822776"
---
# <a name="step-1-plan-the-advanced-directaccess-infrastructure"></a>1 단계 고급 DirectAccess 인프라 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

단일 서버에 대한 고급 DirectAccess 배포 계획의 첫 번째 단계는 배포에 필요한 인프라를 계획하는 것입니다. 이 항목에서는 인프라 계획 단계에 대해 설명합니다. 이러한 계획 작업은 특정 순서대로 완료할 필요가 없습니다.  
  
|작업|설명|
|----|--------|  
|[1.1 네트워크 토폴로지 및 설정 계획](#11-plan-network-topology-and-settings)|DirectAccess 서버의 위치(NAT(네트워크 주소 변환) 디바이스 또는 방화벽의 경계면이나 뒤)를 결정하고 IP 주소 지정, 라우팅 및 강제 터널링을 계획합니다.|  
|[1.2 방화벽 요구 사항 계획](#12-plan-firewall-requirements)|DirectAccess 트래픽이 경계면 방화벽을 통과하도록 허용할 계획을 수립합니다.|  
|[1.3 인증서 요구 사항 계획](#13-plan-certificate-requirements)|클라이언트 인증에 Kerberos를 사용할지 또는 인증서를 사용할지 결정하고 웹 사이트 인증서를 계획합니다. IP-HTTPS는 DirectAccess 클라이언트가 IPv4 네트워크상의 IPv6 트래픽을 터널링하는 데 사용되는 변환 프로토콜입니다. CA(인증 기관)에서 발급한 인증서를 사용하여 IP-HTTPS 서버의 인증을 받을지 또는 DirectAccess 서버에서 자동으로 발급한 자체 서명된 인증서를 사용하여 IP-HTTPS 서버의 인증을 받을지 결정합니다.|  
|[1.4 DNS 요구 사항 계획](#14-plan-dns-requirements)|Domain Name System 서버, 인프라 서버, 로컬 이름 확인 옵션 및 클라이언트 연결에 대한 DNS(Domain Name System) 설정을 계획합니다.|  
|[1.5 네트워크 위치 서버 계획](#15-plan-the-network-location-server)|네트워크 위치 서버는 DirectAccess 클라이언트가 내부 네트워크에 있는지 확인하는 데 사용됩니다. 조직에서 네트워크 위치 서버 웹 사이트를 배치할 위치(DirectAccess 서버 또는 대체 서버)를 결정하고, 네트워크 위치 서버를 DirectAccess 서버에 둘 경우 인증서 요구 사항을 계획합니다.|  
|[1.6 관리 서버 계획](#16-plan-management-servers)|인터넷에서 회사 네트워크 외부에 있는 DirectAccess 클라이언트 컴퓨터를 원격으로 관리할 수 있습니다. 원격 클라이언트 관리 시 사용되는 관리 서버(예: 업데이트 서버)를 계획합니다.|  
|[1.7 계획 Active Directory Domain Services](#17-plan-active-directory-domain-services)|도메인 컨트롤러, Active Directory 요구 사항, 클라이언트 인증 및 여러 도메인을 계획합니다.|  
|[1.8 그룹 정책 개체 계획](#18-plan-group-policy-objects)|조직에 필요한 GPO 및 GPO를 만들거나 편집할 방법을 결정합니다.|  
  
## <a name="11-plan-network-topology-and-settings"></a>1.1 네트워크 토폴로지 및 설정 계획

이 섹션에서는 다음을 비롯한 네트워크 계획 방법을 설명합니다.  
  
- [1.1.1 네트워크 어댑터 및 IP 주소 지정 계획](#111-plan-network-adapters-and-ip-addressing)  
  
- [1.1.2 Plan IPv6 인트라넷 연결](#112-plan-ipv6-intranet-connectivity)  
  
- [강제 터널링에 대 한 1.1.3 계획](#113-plan-for-force-tunneling)  
  
### <a name="111-plan-network-adapters-and-ip-addressing"></a>1.1.1 네트워크 어댑터 및 IP 주소 지정 계획  
  
1. 사용할 네트워크 어댑터 토폴로지를 확인합니다. 다음 토폴로지 중 하나를 사용하여 DirectAccess를 설정할 수 있습니다.  
  
    - **두 개의 네트워크 어댑터가**합니다. 네트워크 어댑터를 인터넷과 내부 네트워크에 각각 하나씩 연결하여 경계면에 DirectAccess 서버를 설치하거나, 네트워크 어댑터를 경계 네트워크와 내부 네트워크에 각각 하나씩 연결하여 NAT, 방화벽 또는 라우터 디바이스 뒤에 DirectAccess 서버를 설치할 수 있습니다.  
  
    - **네트워크 어댑터 1 개**합니다. DirectAccess 서버를 NAT 디바이스 뒤에 설치하고, 단일 네트워크 어댑터를 인터넷 네트워크에 연결합니다.  
  
2. IP 주소 지정 요구 사항을 확인합니다.  
  
    DirectAccess는 IPsec에서 IPv6을 사용하여 DirectAccess 클라이언트 컴퓨터와 회사 내부 네트워크 사이의 보안 연결을 만듭니다. 그러나 DirectAccess를 사용하기 위해 반드시 IPv6 인터넷 또는 내부 네트워크에서 지원되는 기본 IPv6에 연결할 필요는 없습니다. 대신, DirectAccess는 IPv6 전환 기술을 자동으로 구성하고 이를 사용하여 IPv4 인터넷(6to4, Teredo 또는 IP-HTTPS 사용) 및 IPv4 전용 인트라넷(NAT64 또는 ISATAP 사용)에서 IPv6 트래픽을 터널링합니다. 이러한 전환 기술에 대한 개요는 다음 리소스를 참조하세요.  
  
    - [IPv6 전환 기술](https://technet.microsoft.com/library/bb726951.aspx)  
  
    - [IP-HTTPS 터널링 프로토콜 사양](https://msdn.microsoft.com/library/dd358571(PROT.10).aspx)  
  
3. 다음 표에 따라 필요한 어댑터 및 주소를 구성합니다. 만 사용 하 여 IP 주소를 구성 하는 단일 네트워크 어댑터를 사용 하는 NAT 디바이스 뒤 설정 하는 배포에 대 한는 **내부 네트워크 어댑터** 열입니다.  
  
    ||외부 네트워크 어댑터|내부 네트워크 어댑터|라우팅 요구 사항|  
    |-|--------------|--------------|------------|  
    |IPv4 인터넷 및 IPv4 인트라넷|적절한 서브넷 마스크를 사용하는 두 개의 연속된 고정 IPv4 주소를 구성합니다(Teredo에만 필요).<br/><br/>또한 인터넷 방화벽이나 로컬 ISP(인터넷 서비스 공급자) 라우터의 기본 게이트웨이 IPv4 주소를 구성합니다. **참고:** DirectAccess 서버가 Teredo 서버 처럼 작동할 수 및 Windows 기반 클라이언트 있는 NAT 디바이스 유형을 검색 하는 DirectAccess 서버를 사용할 수 있도록 두 개의 공용 IPv4 주소가 필요 합니다.|다음을 구성합니다.<br/><br/>-적절 한 서브넷 마스크는 IPv4 인트라넷 주소입니다.<br/>인트라넷 네임 스페이스의 연결별 DNS 접미사. DNS 서버도 내부 인터페이스에 구성해야 합니다. **주의:** 인트라넷 인터페이스의 기본 게이트웨이 구성 하지 마십시오.|DirectAccess 서버에서 내부 IPv4 네트워크의 모든 서브넷에 연결하도록 구성하려면 다음을 수행합니다.<br/><br/>-인트라넷의 모든 위치에 대 한 IPv4 주소 공간을 나열 합니다.<br/>-사용는 **경로 추가-p** 또는**경로 추가 하는 netsh interface ipv4** DirectAccess 서버의 IPv4 라우팅 테이블에 고정 경로로 IPv4 주소 공간을 추가 하는 명령입니다.|  
    |IPv6 인터넷 및 IPv6 인트라넷|다음을 구성합니다.<br/><br/>-ISP에서 제공 되는 주소 구성을 사용 합니다.<br/>-사용 된 **Route Print** 기본 IPv6 경로가 존재 하 고 IPv6 라우팅 테이블에서 ISP 라우터를 가리키는지 확인 하는 명령입니다.<br/>-ISP 및 인트라넷 라우터가 RFC 4191에 설명 하 고 로컬 인트라넷 라우터 보다 높은 기본 기본 설정을 사용 하 여 기본 라우터 설정을 사용 하는 여부를 결정 합니다.<br/>    둘 다에 해당되면 기본 경로에 대한 다른 구성이 필요하지 않습니다. ISP 라우터의 우선 순위가 높으면 DirectAccess 서버의 활성 기본 IPv6 경로가 IPv6 인터넷을 가리킵니다.<br/><br/>DirectAccess 서버가 IPv6 라우터이므로 기본 IPv6 인프라가 있는 경우 인터넷 인터페이스에서 인트라넷의 도메인 컨트롤러에도 연결할 수 있습니다. 이 경우 경계 네트워크의 도메인 컨트롤러에 패킷 필터를 추가하여 DirectAccess 서버의 인터넷 연결 인터페이스에 대한 IPv6 주소 연결을 방지할 수 있습니다.|다음을 구성합니다.<br/><br/>-기본 우선 수준을 사용 하지 않는 경우 다음 명령을 사용 하 여 인트라넷 인터페이스를 구성할 수 있습니다**netsh 인터페이스 ipv6 set InterfaceIndex ignoredefaultroutes = 활성화**합니다.<br/>    이 명령을 사용하면 인트라넷 라우터를 가리키는 추가 기본 경로가 IPv6 라우팅 테이블에 추가되지 않습니다. 다음 명령을 사용 하 여 인트라넷 인터페이스의 인터페이스 인덱스를 가져올 수 있습니다: **인터페이스를 표시 하는 netsh interface ipv6**합니다.|IPv6 인트라넷을 사용하는 경우 모든 IPv6 위치에 연결하도록 DirectAccess 서버를 구성하려면 다음을 수행합니다.<br/><br/>-인트라넷의 모든 위치에 대 한 IPv6 주소 공간을 나열 합니다.<br/>-사용 된 **netsh interface ipv6 경로 추가** DirectAccess 서버의 IPv6 라우팅 테이블에 고정 경로로 IPv6 주소 공간을 추가 하는 명령.|  
    |IPv4 인터넷 및 IPv6 인트라넷|DirectAccess 서버는 Microsoft 6to4 어댑터를 통해 기본 IPv6 경로 트래픽을 IPv4 인터넷의 6to4 릴레이에 전달합니다. `netsh interface ipv6 6to4 set relay name=<ipaddress> state=enabled` 명령을 사용하여 Microsoft 6to4 어댑터의 IPv4 주소에 대한 DirectAccess 서버를 구성할 수 있습니다.|||  
  
    > [!NOTE]  
    > - DirectAccess 클라이언트에 공용 IPv4 주소가 할당된 경우 DirectAccess 클라이언트는 6to4 전환 기술을 사용하여 인트라넷에 연결합니다. 개인 IPv4 주소를 할당된 경우에는 Teredo를 사용합니다. DirectAccess 클라이언트는 6to4 또는 Teredo를 사용하여 DirectAccess 서버에 연결할 수 없는 경우 IP-HTTPS를 사용합니다.  
    > - Teredo를 사용하려면 외부 연결 네트워크 어댑터에서 두 개의 연속된 IP 주소를 구성해야 합니다.  
    > - DirectAccess 서버에 네트워크 어댑터가 하나만 있는 경우에는 Teredo를 사용할 수 없습니다.  
    > - 기본 IPv6 클라이언트 컴퓨터는 기본 IPv6을 통해 DirectAccess 서버에 연결할 수 있으므로 전환 기술이 필요 없습니다.  
  
### <a name="112-plan-ipv6-intranet-connectivity"></a>1.1.2 IPv6 인트라넷 연결 계획

원격 DirectAccess 클라이언트를 관리하려면 IPv6이 필요합니다. IPv6을 통해 DirectAccess 관리 서버는 인터넷에 있는 DirectAccess 클라이언트에 연결하여 원격 관리를 수행할 수 있습니다.  
  
> [!NOTE]  
> - 네트워크에서 IPv6을 사용하는 것은 DirectAccess 클라이언트 컴퓨터에서 조직 네트워크의 IPv4 리소스에 연결하도록 지원하는 데 필요한 것이 아닙니다. 이 용도에는 NAT64/DNS64가 사용됩니다.  
> - 원격 DirectAccess 클라이언트를 관리하지 않는 경우에는 IPv6을 배포할 필요가 없습니다.  
> - ISATAP(Intra-Site Automatic Tunnel Addressing Protocol)는 DirectAccess 배포에서 지원되지 않습니다.  
> - I p v 6을 사용 하면 가능 IPv6 호스트 (AAAA) 리소스 레코드 쿼리 d n s 64에 대 한 다음 Windows PowerShell 명령을 사용 하 여:   **집합 NetDnsTransitionConfiguration-OnlySendAQuery $false**합니다.  
  
### <a name="113-plan-for-force-tunneling"></a>1.1.3 강제 터널링 계획

IPv6과 NRPT(이름 확인 정책 테이블)를 사용하는 경우 DirectAccess 클라이언트는 기본적으로 다음과 같이 해당 인트라넷 트래픽과 인터넷 트래픽을 구분합니다.  
  
- DNS 이름에서 인트라넷 FQDN(정규화된 도메인 이름)을 쿼리하며, 모든 인트라넷 트래픽이 DirectAccess 서버에서 만든 터널 또는 인트라넷 서버에서 직접 만든 터널을 통해 교환됩니다. DirectAccess 클라이언트의 인트라넷 트래픽은 IPv6 트래픽입니다.  
  
- DNS 이름이 예외 규칙에 해당하거나 인트라넷 네임스페이스와 일치하지 않는 FQDN을 쿼리하며, 인터넷 서버의 모든 트래픽이 인터넷에 연결된 실제 인터페이스를 통해 교환됩니다. DirectAccess 클라이언트의 인터넷 트래픽은 일반적으로 IPv4 트래픽입니다.  
  
반면, VPN 클라이언트를 비롯한 일부 원격 액세스 VPN(가상 사설망) 구현에서는 원격 액세스 VPN 연결을 통해 모든 인트라넷 및 인터넷 트래픽을 전송합니다. 인터넷에 바인딩된 트래픽은 IPv4 인터넷 리소스에 액세스할 수 있도록 VPN 서버에서 인트라넷 IPv4 웹 프록시 서버로 라우팅됩니다. 분할 터널링을 사용하여 원격 액세스 VPN 클라이언트에 대한 인트라넷 및 인터넷 트래픽을 구분할 수 있습니다. 인트라넷 위치로의 트래픽은 VPN 연결을 통해 전송되고 다른 모든 위치로의 트래픽은 인터넷에 연결된 실제 인터페이스를 사용하여 전송되도록 VPN 클라이언트의 IP(인터넷 프로토콜) 라우팅 테이블을 구성하는 것도 여기에 포함됩니다.  
  
강제 터널링을 사용하여 모든 트래픽을 터널을 통해 DirectAccess 서버에 전송하도록 DirectAccess 클라이언트를 구성할 수 있습니다. 강제 터널링이 구성된 경우 DirectAccess 클라이언트는 인터넷에 있음을 감지하여 해당 IPv4 기본 경로를 제거합니다. 로컬 서브넷 트래픽을 제외하고 DirectAccess 클라이언트에서 보내는 모든 트래픽은 터널을 통해 DirectAccess 서버로 전송되는 IPv6 트래픽입니다.  
  
> [!IMPORTANT]  
> 강제 터널링을 사용할 예정이거나 나중에 추가할 가능성이 있는 경우 2터널 구성을 배포해야 합니다. 보안을 고려하여 단일 터널 구성의 강제 터널링은 지원되지 않습니다.  
  
강제 터널링을 사용하면 다음과 같은 결과가 발생합니다.  
  
- DirectAccess 클라이언트가 IP-HTTPS(Internet Protocol over Secure Hypertext Transfer Protocol)만을 사용하여 IPv4 인트라넷을 통해 DirectAccess 서버에 대한 IPv6 연결을 가져옵니다.  
  
- DirectAccess 클라이언트에서 기본적으로 IPv4 트래픽과 연결할 수 있는 위치는 해당 로컬 서브넷에 있는 위치뿐입니다. DirectAccess 클라이언트에서 실행되는 애플리케이션 및 서비스에서 보낸 모든 트래픽은 DirectAccess 연결을 통해 전송되는 IPv6 트래픽입니다. 따라서 DirectAccess 클라이언트의 IPv4 전용 애플리케이션은 로컬 서브넷에 있는 것을 제외하고는 인터넷 리소스에 연결하는 데 사용될 수 없습니다.  
  
> [!IMPORTANT]  
> DNS64 및 NAT64를 통해 강제 터널링을 실행하려면 IPv6 인터넷 연결을 구현해야 합니다. 이를 구현하는 한 가지 방법은 IPv6을 통해 ipv6.msftncsi.com에 연결할 수 있고 인터넷 서버의 응답이 DirectAccess 서버를 통해 IP-HTTPS 클라이언트로 반환될 수 있도록 IP-HTTPS 접두사를 전역적으로 라우팅 가능하게 만드는 것입니다.  
>
> 그러나 이 방법은 대부분의 경우 실현 불가능하므로 다음과 같이 회사 네트워크 내에 가상 NCSI 서버를 만드는 것이 가장 좋습니다.  
>
> 1. ipv6.msftncsi.com에 대한 NRPT 항목을 추가하고 DNS64에서 내부 웹 사이트(IPv4 웹 사이트일 수 있음)에 확인합니다.  
> 2. dns.msftncsi.com에 대한 NRPT 항목을 추가하고 회사 DNS 서버에서 확인하여 IPv6 호스트(AAAA) 리소스 레코드 fd3e:4f5a:5b81::1을 반환합니다. DNS64를 사용하여 이 FQAN에 대한 호스트(A) 리소스 레코드 쿼리만 보내는 것은 작동하지 않을 수 있습니다. DNS64는 IPv4 전용 배포에 구성되므로 회사 DNS에서 직접 확인하도록 구성해야 하기 때문입니다.  
  
## <a name="12-plan-firewall-requirements"></a>1.2 방화벽 요구 사항 계획

DirectAccess 서버가 경계면 방화벽 뒤에 있는 경우 DirectAccess 서버가 IPv4 인터넷에 있으면 원격 액세스 트래픽에 대한 다음과 같은 예외가 필요합니다.  
  
- Teredo 트래픽-사용자 데이터 그램 프로토콜 (UDP) 대상 포트 3544 인바운드, UDP 원본 포트 3544 아웃 바운드입니다.  
  
- 6to4 트래픽-IP 프로토콜 41 인바운드 및 아웃 바운드입니다.  
  
- IP HTTPS 전송 제어 프로토콜 (TCP) 대상 포트 443 및 TCP 포트 443 아웃 바운드 원본입니다.  
  
- 단일 네트워크 어댑터를 사용하여 원격 액세스를 배포하고 DirectAccess 서버에 네트워크 위치 서버를 설치하려는 경우에는 TCP 포트 62000도 제외해야 합니다.  
  
    > [!NOTE]  
    > 이 예외는 DirectAccess 서버에서 적용되고, 다른 모든 예외는 경계면 방화벽에서 적용됩니다.  
  
Teredo 및 6to4 트래픽의 경우 이 예외는 DirectAccess 서버의 연속된 인터넷 연결 공용 IPv4 주소 둘 다에 대해 적용되어야 합니다. IP-HTTPS의 경우 이 예외는 공용 DNS 서버에 등록된 주소에 적용되어야 합니다.  
  
다음 예외는 DirectAccess 서버가 IPv6 인터넷에 있는 경우 원격 액세스 트래픽에 대해 필요합니다.  
  
- IP 프로토콜 ID 50  
  
- UDP 대상 포트 500 인바운드, UDP 원본 포트 500 아웃바운드  
  
- ICMPv6 트래픽 인바운드 및 아웃바운드(Teredo를 사용하는 경우에만)  
  
추가 방화벽을 사용하는 경우 원격 액세스 트래픽에 대해 다음 내부 네트워크 방화벽 예외를 적용합니다.  
  
- ISATAP 프로토콜 41 인바운드 및 아웃 바운드  
  
- TCP/UDP - 모든 IPv4 및 IPv6 트래픽  
  
- ICMP - 모든 IPv4 및 IPv6 트래픽(Teredo를 사용하는 경우에만)  
  
## <a name="13-plan-certificate-requirements"></a>1.3 인증서 요구 사항 계획

단일 DirectAccess 서버를 배포할 때 인증서가 필요한 세 가지 시나리오가 있습니다.  
  
- [IPsec 인증용 1.3.1 컴퓨터 인증서 계획](#131-plan-computer-certificates-for-ipsec-authentication)  
  
    IPsec에 대한 인증서 요구 사항에는 클라이언트와 DirectAccess 서버 간의 IPsec 연결을 설정할 때 DirectAccess 클라이언트 컴퓨터에서 사용하는 컴퓨터 인증서 및 DirectAccess 클라이언트와의 IPsec 연결을 설정할 때 DirectAccess 서버에서 사용하는 컴퓨터 인증서가 포함됩니다.  
  
    Windows Server 2012의 DirectAccess에 대 한 이러한 IPsec 인증서의 사용 하지 않아도 됩니다. 대체 방법으로, DirectAccess 서버가 Kerberos 프록시 역할을 하여 인증서를 요구하지 않고 IPsec 인증을 수행할 수 있습니다. Kerberos 프로토콜을 사용하는 경우 이 프로토콜은 SSL을 통해 작동하므로 Kerberos 프록시에서 IP-HTTPS용으로 구성된 인증서를 이 용도에 사용합니다. 일부 엔터프라이즈 시나리오(멀티 사이트 배포 및 OTP(일회용 암호) 클라이언트 인증 포함)에서는 Kerberos 프로토콜이 아니라 인증서 인증을 사용해야 합니다.  
  
-   [IP-HTTPS 용 1.3.2 계획 인증서](#132-plan-certificates-for-ip-https)  
  
    원격 액세스를 구성할 때 DirectAccess 서버가 IP-HTTPS 수신기 역할을 하도록 자동으로 구성됩니다. IP-HTTPS 사이트에는 웹 사이트 인증서가 필요하므로 클라이언트 컴퓨터에서 인증서의 CRL(인증서 해지 목록) 사이트에 연결할 수 있어야 합니다.  
  
-   [1.3.3 네트워크 위치 서버용 웹 사이트 인증서 계획](#133-plan-website-certificates-for-the-network-location-server)  
  
    네트워크 위치 서버는 클라이언트 컴퓨터가 회사 네트워크에 있는지 검색하는 데 사용되는 웹 사이트입니다. 네트워크 위치 서버에는 웹 사이트 인증서가 필요합니다. DirectAccess 클라이언트에서 인증서의 CRL 사이트에 연결할 수 있어야 합니다.  
  
다음 표에는 각 시나리오에 대한 CA(인증 기관) 요구 사항이 요약되어 있습니다.  
  
|IPsec 인증|IP-HTTPS 서버|네트워크 위치 서버|  
|------------|----------|--------------|  
|내부 CA가 인증에 Kerberos 프록시를 사용 하지 않는 경우 DirectAccess 서버 및 클라이언트에 IPsec 인증용 컴퓨터 인증서를 발급 하는 데 필요한|내부 CA:<br/><br/>내부 CA를 사용하여 IP-HTTPS 인증서를 발급할 수 있습니다. 그러나 CRL 배포 지점을 외부에서 사용할 수 있어야 합니다.|내부 CA:<br/><br/>내부 CA를 사용하여 네트워크 위치 서버 웹 사이트 인증서를 발급할 수 있습니다. 그러나 내부 네트워크에서 CRL 배포 지점을 항상 사용할 수 있어야 합니다.|  
||자체 서명된 인증서:<br/><br/>IP-HTTPS 서버에 자체 서명된 인증서를 사용할 수 있습니다. 그러나 CRL 배포 지점을 외부에서 사용할 수 있어야 합니다.<br/><br/>멀티 사이트 배포에는 자체 서명된 인증서를 사용할 수 없습니다.|자체 서명된 인증서:<br/><br/>네트워크 위치 서버 웹 사이트에 자체 서명된 인증서를 사용할 수 있습니다.<br/><br/>멀티 사이트 배포에는 자체 서명된 인증서를 사용할 수 없습니다.|  
||**바람직하지**<br/><br/>공용 CA:<br/><br/>공용 CA를 사용하여 IP-HTTPS 인증서를 발급하는 것이 좋습니다. 이렇게 하면 외부에서 CRL 배포 지점을 사용할 수 있습니다.|  
  
### <a name="131-plan-computer-certificates-for-ipsec-authentication"></a>1.3.1 IPsec 인증용 컴퓨터 인증서 계획  
인증서 기반 IPsec 인증을 사용하는 경우 DirectAccess 서버와 클라이언트에서 컴퓨터 인증서를 가져와야 합니다. 인증서를 설치하는 가장 간단한 방법은 컴퓨터 인증서에 대한 그룹 정책 기반 자동 등록을 구성하는 것입니다. 이렇게 하면 모든 도메인 구성원이 엔터프라이즈 CA에서 인증서를 가져옵니다. 엔터프라이즈 조직에서 설정 하는 CA가 참조 [Active Directory 인증서 서비스](https://technet.microsoft.com/library/cc770357.aspx)합니다.  
  
이 인증서에는 다음과 같은 요구 사항이 있습니다.  
  
-   인증서에 클라이언트 인증 EKU(확장된 키 사용)가 있어야 합니다.  
  
-   클라이언트 인증서와 서버 인증서가 동일한 루트 인증서에 연결되어야 합니다. DirectAccess 구성 설정에서 이 루트 인증서를 선택해야 합니다.  
  
### <a name="132-plan-certificates-for-ip-https"></a>1.3.2 IP-HTTPS용 인증서 계획  
DirectAccess 서버가 IP-HTTPS 수신기 역할을 하므로 서버에 HTTPS 웹 사이트 인증서를 수동으로 설치해야 합니다. 계획 시 고려할 사항은 다음과 같습니다.  
  
-   CRL(인증서 해지 목록)을 항상 사용할 수 있도록 공용 CA를 사용하는 것이 좋습니다.  
  
-   에 **주체** 필드에 DirectAccess 서버 인터넷 어댑터 또는 IP-HTTPS URL (ConnectTo 주소)의 FQDN의 IPv4 주소를 지정 합니다. DirectAccess 서버가 NAT 디바이스 뒤에 있는 경우에는 NAT 디바이스의 공개 이름 또는 주소를 지정해야 합니다.  
  
-   인증서의 일반 이름이 IP-HTTPS 사이트의 이름과 일치해야 합니다.  
  
-   에 대 한는 **향상 된 키 용도** 필드의 경우는 서버 인증 OID (개체 식별자)를 사용 합니다.  
  
-   에 대 한는 **CRL 배포 지점** 필드에서 인터넷에 연결 된 DirectAccess 클라이언트에서 액세스할 수 있는 CRL 배포 지점을 지정 합니다.  
  
-   IP-HTTPS 인증서에 프라이빗 키가 있어야 합니다.  
  
-   IP-HTTPS 인증서를 개인 저장소로 직접 가져와야 합니다.  
  
-   IP-HTTPS 인증서 이름에 와일드카드 문자를 사용할 수 있습니다.  
  
비표준 포트에서 IP-HTTPS를 사용하려면 DirectAccess 서버에서 다음 단계를 수행합니다.  
  
1.  0\.0.0.0:443에 대한 기존 인증서 바인딩을 제거하고 선택한 포트에 대한 인증서 바인딩으로 대체합니다. 이 예제에서는 포트 44500이 사용되었습니다. 인증서를 삭제 하기 전에 표시 하 고 복사는 **appid**합니다.  
  
    1.  인증서 바인딩을 삭제하려면 다음을 입력합니다.  
  
        ```  
        netsh http delete ssl ipport=0.0.0.0:443  
        ```  
  
    2.  새 인증서 바인딩을 추가하려면 다음을 입력합니다.  
  
        ```  
        netsh http add ssl ipport=0.0.0.0:44500 certhash=<use the thumbprint from the DirectAccess server SSL cert> appid=<use the appid from the binding that was deleted>  
        ```  
  
2.  서버에서 IP-HTTPS URL을 수정하려면 다음을 입력합니다.  
  
    ```  
    Netsh int http set int url=https://<DirectAccess server name (for example server.contoso.com)>:44500/IPHTTPS  
    ```  
  
    ```  
    Net stop iphlpsvc & net start iphlpsvc  
    ```  
  
3.  kdcproxy에 대한 URL 예약을 변경합니다.  
  
    1.  기존 URL 예약을 삭제하려면 다음을 입력합니다.  
  
        ```  
        netsh http del urlacl url=https://+:443/KdcProxy/  
        ```  
  
    2.  새 URL 예약을 추가하려면 다음을 입력합니다.  
  
        ```  
        netsh http add urlacl url=https://+:44500/KdcProxy/ sddl=D:(A;;GX;;;NS)  
        ```  
  
4.  kppsvc가 비표준 포트에서 수신 대기하도록 하는 설정을 추가합니다. 레지스트리 항목을 추가하려면 다음을 입력합니다.  
  
    ```  
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\KPSSVC\Settings /v HttpsUrlGroup /t REG_MULTI_SZ /d +:44500 /f  
    ```  
  
5.  도메인 컨트롤러에서 kdcproxy 서비스를 다시 시작하려면 다음을 입력합니다.  
  
    ```  
    net stop kpssvc & net start kpssvc  
    ```  
  
비표준 포트에서 IP-HTTPS를 사용하려면 도메인 컨트롤러에서 다음 단계를 수행합니다.  
  
1.  클라이언트 GPO에서 IP-HTTPS 설정을 수정합니다.  
  
    1.  그룹 정책 편집기를 엽니다.  
  
    2.  컴퓨터 구성=>정책=>관리 템플릿=>네트워크=>TCPIP 설정=>IPv6 전환 기술로 이동합니다.  
  
    3.  IP-HTTPS 상태 설정을 열고 URL을 변경 하 고 **https://<DirectAccess 서버 이름 (예: server.contoso.com) >: 44500/IPHTTPS**합니다.  
  
    4.  **적용**을 클릭합니다.  
  
2.  클라이언트 GPO에서 Kerberos 프록시 클라이언트 설정을 수정합니다.  
  
    1.  그룹 정책 편집기에서 컴퓨터 구성=>정책=>관리 템플릿=>시스템=>Kerberos =>Kerberos 클라이언트용 KDC 프록시 서버 지정으로 이동합니다.  
  
    2.  IPHTTPS 상태 설정을 열고 URL을 변경 하 고 **https://<DirectAccess 서버 이름 (예: server.contoso.com) >: 44500/IPHTTPS**합니다.  
  
    3.  **적용**을 클릭합니다.  
  
3.  ComputerKerb 및 UserKerb를 사용하도록 클라이언트 IPsec 정책 설정을 수정합니다.  
  
    1.  그룹 정책 편집기에서 컴퓨터 구성=>정책=>Windows 설정=>보안 설정=>고급 보안이 포함된 Windows 방화벽으로 이동합니다.  
  
    2.  클릭 **연결 보안 규칙**, 를 두 번 클릭 하 고 **IPsec 규칙**합니다.  
  
    3.  에 **인증** 탭을 클릭 하 여 **고급**합니다.  
  
    4.  Auth1에 대해 기존 인증 방법을 제거하고 ComputerKerb로 대체합니다. Auth2에 대해 기존 인증 방법을 제거하고 UserKerb로 대체합니다.  
  
    5.  클릭 **적용**, 차례로 **확인**합니다.  
  
IP-HTTPS 비표준 포트를 사용 하기 위한 수동 프로세스를 완료 하려면 실행 **gpupdate /force** 클라이언트 컴퓨터와 DirectAccess 서버에 있습니다.  
  
### <a name="133-plan-website-certificates-for-the-network-location-server"></a>1.3.3 네트워크 위치 서버용 웹 사이트 인증서 계획  
네트워크 위치 서버 웹 사이트를 계획할 때 고려할 사항은 다음과 같습니다.  
  
-   에 **주체** 필드에 네트워크 위치 서버의 인트라넷 인터페이스 또는 네트워크 위치 URL의 FQDN의 IP 주소를 지정 합니다.  
  
-   에 **향상 된 키 용도** 필드의 경우 서버 인증 OID를 사용 합니다.  
  
-   에 **CRL 배포 지점** 필드의 경우 인트라넷에 연결 된 DirectAccess 클라이언트에서 액세스할 수 있는 CRL 배포 지점을 사용 합니다. 이 CRL 배포 지점에는 내부 네트워크 외부에서 액세스할 수 없습니다.  
  
-   나중에 멀티 사이트 또는 클러스터 배포를 구성하려는 경우에는 인증서 이름이 배포에 추가할 DirectAccess 서버의 내부 이름과 일치해서는 안 됩니다.  
  
    > [!NOTE]  
    > IP-HTTPS 및 네트워크 위치 서버에 대 한 인증서가 있는지 확인 한 **주체 이름**합니다. 인증서에 없는 경우는 **주체 이름**, 되었지만 **대체 이름**, 원격 액세스 마법사에서 허용 되지 것입니다.  
  
## <a name="14-plan-dns-requirements"></a>1.4 DNS 요구 사항 계획  
이 섹션에서는 원격 액세스 배포의 DirectAccess 클라이언트 요청 및 인프라 서버에 대한 DNS 요구 사항을 설명합니다. 섹션 내용은 다음과 같습니다.  
  
-   [DNS 서버 요구 사항에 대 한 1.4.1 계획](#141-plan-for-dns-server-requirements)  
  
-   [로컬 이름 확인에 대 한 1.4.2 계획](#142-plan-for-local-name-resolution)  
  
**DirectAccess 클라이언트 요청**  
  
DNS는 내부(또는 회사) 네트워크에 있지 않은 DirectAccess 클라이언트 컴퓨터의 요청을 확인하는 데 사용됩니다. DirectAccess 클라이언트는 인터넷에 있는지 또는 내부 네트워크에 있는지 확인하기 위해 DirectAccess 네트워크 위치 서버에 연결합니다.  
  
-   연결에 성공하면 클라이언트가 내부 네트워크에 있는 것으로 식별되므로 DirectAccess가 사용되지 않고 클라이언트 요청이 클라이언트 컴퓨터의 네트워크 어댑터에 구성된 DNS 서버를 통해 확인됩니다.  
  
-   연결에 실패한 경우에는 클라이언트가 인터넷에 있는 것으로 간주되므로 DirectAccess 클라이언트에서 NRPT(이름 확인 정책 테이블)를 사용하여 이름 요청을 확인할 때 사용할 DNS 서버를 결정합니다.  
  
클라이언트에서 DirectAccess DNS64를 사용하여 이름을 확인하거나, 대체 내부 DNS 서버를 사용하도록 지정할 수 있습니다. 이름 확인을 수행할 때 NRPT는 DirectAccess 클라이언트에서 요청을 처리할 방법을 식별하는 데 사용됩니다. 클라이언트는 <https://internal>와 같은 FQDN 또는 단일 레이블 이름을 요청 합니다. 단일 레이블 이름이 요청된 경우 FQDN을 만들기 위해 DNS 접미사가 추가됩니다. DNS 쿼리가 NRPT의 항목과 일치하고 내부 네트워크의 DNS64 또는 DNS 서버가 해당 항목에 지정되어 있는 경우 해당 쿼리는 지정된 서버를 사용하여 이름 확인을 위해 전송됩니다. 일치하지만 지정된 DNS 서버가 없는 경우에는 예외 규칙을 나타내므로 일반 이름 확인이 적용됩니다.  
  
> [!NOTE]  
> 새 접미사가 nrpt는 원격 액세스 관리 콘솔에 추가 되는 접미사에 대 한 기본 DNS 서버 수 자동으로 검색할 수 클릭 하 여 **검색**합니다.  
  
자동 검색은 다음과 같이 작동합니다.  
  
-   회사 네트워크가 IPv4 기반이거나 IPv4와 IPv6을 사용하는 경우 기본 주소는 DirectAccess 서버에 있는 내부 어댑터의 DNS64 주소입니다.  
  
-   회사 네트워크가 IPv6 기반인 경우 기본 주소는 회사 네트워크에 있는 DNS의 IPv6 주소입니다.  
  
**인프라 서버**  
  
-   **네트워크 위치 서버**  
  
    DirectAccess 클라이언트는 내부 네트워크에 있는지 확인하기 위해 네트워크 위치 서버에 연결합니다. 내부 네트워크의 클라이언트는 네트워크 위치 서버의 이름을 확인할 수 있어야 하지만, 인터넷에 있을 때는 이름을 확인하지 못하도록 설정되어야 합니다. 이를 위해 기본적으로 네트워크 위치 서버의 FQDN이 NRPT에 예외 규칙으로 추가됩니다. 또한 원격 액세스를 구성하는 경우 다음 규칙이 자동으로 만들어집니다.  
  
    -   루트 도메인 또는 DirectAccess 서버의 도메인 이름과 DNS64 주소에 해당하는 IPv6 주소에 대한 DNS 접미사 규칙. IPv6 전용 회사 네트워크에서는 DirectAccess 서버에 인트라넷 DNS 서버가 구성됩니다. 예를 들어 DirectAccess 서버가 corp.contoso.com 도메인의 구성원인 경우 corp.contoso.com DNS 접미사에 대한 규칙이 만들어집니다.  
  
    -   네트워크 위치 서버의 FQDN에 대한 예외 규칙. 예를 들어 네트워크 위치 서버 URL이 <https://nls.corp.contoso.com>인 경우 FQDN nls.corp.contoso.com에 대 한 예외 규칙이 만들어집니다.  
  
-   **IP-HTTPS 서버**  
  
    DirectAccess 서버는 IP-HTTPS 수신기 역할을 하며 해당 서버 인증서를 사용하여 IP-HTTPS 클라이언트를 인증합니다. IP-HTTPS 이름은 공용 DNS 서버를 사용하는 DirectAccess 클라이언트에서 확인할 수 있어야 합니다.  
  
-   **CRL 해지 확인**  
  
    DirectAccess는 DirectAccess 클라이언트와 DirectAccess 서버 간의 IP-HTTPS 연결 및 DirectAccess 클라이언트와 네트워크 위치 서버 간의 HTTPS 기반 연결에 인증서 해지 확인을 사용합니다. 두 경우 모두 DirectAccess 클라이언트에서 CRL 배포 지점 위치를 확인하고 액세스할 수 있어야 합니다.  
  
-   **ISATAP**  
  
    ISATAP는 회사 컴퓨터에서 IPv6 주소를 가져와 IPv4 헤더 내에 IPv6 패킷을 캡슐화할 수 있도록 해줍니다. ISATAP는 DirectAccess 서버에서 인트라넷을 통해 ISATAP 호스트에 IPv6 연결을 제공하는 데 사용됩니다. 기본이 아닌 IPv6 네트워크 환경에서는 DirectAccess 서버가 자동으로 ISATAP 라우터로 구성됩니다.  
  
    ISATAP는 DirectAccess에서 더 이상 지원되지 않으므로 DNS 서버를 ISATAP 쿼리에 응답하지 않도록 구성해야 합니다. 기본적으로 DNS 서버 서비스는 DNS 글로벌 쿼리 차단 목록을 통해 ISATAP 이름에 대한 이름 확인을 차단합니다. 글로벌 쿼리 차단 목록에서 ISATAP 이름을 제거하지 마세요.  
  
-   **연결 검증 도구**  
  
    원격 액세스는 DirectAccess 클라이언트 컴퓨터에서 내부 네트워크에 대한 연결을 확인하는 데 사용하는 기본 웹 검색을 만듭니다. 검색이 정상적으로 작동하려면 다음 이름을 DNS에 수동으로 등록해야 합니다.  
  
    -   **directaccess webprobehost**-DirectAccess 서버의 내부 IPv4 주소 또는 IPv6 전용 환경의 IPv6 주소를 확인 합니다.  
  
    -   **directaccess corpconnectivityhost**-로컬 호스트 (루프백) 주소를 확인 합니다. 값이 127.0.0.1인 호스트(A) 리소스 레코드와 값의 마지막 32비트가 NAT64 접두사에서 127.0.0.1로 생성된 호스트(AAAA) 리소스 레코드를 만들어야 합니다. NAT64 접두사는 Windows PowerShell 명령을 실행 하 여 검색할 수 있습니다 **get netnattransitionconfiguration**합니다.  
  
        > [!NOTE]  
        > 이는 IPv4 전용 환경에서만 유효합니다. IPv4와 IPv6을 함께 사용하는 환경 또는 IPv6 전용 환경에서는 루프백 IP 주소 ::1을 사용하여 호스트(AAAA) 리소스 레코드만 만들어야 합니다.  
  
    HTTP 통해 다른 웹 주소를 사용 하 여 또는 사용 하 여 추가 연결 검증 도구를 만들 수 있습니다 **ping**합니다. 각 연결 검증 도구에 대한 DNS 항목이 있어야 합니다.  
  
### <a name="141-plan-for-dns-server-requirements"></a>1.4.1 DNS 서버 요구 사항 계획  
다음은 DirectAccess를 배포할 때의 DNS에 대한 요구 사항입니다.  
  
-   DirectAccess 클라이언트에 대 한 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 또는 i p v 6을 지 원하는 다른 DNS 서버를 실행 하는 DNS 서버를 사용 해야 합니다.  
  
    > [!NOTE]  
    > DirectAccess를 배포하는 경우 Windows Server 2003을 실행하는 DNS 서버를 사용하지 않는 것이 좋습니다. Windows Server 2003 DNS 서버는 IPv6 레코드를 지원하지만 Microsoft에서 Windows Server 2003을 더 이상 지원하지 않습니다. 또한 도메인 컨트롤러가 Windows Server 2003을 실행하는 경우 파일 복제 서비스 문제로 인해 DirectAccess를 배포하면 안 됩니다. 자세한 내용은 참조 [DirectAccess 구성은 지원 되지 않으므로](https://technet.microsoft.com/library/dn464274.aspx)합니다.  
  
-   동적 업데이트를 지원하는 DNS 서버를 사용합니다. 동적 업데이트를 지원하지 않는 DNS 서버를 사용할 수 있지만 이러한 서버에서는 항목을 수동으로 업데이트해야 합니다.  
  
-   인터넷에 액세스할 수 있는 CRL 배포 지점에 대한 FQDN을 인터넷 DNS 서버를 사용하여 확인할 수 있어야 합니다. 예를 들어 URL <https://crl.contoso.com/crld/corp-DC1-CA.crl> DirectAccess 서버 IP-HTTPS 인증서의 **CRL 배포 요소** 필드에 있는 경우 인터넷 DNS 서버를 사용 하 여 FQDN crld.contoso.com을 확인할 수 있는지 확인 해야 합니다.  
  
### <a name="142-plan-for-local-name-resolution"></a>1.4.2 로컬 이름 확인 계획  
로컬 이름 확인을 계획할 때 고려할 문제는 다음과 같습니다.  
  
**NRPT**  
  
다음과 같은 경우 추가 NRPT 규칙을 만들어야 할 수도 있습니다.  
  
-   인트라넷 네임스페이스에 대한 DNS 접미사를 추가해야 하는 경우  
  
-   CRL 배포 지점의 FQDN(정규화된 도메인 이름)이 인트라넷 네임스페이스를 기반으로 하는 경우 CRL 배포 지점의 FQDN에 대한 예외 규칙을 추가해야 합니다.  
  
-   스플릿 브레인(Split-Brain) DNS 환경을 사용하는 경우 인터넷에 있는 DirectAccess 클라이언트가 인트라넷 버전 대신 인터넷 버전에 액세스할 수 있도록 할 리소스 이름에 대한 예외 규칙을 추가해야 합니다.  
  
-   인트라넷 웹 프록시 서버를 통해 외부 웹 사이트로 트래픽을 리디렉션하는 경우 해당 외부 웹 사이트는 인트라넷에서만 사용할 수 있으며 웹 프록시 서버의 주소를 사용하여 인바운드 요청을 허용합니다. 이 경우 외부 웹 사이트의 FQDN에 대한 예외 규칙을 추가하고 해당 규칙에서 인트라넷 DNS 서버의 IPv6 주소 대신 인트라넷 웹 프록시 서버를 사용하도록 지정합니다.  
  
    예를 들어 test.contoso.com이라는 외부 웹 사이트를 테스트하는 경우, 인터넷 DNS 서버를 통해 이 이름을 확인할 수는 없지만 Contoso 웹 프록시 서버는 이름을 확인하고 웹 사이트에 대한 요청을 외부 웹 서버로 전달하는 방법을 알고 있습니다. Contoso 인트라넷에 없는 사용자가 사이트에 액세스하지 못하도록 하기 위해 외부 웹 사이트에서는 Contoso 웹 프록시의 IPv4 인터넷 주소에서 보내는 요청만 허용합니다. 따라서 인트라넷 사용자는 Contoso 웹 프록시를 사용하기 때문에 웹 사이트에 액세스할 수 있지만 DirectAccess 사용자는 Contoso 웹 프록시를 사용하지 않으므로 액세스할 수 없습니다. Contoso 웹 프록시를 사용하는 test.contoso.com에 대한 NRPT 예외 규칙을 구성하면 test.contoso.com에 대한 웹 페이지 요청이 IPv4 인트라넷을 통해 인트라넷 웹 프록시 서버로 라우팅됩니다.  
  
**단일 레이블 이름**  
  
<https://paycheck>와 같은 단일 레이블 이름이 인트라넷 서버에 사용 되는 경우도 있습니다. DNS 접미사 검색 목록이 구성되어 있는 경우 단일 레이블 이름이 요청되면 목록에 있는 DNS 접미사가 단일 레이블 이름에 추가됩니다. 예를 들어 corp.contoso.com 도메인 형식의 구성원 인 컴퓨터의 사용자가 웹 브라우저에서 <https://paycheck> 경우 이름으로 생성 된 FQDN은 paycheck.corp.contoso.com입니다. 추가되는 접미사는 기본적으로 클라이언트 컴퓨터의 주 DNS 접미사를 기반으로 합니다.  
  
> [!NOTE]  
> 연결되지 않은 이름 공간 시나리오(하나 이상의 도메인 컴퓨터에 해당 컴퓨터가 속한 Active Directory 도메인과 일치하지 않는 DNS 접미사가 있는 경우)에서는 필요한 모든 접미사를 포함하도록 검색 목록을 사용자 지정해야 합니다. 기본적으로 원격 액세스 마법사는 Active Directory DNS 이름을 클라이언트의 주 DNS 접미사로 구성합니다. 클라이언트에서 이름 확인에 사용하는 DNS 접미사를 추가해야 합니다.  
  
여러 도메인과 WINS(Windows 인터넷 이름 서비스)가 배포되어 있는 조직에서 원격으로 연결하는 경우 다음과 같이 단일 이름을 확인할 수 있습니다.  
  
-   DNS에 WINS 정방향 조회 영역을 배포합니다. computername.dns.zone1.corp.contoso.com을 확인하려고 하면 computername만 사용하는 WINS 서버로 요청이 전달됩니다. 클라이언트는 일반 DNS 호스트(A) 리소스 레코드를 발급 중인 것으로 인식하지만 이는 실제로 NetBIOS 요청입니다. 자세한 내용은 정방향 조회 영역을 관리를 참조하세요.  
  
-   기본 도메인 정책 GPO에 DNS 접미사(예: dns.zone1.corp.contoso.com)를 추가합니다.  
  
**스플릿 브레인(Split-Brain) DNS**  
  
스플릿 브레인 DNS는 인터넷 및 인트라넷 이름 확인에 동일한 DNS 도메인을 사용하는 것을 의미합니다.  
  
스플릿 브레인 DNS 배포에 대 한 인터넷 및 인트라넷에 중복 된 리소스를 결정 하는 Fqdn을 나열 해야 도달률은 인트라넷 또는 인터넷 버전 DirectAccess 클라이언트 해야 합니다. DirectAccess 클라이언트에서 인터넷 버전에 연결할 리소스에 해당하는 각 이름에 대해 해당 FQDN을 DirectAccess 클라이언트의 NRPT에 예외 규칙으로 추가해야 합니다.  
  
스플릿 브레인 DNS 환경에서 두 버전의 리소스를 모두 사용할 수 있도록 하려면 인터넷에서 사용되는 이름과 중복되지 않는 대체 이름으로 인트라넷 리소스를 구성하고 사용자에게 인트라넷에서는 대체 이름을 사용하도록 안내합니다. 예를 들어 내부 이름 www.contoso.com에 대해 www.internal.contoso.com이라는 대체 이름을 구성합니다.  
  
스플릿 브레인이 아닌 DNS 환경에서는 인터넷 네임스페이스가 인트라넷 네임스페이스와 다릅니다. 예를 들어 인터넷의 네임스페이스는 Contoso Corporation uses contoso.com이고 인트라넷의 네임스페이스는 corp.contoso.com인 경우를 살펴보겠습니다. 모든 인트라넷 리소스는 corp.contoso.com DNS 접미사를 사용하므로 corp.contoso.com에 대한 NRPT 규칙에 따라 인트라넷 리소스에 대한 모든 DNS 이름 쿼리가 인트라넷 DNS 서버로 라우팅됩니다. 접미사가 contoso.com인 이름에 대한 DNS 이름 쿼리는 NRPT의 corp.contoso.com intranet 네임스페이스 규칙과 일치하지 않으므로 인터넷 DNS 서버로 전송됩니다. 스플릿 브레인이 아닌 DNS 환경에서는 인트라넷 리소스와 인터넷 리소스의 FQDN이 중복되지 않으므로 NRPT에 대한 추가 구성이 필요 없습니다. DirectAccess 클라이언트에서 조직의 인터넷 리소스와 인트라넷 리소스 모두에 액세스할 수 있습니다.  
  
**DirectAccess 클라이언트에 대한 로컬 이름 확인 동작**  
  
Dns 이름을 확인할 수 없으면, 로컬 서브넷에서 이름을 확인 하려면 DNS 클라이언트 서비스는 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows 8 및 Windows 7에서 사용할 수 로컬 이름 확인 링크-로컬 멀티 캐스트 이름 확인 LLMNR () 및 NetBIOS over TCP/IP 프로토콜.  
  
로컬 이름 확인은 컴퓨터가 단일 서브넷 홈 네트워크와 같은 개인 네트워크에 있는 경우 일반적으로 피어-투-피어 연결에 필요합니다. 컴퓨터가 인터넷의 공유 서브넷에 연결되어 있는 경우 DNS 클라이언트 서비스에서 인트라넷 서버 이름에 대한 로컬 이름 확인을 수행하면 악의적인 사용자가 LLMNR 및 NetBIOS over TCP/IP 메시지를 캡처하여 인트라넷 서버 이름을 확인할 수 있습니다. DNS 인프라 서버 설치 마법사의 DNS 페이지에서 인트라넷 DNS 서버로부터 받은 응답 유형에 따라 로컬 이름 확인 동작을 구성합니다. 다음 옵션을 사용할 수 있습니다.  
  
-   **이름을 DNS에 존재 하지 않는 경우 로컬 이름 확인을 사용 하 여**합니다. 이 옵션은 DirectAccess 클라이언트가 인트라넷 DNS 서버에서 확인할 수 없는 서버 이름에 대해서만 로컬 이름 확인을 수행하기 때문에 가장 안전합니다. 인트라넷 DNS 서버에 연결할 수 있는 경우 인트라넷 서버의 이름이 확인됩니다. 인트라넷 DNS 서버에 연결할 수 없거나 다른 유형의 DNS 오류가 있는 경우에는 인트라넷 서버 이름이 로컬 이름 확인을 통해 서브넷에 유출되지 않습니다.  
  
-   **이름을 DNS에 존재 하지 않거나 클라이언트 컴퓨터가 개인 네트워크 (권장)에 있을 때 DNS 서버에 연결할 수 없는 경우 로컬 이름 확인을 사용 하 여**합니다. 이 옵션은 인트라넷 DNS 서버에 연결할 수 없는 경우에만 개인 네트워크에서 로컬 이름 확인을 사용하도록 허용하기 때문에 권장되는 옵션입니다.  
  
-   **모든 종류의 DNS 확인 오류 (가장 취약)에 대 한 로컬 이름 확인을 사용 하 여**합니다. 인트라넷 네트워크 서버의 이름이 로컬 이름 확인을 통해 로컬 서브넷에 유출될 수 있으므로 보안 수준이 가장 낮은 옵션입니다.  
  
## <a name="15-plan-the-network-location-server"></a>1.5 네트워크 위치 서버 계획  
네트워크 위치 서버는 DirectAccess 클라이언트가 회사 네트워크에 있는지 검색하는 데 사용되는 웹 사이트입니다. 회사 네트워크의 클라이언트는 DirectAccess를 사용하여 내부 리소스에 연결하는 것이 아니라 직접 연결합니다.  
  
네트워크 위치 서버 웹 사이트는 DirectAccess 서버 또는 조직의 다른 서버에서 호스트될 수 있습니다. DirectAccess 서버에서 네트워크 위치 서버를 호스트하는 경우 원격 액세스 서버 역할을 설치할 때 웹 사이트가 자동으로 만들어집니다. Windows 운영 체제를 실행하는 조직의 다른 서버에서 네트워크 위치 서버를 호스트하려면 해당 서버에 IIS(인터넷 정보 서비스)가 설치되어 있고 웹 사이트가 만들어졌는지 확인해야 합니다. DirectAccess는 원격 네트워크 위치 서버에서 설정을 구성하지 않습니다.  
  
네트워크 위치 서버 웹 사이트가 다음 요구 사항을 충족하는지 확인합니다.  
  
-   HTTPS 서버 인증서를 사용하는 웹 사이트입니다.  
  
-   DirectAccess 클라이언트 컴퓨터가 네트워크 위치 서버 웹 사이트에 서버 인증서를 발급한 CA를 신뢰해야 합니다.  
  
-   내부 네트워크의 DirectAccess 클라이언트 컴퓨터에서 네트워크 위치 서버 사이트의 이름을 확인할 수 있어야 합니다.  
  
-   내부 네트워크의 컴퓨터에서 네트워크 위치 서버 사이트를 항상 사용할 수 있어야 합니다.  
  
-   인터넷의 DirectAccess 클라이언트 컴퓨터에서 네트워크 위치 서버에 액세스할 수 없어야 합니다.  
  
-   CRL에서 서버 인증서를 검사해야 합니다.  
  
### <a name="151-plan-certificates-for-the-network-location-server"></a>1.5.1 네트워크 위치 서버용 인증서 계획  
네트워크 위치 서버에 사용할 웹 사이트 인증서를 가져올 때 고려할 사항은 다음과 같습니다.  
  
1.  에 **주체** 필드에 네트워크 위치 URL의 FQDN 또는 네트워크 위치 서버의 인트라넷 인터페이스의 IP 주소를 지정 합니다.  
  
2.  에 **향상 된 키 용도** 필드의 경우 서버 인증 OID를 사용 합니다.  
  
3.  에 **CRL 배포 지점** 필드의 경우 인트라넷에 연결 된 DirectAccess 클라이언트에서 액세스할 수 있는 CRL 배포 지점을 사용 합니다. 이 CRL 배포 지점에는 내부 네트워크 외부에서 액세스할 수 없습니다.  
  
### <a name="152-plan-dns-for-the-network-location-server"></a>1.5.2 네트워크 위치 서버용 DNS 계획  
DirectAccess 클라이언트는 내부 네트워크에 있는지 확인하기 위해 네트워크 위치 서버에 연결합니다. 내부 네트워크의 클라이언트는 네트워크 위치 서버의 이름을 확인할 수 있어야 하지만, 인터넷에 있을 때는 이름을 확인하지 못하도록 설정되어야 합니다. 이를 위해 기본적으로 네트워크 위치 서버의 FQDN이 NRPT에 예외 규칙으로 추가됩니다.  
  
## <a name="16-plan-management-servers"></a>1.6 관리 서버 계획  
DirectAccess 클라이언트는 Windows 업데이트 및 바이러스 백신 업데이트와 같은 서비스를 제공하는 관리 서버와의 통신을 시작합니다. 또한 DirectAccess 클라이언트는 내부 네트워크에 액세스하기 전에 인증을 받기 위해 Kerberos 프로토콜을 사용하여 도메인 컨트롤러에 연결합니다. DirectAccess 클라이언트의 원격 관리 중에 관리 서버는 클라이언트 컴퓨터와 통신하여 소프트웨어 또는 하드웨어 인벤토리 평가와 같은 관리 기능을 수행합니다. 원격 액세스에서는 다음을 비롯한 일부 관리 서버를 자동으로 검색할 수 있습니다.  
  
-   도메인 컨트롤러-자동 검색 도메인 컨트롤러의 DirectAccess 서버와 클라이언트 컴퓨터와 동일한 포리스트에 있는 모든 도메인에 대해 수행 됩니다.  
  
-   Microsoft 끝점 Configuration Manager 서버-DirectAccess 서버 및 클라이언트 컴퓨터와 동일한 포리스트에 있는 모든 도메인에 대해 Configuration Manager 서버의 자동 검색이 수행 됩니다.  
  
도메인 컨트롤러 및 Configuration Manager 서버는 DirectAccess가 처음 구성 될 때 자동으로 검색 됩니다. 검색 된 도메인 컨트롤러가 콘솔에 표시 되지 않지만 Windows PowerShell cmdlet을 사용 하 여 설정을 검색할 수 있습니다 **Get-damgmtserver-Type All**합니다. 도메인 컨트롤러 또는 Configuration Manager 서버가 수정 된 경우 원격 액세스 관리 콘솔에서 **관리 서버 새로 고침** 을 클릭 하면 관리 서버 목록이 새로 고쳐집니다.  
  
**관리 서버 요구 사항**  
  
-   첫 번째(인프라) 터널을 통해 관리 서버에 액세스할 수 있어야 합니다. 원격 액세스를 구성할 때 관리 서버 목록에 서버를 추가하면 이 터널을 통해 해당 서버에 액세스할 수 있도록 자동으로 설정됩니다.  
  
-   DirectAccess 클라이언트 연결을 시작하는 관리 서버는 기본 IPv6 주소 또는 ISATAP를 통해 할당된 IPv6 주소를 사용하여 IPv6을 완전히 지원할 수 있어야 합니다.  
  
## <a name="17-plan-active-directory-domain-services"></a>1.7 Active Directory 도메인 서비스 계획  
이 섹션에서는 DirectAccess에서 AD DS(Active Directory Domain Services)를 사용하는 방법에 대해 설명하며, 다음 하위 섹션으로 구성되어 있습니다.  
  
-   [1.7.1 for 계획 클라이언트 인증](#171-plan-client-authentication)  
  
-   [1.7.2 여러 도메인 계획](#172-plan-multiple-domains)  
  
DirectAccess는 다음과 같이 AD DS 및 Active Directory 그룹 정책 개체 (Gpo)를 사용합니다.  
  
-   **인증**  
  
    AD DS는 인증에 사용됩니다. 인프라 터널에서는 DirectAccess 서버에 연결하는 컴퓨터 계정에 NTLMv2 인증을 사용하므로 Active Directory 도메인에 계정이 나열되어 있어야 합니다. 인트라넷 터널에서는 사용자에 대해 Kerberos 인증을 사용하여 두 번째 터널을 만듭니다.  
  
-   **개체 그룹 정책**  
  
    DirectAccess는 DirectAccess 서버, 클라이언트 및 내부 애플리케이션 서버에 적용되는 GPO로 구성 설정을 수집합니다.  
  
-   **보안 그룹**  
  
    DirectAccess에서는 보안 그룹을 사용하여 DirectAccess 클라이언트 컴퓨터를 수집 및 식별합니다. GPO는 필요한 보안 그룹에 적용됩니다.  
  
-   **확장 된 IPsec 정책**  
  
    DirectAccess에서는 클라이언트와 DirectAccess 서버 간에 IPsec 인증 및 암호화를 사용할 수 있습니다. 클라이언트에서 지정된 내부 애플리케이션 서버로 IPsec 인증 및 암호화를 확장할 수 있습니다. 이렇게 하려면 필요한 애플리케이션 서버를 보안 그룹에 추가합니다.  
  
**AD DS 요구 사항**  
  
DirectAccess 배포를 위해 AD DS를 계획할 때 고려할 요구 사항은 다음과 같습니다.  
  
-   Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008 운영 체제와 하나 이상의 도메인 컨트롤러를 설치 해야 합니다.  
  
    도메인 컨트롤러가 경계 네트워크에 있는 경우(따라서 DirectAccess 서버의 인터넷 연결 네트워크 어댑터에서 연결할 수 있는 경우) 도메인 컨트롤러에 인터넷 어댑터의 IP 주소 연결을 방지하는 패킷 필터를 추가하여 DirectAccess 서버에서 해당 도메인 컨트롤러에 연결하지 못하도록 해야 합니다.  
  
-   DirectAccess 서버가 도메인 구성원이어야 합니다.  
  
-   DirectAccess 클라이언트가 도메인 구성원이어야 합니다. 클라이언트는 다음에 속할 수 있습니다.  
  
    -   DirectAccess 서버와 동일한 포리스트의 모든 도메인  
  
    -   DirectAccess 서버 도메인과 양방향 트러스트 관계에 있는 모든 도메인  
  
    -   DirectAccess 도메인이 속한 포리스트와 양방향 트러스트 관계에 있는 포리스트의 모든 도메인  
  
> [!NOTE]  
> -   DirectAccess 서버는 도메인 컨트롤러일 수 없습니다.  
> -   DirectAccess 서버의 외부 인터넷 어댑터에서 DirectAccess에 사용되는 AD DS 도메인 컨트롤러에 연결할 수 없어야 합니다. 즉, 어댑터가 Windows 방화벽의 도메인 프로필에 없어야 합니다.  
  
### <a name="171-plan-client-authentication"></a>1.7.1 클라이언트 인증 계획  
DirectAccess를 사용하면 IPsec 컴퓨터 인증용 인증서를 사용할지 또는 사용자 이름과 암호를 사용하여 인증하는 기본 제공 Kerberos 프록시를 사용할지 선택할 수 있습니다.  
  
인증에서 AD DS 자격 증명을 사용하도록 선택한 경우 DirectAccess에서는 첫 번째 인증에 컴퓨터 Kerberos를 사용하고 두 번째 인증에 사용자 Kerberos를 사용하는 하나의 보안 터널을 사용합니다. 이 모드를 인증에 사용할 경우 DirectAccess에서는 DNS 서버, 도메인 컨트롤러 및 내부 네트워크의 다른 서버에 대한 액세스를 제공하는 단일 보안 터널을 사용합니다.  
  
2단계 인증 또는 네트워크 액세스 보호를 사용하도록 선택한 경우 DirectAccess에서는 두 개의 보안 터널을 사용합니다. 원격 액세스 설치 마법사에서 DirectAccess 서버의 터널에 대해 IPsec 보안 연결을 협상할 때 다음 유형의 자격 증명을 사용하도록 지정하는 고급 보안이 포함된 Windows 방화벽 연결 보안 규칙을 구성합니다.  
  
-   인프라 터널에서는 첫 번째 인증에 컴퓨터 Kerberos를 사용하고 두 번째 인증에 사용자 Kerberos를 사용합니다.  
  
-   인트라넷 터널에서는 첫 번째 인증에 컴퓨터 인증서 자격 증명을 사용하고 두 번째 인증에 사용자 Kerberos를 사용합니다.  
  
DirectAccess 멀티 사이트 배포 또는 Windows 7을 실행 하는 클라이언트에 액세스할 수 있도록을 선택할 때 두 개의 보안 터널을 사용 합니다. 원격 액세스 설치 마법사에서 DirectAccess 서버의 터널에 대해 IPsec 보안 연결을 협상할 때 다음 유형의 자격 증명을 사용하도록 지정하는 고급 보안이 포함된 Windows 방화벽 연결 보안 규칙을 구성합니다.  
  
-   인프라 터널에서는 첫 번째 인증에 컴퓨터 인증서 자격 증명을 사용하고 두 번째 인증에 NTLMv2를 사용합니다. NTLMv2 자격 증명은 AuthIP(인증된 인터넷 프로토콜)를 강제로 사용하며, DirectAccess 클라이언트에서 인트라넷 터널에 Kerberos 자격 증명을 사용하기 전에 DNS 서버 및 도메인 컨트롤러에 대한 액세스를 제공합니다.  
  
-   인트라넷 터널에서는 첫 번째 인증에 컴퓨터 인증서 자격 증명을 사용하고 두 번째 인증에 사용자 Kerberos를 사용합니다.  
  
### <a name="172-plan-multiple-domains"></a>1.7.2 여러 도메인 계획  
관리 서버 목록에는 DirectAccess 클라이언트 컴퓨터가 포함된 보안 그룹을 포함하는 모든 도메인의 도메인 컨트롤러가 포함되어야 합니다. 또한 DirectAccess 클라이언트로 구성된 컴퓨터를 사용할 수 있는 사용자 계정을 포함하는 모든 도메인이 포함되어야 합니다. 그러면 사용 중인 클라이언트 컴퓨터와 동일한 도메인에 있지 않은 사용자가 사용자 도메인의 도메인 컨트롤러로 인증을 받을 수 있게 됩니다. 이 동작은 도메인이 동일한 포리스트에 있는 경우 자동으로 수행됩니다.  
  
> [!NOTE]  
> 다른 포리스트의 클라이언트 컴퓨터 또는 애플리케이션 서버에 사용되는 컴퓨터가 보안 그룹에 있는 경우 해당 포리스트의 도메인 컨트롤러는 자동으로 검색되지 않습니다. 작업을 실행할 수 있습니다 **관리 서버 새로 고침** 이러한 도메인 컨트롤러를 검색 하는 원격 액세스 관리 콘솔에서.  
  
가능하면 원격 액세스 배포 중에 공통 도메인 이름 접미사를 NRPT(이름 확인 정책 테이블)에 추가해야 합니다. 예를 들어 두 개의 도메인 domain1.corp.contoso.com과 domain2.corp.contoso.com이 있는 경우 NRPT에 두 항목을 추가하는 대신 공통 DNS 접미사 항목(여기서 도메인 이름 접미사는 corp.contoso.com)을 추가할 수 있습니다. 이 동작은 같은 루트에 있는 도메인에 대해서는 자동으로 수행되지만 같은 루트에 있지 않은 도메인은 수동으로 추가해야 합니다.  
  
WINS(Windows 인터넷 이름 서비스)가 다중 도메인 환경에 배포된 경우 DNS에 WINS 정방향 조회 영역을 배포해야 합니다. 자세한 내용은 참조 **단일 레이블 이름을** 에 [1.4.2 로컬 이름 확인 계획](#142-plan-for-local-name-resolution) 이 문서 앞부분에 나오는 섹션입니다.  
  
## <a name="18-plan-group-policy-objects"></a>1.8 그룹 정책 개체 계획  
이 섹션에서는 원격 액세스 인프라에서 GPO(그룹 정책 개체)의 역할에 대해 설명하며, 다음 하위 섹션으로 구성되어 있습니다.  
  
-   [1.8.1 자동으로 만들어진 Gpo 구성](#181-configure-automatically-created-gpos)  
  
-   [수동으로 만든 Gpo 구성 1.8.2](#182-configure-manually-created-gpos)  
  
-   [1.8.3 다중 도메인 컨트롤러 환경에서 Gpo 관리](#183-manage-gpos-in-a-multi-domain-controller-environment)  
  
-   [제한 된 권한으로 원격 액세스 Gpo 관리 1.8.4](#184-manage-remote-access-gpos-with-limited-permissions)  
  
-   [삭제 된 GPO에서 복구 1.8.5](#185-recover-from-a-deleted-gpo)  
  
원격 액세스를 구성할 때 구성된 DirectAccess 설정은 GPO에 수집됩니다. 다음 유형의 GPO가 DirectAccess 설정으로 채워지며 다음과 같이 배포됩니다.  
  
-   **DirectAccess 클라이언트 GPO**  
  
    이 GPO는 IPv6 전환 기술 설정, NRPT 항목, 고급 보안이 포함된 Windows 방화벽 연결 보안 규칙 등의 클라이언트 설정을 포함하며, 클라이언트 컴퓨터에 지정된 보안 그룹에 적용됩니다.  
  
-   **DirectAccess 서버 GPO**  
  
    이 GPO는 배포에서 DirectAccess 서버로 구성된 모든 서버에 적용되는 DirectAccess 구성 설정을 포함합니다. 또한 고급 보안이 포함된 Windows 방화벽 연결 보안 규칙을 포함합니다.  
  
-   **응용 프로그램 서버 GPO**  
  
    이 GPO는 필요에 따라 DirectAccess 클라이언트에서 인증 및 암호화를 확장하기 위해 선택한 대상 애플리케이션 서버의 설정을 포함합니다. 인증 및 암호화를 확장하지 않는 경우에는 사용되지 않습니다.  
  
다음 두 가지 방법으로 GPO를 구성할 수 있습니다.  
  
-   **자동으로**-자동으로 만들도록 지정할 수 있습니다. 각 GPO에 기본 이름이 지정됩니다.  
  
-   **수동으로**-Active Directory 관리자가 미리 정의한 Gpo를 사용할 수 있습니다.  
  
> [!NOTE]  
> DirectAccess가 특정 GPO를 사용하도록 구성된 후에는 다른 GPO를 사용하도록 구성할 수 없습니다.  
  
자동으로 구성된 GPO를 사용하든, 수동으로 구성된 GPO를 사용하든 상관없이, 클라이언트에서 3G 네트워크를 사용하는 경우 저속 연결 검색에 대한 정책을 추가해야 합니다. 에 대 한 경로 **정책: 구성 그룹 정책 저속 연결 검색** 는: **컴퓨터 구성/정책/관리 템플릿/시스템/그룹 정책**합니다.  
  
> [!CAUTION]  
> DirectAccess cmdlet을 실행 하기 전에 모든 원격 액세스 Gpo를 백업 하려면 다음 절차를 사용 하 여: [를 백업 및 원격 액세스 구성 복원](https://go.microsoft.com/fwlink/?LinkID=257928)합니다.  
  
GPO 연결을 위한 올바른 권한(다음 섹션 참조)이 없으면 경고가 발생합니다. 이 경우 원격 액세스 작업은 계속되지만 연결이 발생하지 않습니다. 이 경고가 발생하면 나중에 권한을 추가한 경우에도 연결이 자동으로 생성되지 않습니다. 대신 관리자가 수동으로 연결을 만들어야 합니다.  
  
### <a name="181-configure-automatically-created-gpos"></a>1.8.1 자동으로 만들어진 GPO 구성  
자동으로 만들어진 GPO를 사용할 때 고려할 사항은 다음과 같습니다.  
  
자동으로 만들어진 GPO는 다음과 같이 위치 및 연결 대상 매개 변수에 따라 적용됩니다.  
  
-   DirectAccess 서버 GPO의 경우 위치 및 연결 매개 변수는 DirectAccess 서버를 포함하는 도메인을 가리킵니다.  
  
-   클라이언트 및 애플리케이션 서버 GPO가 만들어지면 해당 GPO가 만들어지는 단일 도메인으로 위치가 설정됩니다. GPO 이름은 각 도메인에서 조회되며 DirectAccess 설정(있는 경우)으로 채워집니다. 연결 대상은 GPO가 만들어진 도메인의 루트로 설정됩니다. GPO는 클라이언트 컴퓨터 또는 애플리케이션 서버가 포함된 각 도메인에 만들어지며 각 도메인의 루트에 연결됩니다.  
  
자동으로 만들어진 GPO를 사용하여 DirectAccess 설정을 적용하는 경우 원격 액세스 관리자에게 다음 권한이 필요합니다.  
  
-   각 도메인 대한 GPO 만들기 권한  
  
-   선택한 모든 클라이언트 도메인 루트에 대한 연결 권한  
  
-   서버 GPO 도메인 루트에 대한 연결 권한  
  
또한 다음 권한도 필요합니다.  
  
-   GPO에 대한 보안 만들기, 편집, 삭제 및 수정 권한이 필요합니다.  
  
-   원격 액세스 관리자에게 필요한 각 도메인에 대한 GPO 읽기 권한이 있는 것이 좋습니다. 그러면 GPO를 만들 때 원격 액세스에서 이름이 중복된 GPO가 없는지 확인할 수 있습니다.  
  
### <a name="182-configure-manually-created-gpos"></a>1.8.2 수동으로 만든 GPO 구성  
수동으로 만든 GPO를 사용할 때 고려할 사항은 다음과 같습니다.  
  
-   원격 액세스 설치 마법사를 실행하기 전에 GPO가 존재해야 합니다.  
  
-   DirectAccess 설정을 적용하려면 원격 액세스 관리자에게 수동으로 만든 GPO에 대한 모든 권한(보안 편집, 삭제, 수정 권한)이 있어야 합니다.  
  
-   전체 도메인에서 GPO 연결에 대한 검색이 수행됩니다. GPO가 도메인에 연결되지 않은 경우 자동으로 도메인 루트에 연결이 만들어집니다. 연결을 만드는 데 필요한 권한이 없으면 경고가 발생합니다.  
  
### <a name="183-manage-gpos-in-a-multi-domain-controller-environment"></a>1.8.3 다중 도메인 컨트롤러 환경에서 GPO 관리  
각 GPO가 다음과 같이 특정 도메인 컨트롤러에 의해 관리됩니다.  
  
-   서버 GPO는 해당 서버에 연결된 Active Directory 사이트에 있는 도메인 컨트롤러 중 하나에 의해 관리됩니다. 해당 사이트의 도메인 컨트롤러가 읽기 전용인 경우 서버 GPO는 DirectAccess 서버와 가장 가까이 있는 쓰기 가능 도메인 컨트롤러에 의해 관리됩니다.  
  
-   클라이언트 및 애플리케이션 서버 GPO는 PDC(주 도메인 컨트롤러)로 실행되는 도메인 컨트롤러에 의해 관리됩니다.  
  
GPO 설정을 수동으로 수정하려면 다음 사항을 고려합니다.  
  
-   서버 GPO에 대 한 실행에 DirectAccess 서버에서 관리자 권한 명령 프롬프트에서 DirectAccess 서버에 연결 된 도메인 컨트롤러를 식별 하려면 **nltest /dsgetdc: /writable**합니다.  
  
-   기본적으로 네트워킹 Windows PowerShell cmdlet 또는 그룹 정책 관리 콘솔을 사용하여 변경하는 경우 PDC 역할을 하는 도메인 컨트롤러가 사용됩니다.  
  
또한 DirectAccess 서버와 연결된 도메인 컨트롤러(서버 GPO의 경우) 또는 PDC(클라이언트 및 애플리케이션 서버 GPO의 경우)가 아닌 도메인 컨트롤러에 대한 설정을 수정하려면 다음 사항을 고려합니다.  
  
-   설정을 수정하기 전에 도메인 컨트롤러가 최신 GPO로 복제되었는지 확인하고 GPO 설정을 백업합니다. 자세한 내용은 참조 [백업 및 원격 액세스 구성 복원](https://go.microsoft.com/fwlink/?LinkID=257928)합니다. GPO가 업데이트되지 않은 경우에는 복제 중에 병합 충돌이 발생할 수 있으며, 이로 인해 원격 액세스 구성이 손상될 수 있습니다.  
  
-   설정을 수정한 후에는 변경 내용이 GPO에 연결된 도메인 컨트롤러에 복제될 때까지 기다려야 합니다. 복제가 완료 될 때까지 원격 액세스 관리 콘솔 또는 원격 액세스 PowerShell cmdlet을 사용하여 추가로 변경하지 마세요. 복제가 완료되기 전에 두 개의 도메인 컨트롤러에서 GPO를 편집하면 병합 충돌이 발생할 수 있으며, 이로 인해 원격 액세스 구성이 손상될 수 있습니다.  
  
또는 기본 설정을 사용 하 여 변경할 수 있습니다는 **도메인 컨트롤러 변경** 대화 상자에서 그룹 정책 관리 콘솔 또는 Windows PowerShell cmdlet을 사용 하 여 **Open-netgpo**, 지정한 도메인 컨트롤러를 사용 하는 변경 되도록 합니다.  
  
-   이를 위해 그룹 정책 관리 콘솔에서 도메인 또는 사이트 컨테이너를 마우스 오른쪽 단추로 클릭 하 고 클릭 **도메인 컨트롤러 변경**합니다.  
  
-   Windows PowerShell에서이 작업을 수행 하려면 지정 된 **DomainController** 에 대 한 매개 변수는 **Open-netgpo** cmdlet입니다. 예를 들어 europe-dc.corp.contoso.com이라는 도메인 컨트롤러를 사용하여 domain1\DA_Server_GPO _Europe이라는 GPO에서 Windows 방화벽의 개인 및 공용 프로필을 사용하도록 설정하려면 다음을 입력합니다.  
  
    ```powershell
    $gpoSession = Open-NetGPO -PolicyStore "domain1\DA_Server_GPO _Europe" -DomainController "europe-dc.corp.contoso.com"  
    Set-NetFirewallProfile -GpoSession $gpoSession -Name @("Private","Public") -Enabled True  
    Save-NetGPO -GpoSession $gpoSession  
    ```  
  
### <a name="184-manage-remote-access-gpos-with-limited-permissions"></a>1.8.4 제한된 권한으로 원격 액세스 GPO 관리  
원격 액세스 배포를 관리하려면 원격 액세스 관리자에게 배포에서 사용되는 GPO에 대한 모든 권한(보안 읽기, 편집, 삭제 및 수정 권한)이 있어야 합니다. 이는 원격 액세스 관리 콘솔 및 원격 액세스 PowerShell 모듈이 원격 액세스 GPO(즉, 클라이언트, 서버 및 애플리케이션 서버 GPO)에서 구성을 읽고 쓰기 때문입니다.  
  
대부분의 조직에서는 GPO를 담당하는 도메인 관리자와 원격 액세스 구성을 담당하는 원격 액세스 관리자가 동일하지 않습니다. 이러한 조직에는 원격 액세스 관리자가 도메인의 GPO에 대한 모든 권한을 가지지 못하도록 제한하는 정책이 있을 수 있습니다. 또한 도메인 관리자가 도메인의 컴퓨터에 적용하기 전에 정책 구성을 검토해야 할 수도 있습니다.  
  
이러한 요구 사항을 충족하려면 도메인 관리자가 GPO마다 두 개의 복사본(준비 및 프로덕션)을 만들어야 합니다. 이 경우 원격 액세스 관리자에게는 준비 GPO에 대한 모든 권한이 부여됩니다. 원격 액세스 관리자는 원격 액세스 관리 콘솔 및 Windows PowerShell cmdlet에서 준비 GPO를 원격 액세스 배포에 사용되는 GPO로 지정합니다. 이렇게 하면 원격 액세스 관리자가 필요에 따라 원격 액세스 구성을 읽고 수정할 수 있습니다.  
  
도메인 관리자는 준비 GPO가 도메인의 관리 범위에 연결되어 있지 않으며 원격 액세스 관리자에게 도메인의 GPO 연결 권한이 없는지 확인해야 합니다. 이 두 가지 사항이 확인되면 원격 액세스 관리자가 준비 GPO에 적용한 변경 내용이 도메인의 컴퓨터에 영향을 주지 않습니다.  
  
도메인 관리자는 프로덕션 GPO를 필요한 관리 범위에 연결하고 적절한 보안 필터링을 적용합니다. 그러면 이러한 GPO의 변경 내용이 도메인의 컴퓨터(클라이언트 컴퓨터, DirectAccess 서버 및 애플리케이션 서버)에 적용됩니다. 원격 액세스 관리자는 프로덕션 GPO에 대한 권한이 없습니다.  
  
준비 GPO가 변경된 경우 도메인 관리자는 해당 GPO의 정책 구성을 검토하여 조직의 보안 요구 사항을 충족하는지 확인할 수 있습니다. 그런 다음 도메인 관리자는 백업 기능을 사용하여 준비 GPO에서 설정을 내보내고 해당 프로덕션 GPO로 설정을 가져옵니다. 이러한 설정이 도메인의 컴퓨터에 적용됩니다.  
  
다음 다이어그램에서는 이 구성을 보여 줍니다.  
  
![원격 액세스 Gpo 관리](../../../media/Step-1-Plan-the-DirectAccess-Infrastructure/DA_Plan_Advanced_Step1_GPOS.png)  
  
### <a name="185-recover-from-a-deleted-gpo"></a>1.8.5 삭제된 GPO 복구  
클라이언트, DirectAccess 서버 또는 애플리케이션 서버 GPO를 실수로 삭제한 경우 사용 가능한 백업이 없다면 구성 설정을 제거하고 다시 구성해야 합니다. 그러나 백업을 사용할 수 있는 경우 백업에서 GPO를 복구할 수 있습니다.  
  
원격 액세스 관리 콘솔에 다음과 같은 오류 메시지가 표시 됩니다. **gpo (gpo 이름)를 찾을 수 없습니다**. 구성 설정을 제거하려면 다음 단계를 따릅니다.  
  
1.  Windows PowerShell cmdlet을 실행 **uninstall-remoteaccess**합니다.  
  
2.  원격 액세스 관리 콘솔을 엽니다.  
  
3.  GPO를 찾을 수 없다는 오류 메시지가 표시됩니다. **구성 설정 제거**를 클릭합니다. 작업이 완료되면 서버가 구성되지 않은 상태로 복원됩니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   [2 단계: DirectAccess 배포 계획](da-adv-plan-s2-deployments.md)  
  


