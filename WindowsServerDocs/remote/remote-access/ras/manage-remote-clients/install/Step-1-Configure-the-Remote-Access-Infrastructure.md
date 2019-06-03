---
title: 1 단계 원격 액세스 인프라 구성
description: 이 항목은 가이드 Windows Server 2016에서 원격으로 관리 DirectAccess 클라이언트의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e7d1f5b-c939-47ca-892f-5bb285027fbc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dc08d89f7d84b5435e97ed5ed77eb72d003b0c84
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888574"
---
# <a name="step-1-configure-the-remote-access-infrastructure"></a>1 단계 원격 액세스 인프라 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

**참고:** Windows Server 2012에는 DirectAccess와 RRAS(Routing and Remote Access Service)가 단일 원격 액세스 역할로 통합되어 있습니다.  
  
이 항목에서는 IPv4 및 IPv6 혼합된 환경에서 단일 원격 액세스 서버를 사용 하는 고급 원격 액세스 배포에 필요한 인프라를 구성 하는 방법을 설명 합니다. 배포 단계를 시작 하기 전에 설명 된 계획 단계를 완료 한 확인 [1 단계: 원격 액세스 인프라 계획](../plan/Step-1-Plan-the-Remote-Access-Infrastructure.md)합니다.  
  
|태스크|설명|  
|----|--------|  
|서버 네트워크 설정 구성|원격 액세스 서버에서 서버 네트워크 설정을 구성합니다.|  
|회사 네트워크의 라우팅을 구성합니다.|트래픽이 적절히 라우팅되도록 회사 네트워크의 라우팅을 구성합니다.|  
|방화벽 구성|필요한 경우 추가 방화벽을 구성합니다.|  
|CA 및 인증서 구성|인증 기관 (CA), 필요한 경우와 배포에 필요한 기타 인증서 템플릿을 구성 합니다.|  
|DNS 서버 구성|원격 액세스 서버에 대한 DNS 설정을 구성합니다.|  
|Active Directory 구성|클라이언트 컴퓨터와 원격 액세스 서버를 Active Directory 도메인에 가입 합니다.|  
|GPO 구성|필요한 경우 배포에 대해 그룹 정책 개체 (Gpo)를 구성 합니다.|  
|보안 그룹 구성|DirectAccess 클라이언트 컴퓨터를 포함할 보안 그룹 및 배포에 필요한 기타 보안 그룹을 구성합니다.|  
|네트워크 위치 서버 구성|네트워크 위치 서버 웹 사이트 인증서 설치를 포함하여 네트워크 위치 서버를 구성합니다.|  
  
> [!NOTE]  
> 이 항목에는 설명한 절차의 일부를 자동화하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 참조 [Cmdlet를 사용 하 여](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
## <a name="BKMK_ConfigNetworkSettings"></a>서버 네트워크 설정 구성  
에 따라 네트워크 주소 변환 (NAT) 장치 뒤 또는 가장자리에 원격 액세스 서버를 배치 하려는 경우 다음 네트워크 인터페이스 주소 설정은 IPv4 및 i p v 6는 환경에서 단일 서버 배포에 필요한입니다. 모든 IP 주소를 사용 하 여 구성 된 **어댑터 설정 변경** 에 **Windows 네트워크 및 공유 센터**합니다.  
  
**지 토폴로지**:  
  
다음 사항이 필요합니다.  
  
-   두 개의 인터넷 연속 된 공용 고정 IPv4 또는 IPv6 주소입니다.  
  
    > [!NOTE]  
    > 두 개의 공용 IPv4 주소가 Teredo 필요 합니다. Teredo를 사용하지 않는 경우에는 단일 공용 고정 IPv4 주소를 구성할 수 있습니다.  
  
-   단일 내부 고정 IPv4 또는 IPv6 주소  
  
**(두 개의 네트워크 어댑터) NAT 장치 뒤**:  
  
단일 내부 네트워크 연결 고정 IPv4 또는 IPv6 주소가 필요합니다.  
  
**NAT (네트워크 어댑터 1 개) 장치 뒤**:  
  
단일 고정 IPv4 또는 IPv6 주소가 필요합니다.  
  
원격 액세스 서버에 두 개의 네트워크 어댑터 (하나는 도메인 프로필 및 공용 또는 프라이빗 프로필에 대 한 기타), 단일 네트워크 어댑터 토폴로지를 사용 하는 표시 되지만 권장은 다음과 같습니다.  
  
1.  도메인 프로필에 두 번째 네트워크 어댑터는 또한 분류 되었는지 확인 합니다.  
  
2.  어떤 이유로 든 도메인 프로필에 대 한 두 번째 네트워크 어댑터를 구성할 수 없거나, DirectAccess IPsec 정책은 수동으로 범위 여야 모든 프로필 다음 Windows PowerShell 명령을 사용 하 여:  
  
    ```  
    $gposession = Open-NetGPO -PolicyStore <Name of the server GPO>  
    Set-NetIPsecRule -DisplayName <Name of the IPsec policy> -GPOSession $gposession -Profile Any  
    Save-NetGPO -GPOSession $gposession  
    ```  
  
    이 명령에서 사용 하 여 IPsec 정책의 이름은 **DirectAccess DaServerToInfra** 및 **DirectAccess DaServerToCorp**합니다.  
  
## <a name="BKMK_ConfigRouting"></a>회사 네트워크의 라우팅을 구성 합니다.  
다음과 같이 회사 네트워크의 라우팅을 구성합니다.  
  
-   조직에 기본 IPv6이 배포된 경우 내부 네트워크의 라우터가 원격 액세스 서버를 통해 IPv6 트래픽을 다시 라우팅할 수 있도록 경로를 추가합니다.  
  
-   원격 액세스 서버에서 조직의 IPv4 및 IPv6 경로를 수동으로 구성합니다. 있는 모든 트래픽이 게시 된 경로 추가 프로그램 (/ 48) IPv6 접두사는 내부 네트워크로 전달 합니다. 또한 IPv4 트래픽의 경우 내부 네트워크로 IPv4 트래픽이 전달되도록 명시적인 경로를 추가합니다.  
  
## <a name="BKMK_ConfigFirewalls"></a>방화벽 구성  
선택한 네트워크 설정에 따라, 배포에서 추가 방화벽을 사용 하면 원격 액세스 트래픽에 대해 다음 방화벽 예외를 적용 합니다.  
  
### <a name="remote-access-server-on-ipv4-internet"></a>IPv4 인터넷에서 원격 액세스 서버  
원격 액세스 서버가 IPv4 인터넷에 있으면 원격 액세스 트래픽에 대해 다음 인터넷 연결 방화벽 예외를 적용 됩니다.  
  
-   **Teredo 트래픽**  
  
    사용자 데이터 그램 프로토콜 (UDP) 대상 포트 3544 인바운드, UDP 원본 포트 3544 아웃 바운드입니다. 이 예외로 인해 인터넷 연속 된 공용 IPv4 주소 둘 다에 대 한 원격 액세스 서버에 적용 됩니다.  
  
-   **6to4 트래픽**  
  
    IP 프로토콜 41 인바운드 및 아웃 바운드입니다. 이 예외로 인해 인터넷 연속 된 공용 IPv4 주소 둘 다에 대 한 원격 액세스 서버에 적용 됩니다.  
  
-   **IP-HTTPS traffic**  
  
    전송 제어 프로토콜 (TCP) 대상 포트 443 및 TCP 포트 443 아웃 바운드 원본입니다. 원격 액세스 서버에 단일 네트워크 어댑터가 포함되고 네트워크 위치 서버가 원격 액세서 서버에 있는 경우 TCP 포트 62000도 필요합니다. 이러한 예외는 서버의 외부 이름을 확인 하는 주소에만 적용 됩니다.  
  
    > [!NOTE]  
    > 이 예외로 인해 원격 액세스 서버에서 구성 됩니다. 다른 모든 예외가 경계 면 방화벽에서 구성 됩니다.  
  
### <a name="remote-access-server-on-ipv6-internet"></a>IPv6 인터넷에서 원격 액세스 서버  
원격 액세스 서버가 IPv6 인터넷에 있으면 원격 액세스 트래픽에 대해 다음 인터넷 연결 방화벽 예외를 적용 됩니다.  
  
-   IP 프로토콜 50  
  
-   UDP 대상 포트 500 인바운드, UDP 원본 포트 500 아웃바운드  
  
-   I p v 6 Internet Control Message Protocol (ICMPv6) 트래픽 인바운드 및 아웃 바운드-Teredo 구현의 합니다.  
  
### <a name="remote-access-traffic"></a>원격 액세스 트래픽  
원격 액세스 트래픽에 대해 다음 내부 네트워크 방화벽 예외를 적용 합니다.  
  
-   ISATAP: 프로토콜 41 인바운드 및 아웃 바운드  
  
-   TCP/UDP-모든 IPv4 또는 IPv6 트래픽  
  
-   ICMP-모든 IPv4 또는 IPv6 트래픽  
  
## <a name="BKMK_ConfigCAs"></a>Ca 및 인증서 구성  
컴퓨터 인증용 인증서를 사용 하 여 또는 사용자 이름 및 암호를 사용 하는 기본 Kerberos 인증을 사용 하 여 중 하나를 선택 하면 Windows Server 2012에 대 한 원격 액세스 합니다. 또한 원격 액세스 서버에서 IP-HTTPS 인증서를 구성 해야 합니다. 이 섹션에서는 이러한 인증서를 구성 하는 방법에 설명 합니다.  
  
공개 키 인프라 (PKI) 설정에 대 한 정보를 참조 하십시오. [Active Directory 인증서 서비스](https://technet.microsoft.com/library/cc770357.aspx)합니다.  
  
### <a name="BKMK_ConfigIPsec"></a>IPsec 인증 구성  
IPsec 인증을 사용할 수 있도록 원격 액세스 서버와 모든 DirectAccess 클라이언트에 인증서가 필요 합니다. 내부 인증 기관 (CA)에서 인증서를 발급 해야 합니다. 원격 액세스 서버와 DirectAccess 클라이언트가 루트 및 중간 인증서를 발급 하는 CA를 신뢰 해야 합니다.  
  
##### <a name="to-configure-ipsec-authentication"></a>IPsec 인증을 구성하려면  
  
1.  내부 CA에서 기본 컴퓨터 인증서 템플릿을 사용 하는 경우 또는에 설명 된 대로 새 인증서 템플릿을 만들지 결정 [인증서 템플릿 만들기](https://technet.microsoft.com/library/cc731705.aspx)합니다.  
  
    > [!NOTE]  
    > 새 서식 파일을 만드는 경우에 클라이언트 인증을 위해 구성 되어야 합니다.  
  
2.  필요한 경우 인증서 템플릿을 배포 합니다. 자세한 내용은 참조 [인증서 템플릿 배포](https://technet.microsoft.com/library/cc770794.aspx)합니다.  
  
3.  필요한 경우 자동 등록에 대 한 서식 파일을 구성 합니다.  
  
4.  필요한 경우 인증서 자동 등록을 구성 합니다. 자세한 내용은 참조 [인증서 자동 등록 구성](https://technet.microsoft.com/library/cc731522.aspx)합니다.  
  
### <a name="BKMK_ConfigCertTemp"></a>인증서 템플릿 구성  
인증서를 발급 하려면 내부 CA를 사용 하는 경우 IP-HTTPS 인증서 및 네트워크 위치 서버 웹 사이트 인증서에 대 한 인증서 템플릿을 구성 해야 합니다.  
  
##### <a name="to-configure-a-certificate-template"></a>인증서 템플릿을 구성하려면  
  
1.  내부 CA에서 인증서 템플릿을에 설명 된 대로 만듭니다 [인증서 템플릿 만들기](https://technet.microsoft.com/library/cc731705.aspx)합니다.  
  
2.  에 설명 된 대로 인증서 템플릿을 배포 [인증서 템플릿 배포](https://technet.microsoft.com/library/cc770794.aspx)합니다.  
  
서식 파일을 준비한 후에 인증서를 구성 하려면 사용할 수 있습니다. 자세한 내용은 다음 절차를 참조 합니다.  
  
-   [IP-HTTPS 인증서 구성](#BKMK_IPHTTPS)  
  
-   [네트워크 위치 서버 구성](#BKMK_ConfigNLS)  
  
### <a name="BKMK_IPHTTPS"></a>IP-HTTPS 인증서 구성  
원격 액세스에는 원격 액세스 서버에 대한 IP-HTTPS 연결을 인증할 IP-HTTPS 인증서가 필요합니다. IP-HTTPS 인증서에 대한 인증서 옵션에는 다음 세 가지가 있습니다.  
  
-   **공용**  
  
    타사에서 제공합니다.  
  
-   **개인**  
  
    인증서에서 만든 인증서 템플릿을 기반 [인증서 템플릿 구성](assetId:///6a5ec5c1-d653-47b1-a567-cc485004e7bc#ConfigCertTemp)합니다. 필요한 공개적으로 확인 가능한 FQDN에서 연결할 수 있는 인증서 해지 목록 (CRL) 배포 지점입니다.  
  
-   **자체 서명**  
  
    이 인증서는 공개적으로 확인 가능한 FQDN에서 연결할 수 있는 CRL 배포 지점에 필요 합니다.  
  
    > [!NOTE]  
    > 멀티 사이트 배포에는 자체 서명된 인증서를 사용할 수 없습니다.  
  
IP-HTTPS 인증에 사용되는 웹 사이트 인증서는 다음 요구 사항을 충족해야 합니다.  
  
-   인증서 주체 이름은 원격 액세스 서버 IP-HTTPS 연결에 대해서만 사용 되는 IP-HTTPS URL (ConnectTo 주소)의 외부에서 확인 가능한 정규화 된 도메인 이름 (FQDN) 이어야 합니다.  
  
-   인증서의 일반 이름이 IP-HTTPS 사이트의 이름과 일치해야 합니다.  
  
-   제목 필드에 대 한 원격 액세스 서버 외부 연결 어댑터 또는 IP-HTTPS URL의 FQDN의 IPv4 주소를 지정 합니다.  
  
-   에 대 한는 **향상 된 키 용도** 필드의 경우는 서버 인증 OID (개체 식별자)를 사용 합니다.  
  
-   **CRL 배포 지점** 필드의 경우 인터넷에 연결된 DirectAccess 클라이언트에서 액세스할 수 있는 CRL 배포 지점을 지정합니다.  
  
-   IP-HTTPS 인증서에 프라이빗 키가 있어야 합니다.  
  
-   IP-HTTPS 인증서를 개인 저장소로 직접 가져와야 합니다.  
  
-   IP-HTTPS 인증서 이름에 와일드카드 문자를 사용할 수 있습니다.  
  
##### <a name="to-install-the-ip-https-certificate-from-an-internal-ca"></a>내부 CA의 IP-HTTPS 인증서를 설치하려면  
  
1.  원격 액세스 서버에서 다음을 수행합니다. 에 **시작** 화면에서 입력**mmc.exe**, 한 다음 ENTER를 누릅니다.  
  
2.  MMC 콘솔에서에 **파일** 메뉴 클릭 **스냅인 추가/제거**합니다.  
  
3.  에 **추가 / 제거 스냅인** 대화 상자, 클릭 **인증서**, 클릭 **추가**, 클릭 **컴퓨터 계정**, 클릭 **다음**, 클릭 **로컬 컴퓨터**, 클릭 **마침**, 클릭 하 고 **확인**합니다.  
  
4.  인증서 스냅인의 콘솔 트리에서 **인증서(로컬 컴퓨터)\개인\인증서**를 엽니다.  
  
5.  마우스 오른쪽 단추로 클릭 **인증서**, 가리킨 **모든 작업**, 클릭 **새 인증서 요청**, 를 클릭 하 고 **다음** 두 번...  
  
6.  에 **인증서 요청** 페이지 인증서 템플릿 구성에서 만든 인증서 템플릿에 대 한 확인란을 선택 하 고 필요한 경우 클릭 **이 인증서를 등록 하려면 추가 정보가 필요**합니다.  
  
7.  에 **인증서 속성** 대화 상자의 **주체** 탭에 **주체 이름** 영역에서 **형식**, 선택, **일반 이름**.  
  
8.  **값**, 원격 액세스 서버 외부 연결 어댑터 또는 IP-HTTPS URL의 FQDN의 IPv4 주소를 지정 하 고 클릭 한 다음 **추가**합니다.  
  
9. 에 **대체 이름** 영역에서 **형식**, 선택, **DNS**합니다.  
  
10. **값**, 원격 액세스 서버 외부 연결 어댑터 또는 IP-HTTPS URL의 FQDN의 IPv4 주소를 지정 하 고 클릭 한 다음 **추가**합니다.  
  
11. **일반** 탭의 **이름**에 인증서를 식별하는 데 도움이 되는 이름을 입력할 수 있습니다.  
  
12. 에 **확장** 탭 옆에 **확장 키 용도**, 화살표를 클릭 하 고 서버 인증에 있는지 확인 하십시오는 **선택한 옵션** 목록입니다.  
  
13. 클릭 **확인**, 클릭 **등록**, 를 클릭 하 고 **마침**합니다.  
  
14. 인증서 스냅인의 세부 정보 창에서 새 인증서가 서버 인증의 원래 용도 등록 있는지를 확인 합니다.  
  
## <a name="BKMK_ConfigDNS"></a>DNS 서버를 구성 합니다.  
배포의 내부 네트워크에 대한 네트워크 위치 서버 웹 사이트의 DNS 항목을 수동으로 구성해야 합니다.  
  
### <a name="NLS_DNS"></a>네트워크 위치 서버와 웹 프로브를 추가 하려면  
  
1.  내부 네트워크 DNS 서버에서 다음을 수행합니다. 에 **시작** 화면에서 입력**dnsmgmt.msc**, 한 다음 ENTER를 누릅니다.  
  
2.  **DNS 관리자** 콘솔의 왼쪽 창에서 도메인에 대한 정방향 조회 영역을 확장합니다. 도메인을 마우스 오른쪽 단추로 클릭 하 고 클릭 **새 호스트 (A 또는 AAAA)** 합니다.  
  
3.  에 **새 호스트** 대화 상자는 **이름 (부모 도메인 이름 사용 비어 있는 경우)** 상자에 네트워크 위치 서버 웹 사이트 (이 이름은 DirectAccess 클라이언트는 네트워크 위치 서버에 연결 하는 데 사용)에 대 한 DNS 이름을 입력 합니다. 에 **IP 주소** 상자, 네트워크 위치 서버의 IPv4 주소를 입력 하 고, 클릭 **호스트 추가**, 를 클릭 하 고 **확인**합니다.  
  
4.  에 **새 호스트** 대화 상자는 **이름 (부모 도메인 이름 사용 비어 있는 경우)** 상자 (기본 웹 검색에 대 한 이름의 이름은 directaccess-webprobehost) 웹 검색 DNS 이름을 입력 합니다. **IP 주소** 상자에 웹 검색의 IPv4 주소를 입력하고 **호스트 추가**를 클릭합니다.  
  
5.  directaccess-corpconnectivityhost 및 수동으로 만든 모든 연결 검증 도구에 대해 이 프로세스를 반복합니다. 에 **DNS** 대화 상자를 클릭 하 여 **확인**합니다.  
  
6.  **완료**를 클릭합니다.  
  
![Windows PowerShell](../../../../media/Step-1-Configure-the-Remote-Access-Infrastructure/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
Add-DnsServerResourceRecordA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv4Address <network_location_server_IPv4_address>  
Add-DnsServerResourceRecordAAAA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv6Address <network_location_server_IPv6_address>  
```  
  
다음에 대한 DNS 항목도 구성해야 합니다.  
  
-   **IP-HTTPS 서버**  
  
    DirectAccess 클라이언트는 인터넷에서 원격 액세스 서버의 DNS 이름을 확인할 수 있어야 합니다.  
  
-   **CRL 해지 확인**  
  
    DirectAccess에서는 DirectAccess 클라이언트 및 원격 액세스 서버 간의 IP-HTTPS 연결 및 DirectAccess 클라이언트와 네트워크 위치 서버 간의 HTTPS 기반 연결에 대 한 인증서 해지 확인을 사용 합니다. 두 경우 모두 DirectAccess 클라이언트에서 CRL 배포 지점 위치를 확인하고 액세스할 수 있어야 합니다.  
  
-   **ISATAP**  
  
    사이트 간 터널 주소 지정 프로토콜 ISATAP (자동) 터널을 사용 하 여 DirectAccess 클라이언트가 IPv4 헤더 내에 IPv6 패킷을 캡슐화 IPv4 인터넷을 통해 원격 액세스 서버에 연결할 수 있도록 합니다. ISATAP는 원격 액세스에서 인트라넷을 통해 ISATAP 호스트에 IPv6 연결을 제공하는 데 사용됩니다. 기본이 아닌 IPv6 네트워크 환경에서 원격 액세스 서버에서 자체 구성을 자동으로 ISATAP 라우터로 합니다. ISATAP 이름에 대한 확인 지원이 필요합니다.  
  
## <a name="BKMK_ConfigAD"></a>Active Directory 구성  
원격 액세스 서버와 모든 DirectAccess 클라이언트 컴퓨터는 Active Directory 도메인에 가입되어 있어야 합니다. DirectAccess 클라이언트 컴퓨터에는 다음 도메인 유형 중 하나의 구성원이어야 합니다.  
  
-   원격 액세스 서버와 동일한 포리스트에 속한 도메인  
  
-   원격 액세스 서버 포리스트와 양방향 트러스트 관계에 있는 포리스트에 속한 도메인  
  
-   원격 액세스 서버 도메인과 양방향 트러스트 관계에 있는 도메인  
  
#### <a name="to-join-the-remote-access-server-to-a-domain"></a>원격 액세스 서버를 도메인에 가입 하려면  
  
1.  서버 관리자에서 **로컬 서버**를 클릭합니다. 세부 정보 창에서 **컴퓨터 이름** 옆의 링크를 클릭합니다.  
  
2.  **시스템 속성** 대화 상자에서 **컴퓨터 이름** 탭, **변경**을 차례로 클릭합니다.  
  
3.  에 **컴퓨터 이름을** 상자에 서버를 도메인에 가입 하는 경우에 컴퓨터 이름을 변경 하려는 경우 컴퓨터의 이름을 입력 합니다. 아래에서 **소속**, 클릭 **도메인**, 다음 (예: corp.contoso.com), 서버를 가입을 클릭 한 다음 원하는 도메인의 이름을 입력 하 고 **확인**합니다.  
  
4.  사용자 이름 및 암호를 묻는 메시지가 나타나면 사용자 이름 및 컴퓨터를 도메인에 가입을 클릭 한 다음 사용 권한이 있는 사용자의 암호를 입력 **확인**합니다.  
  
5.  도메인을 시작한다는 내용의 대화 상자가 표시되면 **확인**을 클릭합니다.  
  
6.  컴퓨터를 다시 시작해야 한다는 메시지가 표시되면 **확인**을 클릭합니다.  
  
7.  **시스템 속성** 대화 상자에서 **닫기**를 클릭합니다.  
  
8.  컴퓨터를 다시 시작할지 묻는 메시지가 표시되면 **지금 다시 시작**을 클릭합니다.  
  
#### <a name="to-join-client-computers-to-the-domain"></a>도메인에 클라이언트 컴퓨터를 가입시키려면  
  
1.  에 **시작** 화면에서 입력**explorer.exe**, 한 다음 ENTER를 누릅니다.  
  
2.  컴퓨터 아이콘을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **속성**합니다.  
  
3.  **시스템** 페이지에서 **고급 시스템 설정**을 클릭합니다.  
  
4.  **시스템 속성** 대화 상자의 **컴퓨터 이름** 탭에서 **변경**을 클릭합니다.  
  
5.  에 **컴퓨터 이름을** 상자에 서버를 도메인에 가입 하는 경우에 컴퓨터 이름을 변경 하려는 경우 컴퓨터의 이름을 입력 합니다. 아래에서 **소속**, 클릭 **도메인**, 다음 서버 (예: corp.contoso.com)을 연결을 클릭 한 다음 원하는 도메인의 이름을 입력 하 고 **확인**합니다.  
  
6.  사용자 이름 및 암호를 묻는 메시지가 나타나면 사용자 이름 및 컴퓨터를 도메인에 가입을 클릭 한 다음 사용 권한이 있는 사용자의 암호를 입력 **확인**합니다.  
  
7.  도메인을 시작한다는 내용의 대화 상자가 표시되면 **확인**을 클릭합니다.  
  
8.  컴퓨터를 다시 시작해야 한다는 메시지가 표시되면 **확인**을 클릭합니다.  
  
9. 에 **시스템 속성** 대화 상자에서 닫기를 클릭 합니다.  
  
10. 클릭 **지금 다시 시작** 메시지가 표시 되 면 합니다.  
  
![Windows PowerShell](../../../../media/Step-1-Configure-the-Remote-Access-Infrastructure/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
> [!NOTE]  
> 다음 명령을 입력 한 후에 도메인 자격 증명을 제공 해야 합니다.  
  
```  
Add-Computer -DomainName <domain_name>  
Restart-Computer  
```  
  
## <a name="BKMK_ConfigGPOs"></a>Gpo 구성  
원격 액세스를 배포 하려면 두 개의 그룹 정책 개체의 최소가 필요 합니다. 한 그룹 정책 개체에는 원격 액세스 서버에 대 한 설정이 포함 되어 및 DirectAccess 클라이언트 컴퓨터에 대 한 설정을 포함 합니다. 원격 액세스를 구성 하는 경우 마법사는 자동으로 필요한 그룹 정책 개체를 만듭니다. 그러나 조직에서 명명 규칙을 적용 또는 만들기 또는 그룹 정책 개체를 편집 하는 데 필요한 권한이 없는 경우 원격 액세스를 구성 하기 전에 만들 수 있어야 합니다.  
  
그룹 정책 개체를 만들려면 참조 [만들고 그룹 정책 개체 편집](https://technet.microsoft.com/library/cc754740.aspx)합니다.  
  
관리자는 조직 구성 단위 (OU)에 DirectAccess 그룹 정책 개체를 수동으로 연결할 수 있습니다. 다음 사항을 고려합니다.  
  
1.  DirectAccess를 구성 하기 전에 만든된 Gpo를 각 Ou에 연결 합니다.  
  
2.  DirectAccess를 구성할 때 클라이언트 컴퓨터의 보안 그룹을 지정합니다.  
  
3.  Gpo는 관리자는 Gpo를 도메인에 연결할 권한이 있는 경우에 관계 없이 자동으로 구성 됩니다.  
  
4.  Gpo에 이미 연결 되어 OU를 하는 경우 링크는 제거 되지 있지만 도메인에 연결 되지 않은.  
  
5.  서버 Gpo에 대 한 OU는 서버 컴퓨터 개체-그렇지 않으면 있어야, GPO가 도메인의 루트에 연결 합니다.  
  
6.  OU에는 구성이 완료 된 후 DirectAccess 설치 마법사를 실행 하 여 이전에 연결 되지 않은, 경우 관리자를 필요한 Ou DirectAccess Gpo를 연결할 수 있으며 도메인에 대 한 링크를 제거 합니다.  
  
    자세한 내용은 참조 [그룹 정책 개체 연결](https://technet.microsoft.com/library/cc732979.aspx)합니다.  
  
> [!NOTE]  
> 그룹 정책 개체를 만든 경우 수동으로 불가능 그룹 정책 개체는 사용할 수 없음을 DirectAccess 구성 중입니다. 그룹 정책 개체 관리 컴퓨터에 가장 가까운 도메인 컨트롤러에 복제 되지 않을 수 있습니다. 관리자가 복제를 완료 하거나 복제를 기다릴 수 있습니다.  
  
## <a name="BKMK_ConfigSGs"></a>보안 그룹 구성  
클라이언트 컴퓨터 그룹 정책 개체에에서 포함 된 DirectAccess 설정은 원격 액세스를 구성할 때 지정 하는 보안 그룹의 구성원 인 컴퓨터에만 적용 됩니다.  
  
### <a name="Sec_Group"></a>DirectAccess 클라이언트에 대 한 보안 그룹을 만들려면  
  
1.  에 **시작** 화면에서 입력**dsa.msc**, 한 다음 ENTER를 누릅니다.  
  
2.  에 **Active Directory 사용자 및 컴퓨터** 보안 그룹에 포함 되 면 마우스 오른쪽 단추로 클릭 하는 도메인을 확장 하는 콘솔의 왼쪽된 창에서 **사용자**, 가리킨 **새로**, 클릭 하 고 **그룹**합니다.  
  
3.  에 **새 개체-그룹** 대화 상자의 **그룹 이름**, 보안 그룹의 이름을 입력 합니다.  
  
4.  **그룹 범위** 아래에서 **전역**을 클릭하고 **그룹 종류**에서 **보안**을 클릭한 다음 **확인**을 클릭합니다.  
  
5.  DirectAccess 클라이언트 컴퓨터 보안 그룹을 두 번 클릭 하 고는 **속성** 대화 상자를 클릭는 **멤버** 탭 합니다.  
  
6.  **구성원** 탭에서 **추가**를 클릭합니다.  
  
7.  **사용자, 연락처, 컴퓨터 또는 서비스 계정 선택** 대화 상자에서 DirectAccess에 사용할 클라이언트 컴퓨터를 선택하고 **확인**을 클릭합니다.  
  
![Windows PowerShell](../../../../media/Step-1-Configure-the-Remote-Access-Infrastructure/PowerShellLogoSmall.gif)**Windows PowerShell 해당 명령**  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
New-ADGroup -GroupScope global -Name <DirectAccess_clients_group_name>  
Add-ADGroupMember -Identity DirectAccess_clients_group_name -Members <computer_name>  
```  
  
## <a name="BKMK_ConfigNLS"></a>네트워크 위치 서버 구성  
네트워크 위치 서버 고가용성을 사용 하 여 서버에 있어야 하 고 DirectAccess 클라이언트에서 신뢰 하는 유효한 Secure Sockets Layer (SSL) 인증서가 필요 합니다.  
  
> [!NOTE]  
> 네트워크 위치 서버 웹 사이트를 원격 액세스 서버에 있는 경우 원격 액세스를 구성 하 고 사용자가 제공한 서버 인증서에 바인딩되어 웹 사이트를 자동으로 생성 됩니다.  
  
네트워크 위치 서버 인증서에 대한 인증서 옵션에는 다음 두 가지가 있습니다.  
  
-   **개인**  
  
    > [!NOTE]  
    > 인증서에서 만든 인증서 템플릿을 기반 [인증서 템플릿 구성](assetId:///6a5ec5c1-d653-47b1-a567-cc485004e7bc#ConfigCertTemp)합니다.  
  
-   **자체 서명**  
  
    > [!NOTE]  
    > 멀티 사이트 배포에는 자체 서명된 인증서를 사용할 수 없습니다.  
  
프라이빗 인증서 또는 자체 서명 된 인증서를 사용하는지 여부를 다음 필요 합니다.  
  
-   네트워크 위치 서버에 사용되는 웹 사이트 인증서. 인증서 주체는 네트워크 위치 서버의 URL이어야 합니다.  
  
-   내부 네트워크에 고가용성이 있는 CRL 배포 지점.  
  
#### <a name="to-install-the-network-location-server-certificate-from-an-internal-ca"></a>내부 CA의 네트워크 위치 서버 인증서를 설치하려면  
  
1.  네트워크 위치 서버 웹 사이트를 호스트할 서버에서 다음을 수행합니다. 에 **시작** 화면에서 입력**mmc.exe**, 한 다음 ENTER를 누릅니다.  
  
2.  MMC 콘솔에서에 **파일** 메뉴 클릭 **스냅인 추가/제거**합니다.  
  
3.  에 **추가 / 제거 스냅인** 대화 상자, 클릭 **인증서**, 클릭 **추가**, 클릭 **컴퓨터 계정**, 클릭 **다음**, 클릭 **로컬 컴퓨터**, 클릭 **마침**, 클릭 하 고 **확인**합니다.  
  
4.  인증서 스냅인의 콘솔 트리에서 **인증서(로컬 컴퓨터)\개인\인증서**를 엽니다.  
  
5.  마우스 오른쪽 단추로 클릭 **인증서**, 가리킨 **모든 작업**, 클릭 **새 인증서 요청**, 를 클릭 하 고 **다음** 두 번입니다.  
  
6.  에 **인증서 요청** 페이지 인증서 템플릿 구성에서 만든 인증서 템플릿에 대 한 확인란을 선택 하 고 필요한 경우 클릭 **이 인증서를 등록 하려면 추가 정보가 필요**합니다.  
  
7.  에 **인증서 속성** 대화 상자의 **주체** 탭에 **주체 이름** 영역에서 **형식**, 선택, **일반 이름**.  
  
8.  **값**, 네트워크 위치 서버 웹 사이트의 FQDN을 입력 하 고 클릭 한 다음 **추가**합니다.  
  
9. 에 **대체 이름** 영역에서 **형식**, 선택, **DNS**합니다.  
  
10. **값**, 네트워크 위치 서버 웹 사이트의 FQDN을 입력 하 고 클릭 한 다음 **추가**합니다.  
  
11. **일반** 탭의 **이름**에 인증서를 식별하는 데 도움이 되는 이름을 입력할 수 있습니다.  
  
12. 클릭 **확인**, 클릭 **등록**, 를 클릭 하 고 **마침**합니다.  
  
13. 인증서 스냅인의 세부 정보 창에서 새 인증서가 서버 인증의 원래 용도 등록을 확인 합니다.  
  
#### <a name="to-configure-the-network-location-server"></a>네트워크 위치 서버를 구성하려면  
  
1.  항상 사용 가능한 서버에서 웹 사이트를 설정합니다. 웹 사이트에 콘텐츠는 필요 없지만 웹 사이트를 테스트할 때 클라이언트가 연결되면 메시지를 제공하는 기본 페이지를 정의할 수 있습니다.  
  
    네트워크 위치 서버 웹 사이트 원격 액세스 서버에서 호스팅되는 경우에이 단계가 필요 하지 않습니다.  
  
2.  HTTPS 서버 인증서를 웹 사이트에 바인딩합니다. 인증서의 일반 이름이 네트워크 위치 서버 사이트의 이름과 일치해야 합니다. DirectAccess 클라이언트에서 발급 CA를 신뢰하는지 확인합니다.  
  
    네트워크 위치 서버 웹 사이트 원격 액세스 서버에서 호스팅되는 경우에이 단계가 필요 하지 않습니다.  
  
3.  CRL 사이트 설정 해당 가진 고가용성 내부 네트워크에 있습니다.  
  
    CRL 배포 지점은 다음을 통해 액세스할 수 있습니다.  
  
    -   와 같은 HTTP 기반 URL을 사용 하는 웹 서버: https://crl.corp.contoso.com/crld/corp-APP1-CA.crl  
  
    -   파일 서버와 같은 범용 명명 규칙 (UNC) 경로 통해 액세스 하는 \\\crl.corp.contoso.com\crld\corp-APP1-CA.crl  
  
    내부 CRL 배포 지점에 연결할 수 경우 i p v 6을 통해서만 고급 보안이 연결 보안 규칙으로 Windows 방화벽을 구성 해야 합니다. IPsec 보호 인트라넷의 IPv6 주소 공간에서 IPv6 주소로 CRL 배포 지점의 제외합니다.  
  
4.  DirectAccess 클라이언트가 내부 네트워크의 네트워크 위치 서버의 이름을 확인할 수 있는지 그리고 인터넷의 DirectAccess 클라이언트에서 이름을 확인할 수 있는지 확인 합니다.  
  
## <a name="BKMK_Links"></a>참고 항목  
  
-   [2단계: 원격 액세스 서버를 구성 합니다.](Step-2-Configure-the-Remote-Access-Server.md)

