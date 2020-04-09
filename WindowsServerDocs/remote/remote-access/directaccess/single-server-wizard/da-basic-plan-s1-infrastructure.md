---
title: 1 단계 기본 DirectAccess 인프라 계획
description: 이 항목은 Windows Server 2016에 대 한 시작 마법사를 사용 하 여 단일 DirectAccess 서버 배포 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 6bab4adbcf006556c73c96f403afe7538079e967
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819346"
---
# <a name="step-1-plan-the-basic-directaccess-infrastructure"></a>1 단계 기본 DirectAccess 인프라 계획
단일 서버에 기본 DirectAccess를 배포 하기 위한 첫 번째 단계는 배포에 필요한 인프라 계획을 수행 하는 것입니다. 이 항목에서는 인프라 계획 단계에 대해 설명합니다.  
  
|작업|설명|  
|----|--------|  
|네트워크 토폴로지 및 설정 계획|DirectAccess 서버를에 지에서 \(하거나 NAT\) 장치 또는 방화벽\)\(네트워크 주소 변환 뒤에 놓을 위치를 결정 하 고 IP 주소 지정 및 라우팅을 계획 합니다.|  
|방화벽 요구 사항 계획|DirectAccess가 경계면 방화벽을 통과하도록 허용할 계획을 수립합니다.|  
|인증서 요구 사항 계획|DirectAccess는 클라이언트 인증에 Kerberos 또는 인증서를 사용할 수 있습니다. 이 기본 DirectAccess 배포에서는 Kerberos 프록시가 자동으로 구성되고 Active Directory 자격 증명을 사용하여 인증이 수행됩니다.|  
|DNS 요구 사항 계획|DirectAccess 서버, 인프라 서버 및 클라이언트 연결에 대한 DNS 설정을 계획합니다.|  
|Active Directory 계획|도메인 컨트롤러 및 Active Directory 요구 사항을 계획합니다.|  
|그룹 정책 개체 계획|조직에 필요한 GPO 및 GPO를 만들거나 편집할 방법을 결정합니다.|  
  
이 계획 작업은 특정 순서대로 완료할 필요가 없습니다.  
  
## <a name="plan-network-topology-and-settings"></a><a name="bkmk_1_1_Network_svr_top_settings"></a>네트워크 토폴로지 및 설정 계획  
  
### <a name="plan-network-adapters-and-ip-addressing"></a>네트워크 어댑터 및 IP 주소 지정 계획  
  
1.  사용할 네트워크 어댑터 토폴로지를 확인합니다. 다음 중 하나를 사용하여 DirectAccess를 설정할 수 있습니다.  
  
    -   네트워크 어댑터 두 개를 사용 하 여 네트워크 어댑터를 인터넷에 연결 하 고 다른 네트워크 어댑터를 내부 네트워크에 연결 하거나 NAT, 방화벽 또는 라우터 장치 뒤에 두 개의 네트워크 어댑터를 경계 네트워크에 연결 하 고 다른 하나는 내부에 연결 합니다. network.  
  
    -   하나의 네트워크 어댑터를 사용 하는 NAT 장치 뒤에-DirectAccess 서버가 NAT 장치 뒤에 설치 되 고 단일 네트워크 어댑터가 내부 네트워크에 연결 됩니다.  
  
2.  IP 주소 지정 요구 사항을 확인합니다.  
  
    DirectAccess는 IPsec에서 IPv6을 사용하여 DirectAccess 클라이언트 컴퓨터와 회사 내부 네트워크 사이의 보안 연결을 만듭니다. 그러나 DirectAccess를 사용하기 위해 반드시 IPv6 인터넷 또는 내부 네트워크에서 지원되는 기본 IPv6에 연결할 필요는 없습니다. 대신, IPv6 전환 기술을 자동으로 구성 하 고 IPv6 전환 기술을 사용 하 여 IPv4 인터넷 \(6to4, Teredo, IP\-HTTPS\)와 IPv4\-인트라넷 \(NAT64 또는 ISATAP\)에만 터널링 합니다. 이러한 전환 기술에 대한 개요는 다음 리소스를 참조하세요.  
  
    -   [IPv6 전환 기술](https://technet.microsoft.com/library/bb726951.aspx)  
  
    -   [IP-HTTPS 터널링 프로토콜 사양](https://msdn.microsoft.com/library/dd358571(PROT.10).aspx)  
  
3.  다음 표에 따라 필요한 어댑터 및 주소를 구성합니다. 단일 네트워크 어댑터를 사용 하는 NAT 장치 뒤에 있는 배포의 경우 **내부 네트워크 어댑터** 열만 사용 하 여 IP 주소를 구성 합니다.  
  
    ||외부 네트워크 어댑터|내부 네트워크 어댑터<sup>1</sup>|라우팅 요구 사항|  
    |-|--------------|--------------------|------------|  
    |IPv4 인트라넷 및 IPv4 인터넷|다음을 구성합니다.<p>-적절 한 서브넷 마스크를 사용 하는 고정 공용 IPv4 주소 하나<br />-인터넷 방화벽이 나 로컬 인터넷 서비스 공급자 \(ISP\) 라우터의 기본 게이트웨이 IPv4 주소입니다.|다음을 구성합니다.<p>-적절 한 서브넷 마스크는 IPv4 인트라넷 주소입니다.<br />-연결\-인트라넷 네임 스페이스의 특정 DNS 접미사입니다. DNS 서버도 내부 인터페이스에 구성해야 합니다.<br />-인트라넷 인터페이스에 기본 게이트웨이를 구성 하지 마십시오.|DirectAccess 서버에서 내부 IPv4 네트워크의 모든 서브넷에 연결하도록 구성하려면 다음을 수행합니다.<p>1. 인트라넷의 모든 위치에 대 한 IPv4 주소 공간을 나열 합니다.<br />2. **경로 add \-p** 또는 **netsh interface ipv4 add route** 명령을 사용 하 여 DirectAccess 서버의 ipv4 라우팅 테이블에 고정 경로로 ipv4 주소 공간을 추가 합니다.|  
    |IPv6 인터넷 및 IPv6 인트라넷|다음을 구성합니다.<p>-ISP에서 제공 하는 자동 구성 된 주소 구성을 사용 합니다.<br />- **Route print** 명령을 사용 하 여 ISP 라우터를 가리키는 기본 IPv6 경로가 IPv6 라우팅 테이블에 존재 하는지 확인 합니다.<br />-ISP 및 인트라넷 라우터가 RFC 4191에 설명 된 기본 라우터 기본 설정을 사용 하 고 로컬 인트라넷 라우터 보다 높은 기본 우선 순위를 사용 하는지 여부를 확인 합니다. 둘 다에 해당되면 기본 경로에 대한 다른 구성이 필요하지 않습니다. ISP 라우터의 우선 순위가 높으면 DirectAccess 서버의 활성 기본 IPv6 경로가 IPv6 인터넷을 가리킵니다.<p>DirectAccess 서버가 IPv6 라우터이므로 기본 IPv6 인프라가 있는 경우 인터넷 인터페이스에서 인트라넷의 도메인 컨트롤러에도 연결할 수 있습니다. 이 경우 경계 네트워크의 도메인 컨트롤러에 패킷 필터를 추가 하 여 DirectAccess 서버의 인터넷\-연결 인터페이스에 대 한 IPv6 주소에 대 한 연결을 방지 합니다.|다음을 구성합니다.<p>-기본 기본 설정 수준을 사용 하지 않는 경우 **netsh interface ipv6 Set InterfaceIndex ignoredefaultroutes\=enabled** 명령을 사용 하 여 인트라넷 인터페이스를 구성 합니다. 이 명령을 사용하면 인트라넷 라우터를 가리키는 추가 기본 경로가 IPv6 라우팅 테이블에 추가되지 않습니다. netsh 인터페이스 표시 인터페이스 명령의 표시에서 인트라넷 인터페이스의 InterfaceIndex를 가져올 수 있습니다.|IPv6 인트라넷을 사용하는 경우 모든 IPv6 위치에 연결하도록 DirectAccess 서버를 구성하려면 다음을 수행합니다.<p>1. 인트라넷의 모든 위치에 대 한 IPv6 주소 공간을 나열 합니다.<br />2. **netsh interface ipv6 add route** 명령을 사용 하 여 DirectAccess 서버의 ipv6 라우팅 테이블에 고정 경로로 ipv6 주소 공간을 추가 합니다.|  
    |IPv4 인터넷 및 IPv6 인트라넷|DirectAccess 서버는 Microsoft 6to4 어댑터 인터페이스를 사용하여 기본 IPv6 경로 트래픽을 IPv4 인터넷의 6to4 릴레이에 전달합니다. 다음 명령을 사용 하 여 기본 i p v 6이 회사\) 네트워크에 배포 되지 않은 경우에 사용 되는 IPv4 \(인터넷에서 Microsoft 6to4 relay의 IPv4 주소에 대 한 DirectAccess 서버를 구성할 수 있습니다. netsh interface IPv6 6to4 set relay name\=192.88.99.1 state state\=enabled 명령입니다.|||  
  
    > [!NOTE]  
    > 유의 사항은 다음과 같습니다.  
    >   
    > 1.  DirectAccess 클라이언트에 공용 IPv4 주소가 할당된 경우 DirectAccess 클라이언트는 6to4 전환 기술을 사용하여 인트라넷에 연결합니다. DirectAccess 클라이언트가 6to4를 사용 하 여 DirectAccess 서버에 연결할 수 없는 경우 IP\-HTTPS를 사용 합니다.  
    > 2.  기본 IPv6 클라이언트 컴퓨터는 기본 IPv6을 통해 DirectAccess 서버에 연결할 수 있으므로 전환 기술이 필요 없습니다.  
  
### <a name="plan-firewall-requirements"></a><a name="ConfigFirewalls"></a>방화벽 요구 사항 계획  
DirectAccess 서버가 경계면 방화벽 뒤에 있는 경우 DirectAccess 서버가 IPv4 인터넷에 있으면 DirectAccess 트래픽에 대한 다음과 같은 예외가 필요합니다.  
  
-   6to4 트래픽-IP 프로토콜 41 인바운드 및 아웃 바운드입니다.  
  
-   IP\-HTTPS-전송 제어 프로토콜 \(TCP\) 대상 포트 443 및 TCP 원본 포트 443 아웃 바운드입니다.  
  
-   단일 네트워크 어댑터를 사용하여 DirectAccess를 배포하고 DirectAccess 서버에 네트워크 위치 서버를 설치하려는 경우에는 TCP 포트 62000도 제외해야 합니다.  
  
    > [!NOTE]  
    > 이 예외는 DirectAccess 서버에 적용됩니다. 다른 모든 예외는 경계면 방화벽에 적용됩니다.  
  
다음 예외는 DirectAccess 서버가 IPv6 인터넷에 있는 경우 DirectAccess 트래픽에 대해 필요합니다.  
  
-   IP 프로토콜 50  
  
-   UDP 대상 포트 500 인바운드, UDP 원본 포트 500 아웃바운드  
  
추가 방화벽을 사용하는 경우 DirectAccess 트래픽에 대해 다음 내부 네트워크 방화벽 예외를 적용합니다.  
  
-   ISATAP 프로토콜 41 인바운드 및 아웃 바운드  
  
-   모든 IPv4\/IPv6 트래픽에 대 한 TCP\/UDP  
  
### <a name="plan-certificate-requirements"></a><a name="bkmk_1_2_CAs_and_certs"></a>인증서 요구 사항 계획  
IPsec에 대한 인증서 요구 사항에는 클라이언트와 DirectAccess 서버 간의 IPsec 연결을 설정할 때 DirectAccess 클라이언트 컴퓨터에서 사용하는 컴퓨터 인증서 및 DirectAccess 클라이언트와의 IPsec 연결을 설정할 때 DirectAccess 서버에서 사용하는 컴퓨터 인증서가 포함됩니다. Windows Server 2012 R2 및 Windows Server 2012의 DirectAccess에서는 이러한 IPsec 인증서를 반드시 사용 해야 하는 것은 아닙니다. 시작 마법사는 DirectAccess 서버가 Kerberos 프록시 역할을 하여 인증서를 요구하지 않고 IPsec 인증을 수행하도록 구성합니다.
  
1.  **IP\-HTTPS 서버**입니다. DirectAccess를 구성 하는 경우 DirectAccess 서버가 자동으로 IP\-HTTPS 웹 수신기 역할을 하도록 구성 됩니다. IP\-HTTPS 사이트에는 웹 사이트 인증서가 필요 하며, 클라이언트 컴퓨터에서 인증서에 대 한 CRL\) 사이트 \(인증서 해지 목록에 연결할 수 있어야 합니다. DirectAccess 사용 마법사에서는 SSTP VPN 인증서를 사용합니다. SSTP가 구성 되지 않은 경우 IP\-HTTPS에 대 한 인증서가 컴퓨터 개인 저장소에 있는지 확인 합니다. 사용할 수 없는 경우 자체\-서명 된 인증서를 자동으로 만듭니다.
  
2.  **네트워크 위치 서버**. 네트워크 위치 서버는 클라이언트 컴퓨터가 회사 네트워크에 있는지 여부를 검색 하는 데 사용 되는 웹 사이트입니다. 네트워크 위치 서버에는 웹 사이트 인증서가 필요 합니다. DirectAccess 클라이언트에서 인증서의 CRL 사이트에 연결할 수 있어야 합니다. 원격 액세스 사용 마법사는 네트워크 위치 서버에 대 한 인증서가 컴퓨터 개인 저장소에 있는지 여부를 확인 합니다. 표시 되지 않는 경우 자동으로 자체\-서명 된 인증서를 만듭니다.
  
이러한 각 항목에 대한 인증 요구 사항은 다음 표에 요약되어 있습니다.  
  
|IPsec 인증|IP\-HTTPS 서버|네트워크 위치 서버|  
|------------|----------|--------------|  
|내부 CA가 인증에 Kerberos 프록시를 사용 하지 않는 경우 DirectAccess 서버 및 클라이언트에 IPsec 인증용 컴퓨터 인증서를 발급 하는 데 필요한|공용 CA-공용 CA를 사용 하 여 IP\-HTTPS 인증서를 발급 하는 것이 좋습니다. 이렇게 하면 외부에서 CRL 배포 지점을 사용할 수 있습니다.|내부 CA-내부 CA를 사용 하 여 네트워크 위치 서버 웹 사이트 인증서를 발급할 수 있습니다. 그러나 내부 네트워크에서 CRL 배포 지점을 항상 사용할 수 있어야 합니다.|  
||내부 CA-내부 CA를 사용 하 여 IP\-HTTPS 인증서를 발급할 수 있습니다. 그러나 CRL 배포 지점을 외부에서 사용할 수 있는지 확인 해야 합니다.|자체\-서명 된 인증서-네트워크 위치 서버 웹 사이트에 자체\-서명 된 인증서를 사용할 수 있습니다. 그러나 멀티 사이트 배포에서는 자체\-서명 된 인증서를 사용할 수 없습니다.|  
||자체\-서명 된 인증서-IP\-HTTPS 서버에 자체\-서명 된 인증서를 사용할 수 있습니다. 그러나 CRL 배포 지점을 외부에서 사용할 수 있는지 확인 해야 합니다. 멀티 사이트 배포에는 자체\-서명 된 인증서를 사용할 수 없습니다.||  
  
#### <a name="plan-certificates-for-ip-https-and-network-location-server"></a><a name="bkmk_website_cert_IPHTTPS"></a>IP\-HTTPS 및 네트워크 위치 서버용 인증서 계획  
이러한 용도의 인증서를 프로비전하려면 [고급 설정을 사용하여 단일 DirectAccess 서버 배포](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)를 참조하세요. 사용할 수 있는 인증서가 없는 경우 시작 마법사는 이러한 목적으로 자체\-서명 된 인증서를 자동으로 만듭니다.
  
> [!NOTE]
> IP\-HTTPS와 네트워크 위치 서버에 대 한 인증서를 수동으로 프로 비전 하는 경우 인증서에 주체 이름이 있는지 확인 합니다. 인증서에 주체 이름 대신 대체 이름이 있는 경우 이는 DirectAccess 마법사에서 허용되지 않습니다.  
  
#### <a name="plan-dns-requirements"></a>DNS 요구 사항 계획  
DirectAccess 배포에서는 다음과 같은 용도에 DNS가 필요합니다.  
  
-   **DirectAccess 클라이언트 요청**. 내부 네트워크에 없는 DirectAccess 클라이언트 컴퓨터의 요청을 확인하는 데 DNS가 사용됩니다. DirectAccess 클라이언트는 인터넷에 있는지 또는 회사 네트워크에 있는지 확인하기 위해 DirectAccess 네트워크 위치 서버에 연결합니다. 연결에 성공하면 클라이언트가 내부 네트워크에 있는 것으로 확인되므로 DirectAccess가 사용되지 않고 클라이언트 요청이 클라이언트 컴퓨터의 네트워크 어댑터에 구성된 DNS 서버를 통해 확인됩니다. 연결에 실패하면 클라이언트가 인트라넷에 있는 것으로 간주됩니다. DirectAccess 클라이언트는 이름 확인 정책 테이블 \(NRPT\)를 사용 하 여 이름 요청을 확인할 때 사용할 DNS 서버를 결정 합니다. 클라이언트에서 DirectAccess DNS64를 사용하여 이름을 확인하거나, 대체 내부 DNS 서버를 사용하도록 지정할 수 있습니다. 이름 확인을 수행할 때 NRPT는 DirectAccess 클라이언트에서 요청을 처리할 방법을 식별하는 데 사용됩니다. 클라이언트는 FQDN 또는 단일\-레이블 이름 (예: http:\/\/internal)을 요청 합니다. 단일\-레이블 이름이 요청인 경우 FQDN을 만들기 위해 DNS 접미사가 추가 됩니다. DNS 쿼리가 NRPT의 항목과 일치하고 DNS64 또는 인트라넷 DNS 서버가 해당 항목에 지정되어 있는 경우 해당 쿼리는 지정된 서버를 사용하여 이름 확인을 위해 전송됩니다. 일치하지만 지정된 DNS 서버가 없는 경우에는 예외 규칙을 나타내므로 일반 이름 확인이 적용됩니다.  
  
    DirectAccess 관리 콘솔에서 NRPT에 새 접미사가 추가된 경우 **검색** 단추를 클릭하여 접미사의 기본 DNS 서버를 자동으로 검색할 수 있습니다. 자동 검색은 다음과 같이 작동합니다.  
  
    1.  회사 네트워크가 IPv4\-기반 이거나 IPv4 및 IPv6 인 경우 기본 주소는 DirectAccess 서버에 있는 내부 어댑터의 DNS64 주소입니다.  
  
    2.  회사 네트워크가 IPv6\-기반으로 하는 경우 기본 주소는 회사 네트워크에 있는 DNS 서버의 IPv6 주소입니다.  
  
-   **인프라 서버**
  
    1.  **네트워크 위치 서버**. DirectAccess 클라이언트는 내부 네트워크에 있는지 확인하기 위해 네트워크 위치 서버에 연결합니다. 내부 네트워크의 클라이언트는 네트워크 위치 서버의 이름을 확인할 수 있어야 하지만, 인터넷에 있을 때는 이름을 확인하지 못하도록 설정되어야 합니다. 이를 위해 기본적으로 네트워크 위치 서버의 FQDN이 NRPT에 예외 규칙으로 추가됩니다. 또한 DirectAccess를 구성하는 경우 다음 규칙이 자동으로 만들어집니다.  
  
        1.  루트 도메인 또는 DirectAccess 서버의 도메인 이름과 DirectAccess 서버에 구성된 인트라넷 DNS 서버에 해당하는 IPv6 주소에 대한 DNS 접미사 규칙. 예를 들어 DirectAccess 서버가 corp.contoso.com 도메인의 구성원인 경우 corp.contoso.com DNS 접미사에 대한 규칙이 만들어집니다.  
  
        2.  네트워크 위치 서버의 FQDN에 대한 예외 규칙. 예를 들어 네트워크 위치 서버 URL이 https:\/\/nls.corp.contoso.com 인 경우 FQDN nls.corp.contoso.com에 대 한 예외 규칙이 만들어집니다.  
  
        **IP\-HTTPS 서버**입니다. DirectAccess 서버는 IP\-HTTPS 수신기 역할을 하며 해당 서버 인증서를 사용 하 여 IP\-HTTPS 클라이언트를 인증 합니다. IP\-HTTPS 이름은 공용 DNS 서버를 사용 하는 DirectAccess 클라이언트에서 확인할 수 있어야 합니다.  
  
        **연결 검증 도구**. DirectAccess는 DirectAccess 클라이언트 컴퓨터에서 내부 네트워크에 대한 연결을 확인하는 데 사용하는 기본 웹 검색을 만듭니다. 검색이 정상적으로 작동하려면 다음 이름을 DNS에 수동으로 등록해야 합니다.  
  
        1.  directaccess\-webprobehost-DirectAccess 서버의 내부 IPv4 주소 또는 IPv6\-환경의 IPv6 주소로 확인 되어야 합니다.  
  
        2.  directaccess\-directaccess-corpconnectivityhost-localhost \(루프백\) 주소로 확인 되어야 합니다. A 및 AAAA 레코드(값이 127.0.0.1인 A 레코드와 값의 마지막 32비트가 NAT64 접두사에서 127.0.0.1로 생성된 AAAA 레코드)가 만들어집니다. NAT64 접두사는 get\-get-netnattransitionconfiguration cmdlet을 실행 하 여 검색할 수 있습니다.  
  
        HTTP 또는 PING을 통해 다른 웹 주소를 사용하여 추가 연결 검증 도구를 만들 수 있습니다. 각 연결 검증 도구에 대한 DNS 항목이 있어야 합니다.  
  
#### <a name="dns-server-requirements"></a>DNS 서버 요구 사항  
  
-   DirectAccess 클라이언트의 경우 Windows Server 2008, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 또는 i p v 6을 지 원하는 DNS 서버를 실행 하는 DNS 서버를 사용 해야 합니다.  
  
> [!NOTE]  
> DirectAccess를 배포하는 경우 Windows Server 2003을 실행하는 DNS 서버를 사용하지 않는 것이 좋습니다. Windows Server 2003 DNS 서버는 IPv6 레코드를 지원하지만 Microsoft에서 Windows Server 2003을 더 이상 지원하지 않습니다. 또한 도메인 컨트롤러가 Windows Server 2003을 실행하는 경우 파일 복제 서비스 문제로 인해 DirectAccess를 배포하면 안 됩니다. 자세한 내용은 참조 [DirectAccess 구성은 지원 되지 않으므로](../DirectAccess-Unsupported-Configurations.md)합니다.  
  
### <a name="plan-the-network-location-server"></a><a name="bkmk_1_4_NLS"></a>네트워크 위치 서버 계획  
네트워크 위치 서버는 DirectAccess 클라이언트가 회사 네트워크에 있는지 검색하는 데 사용되는 웹 사이트입니다. 회사 네트워크의 클라이언트는 DirectAccess를 사용하여 내부 리소스에 연결하는 것이 아니라 직접 연결합니다.  
  
시작 마법사가 DirectAccess 서버에서 네트워크 위치 서버를 자동으로 설정하며, DirectAccess를 배포할 때 웹 사이트가 자동으로 만들어집니다. 따라서 인증서 인프라를 사용하지 않고 간편하게 설치할 수 있습니다.
  
자체\-서명 된 인증서를 사용 하지 않고 네트워크 위치 서버를 배포 하려는 경우 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)를 참조 하세요.
  
### <a name="plan-active-directory"></a><a name="bkmk_1_6_AD"></a>계획 Active Directory  
DirectAccess는 다음과 같이 Active Directory 및 Active Directory 그룹 정책 개체를 사용 합니다.
  
-   **인증**: 인증에 Active Directory가 사용됩니다. DirectAccess 터널에서는 사용자에 대해 Kerberos 인증을 사용하여 내부 리소스에 액세스합니다.
  
-   **그룹 정책 개체**. DirectAccess는 DirectAccess 서버 및 클라이언트에 적용되는 그룹 정책 개체로 구성 설정을 수집합니다.
  
-   **보안 그룹**. DirectAccess는 보안 그룹을 사용하여 DirectAccess 클라이언트 컴퓨터와 DirectAccess 서버를 함께 수집하고 식별합니다. 그룹 정책은 필요한 보안 그룹에 적용됩니다.

**Active Directory 요구 사항**  
  
DirectAccess 배포에서 Active Directory를 계획할 때 필요한 사항은 다음과 같습니다.  
  
-   Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008에 하나 이상의 도메인 컨트롤러가 설치 되어 있어야 합니다. 
  
    도메인 컨트롤러가 \(경계 네트워크에 있는 경우 인터넷 어댑터의 IP 주소에 대 한 연결을 방지 하기 위해 directaccess 서버의 인터넷\-연결 된 네트워크 어댑터를 통해 DirectAccess 서버에 연결할 수\).  
  
-   DirectAccess 서버가 도메인 구성원이어야 합니다.  
  
-   DirectAccess 클라이언트가 도메인 구성원이어야 합니다. 클라이언트는 다음에 속할 수 있습니다.  
  
    -   DirectAccess 서버와 동일한 포리스트의 모든 도메인  
  
    -   DirectAccess 서버 도메인과\-양방향 트러스트 관계가 있는 모든 도메인  
  
    -   DirectAccess 도메인이 속한 포리스트와 양방향 트러스트 관계가 있는 포리스트의 모든 도메인 (\-).  
  
> [!NOTE]
> - DirectAccess 서버는 도메인 컨트롤러일 수 없습니다.  
> - Directaccess 서버의 외부 인터넷 어댑터에서 DirectAccess에 사용 되는 Active Directory 도메인 컨트롤러에 연결할 수 없어야 \(어댑터가 Windows 방화벽\)의 도메인 프로필에 없어야 합니다.  
  
### <a name="plan-group-policy-objects"></a><a name="bkmk_1_7_GPOs"></a>그룹 정책 개체 계획  
DirectAccess를 구성할 때 구성 된 DirectAccess 설정은 GPO\)\(그룹 정책 개체에 수집 됩니다. 두 가지 GPO가 DirectAccess 설정으로 채워지며 다음과 같이 배포됩니다.  
  
-   **DirectAccess 클라이언트 GPO**. 이 GPO는 IPv6 전환 기술 설정, NRPT 항목, 고급 보안이 포함된 Windows 방화벽 연결 보안 규칙 등의 클라이언트 설정을 포함하며, 클라이언트 컴퓨터에 지정된 보안 그룹에 적용됩니다.  
  
-   **DirectAccess 서버 GPO**. 이 GPO는 배포에서 DirectAccess 서버로 구성된 모든 서버에 적용되는 DirectAccess 구성 설정을 포함합니다. 또한 고급 보안이 포함된 Windows 방화벽 연결 보안 규칙을 포함합니다.  
  
다음 두 가지 방법으로 GPO를 구성할 수 있습니다.  
  
1.  **자동**. 자동으로 만들어지도록 지정할 수 있습니다. 각 GPO에 기본 이름이 지정됩니다. GPO는 시작 마법사에 의해 자동으로 만들어집니다.
  
2.  **수동**. Active Directory 관리자가 미리 정의한 GPO를 사용할 수 있습니다.
  
DirectAccess가 특정 GPO를 사용하도록 구성된 후에는 다른 GPO를 사용하도록 구성할 수 없습니다.
  
> [!IMPORTANT]
> 자동으로 구성된 GPO를 사용하든, 수동으로 구성된 GPO를 사용하든 상관없이, 클라이언트에서 3G를 사용하는 경우 저속 연결 검색에 대한 정책을 추가해야 합니다. 정책에 대 한 그룹 정책 경로 **: 그룹 정책 저속 연결 검색 구성** : **컴퓨터 구성 \/ 정책 \/ 관리 템플릿 \/ System \/ 그룹 정책**.  
  
> [!CAUTION]  
> Directaccess cmdlet을 실행 하기 전에 모든 DirectAccess 그룹 정책 개체를 백업 하려면 다음 절차를 따르십시오. [Directaccess 구성 백업 및 복원](https://go.microsoft.com/fwlink/?LinkID=257928)  
  
#### <a name="automatically-created-gpos"></a>자동으로 만들어진 Gpo\-  
자동으로\-만든 Gpo를 사용할 때는 다음 사항에 유의 하세요.  
  
자동으로 만들어진 GPO는 다음과 같이 위치 및 연결 대상 매개 변수에 따라 적용됩니다.  
  
-   DirectAccess 서버 GPO의 경우 위치 및 연결 매개 변수는 둘 다 DirectAccess 서버를 포함하는 도메인을 가리킵니다.  
  
-   클라이언트 GPO가 만들어지면 해당 GPO가 만들어지는 단일 도메인으로 위치가 설정됩니다. GPO 이름은 각 도메인에서 조회되며 DirectAccess 설정(있는 경우)으로 채워집니다. 연결 대상은 GPO가 만들어진 도메인의 루트로 설정됩니다. GPO는 클라이언트 컴퓨터가 포함된 각 도메인에 만들어지며 각 도메인의 루트에 연결됩니다.  
  
자동으로 만들어진 GPO를 사용하는 경우 DirectAccess 설정을 적용하려면 DirectAccess 서버 관리자에게 다음 권한이 필요합니다.  
  
-   각 도메인 대한 GPO 만들기 권한  
  
-   선택한 모든 클라이언트 도메인 루트에 대한 연결 권한  
  
-   서버 GPO 도메인 루트에 대한 연결 권한  
  
-   GPO에 대한 보안 만들기, 편집, 삭제 및 수정 권한이 필요합니다.  
  
-   DirectAccess 관리자에게 필요한 각 도메인에 대한 GPO 읽기 권한이 있는 것이 좋습니다. 그러면 GPO를 만들 때 DirectAccess에서 이름이 중복된 GPO가 없는지 확인할 수 있습니다.  
  
GPO 연결을 위한 올바른 권한이 없으면 경고가 발생합니다. 이 경우 DirectAccess 작업은 계속되지만 연결이 발생하지 않습니다. 이 경고가 발생하면 나중에 권한을 추가한 후에도 연결이 자동으로 생성되지 않습니다. 대신 관리자가 수동으로 연결을 만들어야 합니다.  
  
#### <a name="manually-created-gpos"></a>수동으로 만든 Gpo\-  
수동으로 만든 Gpo를 사용 하\-다음 사항에 유의 하세요.  
  
-   원격 액세스 시작 마법사를 실행하기 전에 GPO가 존재해야 합니다.  
  
-   수동으로 만든 Gpo를 사용 하\-하는 경우 directaccess 설정을 적용 하려면 DirectAccess 관리자에 게\-수동으로 만든 Gpo에 대 한 보안\) 편집, 삭제, 수정 \(모든 GPO 권한이 있어야 합니다.  
  
-   수동으로 만든 GPO를 사용할 때는 전체 도메인에서 GPO에 대한 연결이 검색됩니다. GPO가 도메인에 연결되지 않은 경우 자동으로 도메인 루트에 연결이 만들어집니다. 연결을 만드는 데 필요한 권한이 없으면 경고가 발생합니다.  
  
GPO 연결을 위한 올바른 권한이 없으면 경고가 발생합니다. 이 경우 DirectAccess 작업은 계속되지만 연결이 발생하지 않습니다. 이 경고가 발생하면 나중에 권한을 추가한 경우에도 연결이 자동으로 생성되지 않습니다. 대신 관리자가 수동으로 연결을 만들어야 합니다.  
  
#### <a name="recovering-from-a-deleted-gpo"></a>삭제된 GPO 복구  
DirectAccess 서버, 클라이언트 또는 응용 프로그램 서버 GPO를 실수로 삭제 하 고 사용할 수 있는 백업이 없는 경우 구성 설정을 제거 하 고 다시 구성 하\-다시 구성 해야 합니다. 그러나 백업을 사용할 수 있는 경우 백업에서 GPO를 복구할 수 있습니다.  
  
**DirectAccess 관리** 에 다음 오류 메시지가 표시 됩니다. **GPO <GPO name>를 찾을 수 없습니다**. 구성 설정을 제거하려면 다음 단계를 따릅니다.  
  
1.  PowerShell cmdlet **제거\-원격 액세스**를 실행 합니다.  
  
2.  \-**DirectAccess 관리**를 다시 엽니다.  
  
3.  GPO를 찾을 수 없다는 오류 메시지가 표시됩니다. **구성 설정 제거**를 클릭합니다. 완료 되 면 서버가\-구성 되지 않은 상태로 복원 됩니다.  
  
### <a name="next-step"></a><a name="BKMK_Links"></a>다음 단계  
  
-   [2 단계: 기본 DirectAccess 배포 계획](da-basic-plan-s2-deployment.md)  
  
