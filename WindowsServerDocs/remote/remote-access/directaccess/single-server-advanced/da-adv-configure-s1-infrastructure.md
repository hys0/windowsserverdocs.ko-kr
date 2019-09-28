---
title: 1 단계 고급 DirectAccess 인프라 구성
description: 이 항목은 Windows Server 2016에 대 한 고급 설정을 사용 하 여 단일 DirectAccess 서버 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 43abc30a-300d-4752-b845-10a6b9f32244
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 30705a9aa55cdc652280c27c327cf865a47c5a11
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404937"
---
# <a name="step-1-configure-advanced-directaccess-infrastructure"></a>1 단계 고급 DirectAccess 인프라 구성

>적용 대상: Windows Server 2012 R2, Windows Server 2012

이 항목에서는 IPv4 및 IPv6 혼합 환경에서 단일 DirectAccess 서버를 사용하는 고급 원격 액세스 배포에 필요한 인프라를 구성하는 방법에 대해 설명합니다. 에 설명 된 계획 단계를 완료 한 배포 단계를 시작 하기 전에 확인 [고급 DirectAccess 배포 계획](../../../remote-access/directaccess/single-server-advanced/Plan-an-Advanced-DirectAccess-Deployment.md)합니다.  
  
|태스크|설명|  
|----|--------|  
|1.1 서버 네트워크 설정 구성|DirectAccess 서버에서 서버 네트워크 설정을 구성합니다.|  
|1.2 강제 터널링 구성|강제 터널링을 구성합니다.|  
|1.3 회사 네트워크의 라우팅 구성|회사 네트워크의 라우팅을 구성합니다.|  
|1.4 방화벽 구성|필요한 경우 추가 방화벽을 구성합니다.|  
|1.5 CA 및 인증서 구성|CA(인증 기관)를 구성하고, 필요한 경우 배포에 필요한 기타 인증서 템플릿을 구성합니다.|  
|1.6 DNS 서버 구성|DirectAccess 서버에 대한 DNS(Domain Name System) 설정을 구성합니다.|  
|1.7 Active Directory 구성|클라이언트 컴퓨터 및 DirectAccess 서버를 Active Directory 도메인에 가입시킵니다.|  
|1.8 GPO 구성|필요한 경우 배포에 사용되는 GPO를 구성합니다.|  
|1.9 보안 그룹 구성|DirectAccess 클라이언트 컴퓨터를 포함할 보안 그룹 및 배포에 필요한 기타 보안 그룹을 구성합니다.|  
|1.10 네트워크 위치 서버 구성|네트워크 위치 서버 웹 사이트 인증서 설치를 포함하여 네트워크 위치 서버를 구성합니다.|  
  
> [!NOTE]  
> 이 항목에는 설명한 절차의 일부를 자동화하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 참조 [Cmdlet를 사용 하 여](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
## <a name="ConfigNetworkSettings"></a>1.1 서버 네트워크 설정 구성  
IPv4 및 IPv6을 사용하는 환경에 단일 서버를 배포하려면 다음 네트워크 인터페이스 설정이 필요합니다. 모든 IP 주소를 사용 하 여 구성 된 **어댑터 설정 변경** 에 **Windows 네트워크 및 공유 센터**합니다.  
  
**Edge 토폴로지**  
  
-   연속된 두 개의 인터넷 연결 공용 고정 IPv4 또는 IPv6 주소  
  
    > [!NOTE]  
    > Teredo에는 두 개의 공용 주소가 필요합니다. Teredo를 사용하지 않는 경우에는 단일 공용 고정 IPv4 주소를 구성할 수 있습니다.  
  
-   단일 내부 고정 IPv4 또는 IPv6 주소  
  
**NAT 장치 뒤 (네트워크 어댑터 2 개 포함)**  
  
-   단일 인터넷 연결 고정 IPv4 또는 IPv6 주소  
  
-   단일 내부 네트워크 연결 고정 IPv4 또는 IPv6 주소  
  
**NAT 장치 뒤 (네트워크 어댑터 1 개 포함)**  
  
-   단일 내부 네트워크 연결 고정 IPv4 또는 IPv6 주소  
  
> [!NOTE]  
> 둘 이상의 네트워크 어댑터(하나는 도메인 프로필에서 분류되고 나머지는 공용 또는 프라이빗 프로필에서 분류됨)를 사용하는 DirectAccess 서버가 단일 네트워크 어댑터 토폴로지로 구성된 경우 다음을 수행하는 것이 좋습니다.  
>   
> -   두 번째 네트워크 어댑터와 모든 추가 네트워크 어댑터를 도메인 프로필에서 분류합니다.  
> -   도메인 프로필에 대 한 두 번째 네트워크 어댑터를 구성할 수 없거나, DirectAccess IPsec 정책은 수동으로 범위 여야 모든 프로필 DirectAccess를 구성한 후 다음 Windows PowerShell 명령을 사용 하 여:  
>   
>     ```  
>     $gposession = Open-NetGPO "PolicyStore <Name of the server GPO>  
>     Set-NetIPsecRule "DisplayName <Name of the IPsec policy> "GPOSession $gposession "Profile Any  
>     Save-NetGPO "GPOSession $gposession  
>     ```  
  
## <a name="BKMK_forcetunnel"></a>1.2 강제 터널링 구성  
원격 액세스 설치 마법사를 통해 강제 터널링을 구성할 수 있습니다. 강제 터널링은 원격 클라이언트 구성 마법사에 확인란으로 표시됩니다. 이 설정은 DirectAccess 클라이언트에만 영향을 줍니다. VPN을 사용하는 경우 VPN 클라이언트는 기본적으로 강제 터널링을 사용합니다. 관리자는 클라이언트 프로필에서 VPN 클라이언트에 대한 설정을 변경할 수 있습니다.  
  
강제 터널링에 대한 확인란을 선택하면 다음 작업이 수행됩니다.  
  
-   DirectAccess 클라이언트에서 강제 터널링이 사용하도록 설정됩니다.  
  
-   추가 **모든** 항목에는 이름 확인 정책 NRPT (테이블) DirectAccess 클라이언트에 대 한 해당 모든 DNS 트래픽이 내부 네트워크 DNS 서버에 이동 의미  
  
-   항상 IP-HTTPS 전환 기술을 사용하도록 DirectAccess 클라이언트가 구성됩니다.  
  
강제 터널링을 사용하는 DirectAccess 클라이언트에서 인터넷 리소스를 사용하도록 설정하려면 할 수 있도록, 인터넷 리소스에 대한 IPv6 기반 요청을 받아서 IPv4 기반 인터넷 리소스에 대한 요청으로 변환할 수 있는 프록시 서버를 사용하면 됩니다. 인터넷 리소스에 대한 프록시 서버를 구성하려면 NRPT에서 기본 항목을 수정하여 프록시 서버를 추가해야 합니다. 원격 액세스 PowerShell cmdlet 또는 DNS PowerShell cmdlet을 사용하여 이를 수행할 수 있습니다. 예를 들어 다음과 같이 원격 액세스 PowerShell cmdlet을 사용합니다.  
  
```  
Set-DAClientDNSConfiguration "DNSSuffix "." "ProxyServer <Name of the proxy server:port>  
```  
  
> [!NOTE]  
> 같은 서버에서 DirectAccess와 VPN을 둘 다 사용하는 경우 VPN이 강제 터널 모드에 있고 서버가 에지 토폴로지 또는 NAT 장치 뒤 토폴로지(네트워크 어댑터 두 개가 각각 도메인과 프라이빗 네트워크에 하나씩 연결)에 배포되면 DirectAccess 서버의 외부 인터페이스를 통해 VPN 인터넷 트래픽을 전달할 수 없습니다. 이 시나리오를 지원하려면 조직에서 단일 네트워크 어댑터 토폴로지의 방화벽 뒤에 있는 서버에 원격 액세스를 배포해야 합니다. 또는 내부 네트워크에서 별도의 프록시 서버를 사용하여 VPN 클라이언트의 인터넷 트래픽을 전달할 수 있습니다.  
  
> [!NOTE]  
> 조직에서 DirectAccess 클라이언트가 인터넷 리소스에 액세스할 수 있도록 웹 프록시를 사용하는 경우 회사 프록시에서 내부 네트워크 리소스를 처리할 수 없으면 인트라넷 외부에 있는 DirectAccess 클라이언트에서 내부 리소스에 액세스할 수 없습니다. 이러한 시나리오에서 DirectAccess 클라이언트가 내부 리소스에 액세스할 수 있도록 하려면 인프라 마법사의 DNS 페이지를 사용 하 여 내부 네트워크 접미사에 대 한 NRPT 항목을 수동으로 만듭니다. 이러한 NRPT 접미사에 프록시 설정을 적용해서는 안 됩니다. 접미사가 기본 DNS 서버 항목으로 채워져야 합니다.  
  
## <a name="ConfigRouting"></a>1.3 회사 네트워크에서 라우팅 구성  
다음과 같이 회사 네트워크의 라우팅을 구성합니다.  
  
-   조직에 기본 IPv6이 배포된 경우 내부 네트워크의 라우터가 DirectAccess 서버를 통해 IPv6 트래픽을 다시 라우팅할 수 있도록 경로를 추가합니다.  
  
-   수동으로 조직 "s IPv4 및 IPv6 경로 구성 DirectAccess 서버에 있습니다. 조직(/48) IPv6 접두사가 있는 모든 트래픽이 내부 네트워크로 전달되도록 게시된 경로를 추가합니다. IPv4 트래픽의 경우 내부 네트워크로 IPv4 트래픽이 전달되도록 명시적인 경로를 추가합니다.  
  
## <a name="ConfigFirewalls"></a>1.4 방화벽 구성  
배포에서 추가 방화벽을 사용하는 경우 DirectAccess 서버가 IPv4 인터넷에 있으면 원격 액세스 트래픽에 대해 다음 인터넷 연결 방화벽 예외를 적용합니다.  
  
-   Teredo 트래픽 "사용자 데이터 그램 프로토콜 (UDP) 대상 포트 3544 인바운드, UDP 원본 포트 3544 아웃 바운드입니다.  
  
-   6to4 트래픽 "IP 프로토콜 41 인바운드 및 아웃 바운드입니다.  
  
-   IP-HTTPS "전송 제어 프로토콜 (TCP) 대상 포트 443 및 TCP 원본 포트 443 아웃 바운드입니다. DirectAccess 서버에 단일 네트워크 어댑터가 포함되고 네트워크 위치 서버가 DirectAccess 서버에 있는 경우 TCP 포트 62000도 필요합니다.  
  
    > [!NOTE]  
    > 다른 모든 예외가 경계면 방화벽에서 구성되어야 하는 반면 이 예외는 DirectAccess 서버에서 구성되어야 합니다.  
  
> [!NOTE]  
> Teredo 및 6to4 트래픽의 경우 이 예외는 DirectAccess 서버의 연속된 인터넷 연결 공용 IPv4 주소 둘 다에 대해 적용되어야 합니다. IP-HTTPS의 경우 서버의 공용 이름이 확인되는 주소에만 예외를 적용해야 합니다.  
  
추가 방화벽을 사용하는 경우 DirectAccess 서버가 IPv6 인터넷에 있으면 원격 액세스 트래픽에 대해 다음 인터넷 연결 방화벽 예외를 적용합니다.  
  
-   IP 프로토콜 50  
  
-   UDP 대상 포트 500 인바운드, UDP 원본 포트 500 아웃바운드  
  
-   I p v 6 Internet Control Message Protocol (ICMPv6) 트래픽 인바운드 및 아웃 바운드 "Teredo 구현에만 해당 합니다.  
  
추가 방화벽을 사용하는 경우 원격 액세스 트래픽에 대해 다음 내부 네트워크 방화벽 예외를 적용합니다.  
  
-   ISATAP "프로토콜 41 인바운드 및 아웃 바운드  
  
-   TCP/UDP - 모든 IPv4/IPv6 트래픽  
  
-   ICMP - 모든 IPv4/IPv6 트래픽  
  
## <a name="ConfigCAs"></a>1.5 Ca 및 인증서 구성  
Windows Server 2012의 원격 액세스를 사용 하면 컴퓨터 인증용 인증서를 사용 또는 사용 하 여 기본 제공 Kerberos 프록시 사용자 이름 및 암호를 사용 하 여 인증 하는 중에 선택할 수 있습니다. 또한 DirectAccess 서버에서 IP-HTTPS 인증서를 구성해야 합니다.  
  
자세한 내용은 참조 [Active Directory 인증서 서비스](https://technet.microsoft.com/library/cc770357.aspx)합니다.  
  
### <a name="151-configure-ipsec-authentication"></a>1.5.1 IPsec 인증 구성  
DirectAccess 서버와 IPsec 인증을 사용하는 모든 DirectAccess 클라이언트에 컴퓨터 인증서가 필요합니다. 내부 CA(인증 기관)에서 인증서를 발급해야 하며, DirectAccess 클라이언트에서 루트 및 중간 인증서를 발급하는 CA 체인을 신뢰해야 합니다.  
  
##### <a name="to-configure-ipsec-authentication"></a>IPsec 인증을 구성하려면  
  
1.  내부 CA에서 사용할 경우 결정은 **컴퓨터** 인증서 템플릿을 설명으로 새 인증서 템플릿을 만들면 또는 [인증서 템플릿 만들기](https://technet.microsoft.com/library/cc731705.aspx)합니다.  
  
    > [!NOTE]  
    > 새 템플릿을 만드는 경우 클라이언트 인증용으로 구성해야 합니다.  
  
2.  필요한 경우 인증서 템플릿을 배포합니다. 자세한 내용은 참조 [인증서 템플릿 배포](https://technet.microsoft.com/library/cc770794.aspx)합니다.  
  
3.  필요한 경우 자동 등록되도록 인증서 템플릿을 구성합니다. 자세한 내용은 참조 [인증서 자동 등록 구성](https://technet.microsoft.com/library/cc731522.aspx)합니다.  
  
### <a name="ConfigCertTemp"></a>1.5.2 인증서 템플릿 구성  
내부 CA를 사용하여 인증서를 발급하는 경우 IP-HTTPS 인증서 및 네트워크 위치 서버 웹 사이트 인증서용 인증서 템플릿을 구성해야 합니다.  
  
##### <a name="to-configure-a-certificate-template"></a>인증서 템플릿을 구성하려면  
  
1.  내부 CA에서 인증서 템플릿을에 설명 된 대로 만듭니다 [인증서 템플릿 만들기](https://technet.microsoft.com/library/cc731705.aspx)합니다.  
  
2.  에 설명 된 대로 인증서 템플릿을 배포 [인증서 템플릿 배포](https://technet.microsoft.com/library/cc770794.aspx)합니다.  
  
### <a name="153-configure-the-ip-https-certificate"></a>1.5.3 IP-HTTPS 인증서 구성  
원격 액세스에는 DirectAccess 서버에 대한 IP-HTTPS 연결을 인증할 IP-HTTPS 인증서가 필요합니다. IP-HTTPS 인증에 사용할 수 있는 인증서 옵션에는 다음 세 가지가 있습니다.  
  
**공용 인증서**  
  
공용 인증서는 타사에서 제공됩니다. 인증서 주체 이름에 와일드카드 문자가 포함되지 않은 경우 인증서 주체 이름은 DirectAccess 서버 IP-HTTPS 연결에만 사용되는 외부에서 확인 가능한 FQDN(정규화된 도메인 이름) URL이어야 합니다.  
  
**개인 인증서**  
  
프라이빗 인증서를 사용하는 경우 다음 사항이 필요합니다(이미 존재하지 않는 경우).  
  
-   IP-HTTPS 인증에 사용되는 웹 사이트 인증서. 인증서 주체는 인터넷에서 연결할 수 있으며 외부에서 확인 가능한 FQDN이어야 합니다. 1\.5.2의 지침에 따라 만든 인증서 템플릿을 기반으로 하는 인증서는 인증서 템플릿을 구성 합니다.  
  
-   공개적으로 확인 가능한 FQDN에서 연결할 수 있는 CRL(인증서 해지 목록) 배포 지점  
  
**자체 서명 된 인증서**  
  
자체 서명된 인증서를 사용하는 경우 다음 사항이 필요합니다(이미 존재하지 않는 경우).  
  
-   IP-HTTPS 인증에 사용되는 웹 사이트 인증서. 인증서 주체는 인터넷에서 연결할 수 있으며 외부에서 확인 가능한 FQDN이어야 합니다.  
  
-   공개적으로 확인 가능한 FQDN에서 연결할 수 있는 CRL 배포 지점  
  
> [!NOTE]  
> 멀티 사이트 배포에는 자체 서명된 인증서를 사용할 수 없습니다.  
  
IP-HTTPS 인증에 사용되는 웹 사이트 인증서는 다음 요구 사항을 충족해야 합니다.  
  
-   인증서의 일반 이름이 IP-HTTPS 사이트의 이름과 일치해야 합니다.  
  
-   에 **주체** 필드 IP-HTTPS URL의 FQDN을 지정 합니다.  
  
-   에 대 한는 **향상 된 키 용도** 필드의 경우는 서버 인증 OID (개체 식별자)를 사용 합니다.  
  
-   **CRL 배포 지점** 필드의 경우 인터넷에 연결된 DirectAccess 클라이언트에서 액세스할 수 있는 CRL 배포 지점을 지정합니다.  
  
-   IP-HTTPS 인증서에 프라이빗 키가 있어야 합니다.  
  
-   IP-HTTPS 인증서를 개인 저장소로 직접 가져와야 합니다.  
  
-   IP-HTTPS 인증서 이름에 와일드카드 문자를 사용할 수 있습니다.  
  
##### <a name="to-install-the-ip-https-certificate-from-an-internal-ca"></a>내부 CA의 IP-HTTPS 인증서를 설치하려면  
  
1.  DirectAccess 서버에서 다음을 수행합니다. **시작** 화면에서**mmc.exe**를 입력 한 다음 enter 키를 누릅니다.  
  
2.  MMC 콘솔에서에 **파일** 메뉴 클릭 **스냅인 추가/제거**합니다.  
  
3.  에 **추가 / 제거 스냅인** 대화 상자, 클릭 **인증서**, 클릭 **추가**, 클릭 **컴퓨터 계정**, 클릭 **다음**, 클릭 **로컬 컴퓨터**, 클릭 **마침**, 클릭 하 고 **확인**합니다.  
  
4.  인증서 스냅인의 콘솔 트리에서 **인증서(로컬 컴퓨터)\개인\인증서**를 엽니다.  
  
5.  **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 가리킨 다음 **새 인증서 요청**을 클릭합니다.  
  
6.  **다음** 을 두 번 클릭합니다.  
  
7.  에 **인증서 요청** 페이지 (자세한 내용은 참조 1.5.2 인증서 템플릿 구성)에 대 한 이전에 만든 인증서 템플릿에 대 한 확인란을 선택 합니다. 필요한 경우 **이 인증서를 등록하려면 추가 정보가 필요합니다. 설정을 구성하려면 여기를 클릭하십시오.** 를 클릭합니다.  
  
8.  에 **인증서 속성** 대화 상자의 **주체** 탭에 **주체 이름** 영역에서 **형식**, 선택, **일반 이름**.  
  
9. **값**에서 DirectAccess 서버 외부 연결 어댑터의 IPv4 주소 또는 IP-HTTPS URL의 FQDN을 지정하고 **추가**를 클릭합니다.  
  
10. 에 **대체 이름** 영역에서 **형식**, 선택, **DNS**합니다.  
  
11. **값**에서 DirectAccess 서버 외부 연결 어댑터의 IPv4 주소 또는 IP-HTTPS URL의 FQDN을 지정하고 **추가**를 클릭합니다.  
  
12. **일반** 탭의 **이름**에 인증서를 식별하는 데 도움이 되는 이름을 입력할 수 있습니다.  
  
13. **확장** 탭에서 **확장된 키 사용** 옆에 있는 화살표를 클릭하고 **서버 인증**이 **선택한 옵션** 목록에 표시되는지 확인합니다.  
  
14. 클릭 **확인**, 클릭 **등록**, 를 클릭 하 고 **마침**합니다.  
  
15. 인증서 스냅인의 세부 정보 창에서 새 인증서가 서버 인증 용도로 등록되었는지 확인합니다.  
  
## <a name="ConfigDNS"></a>1.6 DNS 서버 구성  
배포의 내부 네트워크에 대한 네트워크 위치 서버 웹 사이트의 DNS 항목을 수동으로 구성해야 합니다.  
  
### <a name="NLS_DNS"></a>네트워크 위치 서버를 만들려면  
  
1.  내부 네트워크 DNS 서버에서 다음을 수행합니다. 에 **시작** 화면에서 입력**dnsmgmt.msc**, 한 다음 ENTER를 누릅니다.  
  
2.  **DNS 관리자** 콘솔의 왼쪽 창에서 도메인에 대한 정방향 조회 영역을 확장합니다. 도메인을 마우스 오른쪽 단추로 클릭하고 **새 호스트(A 또는 AAAA)** 를 클릭합니다.  
  
3.  **새 호스트** 대화 상자의 **IP 주소** 상자에서 다음을 수행합니다.  
  
    -   **이름(입력하지 않으면 부모 도메인 이름 사용)** 상자에 네트워크 위치 서버 웹 사이트의 DNS 이름(DirectAccess 클라이언트에서 네트워크 위치 서버에 연결하는 데 사용하는 이름)을 입력합니다.  
  
    -   네트워크 위치 서버의 IPv4 또는 IPv6 주소를 입력하고 **호스트 추가**를 클릭한 다음 **확인**을 클릭합니다.  
  
4.  **새 호스트** 대화 상자에서 다음을 수행합니다.  
  
    -   에 **이름 (부모 도메인 이름 사용 비어 있는 경우)** 상자 웹 검색 DNS 이름을 입력 합니다 (기본 웹 검색의 이름은 **directaccess webprobehost**).  
  
    -   **IP 주소** 상자에 웹 검색의 IPv4 또는 IPv6 주소를 입력하고 **호스트 추가**를 클릭합니다.  
  
    -   이 프로세스를 반복 **directaccess corpconnectivityhost** 및 모든 수동으로 만든된 연결 검증 도구입니다.  
  
5.  에 **DNS** 대화 상자에서 클릭 **확인**, 를 클릭 하 고 **수행**합니다.  
  
![Windows PowerShell](../../../media/Step-1-Configuring-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)***<em>windows powershell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
Add-DnsServerResourceRecordA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv4Address <network_location_server_IPv4_address>  
Add-DnsServerResourceRecordAAAA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv6Address <network_location_server_IPv6_address>  
```  
  
다음에 대한 DNS 항목도 구성해야 합니다.  
  
-   **IP-HTTPS 서버**  
  
    DirectAccess 클라이언트는 인터넷에서 DirectAccess 서버의 DNS 이름을 확인할 수 있어야 합니다.  
  
-   **CRL 해지 확인**  
  
    DirectAccess는 DirectAccess 클라이언트와 DirectAccess 서버 간의 IP-HTTPS 연결 및 DirectAccess 클라이언트와 네트워크 위치 서버 간의 HTTPS 기반 연결에 인증서 해지 확인을 사용합니다. 두 경우 모두 DirectAccess 클라이언트에서 CRL 배포 지점 위치를 확인하고 액세스할 수 있어야 합니다.  
  
-   **ISATAP**  
  
    ISATAP(Intrasite Automatic Tunnel Addressing Protocol)에서는 터널링을 사용하여 IPv4 헤더 내에 IPv6 패킷을 캡슐화함으로써 DirectAccess 클라이언트에서 IPv4 인터넷을 통해 DirectAccess 서버에 연결하도록 지원합니다. ISATAP는 원격 액세스에서 인트라넷을 통해 ISATAP 호스트에 IPv6 연결을 제공하는 데 사용됩니다. 기본이 아닌 IPv6 네트워크 환경에서는 DirectAccess 서버가 자동으로 ISATAP 라우터로 구성됩니다. ISATAP 이름에 대한 확인 지원이 필요합니다.  
  
## <a name="ConfigAD"></a>1.7 Active Directory 구성  
DirectAccess 서버와 모든 DirectAccess 클라이언트 컴퓨터는 Active Directory 도메인에 가입되어 있어야 합니다. DirectAccess 클라이언트 컴퓨터에는 다음 도메인 유형 중 하나의 구성원이어야 합니다.  
  
-   DirectAccess 서버와 동일한 포리스트에 속한 도메인  
  
-   DirectAccess 서버 포리스트와 양방향 트러스트 관계에 있는 포리스트에 속한 도메인  
  
-   DirectAccess 서버 도메인과 양방향 트러스트 관계에 있는 도메인  
  
#### <a name="to-join-the-directaccess-server-to-a-domain"></a>도메인에 DirectAccess 서버를 가입시키려면  
  
1.  서버 관리자에서 **로컬 서버**를 클릭합니다. 세부 정보 창에서 **컴퓨터 이름** 옆의 링크를 클릭합니다.  
  
2.  **시스템 속성** 대화 상자에서 **컴퓨터 이름** 탭, **변경**을 차례로 클릭합니다.  
  
3.  **컴퓨터 이름**에 컴퓨터 이름을 입력합니다(서버를 도메인에 가입시킬 때 컴퓨터 이름을 변경하려는 경우). 아래에서 **소속**, 클릭 **도메인**, 다음 서버 (예: corp.contoso.com)을 연결을 클릭 한 다음 원하는 도메인의 이름을 입력 하 고 **확인**합니다.  
  
4.  사용자 이름 및 암호를 묻는 메시지가 나타나면 컴퓨터를 도메인에 가입시킬 권한이 있는 사용자의 사용자 이름 및 암호를 입력한 다음 **확인**을 클릭합니다.  
  
5.  도메인 시작 한다는 내용의 대화 상자가 나타나면 클릭 **확인**합니다.  
  
6.  컴퓨터를 다시 시작해야 한다는 메시지가 표시되면 **확인**을 클릭합니다.  
  
7.  **시스템 속성** 대화 상자에서 **닫기**를 클릭합니다.  
  
8.  컴퓨터를 다시 시작할지 묻는 메시지가 표시되면 **지금 다시 시작**을 클릭합니다.  
  
#### <a name="to-join-client-computers-to-the-domain"></a>도메인에 클라이언트 컴퓨터를 가입시키려면  
  
1.  에 **시작** 화면에서 입력**explorer.exe**, 한 다음 ENTER를 누릅니다.  
  
2.  컴퓨터 아이콘을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **속성**합니다.  
  
3.  **시스템** 페이지에서 **고급 시스템 설정**을 클릭합니다.  
  
4.  **시스템 속성** 대화 상자의 **컴퓨터 이름** 탭에서 **변경**을 클릭합니다.  
  
5.  **컴퓨터 이름**, 서버를 도메인에 가입 하는 경우에 컴퓨터 이름을 변경 하려는 경우 컴퓨터의 이름을 입력 합니다. 아래에서 **소속**, 클릭 **도메인**, 다음 서버 (예: corp.contoso.com)을 연결을 클릭 한 다음 원하는 도메인의 이름을 입력 하 고 **확인**합니다.  
  
6.  사용자 이름 및 암호를 묻는 메시지가 나타나면 컴퓨터를 도메인에 가입시킬 권한이 있는 사용자의 사용자 이름 및 암호를 입력한 다음 **확인**을 클릭합니다.  
  
7.  도메인 시작 한다는 내용의 대화 상자가 나타나면 클릭 **확인**합니다.  
  
8.  컴퓨터를 다시 시작해야 한다는 메시지가 표시되면 **확인**을 클릭합니다.  
  
9. **시스템 속성** 대화 상자에서 **닫기**를 클릭합니다.  
  
10. 컴퓨터를 다시 시작할지 묻는 메시지가 표시되면 **지금 다시 시작**을 클릭합니다.  
  
![Windows PowerShell](../../../media/Step-1-Configuring-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)***<em>windows powershell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
> [!NOTE]  
> 다음 **Add-Computer** 명령을 입력할 때는 도메인 자격 증명을 제공해야 합니다.  
  
```  
Add-Computer -DomainName <domain_name>  
Restart-Computer  
```  
  
## <a name="ConfigGPOs"></a>1.8 Gpo 구성  
두 개의 그룹 정책 개체의 최소 함께 원격 액세스 배포 해야 합니다.  
  
-   DirectAccess 서버에 대한 설정을 포함하는 GPO  
  
-   DirectAccess 클라이언트 컴퓨터에 대한 설정을 포함하는 GPO  
  
원격 액세스를 구성 하는 경우 마법사는 자동으로 필요한 그룹 정책 개체를 만듭니다. 그러나 조직에서 명명 규칙을 적용하는 경우 원격 액세스 관리 콘솔의 GPO 대화 상자에 이름을 입력할 수 있습니다. 자세한 내용은 2.7을 참조 하십시오. 구성 요약 및 대체 Gpo 사용 권한을 만든 경우 GPO가 만들어집니다. GPO를 만드는 데 필요한 권한이 없는 경우 원격 액세스를 구성하기 전에 만들어야 합니다.  
  
그룹 정책 개체를 만들려면 참조 [만들고 그룹 정책 개체 편집](https://technet.microsoft.com/library/cc754740.aspx)합니다.  
  
> [!IMPORTANT]  
> 관리자가 수동으로 연결할 수 있습니다 DirectAccess 그룹 정책 개체는 조직 구성 단위 (OU)에 다음 단계:  
>   
> 1.  DirectAccess를 구성하기 전에, 만든 GPO를 각 OU에 연결합니다.  
> 2.  DirectAccess를 구성할 때 클라이언트 컴퓨터의 보안 그룹을 지정합니다.  
> 3.  원격 액세스 관리자 수도 도메인 그룹 정책 개체에 연결 하는 권한이 없을 수도 있습니다. 두 경우 모두의 그룹 정책 개체를 자동으로 구성 됩니다. GPO가 OU에 이미 연결되어 있는 경우에는 연결이 제거되지 않으며 GPO가 도메인에 연결되지 않습니다. 서버 GPO의 경우 OU에 서버 컴퓨터 개체가 있어야 하며, 그렇지 않으면 GPO가 도메인의 루트에 연결됩니다.  
> 4.  연결 하지 않은 OU에는 구성이 완료 된 후 DirectAccess 마법사를 실행 하기 전에, 도메인 관리자를 필요한 Ou DirectAccess 그룹 정책 개체를 연결할 수 있습니다. 이 도메인 연결은 제거할 수 있습니다. 자세한 내용은 참조 [그룹 정책 개체 연결](https://technet.microsoft.com/library/cc732979.aspx)합니다.  
  
> [!NOTE]  
> 그룹 정책 개체를 만든 경우 수동으로 불가능 그룹 정책 개체는 사용할 수 없음을 DirectAccess 구성 중입니다. 그룹 정책 개체 관리 컴퓨터에 가장 가까운 도메인 컨트롤러에 복제 되지 않을 수 있습니다. 이 경우 관리자는 복제가 완료될 때까지 기다리거나 복제를 강제로 실행할 수 있습니다.  
  
### <a name="181-configure-remote-access-gpos-with-limited-permissions"></a>1.8.1 제한된 권한으로 원격 액세스 GPO 구성  
준비 및 프로덕션 GPO를 사용하는 배포에서 도메인 관리자는 다음을 수행해야 합니다.  
  
1.  원격 액세스 관리자로부터 원격 액세스 배포에 필요한 GPO 목록을 가져옵니다. 자세한 내용은 1.8 그룹 정책 개체 계획을 참조 하십시오.  
  
2.  원격 액세스 관리자가 요청한 각 GPO에 대해 이름이 다른 GPO 쌍을 만듭니다. 첫 번째 GPO는 준비 GPO로 사용되고 두 번째 GPO는 프로덕션 GPO로 사용됩니다.  
  
    그룹 정책 개체를 만들려면 참조 [만들고 그룹 정책 개체 편집](https://technet.microsoft.com/library/cc754740.aspx)합니다.  
  
3.  프로덕션 Gpo을 연결 하려면 참조 [그룹 정책 개체 연결](https://technet.microsoft.com/library/cc732979)합니다.  
  
4.  원격 액세스 관리자에게 모든 준비 GPO에 대한 **보안 설정 편집, 삭제, 수정** 권한을 부여합니다. 자세한 내용은 참조 하십시오. [그룹 또는 사용자 그룹 정책 개체에 대 한 권한 위임](https://technet.microsoft.com/library/cc754542)합니다.  
  
5.  모든 도메인에서 Gpo를 연결 하려면 원격 액세스 관리자 사용 권한을 거부 (또는 확인 하는 원격 액세스 관리자 대상이 "t 이러한 권한이). 자세한 내용은 참조 [에 그룹 정책 개체 연결 권한 위임](https://technet.microsoft.com/library/cc755086)합니다.  
  
원격 액세스 관리자는 원격 액세스를 구성할 때 프로덕션 GPO는 지정하지 말고 항상 준비 GPO만 지정해야 합니다. 이는 원격 액세스의 초기 구성뿐만 아니라 추가 GPO가 필요한 추가 구성 작업을 수행할 때(예: 멀티 사이트 배포에서 진입점을 추가하거나 추가 도메인의 클라이언트 컴퓨터를 지원하는 경우)도 마찬가지입니다.  
  
원격 액세스 관리자가 원격 액세스 구성 변경을 완료한 경우 도메인 관리자는 준비 GPO의 설정을 검토하고 다음 절차에 따라 프로덕션 GPO에 설정을 복사해야 합니다.  
  
> [!TIP]  
> 원격 액세스 구성이 변경될 때마다 다음 절차를 수행합니다.  
  
##### <a name="to-copy-settings-to-the-production-gpos"></a>프로덕션 GPO에 설정을 복사하려면  
  
1.  원격 액세스 배포의 모든 준비 GPO가 도메인의 모든 도메인 컨트롤러에 복제되었는지 확인합니다. 이는 가장 최신 구성을 프로덕션 GPO로 가져왔는지 확인하기 위해 필요합니다. 자세한 내용은 그룹 정책 인프라 상태 확인을 참조 하십시오.  
  
2.  원격 액세스 배포에서 모든 준비 GPO를 백업하여 설정을 내보냅니다. 자세한 내용은 다시를 그룹 정책 개체를 참조 하십시오.  
  
3.  각 프로덕션 GPO에 대해 해당 준비 GPO의 보안 필터와 일치하도록 보안 필터를 변경합니다. 자세한 내용은 필터를 사용 하 여 보안 그룹을 참조 하십시오.  
  
    > [!NOTE]  
    > 이는 **설정 가져오기**에서 원본 GPO의 보안 필터를 복사하기 때문에 필요합니다.  
  
4.  각 프로덕션 GPO에 대해 다음과 같이 해당 준비 GPO의 백업에서 설정을 가져옵니다.  
  
    1.  GPMC 그룹 정책 관리 콘솔 (), 포리스트 및 프로덕션 그룹 정책 개체에는 설정을 가져올 수 있는 도메인 그룹 정책 개체 노드를 확장 합니다.  
  
    2.  GPO를 마우스 오른쪽 단추로 클릭 하 고 클릭 **설정 가져오기**합니다.  
  
    3.  에 **설정 가져오기 마법사**, 에 **시작** 페이지에서 클릭 **다음**합니다.  
  
    4.  **GPO 백업** 페이지에서 **백업**을 클릭합니다.  
  
    5.  **그룹 정책 개체 백업** 대화 상자의 **위치** 상자에 GPO 백업을 저장할 위치의 경로를 입력하고 **찾아보기**를 클릭하여 폴더를 찾습니다.  
  
    6.  **설명** 상자에 프로덕션 GPO에 대한 설명을 입력하고 **백업**을 클릭합니다.  
  
    7.  백업이 완료 되 면 클릭 **확인**, 를 선택한 다음는 **GPO 백업** 페이지에서 클릭 **다음**합니다.  
  
    8.  에 **백업 위치** 페이지는 **백업 폴더** 상자는 해당 준비 GPO의 백업을 2 단계에서에서 저장 된 위치에 대 한 경로 입력 하거나 클릭 **찾아보기** 폴더를 찾은 다음 클릭을 **다음**합니다.  
  
    9. **원본 GPO** 페이지에서 **각 GPO의 최신 버전만 표시** 확인란을 선택하여 이전 백업을 숨기고 해당 준비 GPO를 선택합니다. 클릭 **설정 보기** 프로덕션 GPO에 적용 하기 전에 원격 액세스 설정을 검토 한 다음 클릭 **다음**합니다.  
  
    10. 에 **백업 검사** 페이지에서 클릭 **다음**, 를 클릭 하 고 **마침**합니다.  
  
![Windows PowerShell](../../../media/Step-1-Configuring-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)***<em>windows powershell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
-   백업 폴더에 도메인 "corp.contoso.com"에서 준비 클라이언트 GPO "DirectAccess Client Settings-Staging"를 백업 하려면 "C:\Backups\":  
  
    ```  
    $backup = Backup-GPO "Name 'DirectAccess Client Settings - Staging' "Domain 'corp.contoso.com' "Path 'C:\Backups\'  
    ```  
  
-   준비 클라이언트 GPO "DirectAccess Client Settings-Staging" 도메인 "corp.contoso.com"에서 보안 필터링을 보려면:  
  
    ```  
    Get-GPPermission "Name 'DirectAccess Client Settings - Staging' "Domain 'corp.contoso.com' "All | ?{ $_.Permission "eq 'GpoApply'}  
    ```  
  
-   프로덕션 클라이언트 GPO의 보안 필터에 보안 그룹 "corp.contoso.com\DirectAccess 클라이언트"를 추가 하려면 "도메인"corp.contoso.com"에서" 프로덕션"DirectAccess 클라이언트 설정:  
  
    ```  
    Set-GPPermission "Name 'DirectAccess Client Settings - Production' "Domain 'corp.contoso.com' "PermissionLevel GpoApply "TargetName 'corp.contoso.com\DirectAccess clients' "TargetType Group  
    ```  
  
-   프로덕션 클라이언트 GPO 백업에서 설정을 가져오려면 "도메인"corp.contoso.com"에서" 프로덕션"DirectAccess 클라이언트 설정:  
  
    ```  
    Import-GPO "BackupId $backup.Id "Path $backup.BackupDirectory "TargetName 'DirectAccess Client Settings - Production' "Domain 'corp.contoso.com'  
    ```  
  
## <a name="ConfigSGs"></a>1.9 보안 그룹 구성  
클라이언트 컴퓨터 그룹 정책 개체에에서 포함 된 DirectAccess 설정은 원격 액세스를 구성할 때 지정 하는 보안 그룹의 구성원 인 컴퓨터에만 적용 됩니다. 또한 보안 그룹을 사용하여 응용 프로그램 서버를 관리하는 경우 이러한 서버의 보안 그룹을 만듭니다.  
  
### <a name="Sec_Group"></a>DirectAccess 클라이언트에 대 한 보안 그룹을 만들려면  
  
1.  에 **시작** 화면에서 입력**dsa.msc**, 한 다음 ENTER를 누릅니다. 에 **Active Directory 사용자 및 컴퓨터** 보안 그룹에 포함 되 면 마우스 오른쪽 단추로 클릭 하는 도메인을 확장 하는 콘솔의 왼쪽된 창에서 **사용자**, 가리킨 **새로**, 클릭 하 고 **그룹**합니다.  
  
2.  에 **새 개체-그룹** 대화 상자의 **그룹 이름**, 보안 그룹의 이름을 입력 합니다.  
  
3.  **그룹 범위** 아래에서 **전역**을 클릭하고 **그룹 종류**에서 **보안**을 클릭한 다음 **확인**을 클릭합니다.  
  
4.  DirectAccess 클라이언트 컴퓨터 보안 그룹을 두 번 클릭 하 고 속성 대화 상자에서 클릭 된 **멤버** 탭 합니다.  
  
5.  **구성원** 탭에서 **추가**를 클릭합니다.  
  
6.  **사용자, 연락처, 컴퓨터 또는 서비스 계정 선택** 대화 상자에서 DirectAccess에 사용할 클라이언트 컴퓨터를 선택하고 **확인**을 클릭합니다.  
  
![Windows PowerShell](../../../media/Step-1-Configuring-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)**windows powershell 해당 명령**  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
New-ADGroup -GroupScope global -Name <DirectAccess_clients_group_name>  
Add-ADGroupMember -Identity DirectAccess_clients_group_name -Members <computer_name>  
```  
  
## <a name="ConfigNLS"></a>1.10 네트워크 위치 서버 구성  
네트워크 위치 서버는 항상 사용 가능한 서버여야 하며, DirectAccess 클라이언트에서 신뢰할 수 있는 유효한 SSL 인증서가 있어야 합니다. 네트워크 위치 서버 인증서에 대한 인증서 옵션에는 다음 두 가지가 있습니다.  
  
-   **개인 인증서**  
  
    이 인증서의 지침에 따라 만든 인증서 템플릿을 기반 [1.5.2 인증서 템플릿 구성](#ConfigCertTemp)합니다.  
  
-   **자체 서명 된 인증서**  
  
    > [!NOTE]  
    > 멀티 사이트 배포에는 자체 서명된 인증서를 사용할 수 없습니다.  
  
다음은 각 인증서 종류에 필요합니다(아직 없는 경우).  
  
-   네트워크 위치 서버에 사용되는 웹 사이트 인증서. 인증서 주체는 네트워크 위치 서버의 URL이어야 합니다.  
  
-   내부 네트워크에서 항상 사용할 수 있는 CRL 배포 지점  
  
> [!NOTE]  
> 네트워크 위치 서버 웹 사이트가 DirectAccess 서버에 있는 경우 원격 액세스를 구성할 때 웹 사이트가 자동으로 만들어집니다. 이 사이트는 제공한 서버 인증서에 바인딩됩니다.  
  
#### <a name="to-install-the-network-location-server-certificate-from-an-internal-ca"></a>내부 CA의 네트워크 위치 서버 인증서를 설치하려면  
  
1.  네트워크 위치 서버 웹 사이트를 호스트할 서버에서 다음을 수행합니다. **시작** 화면에서**mmc.exe**를 입력 한 다음 enter 키를 누릅니다.  
  
2.  MMC 콘솔에서에 **파일** 메뉴 클릭 **스냅인 추가/제거**합니다.  
  
3.  에 **추가 / 제거 스냅인** 대화 상자, 클릭 **인증서**, 클릭 **추가**, 클릭 **컴퓨터 계정**, 클릭 **다음**, 클릭 **로컬 컴퓨터**, 클릭 **마침**, 클릭 하 고 **확인**합니다.  
  
4.  인증서 스냅인의 콘솔 트리에서 **인증서(로컬 컴퓨터)\개인\인증서**를 엽니다.  
  
5.  **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 가리킨 다음 **새 인증서 요청**을 클릭합니다.  
  
6.  **다음** 을 두 번 클릭합니다.  
  
7.  에 **인증서 요청** 페이지에서 확인란의 1.5.2의 지침에 따라 만든 인증서 템플릿에 대 한 인증서 템플릿을 구성 합니다. 필요한 경우 **이 인증서를 등록하려면 추가 정보가 필요합니다. 설정을 구성하려면 여기를 클릭하십시오.** 를 클릭합니다.  
  
8.  에 **인증서 속성** 대화 상자의 **주체** 탭에 **주체 이름** 영역에서 **형식**, 선택, **일반 이름**.  
  
9. **값**, 네트워크 위치 서버 웹 사이트의 FQDN을 입력 하 고 클릭 한 다음 **추가**합니다.  
  
10. 에 **대체 이름** 영역에서 **형식**, 선택, **DNS**합니다.  
  
11. **값**, 네트워크 위치 서버 웹 사이트의 FQDN을 입력 하 고 클릭 한 다음 **추가**합니다.  
  
12. **일반** 탭의 **이름**에 인증서를 식별하는 데 도움이 되는 이름을 입력할 수 있습니다.  
  
13. 클릭 **확인**, 클릭 **등록**, 를 클릭 하 고 **마침**합니다.  
  
14. 인증서 스냅인의 세부 정보 창에서 새 인증서가 서버 인증 용도로 등록되었는지 확인합니다.  
  
#### <a name="to-configure-the-network-location-server"></a>네트워크 위치 서버를 구성하려면  
  
1.  항상 사용 가능한 서버에서 웹 사이트를 설정합니다. 웹 사이트에 콘텐츠는 필요 없지만 웹 사이트를 테스트할 때 클라이언트가 연결되면 메시지를 제공하는 기본 페이지를 정의할 수 있습니다.  
  
    > [!NOTE]  
    > 네트워크 위치 서버 웹 사이트가 DirectAccess 서버에서 호스트되는 경우에는 이 단계가 필요하지 않습니다.  
  
2.  HTTPS 서버 인증서를 웹 사이트에 바인딩합니다. 인증서의 일반 이름이 네트워크 위치 서버 사이트의 이름과 일치해야 합니다. DirectAccess 클라이언트에서 발급 CA를 신뢰하는지 확인합니다.  
  
    > [!NOTE]  
    > 네트워크 위치 서버 웹 사이트가 DirectAccess 서버에서 호스트되는 경우에는 이 단계가 필요하지 않습니다.  
  
3.  내부 네트워크에서 항상 사용할 수 있는 CRL 사이트를 설정합니다.  
  
    CRL 배포 지점은 다음을 통해 액세스할 수 있습니다.  
  
    -   HTTP 기반 URL을 사용 하는 웹 서버: https://crl.corp.contoso.com/crld/corp-APP1-CA.crl  
  
    -   파일 서버와 같은 범용 명명 규칙 (UNC) 경로 통해 액세스 하는 \\\crl.corp.contoso.com\crld\corp-APP1-CA.crl  
  
    IPv6을 통해서만 내부 CRL 배포 지점에 연결할 수 경우 인트라넷의 IPv6 주소와 CRL 배포 지점 간의 IPsec 보호를 제외하도록 고급 보안이 포함된 Windows 방화벽 연결 보안 규칙을 구성해야 합니다.  
  
4.  내부 네트워크의 DirectAccess 클라이언트가 네트워크 위치 서버의 이름을 확인할 수 있는지 확인합니다. 또한 인터넷의 DirectAccess 클라이언트가 이름을 확인할 수 없는지 확인합니다.  
  
## <a name="BKMK_Links"></a>다음 단계  
  
-   [2단계: 고급 DirectAccess 서버 구성](da-adv-configure-s2-servers.md)  
  


