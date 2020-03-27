---
title: 핵심 네트워크 구성 요소
description: 이 가이드에서는 완벽 하 게 작동 하는 네트워크에 필요한 핵심 구성 요소를 계획 하 고 배포 하는 방법에 대 한 지침과 Windows Server 2016를 사용 하는 새 포리스트에 새 Active Directory 도메인을 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: b3cd60f7-d380-4712-9a78-0a8f551e1121
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a0da2265f8f66256ed2ba71d4847bf8a548626f8
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319139"
---
# <a name="core-network-components"></a>핵심 네트워크 구성 요소

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 가이드에서는 완벽 하 게 작동 하는 네트워크와 새 포리스트의 새 Active Directory 도메인에 필요한 핵심 구성 요소를 계획 하 고 배포 하는 방법에 대 한 지침을 제공 합니다.

> [!NOTE]
> 이 가이드는 TechNet 갤러리에서 Microsoft Word 형식으로 다운로드할 수 있습니다. 자세한 내용은 [Windows Server 2016에 대 한 핵심 네트워크 가이드](https://gallery.technet.microsoft.com/Core-Network-Guide-for-9da2e683)를 참조 하세요.

이 가이드에는 다음 섹션이 수록되어 있습니다.

- [이 가이드 정보](#BKMK_about)

- [핵심 네트워크 개요](#BKMK_overview)

- [핵심 네트워크 계획](#BKMK_planning)

- [핵심 네트워크 배포](#BKMK_deployment)

- [추가 기술 리소스](#BKMK_resources)

- [부록 A ~ E](#BKMK_appendix)

## <a name="about-this-guide"></a><a name="BKMK_about"></a>이 가이드 정보
이 가이드는 새 네트워크를 설치하고 있는 네트워크 및 시스템 관리자나, 작업 그룹으로 구성된 네트워크를 바꾸기 위해 도메인 기반 네트워크를 만들려는 네트워크 및 시스템 관리자를 대상으로 합니다. 이 가이드에서 제공하는 배포 시나리오는 향후에 네트워크에 서비스와 기능을 추가해야 하는 경우에 특히 유용합니다.

이 배포 시나리오에서 사용되는 각 기술에 대한 디자인 및 배포 가이드를 검토하여 이 가이드가 자신에게 필요한 서비스나 구성을 제공하는지 파악하는 것이 좋습니다.

핵심 네트워크는 조직의 IT(정보 기술) 요구 사항에 맞는 기반 서비스를 제공하는 네트워크 하드웨어, 디바이스 및 소프트웨어의 모음입니다.

Windows Server 핵심 네트워크는 다음을 포함한 다양한 이점을 제공합니다.

-   컴퓨터와 다른 TCP/IP 호환 디바이스 사이의 네트워크 연결을 위한 핵심 프로토콜. TCP/IP는 컴퓨터를 연결하고 네트워크를 구성하기 위한 표준 프로토콜 집합입니다. TCP/IP는 TCP/IP 프로토콜 모음을 구현 하 고 지 원하는 Microsoft Windows 운영 체제와 함께 제공 되는 네트워크 프로토콜 소프트웨어입니다.

-   DHCP 클라이언트로 구성된 컴퓨터 및 다른 디바이스에 DHCP(Dynamic Host Configuration Protocol) 자동 IP 주소 할당. 네트워크에 있는 모든 컴퓨터의 IP 주소를 수동으로 구성하는 작업은 DHCP 서버를 사용하여 컴퓨터 및 기타 디바이스에 IP 주소를 동적으로 제공하는 것보다 시간이 많이 걸리고 유연성도 낮습니다.

-   DNS(Domain Name System) 이름 확인 서비스. DNS를 통해 사용자, 컴퓨터, 응용 프로그램 및 서비스는 컴퓨터나 디바이스의 정규화된 도메인 이름을 사용하여 네트워크에 있는 컴퓨터와 디바이스의 IP 주소를 찾을 수 있습니다.

-   동일한 클래스와 특성 정의(스키마), 사이트와 복제 정보(구성) 및 포리스트 전체 검색 기능(글로벌 카탈로그)을 공유하는 하나 이상의 Active Directory 도메인인 포리스트

-   새 포리스트에서 처음으로 만든 도메인인 포리스트 루트 도메인. 포리스트 전체 관리 그룹인 Enterprise Admins 및 Schema Admins 그룹은 포리스트 루트 도메인에 위치합니다. 또한 포리스트 루트 도메인은 다른 도메인과 마찬가지로 AD DS(Active Directory 도메인 서비스)에서 관리자가 정의한 컴퓨터, 사용자 및 그룹 개체의 모음입니다. 이러한 개체는 공통의 디렉터리 데이터베이스 및 보안 정책을 공유합니다. 또한 조직의 규모가 커짐에 따라 도메인을 추가하는 경우 다른 도메인과의 보안 관계도 공유할 수 있습니다. 또한 디렉터리 서비스는 디렉터리 데이터를 저장하고, 권한 있는 컴퓨터, 애플리케이션 및 사용자는 이 서비스를 통해 데이터에 액세스할 수 있습니다.

-   사용자 및 컴퓨터 계정 데이터베이스. 디렉터리 서비스는 네트워크에 연결할 수 있도록 권한이 부여된 사람 및 컴퓨터를 위한 사용자 및 컴퓨터 계정을 만들고 애플리케이션, 데이터베이스, 공유된 파일과 폴더, 프린터 등의 네트워크 리소스에 액세스할 수 있는 중앙 집중식 사용자 계정 데이터베이스를 제공합니다.

또한 핵심 네트워크를 사용하면 조직의 규모가 커지고 IT 요구 사항이 변함에 따라 네트워크를 조정할 수 있습니다. 예를 들어 핵심 네트워크를 사용 하면 도메인, IP 서브넷, 원격 액세스 서비스, 무선 서비스 및 Windows Server 2016에서 제공 하는 기타 기능 및 서버 역할을 추가할 수 있습니다.

### <a name="network-hardware-requirements"></a>네트워크 하드웨어 요구 사항
핵심 네트워크를 배포하려면 다음을 포함한 네트워크 하드웨어를 배포해야 합니다.

-   이더넷, Fast Ethernet 또는 Gigabyte Ethernet 케이블

-   컴퓨터와 디바이스 사이에서 네트워크 트래픽을 릴레이하는 허브, 계층 2 또는 3 스위치, 라우터 또는 기타 디바이스

-   각 클라이언트 서버 운영 체제의 최소 하드웨어 요구 사항을 충족하는 컴퓨터

## <a name="what-this-guide-does-not-provide"></a>이 가이드에서 설명하지 않는 정보
이 가이드에서는 다음을 배포하기 위한 지침은 제공하지 않습니다.

-   케이블, 라우터, 스위치, 허브 등의 네트워크 하드웨어

-   프린터, 파일 서버 등의 추가 네트워크 리소스

-   인터넷 연결

-   원격 액세스

-   무선 액세스

-   클라이언트 컴퓨터 배포

> [!NOTE]
> Windows 클라이언트 운영 체제를 실행 하는 컴퓨터는 기본적으로 DHCP 서버에서 IP 주소 임대를 받도록 구성 됩니다. 따라서 클라이언트 컴퓨터의 DHCP 또는 IPv4(인터넷 프로토콜 버전 4)를 추가로 구성할 필요가 없습니다.

## <a name="technology-overviews"></a>기술 개요
다음 섹션에서는 핵심 네트워크를 만들기 위해 배포된 필수 기술에 대한 간략한 개요를 제공합니다.

### <a name="active-directory-domain-services"></a>Active Directory 도메인 서비스
디렉터리는 사용자 및 컴퓨터 등과 같은 네트워크의 개체에 대한 정보를 저장하는 계층 구조입니다. AD DS와 같은 디렉터리 서비스는 디렉터리 데이터를 저장 하 고이 데이터를 네트워크 사용자 및 관리자가 사용할 수 있도록 하는 방법을 제공 합니다. 예를 들어 AD DS은 이름, 전자 메일 주소, 암호 및 전화 번호를 포함 하 여 사용자 계정에 대 한 정보를 저장 하 고 같은 네트워크에 있는 다른 권한 있는 사용자가이 정보에 액세스할 수 있도록 합니다.

### <a name="dns"></a>DNS
DNS는 인터넷 또는 조직 네트워크와 같은 TCP/IP 네트워크를 위한 이름 확인 프로토콜입니다. DNS 서버는 클라이언트 컴퓨터 및 서비스에서 쉽게 인식할 수 있는 영숫자 DNS 이름을 컴퓨터가 서로 통신하는 데 사용하는 IP 주소로 확인하는 데 사용할 수 있는 정보를 호스트합니다.

### <a name="dhcp"></a>DHCP
DHCP는 호스트 IP 구성의 관리를 단순화하기 위한 IP 표준입니다. DHCP 표준은 DHCP 서버를 IP 주소의 동적 할당 및 네트워크에서 DHCP가 설정된 클라이언트에 대한 기타 관련 구성 정보를 관리하는 방법으로 사용할 수 있도록 합니다.

DHCP에서는 DHCP 서버를 사용하여 로컬 네트워크에 있는 컴퓨터 또는 프린터와 같은 다른 디바이스에 IP 주소를 동적으로 할당할 수 있습니다. IP 주소 및 해당 관련 서브넷 마스크는 컴퓨터가 연결된 호스트 컴퓨터 및 서브넷을 모두 식별하므로 TCP/IP 네트워크의 모든 컴퓨터에는 고유한 IP 주소가 있어야 합니다. DHCP를 사용하여 DHCP 클라이언트로 구성된 모든 컴퓨터에 해당 네트워크 위치 및 서브넷에 적합한 IP 주소가 수신되도록 하고 기본 게이트웨이 및 DNS 서버와 같은 DHCP 옵션을 사용하여 DHCP 클라이언트가 네트워크에서 제대로 작동하는 데 필요한 정보를 이 클라이언트에 자동으로 제공할 수 있습니다.

TCP/IP 기반 네트워크의 경우 DHCP를 사용하면 컴퓨터를 다시 구성하는 작업에 수반되는 관리 작업의 양과 복잡성이 줄어듭니다.

### <a name="tcpip"></a>TCP/IP
Windows Server 2016의 TCP/IP는 다음과 같습니다.

-   업계 표준 네트워킹 프로토콜을 기준으로 하는 네트워킹 소프트웨어

-   Windows 기반 컴퓨터를 LAN(Local Area Network)과 WAN(Wide Area Network) 환경 모두에 연결할 수 있는, 라우트 가능한 엔터프라이즈 네트워킹 프로토콜

-   정보 공유를 목적으로 Windows 기반 컴퓨터를 상이한 시스템과 연결하기 위한 핵심 기술 및 유틸리티

-   World Wide Web 및 FTP(File Transfer Protocol) 서버와 같은 글로벌 인터넷 서비스에 액세스하기 위한 토대

-   강력하고, 확장 가능하며, 플랫폼 간 작동이 가능한 클라이언트/서버 프레임워크

TCP/IP는 Windows 기반 컴퓨터를 다음과 같은 Microsoft 시스템 및 타사 시스템에 연결하고 해당 시스템과 정보를 공유할 수 있는 기본 TCP/IP 유틸리티를 제공합니다.

-    Windows Server 2016

-   Windows 10

-    Windows Server 2012 R2

-   Windows 8.1

-    Windows Server 2012

-   Windows 8

-    Windows Server 2008 R2

-    Windows 7

-    Windows Server 2008

-   Windows Vista

-   인터넷 호스트

-   Apple Macintosh 시스템

-   IBM 메인프레임

-   UNIX 및 Linux 시스템

-   Open VMS 시스템

-   네트워크로 준비 된 프린터

-   유선 이더넷 또는 무선 802.11 기술을 사용 하는 태블릿 및 휴대폰 전화

## <a name="core-network-overview"></a><a name="BKMK_overview"></a>핵심 네트워크 개요
다음 그림에서는 Windows Server 핵심 네트워크 토폴로지를 보여 줍니다.

![Windows Server 핵심 네트워크 토폴로지](../media/Core-Network-Guide/cng16_overview.jpg)

> [!NOTE]
> 이 가이드에는 핵심 네트워크 부록 가이드를 사용하여 구현할 수 있는 802.1X 유선 및 무선 배포와 같은 보안 네트워크 액세스 솔루션에 대한 토대를 제공하기 위해 네트워크 토폴로지에 선택적 NPS(네트워크 정책 서버) 및 웹 서버(IIS) 서버를 추가하는 방법에 대한 지침도 포함됩니다. 자세한 내용은 [네트워크 액세스 인증 및 웹 서비스에 대한 선택적 기능 배포](#BKMK_optionalfeatures)를 참조하십시오.

### <a name="core-network-components"></a>핵심 네트워크 구성 요소
핵심 네트워크의 구성 요소는 다음과 같습니다.

##### <a name="router"></a>라우터
이 배포 가이드에서는 DHCP 전달을 사용하는 라우터로 분리된 두 개의 서브넷으로 구성된 핵심 네트워크를 배포하는 지침을 설명하지만, 사용자의 요구 사항과 리소스에 따라 계층 2 스위치, 계층 3 스위치 또는 허브를 배포할 수 있습니다. 스위치를 배포하는 경우에는 스위치에 DHCP 전달 기능이 있거나 각 서브넷에 DHCP 서버를 배치해야 합니다. 허브를 배포하려면 단일 서브넷을 배포하는 경우여야 하며 이때는 DHCP 전달이 필요 없거나 DHCP 서버에 두 번째 범위가 필요하지 않습니다.

##### <a name="static-tcpip-configurations"></a>고정 TCP/IP 구성
이 배포의 서버는 고정 IPv4 주소로 구성되며, 클라이언트 컴퓨터는 기본적으로 DHCP 서버에서 IP 주소 임대를 받도록 구성됩니다.

##### <a name="active-directory-domain-services-global-catalog-and-dns-server-dc1"></a>Active Directory Domain Services 글로벌 카탈로그 및 DNS 서버 DC1
네트워크의 모든 컴퓨터와 장치에 디렉터리 및 이름 확인 서비스를 제공 하는 d c 1 이라는 서버에 Active Directory Domain Services (AD DS) 및 DNS (Domain Name System)가 모두 설치 됩니다.

##### <a name="dhcp-server-dhcp1"></a>DHCP 서버 DHCP1
DHCP1이라고 하는 DHCP 서버는 로컬 서브넷의 컴퓨터에 IP(인터넷 프로토콜) 주소 임대를 제공하는 범위로 구성됩니다. 라우터에 DHCP 전달이 구성된 경우 다른 서브넷의 컴퓨터에 IP 주소 임대를 제공하도록 추가 범위로 DHCP 서버를 구성할 수도 있습니다.

##### <a name="client-computers"></a>클라이언트 컴퓨터
Windows 클라이언트 운영 체제를 실행 하는 컴퓨터는 기본적으로 dhcp 서버에서 자동으로 IP 주소와 DHCP 옵션을 가져오는 DHCP 클라이언트로 구성 됩니다.

## <a name="core-network-planning"></a><a name="BKMK_planning"></a>핵심 네트워크 계획
핵심 네트워크를 배포하기 전에 다음과 같은 항목을 계획해야 합니다.

-   [서브넷 계획](#bkmk_NetFndtn_Pln_Subnt)

-   [모든 서버의 기본 구성 계획](#bkmk_NetFndtn_Pln_AllSrvrs)

-   [DC1 배포 계획](#bkmk_NetFndtn_Pln_AD-DNS-01)

-   [도메인 액세스 계획](#bkmk_NetFndtn_Pln_DomAccess)

-   [DHCP1 배포 계획](#bkmk_NetFndtn_Pln_DHCP-01)

다음 섹션에서는 이러한 각 항목에 대해 보다 자세히 설명합니다.

> [!NOTE]
> 배포 계획에 대 한 도움이 필요 하면 [부록 E-핵심 네트워크 계획 준비 시트](#BKMK_E)도 참조 하세요.

### <a name="planning-subnets"></a><a name="bkmk_NetFndtn_Pln_Subnt"></a>서브넷 계획
TCP/IP(Transmission Control Protocol/Internet Protocol) 네트워킹에서 라우터는 서브넷이라고 하는 여러 개의 실제 네트워크 세그먼트에서 사용되는 하드웨어와 소프트웨어를 상호 연결하는 데 사용됩니다. 라우터는 또한 각 서브넷 간에 IP 패킷을 전달하는 데도 사용됩니다. 이 가이드의 지침을 계속하기 전에 필요한 라우터와 서브넷의 수를 비롯하여 네트워크의 물리적 레이아웃을 결정하십시오.

또한 네트워크의 서버를 고정 IP 주소로 구성하려면 핵심 네트워크 서버가 있는 서브넷에 사용할 IP 주소 범위를 결정해야 합니다. 이 가이드에서는 개인 IP 주소 범위 10.0.0.1-10.0.0.254 및 10.0.1.1-10.0.1.254를 예로 사용 하지만 원하는 개인 IP 주소 범위를 사용할 수 있습니다.

> [!IMPORTANT]
> 각 서브넷에 사용하려는 IP 주소 범위를 선택했으면 라우터가 설치된 서브넷에서 사용된 IP 주소 범위와 동일한 IP 주소 범위의 IP 주소로 라우터를 구성했는지 확인합니다. 예를 들어 기본적으로 라우터가 IP 주소 192.168.1.1로 구성되었지만 IP 주소 범위 10.0.0.0/24를 사용하여 서브넷에 라우터를 설치하고 있는 경우 IP 주소 범위 10.0.0.0/24의 IP 주소를 사용하도록 라우터를 다시 구성해야 합니다.

인터넷 RFC(Request for Comments) 1918에서 다음과 같은 인식된 개인 IP 주소 범위가 지정되어 있습니다.

-   10.0.0.0-10.255.255.255

-   172.16.0.0-172.31.255.255

-   192.168.0.0-192.168.255.255

RFC 1918에 지정된 개인 IP 주소 범위를 사용할 때는 이 주소로 전송되거나 이 주소에서 송신되는 요청이 자동으로 ISP(인터넷 서비스 공급자) 라우터에 의해 폐기되므로 개인 IP 주소를 사용하여 인터넷에 직접 연결할 수 없습니다. 나중에 핵심 네트워크에 인터넷 연결을 추가하려면 ISP에 문의하여 공용 IP 주소를 받아야 합니다.

> [!IMPORTANT]
> 개인 IP 주소를 사용할 때는 특정 유형의 프록시 또는 NAT(Network Address Translation) 서버를 사용하여 로컬 네트워크의 개인 IP 주소를 인터넷에서 라우팅 가능한 공용 IP 주소로 변환해야 합니다. 대부분의 라우터는 NAT 서비스를 제공하므로 NAT 가능 라우터를 선택하는 것은 아주 간단합니다.

자세한 내용은 [DHCP1 배포 계획](#bkmk_NetFndtn_Pln_DHCP-01)을 참조하십시오.

### <a name="planning-basic-configuration-of-all-servers"></a><a name="bkmk_NetFndtn_Pln_AllSrvrs"></a>모든 서버의 기본 구성 계획
핵심 네트워크의 각 서버에 대해 컴퓨터 이름을 바꾸고 컴퓨터에 대해 고정 IPv4 주소 및 기타 TCP/IP 속성을 할당 및 구성해야 합니다.

#### <a name="planning-naming-conventions-for-computers-and-devices"></a>컴퓨터 및 디바이스에 대한 명명 규칙 계획
네트워크에서의 일관성을 유지하기 위해 서버, 프린터 및 기타 디바이스에 일관된 이름을 사용하는 것이 좋습니다. 컴퓨터 이름은 사용자와 관리자가 서버, 프린터 또는 기타 디바이스의 용도와 위치를 쉽게 파악하는 데 도움이 될 수 있습니다. 예를 들어 세 개의 DNS 서버가 샌프란시스코에 하나, 로스앤젤레스에 하나, 시카고에 하나씩 있는 경우 명명 규칙 *서버 함수*-*위치*-*번호*를 사용할 수 있습니다.

-   DNS-DEN-01. 이 이름은 콜로라도, 덴버의 DNS 서버를 나타냅니다. 덴버에 DNS 서버가 더 추가되면 DNS-DEN-02 및 DNS-DEN-03과 같이 이름의 숫자 값을 늘릴 수 있습니다.

-   DNS-SPAS-01. 이 이름은 캘리포니아, 사우스파사데나의 DNS 서버를 나타냅니다.

-   DNS-ORL-01. 이 이름은 플로리다, 올랜도의 DNS 서버를 나타냅니다.

이 가이드에서 서버 명명 규칙은 매우 간단합니다. 주 서버 기능과 숫자로 구성됩니다. 예를 들어 도메인 컨트롤러 이름은 DC1이고 DHCP 서버 이름은 DHCP1입니다.

이 가이드를 사용하여 핵심 네트워크를 설치하기 전에 명명 규칙을 선택하는 것이 좋습니다.

#### <a name="planning-static-ip-addresses"></a>고정 IP 주소 계획
각 컴퓨터를 고정 IP 주소로 구성하기 전에 서브넷 및 IP 주소 범위를 계획해야 합니다. 또한 DNS 서버의 IP 주소를 결정해야 합니다. 추가적인 서브넷 또는 인터넷과 같은 다른 네트워크에 액세스를 제공하는 라우터를 설치할 계획일 때는 고정 IP 구성을 위해 기본 게이트웨이라고도 하는 라우터의 IP 주소를 알아야 합니다.

다음 표에서는 고정 IP 주소 구성에 대한 예제 값을 보여 줍니다.

|구성 항목|예제 값|
|-----------------------|------------------|
|IP 주소|10.0.0.2|
|서브넷 마스크|255.255.255.0|
|기본 게이트웨이(라우터 IP 주소)|10.0.0.1|
|기본 설정 DNS 서버|10.0.0.2|

> [!NOTE]
> 둘 이상의 DNS 서버를 배포하도록 계획하는 경우 대체 DNS 서버 IP 주소도 계획할 수 있습니다.

### <a name="planning-the-deployment-of-dc1"></a><a name="bkmk_NetFndtn_Pln_AD-DNS-01"></a>DC1 배포 계획
다음은 d c 1에서 Active Directory Domain Services (AD DS) 및 DNS를 설치 하기 전의 주요 계획 단계입니다.

#### <a name="planning-the-name-of-the-forest-root-domain"></a>포리스트 루트 도메인의 이름 계획
AD DS 디자인 프로세스의 첫 번째 단계는 조직에 필요한 포리스트 수를 결정 하는 것입니다. 포리스트는 최상위 AD DS 컨테이너 이며 공통 스키마 및 글로벌 카탈로그를 공유 하는 하나 이상의 도메인으로 구성 됩니다. 조직에는 여러 포리스트가 있을 수 있지만 대부분의 조직에서는 단일 포리스트 디자인이 많이 사용되는 모델이며 관리도 단순합니다.

조직에 첫 번째 도메인 컨트롤러를 만들 때 첫 번째 도메인(포리스트 루트 도메인이라고도 함)과 첫 번째 포리스트를 만듭니다. 하지만 이 가이드를 사용하여 이 작업을 수행하기 전에 먼저 조직에 가장 적합한 도메인 이름을 결정해야 합니다. 대개의 경우 조직 이름은 도메인 이름으로 사용되며 이 도메인 이름이 등록되는 경우가 많습니다. 외부 연결 인터넷 기반 웹 서버를 배포하여 고객이나 파트너에게 정보 및 서비스를 제공하도록 계획하는 경우 아직 사용되지 않은 도메인 이름을 선택한 후 이 도메인 이름이 사용자 조직의 소유가 되도록 도메인 이름을 등록하십시오.

#### <a name="planning-the-forest-functional-level"></a>포리스트 기능 수준 계획
AD DS를 설치 하는 동안 사용할 포리스트 기능 수준을 선택 해야 합니다. Windows Server 2003 Active Directory에 도입 된 도메인 및 포리스트 기능은 네트워크 환경 내에서 도메인 또는 포리스트 전체 Active Directory 기능을 사용 하도록 설정 하는 방법을 제공 합니다. 환경에 따라 서로 다른 수준의 도메인 기능 및 포리스트 기능을 사용할 수 있습니다.

포리스트 기능은 포리스트의 모든 도메인에서 기능을 사용하도록 설정합니다. 사용할 수 있는 포리스트 기능 수준은 다음과 같습니다.

-    Windows Server 2008. 이 포리스트 기능 수준은 windows server 2008 이상 버전의 Windows Server 운영 체제를 실행 하는 도메인 컨트롤러만 지원 합니다.

-    Windows Server 2008 R2. 이 포리스트 기능 수준은 windows server 2008 R2 도메인 컨트롤러 및 이후 버전의 Windows Server 운영 체제를 실행 하는 도메인 컨트롤러를 지원 합니다.

-    Windows Server 2012. 이 포리스트 기능 수준은 windows server 2012 도메인 컨트롤러 및 이후 버전의 Windows Server 운영 체제를 실행 하는 도메인 컨트롤러를 지원 합니다.

-    Windows Server 2012 R2. 이 포리스트 기능 수준은 windows server 2012 R2 도메인 컨트롤러 및 이후 버전의 Windows Server 운영 체제를 실행 하는 도메인 컨트롤러를 지원 합니다.

-    Windows Server 2016. 이 포리스트 기능 수준은 windows server 2016 도메인 컨트롤러 및 이후 버전의 Windows Server 운영 체제를 실행 하는 도메인 컨트롤러만 지원 합니다.

새 포리스트에 새 도메인을 배포 하 고 모든 도메인 컨트롤러가 Windows Server 2016를 실행 하는 경우 AD DS 설치 하는 동안 Windows Server 2016 포리스트 기능 수준으로 AD DS를 구성 하는 것이 좋습니다.

> [!IMPORTANT]
> 포리스트 기능 수준을 올리면 이전 버전의 운영 체제를 실행하는 도메인 컨트롤러를 포리스트에 추가할 수 없습니다. 예를 들어 포리스트 기능 수준을 Windows Server 2016로 올리면 Windows Server 2012 R2 또는 Windows Server 2008를 실행 하는 도메인 컨트롤러를 포리스트에 추가할 수 없습니다.

다음 표에서는 AD DS에 대 한 구성 항목 예제를 제공 합니다.

|구성 항목:|예제 값:|
|------------------------|-------------------|
|전체 DNS 이름|예를 들면 다음과 같습니다.<br /><br />-corp.contoso.com<br />-example.com|
|포리스트 기능 수준|-Windows Server 2008 <br />-Windows Server 2008 R2 <br />-Windows Server 2012 <br />-Windows Server 2012 R2 <br />-Windows Server 2016|
|Active Directory Domain Services 데이터베이스 폴더 위치|E:\Configuration\\<br /><br />또는 기본 위치를 적용합니다.|
|Active Directory Domain Services 로그 파일 폴더 위치|E:\Configuration\\<br /><br />또는 기본 위치를 적용합니다.|
|Active Directory Domain Services SYSVOL 폴더 위치|E:\Configuration\\<br /><br />또는 기본 위치를 적용합니다.|
|디렉터리 복원 모드 관리자 암호|**J\*p2leO4 $ F**|
|응답 파일 이름(옵션)|**AD DS_AnswerFile**|

#### <a name="planning-dns-zones"></a>DNS 영역 계획
Active Directory 통합 주 DNS 서버에서는 DNS 서버 역할을 설치하는 동안 기본적으로 정방향 조회 영역이 만들어집니다. 컴퓨터와 디바이스는 정방향 조회 영역을 통해 DNS 이름을 기반으로 다른 컴퓨터나 디바이스의 IP 주소를 쿼리할 수 있습니다. 정방향 조회 영역 이외에 DNS 역방향 조회 영역도 만드는 것이 좋습니다. 컴퓨터와 디바이스는 DNS 역방향 조회 영역을 통해, IP 주소를 사용하여 다른 컴퓨터나 디바이스의 이름을 찾을 수 있습니다. 역방향 조회 영역을 배포하면 일반적으로 DNS 성능이 향상되고 DNS 쿼리의 성공률이 크게 높아집니다.

역방향 조회 영역을 만들면 in-addr.arpa 도메인이 DNS에 구성됩니다. 이 도메인은 실용적이고 안정적인 방법으로 역방향 쿼리를 수행하기 위해 DNS 표준에 정의되고 인터넷 DNS 네임스페이스에 예약되었습니다. 역방향 네임스페이스를 만들려면 점으로 구분된 십진수 IP 주소 표시에서 숫자의 순서를 역으로 정렬하여 in-addr.arpa 도메인 내에 하위 도메인을 구성합니다.

In-addr.arpa 도메인은 IPv4 (인터넷 프로토콜 버전 4) 주소 지정을 기반으로 하는 모든 TCP/IP 네트워크에 적용 됩니다. 새 영역 마법사에서는 새 역방향 조회 영역을 만들 때 이 도메인을 사용한다고 자동으로 가정합니다.

새 영역 마법사를 실행할 때 다음과 같이 선택하는 것이 좋습니다.

|구성 항목|예제 값|
|-----------------------|------------------|
|영역 종류|**주 영역** 및 **Active Directory에 영역 저장**이 선택됩니다.|
|Active Directory 영역 복제 범위|**이 도메인의 모든 DNS 서버로**|
|첫 번째 역방향 조회 영역 이름 마법사 페이지|**IPv4 역방향 조회 영역**|
|두 번째 역방향 조회 영역 이름 마법사 페이지|네트워크 ID = 10.0.0.|
|동적 업데이트|**보안 동적 업데이트만 허용**|

### <a name="planning-domain-access"></a><a name="bkmk_NetFndtn_Pln_DomAccess"></a>도메인 액세스 계획
하려면 도메인에 로그온 컴퓨터는 도메인 구성원 컴퓨터 및 사용자 계정에 로그온 하기 전에 AD DS에 만들어야 합니다.

> [!NOTE]
> Windows를 실행하는 개별 컴퓨터에는 SAM(보안 계정 관리자) 사용자 계정 데이터베이스라고 하는 로컬 사용자 및 그룹 사용자 계정 데이터베이스가 있습니다. SAM 데이터베이스에서 로컬 컴퓨터에 대해 사용자 계정을 만들면 로컬 컴퓨터에는 로그온할 수는 있지만 도메인에는 로그온할 수 없습니다. 도메인 사용자 계정은 도메인 컨트롤러의 Active Directory 사용자 및 컴퓨터 MMC(Microsoft Management Console)에서는 만들어지지만 로컬 컴퓨터의 로컬 사용자 및 그룹에서는 만들어지지 않습니다.

도메인 로그온 자격 증명으로 처음 로그온에 성공하면 컴퓨터가 도메인에서 제거되거나 로그온 설정을 수동으로 변경하기 전까지 로그온 설정이 유지됩니다.

도메인에 로그온하기 전에 다음을 수행합니다.

-   Active Directory 사용자 및 컴퓨터에서 사용자 계정을 만듭니다. 각 사용자에게는 Active Directory 사용자 및 컴퓨터에 Active Directory Domain Services 사용자 계정이 있어야 합니다. 자세한 내용은 [Active Directory 사용자 및 컴퓨터에서 사용자 계정 만들기](#BKMK_createUA)를 참조하십시오.

-   IP 주소 구성이 정확한지 확인합니다. 컴퓨터를 도메인에 가입하려면 컴퓨터에 IP 주소가 있어야 합니다. 이 가이드에서는 서버가 고정 IP 주소로 구성되며 클라이언트 컴퓨터는 DHCP 서버에서 IP 주소 임대를 받습니다. 따라서 클라이언트를 도메인에 가입하기 전에 DHCP 서버를 배포해야 합니다. 자세한 내용은 [DHCP1 배포](#BKMK_deployDHCP01)를 참조하십시오.

-   도메인에 컴퓨터를 가입합니다. 네트워크 리소스를 제공하거나 이 리소스에 액세스하는 모든 컴퓨터는 도메인에 가입해야 합니다. 자세한 내용은 [도메인에 서버 컴퓨터 가입 및 로그온](#BKMK_joinlogserver) 및 [도메인에 클라이언트 컴퓨터 가입 및 로그온](#BKMK_joinlogclients)을 참조하십시오.

### <a name="planning-the-deployment-of-dhcp1"></a><a name="bkmk_NetFndtn_Pln_DHCP-01"></a>DHCP1 배포 계획
다음은 DHCP1에 DHCP 서버 역할을 설치하기 전의 주요 계획 단계입니다.

#### <a name="planning-dhcp-servers-and-dhcp-forwarding"></a>DHCP 서버 및 DHCP 전달 계획
DHCP 메시지는 브로드캐스트 메시지이기 때문에 라우터에 의해 서브넷 간에 전달되지 않습니다. 서브넷이 여러 개이고 각 서브넷에 대해 DHCP 서비스를 제공하려면 다음 중 하나를 수행해야 합니다.

-   각 서브넷에 DHCP 서버 설치

-   라우터가 서브넷을 가로질러 DHCP 브로드캐스트 메시지를 전달하도록 구성하고 각 서브넷당 하나씩 여러 범위를 DHCP 서버에 구성합니다.

대개의 경우 DHCP 브로드캐스트 메시지를 전달하도록 라우터를 구성하는 경우가 네트워크의 실제 세그먼트 각각에 DHCP 서버를 배포하는 경우보다 비용 효율적입니다.

#### <a name="planning-ip-address-ranges"></a>IP 주소 범위 계획
각 서브넷에는 자체의 고유한 IP 주소 범위가 있어야 합니다. 이 주소 범위는 DHCP 서버에서 범위로 표현됩니다.

범위는 DHCP 서비스를 사용하는 서브넷에 있는 컴퓨터의 IP 주소에 대한 관리 그룹화입니다. 관리자는 먼저 실제 서브넷마다 범위를 하나씩 만든 다음 범위를 사용하여 클라이언트에서 사용하는 매개 변수를 정의합니다.

범위에는 다음과 같은 속성이 있습니다.

-   DHCP 서비스 임대에 사용되는 주소를 포함하거나 제외할 IP 주소의 범위

-   지정된 IP 주소의 서브넷을 결정하는 서브넷 마스크

-   범위 이름은 생성되면 할당됩니다.

-   임대 기간 값은 동적으로 할당된 IP 주소를 수신하는 DHCP 클라이언트에 할당됩니다.

-   DHCP 클라이언트에 할당하도록 구성된 모든 DHCP 범위 옵션(예: DNS 서버 IP 주소, 라우터/기본 게이트웨이 IP 주소)

-   DHCP 클라이언트가 항상 같은 IP 주소를 받도록 하기 위해 선택적으로 사용되는 예약

서버를 배포하기 전에 서브넷과 각 서브넷에 대해 사용할 IP 주소 범위를 나열합니다.

#### <a name="planning-subnet-masks"></a>서브넷 마스크 계획
IP 주소 내에서 네트워크 ID와 호스트 ID는 서브넷 마스크를 사용하여 구분됩니다. 각 서브넷 마스크는 네트워크 ID를 식별하는 모두 1인 연속적인 비트 그룹과 IP 주소의 호스트 ID 부분을 식별하는 모두 0인 비트 그룹을 사용하는 32비트 숫자입니다.

예를 들어 IP 주소 131.107.16.200에 일반적으로 사용되는 서브넷 마스크는 다음의 32비트 이진 번호입니다.

```
11111111 11111111 00000000 00000000
```

이 서브넷 마스크 번호는 16 1 비트, 16 비트 16 비트 (이 IP 주소의 네트워크 ID 및 호스트 ID 섹션의 길이는 모두 16 비트) 임을 나타냅니다. 일반적으로 이 서브넷 마스크는 255.255.0.0과 같은 점으로 구분된 10진수 표기법으로 표시됩니다.

다음 표에서 인터넷 주소 클래스에 대한 서브넷 마스크를 볼 수 있습니다.

|주소 클래스|서브넷 마스크의 비트|서브넷 마스크|
|-----------------|------------------------|---------------|
|클래스 A|11111111 00000000 00000000 00000000|255.0.0.0|
|클래스 B|11111111 11111111 00000000 00000000|255.255.0.0|
|클래스 C|11111111 11111111 11111111 00000000|255.255.255.0|

DHCP에서 범위를 만들고 범위에 대한 IP 주소 범위를 입력하면 DHCP에서는 이 기본 서브넷 마스크 값을 제공합니다. 일반적으로 특별한 요구 사항이 없으며 각 IP 네트워크 세그먼트가 하나의 실제 네트워크에 해당하는 대부분의 네트워크에는 기본 서브넷 마스크 값이 적합합니다.

대개의 경우 사용자 지정된 서브넷 마스크를 사용하여 IP 서브넷 지정을 구현할 수 있습니다. IP 서브넷 지정을 사용하면 IP 주소의 기본 호스트 ID 부분을 다시 분할하여 원래 클래스 기반 네트워크 ID의 하위 분할인 서브넷을 지정할 수 있습니다.

서브넷 마스크 길이를 사용자 지정하면 실제 호스트 ID에 사용되는 비트 수를 줄일 수 있습니다.

주소 지정 및 라우팅 문제를 해결하려면 네트워크 세그먼트의 모든 TCP/IP 컴퓨터가 같은 서브넷 마스크를 사용하고 각 컴퓨터 또는 디바이스에 고유한 IP 주소가 있어야 합니다.

#### <a name="planning-exclusion-ranges"></a>제외 범위 계획
DHCP 서버에 대해 범위를 만들면 DHCP 서버가 컴퓨터 및 기타 디바이스와 같은 DHCP 클라이언트에 임대되도록 허용된 모든 IP 주소를 포함하는 IP 주소 범위를 지정할 수 있습니다. 이때 DHCP 서버가 사용하는 IP 주소 범위와 동일한 범위에서 고정 IP 주소로 일부 서버 및 기타 디바이스를 수동으로 구성한 경우 사용자 및 DHCP 서버 둘 다가 다른 디바이스에 동일한 IP 주소를 할당하는, IP 주소 충돌이 발생할 수 있습니다.

이 문제를 해결하기 위해 DHCP 범위에 대해 제외 범위를 만들 수 있습니다. 제외 범위는 DHCP 서버에서 사용할 수 없는 범위 IP 주소 범위 내에 있는 연속 된 IP 주소 범위입니다. 제외 범위를 만든 경우 DHCP 서버가 해당 범위의 주소를 할당하지 않으므로 IP 주소 충돌 없이 이 주소를 수동으로 할당할 수 있습니다.

각 범위에 대한 제외 범위를 만들어 해당 IP 주소를 DHCP 서버의 배포에서 제외할 수 있습니다. 고정 IP 주소로 구성된 모든 디바이스를 제외해야 합니다. 제외 주소 범위에는 다른 서버, 비 DHCP 클라이언트, 디스크가 없는 워크스테이션 또는 라우팅 및 원격 액세스 및 PPP 클라이언트에 수동으로 할당한 모든 IP 주소가 포함되어야 합니다.

향후의 네트워크 확장을 고려하여 추가적인 주소로 제외 범위를 구성하는 것이 좋습니다. 다음 표에서는 IP 주소 범위가 10.0.0.1-10.0.0.254이 고 서브넷 마스크가 255.255.255.0 인 범위에 대 한 예제 제외 범위를 제공 합니다.

|구성 항목|예제 값|
|-----------------------|------------------|
|제외 범위 시작 IP 주소|10.0.0.1|
|제외 범위 끝 IP 주소|10.0.0.25|

#### <a name="planning-tcpip-static-configuration"></a>TCP/IP 고정 구성 계획
라우터, DHCP 서버 및 DNS 서버와 같은 특정 디바이스는 고정 IP 주소로 구성해야 합니다. 또한 프린터와 같이 항상 같은 IP 주소를 사용하는 것이 편리한 디바이스도 있습니다. 각 서브넷에 대해 정적으로 구성할 디바이스를 나열한 다음 고정적으로 구성된 디바이스의 IP 주소를 DHCP 서버에서 임대하지 않도록 하기 위해 DHCP 서버에서 사용할 제외 범위를 계획합니다. 제외 범위는 DHCP 서비스 제공에서 제외되는 범위로, 범위 내의 제한된 연속 IP 주소입니다. 제외 범위에 속하는 주소는 서버가 네트워크의 DHCP 클라이언트에 제공하지 않습니다.

예를 들어 서브넷에 대한 IP 주소 범위가 192.168.0.1부터 192.168.0.254까지이며 고정 IP 주소로 구성할 장치가 10개인 경우에는 10개 이상의 IP 주소가 포함된 192.168.0.*x* 범위에 대한 제외 범위(192.168.0.1 - 192.168.0.15)를 만들 수 있습니다.

이 예제에서는 제외되는 IP 주소 중 10개를 고정 IP 주소를 가진 서버 및 기타 디바이스로 구성하고 나머지 5개의 주소는 향후에 추가할 수 있는 새 디바이스의 고정 구성을 위해 남겨둡니다. 이 제외 범위를 적용하면 DHCP 서버는 192.168.0.16부터 192.168.0.254까지의 주소 풀을 사용합니다.

다음 표에서는 AD DS 및 DNS에 대 한 추가 예제 구성 항목을 제공 합니다.

|구성 항목|예제 값|
|-----------------------|------------------|
|네트워크 연결 바인딩|이더넷|
|DNS 서버 설정|DC1.corp.contoso.com|
|기본 설정 DNS 서버 IP 주소|10.0.0.2|
|범위 추가 대화 상자 값<br /><br />1. 범위 이름<br />2. 시작 IP 주소<br />3. 끝 IP 주소<br />4. 서브넷 마스크<br />5. 기본 게이트웨이 (옵션)<br />6. 임대 기간|1. 기본 서브넷<br />2.10.0.0.1<br />3.10.0.0.254<br />4.255.255.255.0<br />5.10.0.0.1<br />6.8 일|
|IPv6 DHCP 서버 작동 모드|사용 안 함|

## <a name="core-network-deployment"></a><a name="BKMK_deployment"></a>핵심 네트워크 배포
핵심 네트워크를 배포하기 위한 기본 단계는 다음과 같습니다.

1.  [모든 서버 구성](#BKMK_configuringAll)

2.  [DC1 배포](#BKMK_deployADDNS01)

3.  [도메인에 서버 컴퓨터 가입 및 로그온](#BKMK_joinlogserver)

4.  [DHCP1 배포](#BKMK_deployDHCP01)

5.  [도메인에 클라이언트 컴퓨터 가입 및 로그온](#BKMK_joinlogclients)

6.  [네트워크 액세스 인증 및 웹 서비스에 대 한 선택적 기능 배포](#BKMK_optionalfeatures)

> [!NOTE]
> -   이 가이드에 나온 대부분의 절차에는 동일한 Windows PowerShell 명령이 제공됩니다. Windows PowerShell에서 이 cmdlet을 실행하기 전에 예제 값을 사용자 네트워크 배포에 적합한 값으로 바꾸십시오. 또한 Windows PowerShell에서 행마다 하나의 cmdlet을 입력해야 합니다. 이 가이드에서는 사용자 브라우저나 다른 애플리케이션에서의 문서 표시 및 형식 지정 제약 조건으로 인해 개별 cmdlet이 여러 행에 걸쳐 나타날 수 있습니다.
> -   이 가이드의 절차에는 계속하기 위해 권한을 요청하는 **사용자 계정 컨트롤** 대화 상자가 열리는 경우에 대한 지침은 포함되어 있지 않습니다. 이 가이드의 절차를 수행하는 동안 이 대화 상자가 열리는 경우와 작업에 대한 응답으로 이 대화 상자가 이미 열린 경우에는 **계속**을 클릭하십시오.

### <a name="configuring-all-servers"></a><a name="BKMK_configuringAll"></a>모든 서버 구성
Active Directory Domain Services 또는 DHCP와 같은 다른 기술을 설치하기 전에 먼저 다음 항목을 구성해야 합니다.

-   [컴퓨터 이름 바꾸기](#BKMK_rename)

-   [고정 IP 주소 구성](#BKMK_ip)

다음 섹션을 사용하여 각 서버에 대해 이러한 작업을 수행할 수 있습니다.

이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

#### <a name="rename-the-computer"></a><a name="BKMK_rename"></a>컴퓨터 이름 바꾸기
이 섹션의 절차를 사용 하 여 컴퓨터 이름을 변경할 수 있습니다. 컴퓨터 이름을 바꾸는 기능은 사용하기를 원하지 않는 컴퓨터 이름이 운영 체제에서 자동으로 만들어지는 경우에 유용합니다.

> [!NOTE]
> Windows PowerShell을 사용하여 이 절차를 수행하려면 PowerShell을 열고 별도의 행에 다음 cmdlet을 입력한 후 Enter 키를 누릅니다. *ComputerName*을, 사용하려는 이름으로 바꾸는 작업도 수행해야 합니다.
>
> `Rename-Computer`*ComputerName*
>
> `Restart-Computer`

###### <a name="to-rename-computers-running-windows-server-2016-windows-server-2012-r2-and-windows-server-2012"></a>Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012를 실행 하는 컴퓨터의 이름을 바꾸려면

1.  서버 관리자에서 **로컬 서버**를 클릭합니다. 컴퓨터 **속성**이 세부 정보 창에 표시됩니다.

2.  **속성**의 **컴퓨터 이름**에서 기존의 컴퓨터 이름을 클릭합니다. **시스템 속성** 대화 상자가 열립니다. **변경**을 클릭합니다. **컴퓨터 이름/도메인 변경** 대화 상자가 열립니다.

3.  **컴퓨터 이름/도메인 변경** 대화 상자의 **컴퓨터 이름**에 컴퓨터의 새 이름을 입력합니다. 예를 들어 컴퓨터 이름을 DC1로 지정하려면 **DC1**을 입력합니다.

4.  **확인** 을 두 번 클릭하고 **닫기**를 클릭합니다. 컴퓨터를 바로 다시 시작하여 이름 변경을 완료하려면 **지금 다시 시작**을 클릭합니다. 그렇지 않으면 **나중에 다시 시작**을 클릭합니다.

> [!NOTE]
> 다른 Microsoft 운영 체제를 실행 하는 컴퓨터의 이름을 바꾸는 방법에 대 한 자세한 내용은 [부록 a-컴퓨터 이름 바꾸기](#BKMK_A)를 참조 하세요.

#### <a name="configure-a-static-ip-address"></a><a name="BKMK_ip"></a>고정 IP 주소 구성
이 항목의 절차를 사용 하 여 Windows Server 2016를 실행 하는 컴퓨터에 대 한 고정 IP 주소를 사용 하는 네트워크 연결의 IPv4 (인터넷 프로토콜 버전 4) 속성을 구성할 수 있습니다.

> [!NOTE]
> Windows PowerShell을 사용하여 이 절차를 수행하려면 PowerShell을 열고 별도의 행에 다음 cmdlet을 입력한 후 Enter 키를 누릅니다. 이 예제의 인터페이스 이름과 IP 주소를, 컴퓨터를 구성하는 데 사용하려는 값으로 바꾸는 작업도 수행해야 합니다.
>
> `New-NetIPAddress -IPAddress 10.0.0.2 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24`
>
> `Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 127.0.0.1`

###### <a name="to-configure-a-static-ip-address-on-computers-running-windows-server-2016-windows-server-2012-r2-and-windows-server-2012"></a>Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012를 실행 하는 컴퓨터에서 고정 IP 주소를 구성 하려면

1.  작업 표시줄에서 네트워크 아이콘을 마우스 오른쪽 단추로 클릭한 후 **네트워크 및 공유 센터 열기**를 클릭합니다.

2.  **네트워크 및 공유 센터**에서 **어댑터 설정 변경**을 클릭 합니다. **네트워크 연결** 폴더가 열리고 사용 가능한 네트워크 연결이 표시됩니다.

3.  **네트워크 연결**에서 구성할 연결을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 네트워크 연결 **속성** 대화 상자가 열립니다.

4.  네트워크 연결 **속성** 대화 상자의 **이 연결에 다음 항목 사용**에서 **Internet Protocol Version 4(TCP/IPv4)** 를 선택하고 **속성**을 클릭합니다. **Internet Protocol Version 4(TCP/IPv4) 속성** 대화 상자가 열립니다.

5.  **Internet Protocol Version 4(TCP/IPv4) 속성**의 **일반** 탭에서 **다음 IP 주소 사용**을 클릭합니다. **IP 주소**에, 사용할 IP 주소를 입력합니다.

6.  Tab 키를 눌러 **서브넷 마스크**에 커서를 놓습니다. 서브넷 마스크의 기본값이 자동으로 입력됩니다. 기본 서브넷 마스크를 그대로 사용하거나 사용할 서브넷 마스크를 입력합니다.

7.  **기본 게이트웨이**에 기본 게이트웨이의 IP 주소를 입력합니다.

    > [!NOTE]
    > 라우터의 LAN(Local Area Network) 인터페이스에서 사용하는 IP 주소와 동일한 IP 주소로 **기본 게이트웨이**를 구성해야 합니다. 예를 들어 인터넷과 같은 WAN(Wide Area Network) 및 LAN에 라우터가 연결된 경우 **기본 게이트웨이**로 지정할 IP 주소와 동일한 IP 주소로 LAN 인터페이스를 구성합니다. 다른 예로, 라우터가 두 개의 LAN에 연결되어 있고 LAN A에서는 주소 범위 10.0.0.0/24가 사용되고 LAN B에서는 주소 범위 192.168.0.0/24가 사용된 경우 10.0.0.1와 같은 해당 주소 범위의 주소로 LAN A 라우터 IP 주소를 구성합니다. 또한 이 주소 범위에 대한 DHCP 범위에서 IP 주소 10.0.0.1로 **기본 게이트웨이**를 구성합니다. LAN B의 경우 192.168.0.1과 같은 해당 주소 범위의 주소로 LAN B 라우터 인터페이스를 구성한 후 **기본 게이트웨이** 값 192.168.0.1로 LAN B 범위 192.168.0.0/24를 구성합니다.

8.  **기본 설정 DNS 서버**에 DNS 서버의 IP 주소를 입력합니다. 로컬 컴퓨터를 기본 설정 DNS 서버로 사용하려는 경우 로컬 컴퓨터의 IP 주소를 입력합니다.

9. **대체 DNS 서버**에 대체 DNS 서버(있는 경우)의 IP 주소를 입력합니다. 로컬 컴퓨터를 대체 DNS 서버로 사용하려는 경우 로컬 컴퓨터의 IP 주소를 입력합니다.

10. **확인**을 클릭한 다음 **닫기**를 클릭합니다.

> [!NOTE]
> 다른 Microsoft 운영 체제를 실행 하는 컴퓨터에서 고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 [부록 B-고정 ip 주소 구성](#BKMK_B)을 참조 하세요.

#### <a name="deploying-dc1"></a><a name="BKMK_deployADDNS01"></a>DC1 배포
Active Directory Domain Services (AD DS) 및 DNS를 실행 하는 컴퓨터인 DC1을 배포 하려면 다음 단계를 순서 대로 완료 해야 합니다.

-   [모든 서버 구성](#BKMK_configuringAll) 섹션의 단계 수행

-   [새 포리스트에 대 한 AD DS 및 DNS 설치](#BKMK_installAD-DNS)

-   [Active Directory 사용자 및 컴퓨터에서 사용자 계정 만들기](#BKMK_createUA)

-   [그룹 멤버 자격 할당](#BKMK_assigngroup)

-   [DNS 역방향 조회 영역 구성](#BKMK_reverse)

**관리 권한**

네트워크의 유일한 관리자로서 소규모 네트워크를 설치 중인 경우, 자신의 사용자 계정을 만든 다음 이 사용자 계정을 Enterprise Admins 및 Domain Admins의 구성원으로 추가하는 것이 좋습니다. 이렇게 하면 더 쉽게 모든 네트워크 리소스에 대해 관리자 역할을 할 수 있습니다. 또한 관리 작업을 수행해야 할 경우에만 이 계정으로 로그온하고 IT에 관련되지 않은 작업에 사용할 별도의 사용자 계정을 만드는 것이 좋습니다.

여러 관리자가 있는 대규모 조직의 경우 AD DS 설명서를 참조 하 여 조직 직원에 게 가장 적합 한 그룹 구성원 자격을 확인 하세요.

**도메인 사용자 계정과 로컬 컴퓨터의 사용자 계정 간 차이점**

도메인 기반 인프라의 장점 중 한 가지는 도메인에 있는 컴퓨터마다 사용자 계정을 만들 필요가 없다는 점입니다. 이는 컴퓨터가 클라이언트 컴퓨터이든 서버이든 상관없습니다.

따라서 도메인의 각 컴퓨터에 사용자 계정을 만들지 않아야 합니다. 모든 사용자 계정을 Active Directory 사용자 및 컴퓨터에서 만들고 앞의 절차에 따라 그룹 구성원을 할당하십시오. 기본적으로 모든 사용자 계정은 Domain Users 그룹의 구성원입니다.

클라이언트 컴퓨터를 도메인에 가입하면, Domain Users 그룹의 모든 구성원은 모든 클라이언트 컴퓨터에 로그온할 수 있습니다.

사용자가 컴퓨터에 로그온할 수 있는 날짜와 시간을 지정하도록 사용자 계정을 구성할 수 있습니다. 또한 각 사용자가 사용할 수 있는 컴퓨터도 지정할 수도 있습니다. 이러한 설정을 구성하려면 Active Directory 사용자 및 컴퓨터를 열고 구성할 사용자 계정을 찾은 다음 해당 계정을 두 번 클릭합니다. 사용자 계정 **속성**에서 **계정** 탭을 클릭한 다음 **로그온 시간** 또는 **로그온 대상**을 클릭합니다.

#### <a name="install-ad-ds-and-dns-for-a-new-forest"></a><a name="BKMK_installAD-DNS"></a>새 포리스트에 대 한 AD DS 및 DNS 설치

다음 절차 중 하나를 사용 하 여 Active Directory Domain Services (AD DS) 및 DNS를 설치 하 고 새 포리스트에 새 도메인을 만들 수 있습니다. 

첫 번째 절차에서는 Windows PowerShell을 사용 하 여 이러한 작업을 수행 하는 방법에 대 한 지침을 제공 하 고 두 번째 절차에서는 서버 관리자를 사용 하 여 AD DS 및 DNS를 설치 하는

>[!IMPORTANT]
>이 절차의 단계를 완료 하면 컴퓨터가 자동으로 다시 시작 됩니다.

**Windows PowerShell을 사용 하 여 AD DS 및 DNS 설치**

다음 명령을 사용 하 여 AD DS 및 DNS를 설치 하 고 구성할 수 있습니다. 이 예에서 도메인 이름을 도메인에 사용 하려는 값으로 바꾸어야 합니다.

>[!NOTE]
>이러한 Windows PowerShell 명령에 대 한 자세한 내용은 다음 참조 항목을 참조 하세요.
>- [설치-Add-windowsfeature](https://docs.microsoft.com/powershell/module/servermanager/install-windowsfeature?view=win10-ps)
>- [설치-ADDSForest](https://docs.microsoft.com/powershell/module/addsdeployment/install-addsforest?view=win10-ps)

이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이어야 합니다.

- 관리자 권한으로 Windows PowerShell을 실행 하 고 다음 명령을 입력 한 후 ENTER 키를 누릅니다.  

`Install-WindowsFeature AD-Domain-Services -IncludeManagementTools`

설치가 성공적으로 완료 되 면 Windows PowerShell에 다음 메시지가 표시 됩니다.


    Success Restart Needed  Exit Code   Feature Result
    ------- --------------  ---------   --------------
    True    No              Success     {Active Directory Domain Services, Group P...


- Windows PowerShell에서 다음 명령을 입력 하 여 **corp.contoso.com** 텍스트를 도메인 이름으로 바꾸고 enter 키를 누릅니다.

````
Install-ADDSForest -DomainName "corp.contoso.com"
````

- Windows PowerShell 창의 맨 위에 표시 되는 설치 및 구성 프로세스 중에 다음과 같은 메시지가 나타납니다. 표시 되 면 암호를 입력 한 다음 ENTER 키를 누릅니다.

    **SafeModeAdministratorPassword**

- 암호를 입력 하 고 ENTER 키를 누르면 다음과 같은 확인 메시지가 나타납니다. 같은 암호를 입력 한 다음 ENTER 키를 누릅니다.

    **Jemode관리자 암호 확인:**

- 다음 프롬프트가 표시 되 면 **Y** 문자를 입력 한 다음 enter 키를 누릅니다.


~~~
The target server will be configured as a domain controller and restarted when this operation is complete.
Do you want to continue with this operation?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
~~~

- 원하는 경우 AD DS 및 DNS를 정상적으로 설치 하는 동안 표시 되는 경고 메시지를 읽을 수 있습니다. 이러한 메시지는 일반적 이며 설치 실패를 표시 하지 않습니다.

- 설치가 성공적으로 완료 되 면 컴퓨터를 다시 시작할 수 있도록 컴퓨터를 로그 오프 한다는 메시지가 표시 됩니다. **닫기**를 클릭 하면 컴퓨터에서 즉시 로그 오프 되 고 컴퓨터가 다시 시작 됩니다. **닫기**를 클릭 하지 않으면 기본 시간 후에 컴퓨터가 다시 시작 됩니다.

- 서버를 다시 시작한 후에 Active Directory Domain Services 및 DNS가 성공적으로 설치 되었는지 확인할 수 있습니다. Windows PowerShell을 열고 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.

````
Get-WindowsFeature
````

이 명령의 결과는 Windows PowerShell에 표시 되며 아래 이미지의 결과와 비슷해야 합니다. 설치 된 기술의 경우 기술 이름 왼쪽의 대괄호에는 문자 **X**가 포함 되 고 **설치 상태** 값이 **설치**됩니다.

![Get Add-windowsfeature 명령의 결과](../media/Core-Network-Guide/server-roles-installed.jpg)

**서버 관리자를 사용 하 여 AD DS 및 DNS 설치**

1.  DC1의 **서버 관리자**에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 열립니다.

2.  **시작하기 전**에서 **다음**을 클릭합니다.

    > [!NOTE]
    > 이전에 역할 및 기능 추가 마법사를 실행할 때 **항상 이 페이지 건너뛰기**를 선택한 경우에는 역할 및 기능 추가 마법사의 **시작하기 전** 페이지가 표시되지 않습니다.

3.  **설치 유형 선택**에서 **역할 기반 또는 기능 기반 설치**가 선택되어 있는지 확인하고 **다음**을 클릭합니다.

4.  **대상 서버 선택**에서 **서버 풀에서 서버 선택**이 선택되어 있는지 확인합니다. **서버 풀**에서 로컬 컴퓨터가 선택되어 있는지 확인합니다. **다음**을 클릭합니다.

5.  **서버 역할 선택**의 **역할**에서 **Active Directory Domain Services**를 클릭합니다. **Active Directory Domain Services에 필요한 기능 추가**에서 **기능 추가**를 클릭합니다. **다음**을 클릭합니다.

6.  **기능 선택**에서 **다음**을 클릭하고 **Active Directory Domain Services**에서 제공된 정보를 검토한 후 **다음**을 클릭합니다.

7.  **설치 선택 확인**에서 **설치**를 클릭합니다. 설치 프로세스가 진행되는 동안 설치 진행률 페이지에 상태가 표시됩니다. 설치 프로세스가 완료되면 메시지 정보에서 **이 서버를 도메인 컨트롤러로 승격**을 클릭합니다. Active Directory Domain Services 구성 마법사가 열립니다.

8.  **배포 구성**에서 **새 포리스트 추가**를 선택합니다. **루트 도메인 이름**에, 도메인에 대한 FQDN(정규화된 도메인 이름)을 입력합니다. 예를 들어 FQDN이 corp.contoso.com이면 **corp.contoso.com**을 입력합니다. **다음**을 클릭합니다.

9. **도메인 컨트롤러 옵션**의 **새 포리스트 및 루트 도메인의 기능 수준을 선택합니다.** 에서 사용하려는 포리스트 기능 수준 및 도메인 기능 수준을 선택합니다. **도메인 컨트롤러 기능을 지정합니다.** 에서 **DNS(Domain Name System) 서버** 및 **GC(글로벌 카탈로그)** 가 선택되어 있는지 확인합니다. **암호** 및 **암호 확인**에, 사용하려는 DSRM(디렉터리 서비스 복원 모드) 암호를 입력합니다. **다음**을 클릭합니다.

10. **DNS 옵션**에서 **다음**을 클릭합니다.

11. **추가 옵션**에서 도메인에 할당된 NetBIOS 이름을 확인하고 필요한 경우에만 이 이름을 변경합니다. **다음**을 클릭합니다.

12. **경로**의 **AD DS 데이터베이스, 로그 파일 및 SYSVOL의 위치를 지정합니다.** 에서 다음 중 하나를 수행합니다.

    -   기본값을 적용합니다.

    -   **데이터베이스 폴더**, **로그 파일 폴더** 및 **SYSVOL 폴더**에 사용할 폴더 위치를 입력합니다.

13. **다음**을 클릭합니다.

14. **검토 옵션**에서 선택 항목을 검토합니다.

15. Windows PowerShell 스크립트로 설정을 내보내려면 **스크립트 보기**를 클릭합니다. 스크립트가 메모장에서 열리며, 이 스크립트를 원하는 폴더 위치에 저장할 수 있습니다. **다음**을 클릭합니다. **필수 구성 요소 확인**에서 선택 항목이 확인됩니다. 확인이 완료되면 **설치**를 클릭합니다. Windows에서 메시지가 표시되면 **닫기**를 클릭합니다. 서버를 다시 시작 하 여 AD DS 및 DNS 설치를 완료 합니다.

16. 성공적으로 설치 되었는지 확인 하려면 서버를 다시 시작한 후 서버 관리자 콘솔을 확인 하십시오. 아래 이미지의 강조 표시 된 항목과 같이 AD DS와 DNS 모두 왼쪽 창에 표시 됩니다.

![서버 관리자의 AD DS 및 DNS](../media/Core-Network-Guide/server-roles-installed-sm.jpg)

##### <a name="create-a-user-account-in-active-directory-users-and-computers"></a><a name="BKMK_createUA"></a>Active Directory 사용자 및 컴퓨터에서 사용자 계정 만들기
다음 절차에 따라 Active Directory 사용자 및 컴퓨터 MMC(Microsoft Management Console)에서 새 도메인 사용자 계정을 만들 수 있습니다.

이 절차를 수행하려면 최소한 **Domain Admins** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

> [!NOTE]
> Windows PowerShell을 사용하여 이 절차를 수행하려면 PowerShell을 열고 하나의 행에 다음 cmdlet을 입력한 후 Enter 키를 누릅니다. 이 예제의 사용자 계정 이름을, 사용하려는 값으로 바꾸는 작업도 수행해야 합니다.
>
> `New-ADUser -SamAccountName User1 -AccountPassword (read-host "Set user password" -assecurestring) -name "User1" -enabled $true -PasswordNeverExpires $true -ChangePasswordAtLogon $false`
>
> Enter 키를 누른 후 사용자 계정에 대한 암호를 입력합니다. 계정이 만들어졌으며, 기본적으로 이 계정에는 Domain Users 그룹의 구성원 자격이 부여됩니다.
>
> 다음 cmdlet을 사용하여 새 사용자 계정에 대해 추가 그룹 구성원을 할당할 수 있습니다. 아래 예제에서는 User1을 Domain Admins 및 Enterprise Admins 그룹에 추가합니다. 이 명령을 실행하기 전에 사용자 요구 사항에 맞도록 사용자 계정 이름, 도메인 이름 및 그룹을 변경했는지 확인하십시오.
>
> `Add-ADPrincipalGroupMembership -Identity "CN=User1,CN=Users,DC=corp,DC=contoso,DC=com" -MemberOf "CN=Enterprise Admins,CN=Users,DC=corp,DC=contoso,DC=com","CN=Domain Admins,CN=Users,DC=corp,DC=contoso,DC=com"`

###### <a name="to-create-a-user-account"></a>사용자 계정을 만들려면

1.  DC1의 서버 관리자에서 **도구**, **Active Directory 사용자 및 컴퓨터**를 차례로 클릭합니다. Active Directory 사용자 및 컴퓨터 MMC가 열립니다. 사용자의 도메인 노드가 선택되어 있지 않으면 이 노드를 클릭합니다. 예를 들어 도메인이 corp.contoso.com이면 **corp.contoso.com**을 클릭합니다.

2.  세부 정보 창에서 사용자 계정을 추가할 폴더를 마우스 오른쪽 단추로 클릭합니다.

    **위치?**

    -   사용자 및 컴퓨터/*도메인 노드*/*폴더* Active Directory

3.  **새로 만들기**를 가리킨 다음 **사용자**를 클릭합니다. **새 개체-사용자** 대화 상자가 열립니다.

4.  **이름**에 사용자의 이름을 입력합니다.

5.  **이니셜**에 사용자의 이니셜을 입력합니다.

6.  **성**에 사용자의 성을 입력합니다.

7.  이니셜을 추가하거나 이름과 성의 순서를 바꾸려면 **전체 이름**을 수정합니다.

8.  **사용자 로그온 이름**에 사용자 로그온 이름을 입력하고 **다음**을 클릭합니다.

9. **새 개체 - 사용자**의 **암호** 및 **암호 확인**에 사용자의 암호를 입력한 다음 적절한 암호 옵션을 선택합니다.

10. **다음**을 클릭하고 새 사용자 계정 설정을 검토한 다음 **마침**을 클릭합니다.

##### <a name="assign-group-membership"></a><a name="BKMK_assigngroup"></a>그룹 멤버 자격 할당
다음 절차에 따라 Active Directory 사용자 및 컴퓨터 MMC(Microsoft Management Console)의 그룹에 사용자, 컴퓨터 또는 그룹을 추가할 수 있습니다.

이 절차를 수행하려면 최소한 **Domain Admins** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

###### <a name="to-assign-group-membership"></a>그룹 구성원을 할당하려면

1.  DC1의 서버 관리자에서 **도구**, **Active Directory 사용자 및 컴퓨터**를 차례로 클릭합니다. Active Directory 사용자 및 컴퓨터 MMC가 열립니다. 사용자의 도메인 노드가 선택되어 있지 않으면 이 노드를 클릭합니다. 예를 들어 도메인이 corp.contoso.com이면 **corp.contoso.com**을 클릭합니다.

2.  세부 정보 창에서 구성원을 추가할 그룹이 포함된 폴더를 두 번 클릭합니다.

    선택 위치

    -   **사용자 및 컴퓨터 Active Directory** *그룹을 포함 하는* *도메인 노드*/폴더/

3.  세부 정보 창에서 사용자나 컴퓨터와 같이 그룹에 추가할 개체를 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다. 개체의 **속성** 대화 상자가 열립니다. **소속 그룹** 탭을 클릭합니다.

4.  **소속 그룹** 탭에서 **추가**를 클릭합니다.

5.  **선택할 개체 이름 입력**에 개체를 추가할 그룹의 이름을 입력한 다음 **확인**을 클릭합니다.

6.  기타 사용자, 그룹 또는 컴퓨터에 그룹 구성원을 할당하려면 이 절차의 4 및 5단계를 반복합니다.

##### <a name="configure-a-dns-reverse-lookup-zone"></a><a name="BKMK_reverse"></a>DNS 역방향 조회 영역 구성
다음 절차에 따라 DNS(Domain Name System)에서 역방향 조회 영역을 구성할 수 있습니다.

이 절차를 수행하려면 최소한 **Domain Admins**의 구성원이어야 합니다.

> [!NOTE]
> -   중간 규모 및 대기업의 경우 Active Directory 사용자 및 컴퓨터에서 DNSAdmins 그룹을 구성 하 고 사용 하는 것이 좋습니다. 자세한 내용은 [추가 기술 리소스](#BKMK_resources)를 참조하십시오.
> -   Windows PowerShell을 사용하여 이 절차를 수행하려면 PowerShell을 열고 하나의 행에 다음 cmdlet을 입력한 후 Enter 키를 누릅니다. 이 예제의 DNS 역방향 조회 영역 및 영역 파일 이름을, 사용하려는 값으로 바꾸는 작업도 수행해야 합니다. 역방향 영역 이름에 대한 네트워크 ID를 반대로 지정했는지 확인합니다. 예를 들어 네트워크 ID가 192.168.0 인 경우 역방향 조회 영역 이름 **0.168.192.in-addr**를 만듭니다.
>
> `Add-DnsServerPrimaryZone 0.0.10.in-addr.arpa -ZoneFile 0.0.10.in-addr.arpa.dns`

###### <a name="to-configure-a-dns-reverse-lookup-zone"></a>DNS 역방향 조회 영역을 구성하려면

1.  DC1의 서버 관리자에서 **도구**를 클릭한 다음 **DNS**를 클릭합니다. DNS MMC가 열립니다.

2.  DNS에서 서버 이름을 두 번 클릭하여 트리를 확장합니다(아직 확장되지 않은 경우). 예를 들어 DNS 서버 이름이 DC1이면 **DC1**을 두 번 클릭합니다.

3.  **역방향 조회 영역**을 선택하고 **역방향 조회 영역**을 마우스 오른쪽 단추로 클릭한 다음 **새 영역**을 클릭합니다. 새 영역 마법사가 열립니다.

4.  **새 영역 마법사 시작**에서 **다음**을 클릭합니다.

5.  **영역 형식**에서 **주 영역**을 선택합니다.

6.  DNS 서버가 쓰기 가능한 도메인 컨트롤러인 경우에는 **Active Directory에 영역 저장**이 선택되어 있는지 확인합니다. **다음**을 클릭합니다.

7.  다른 옵션을 선택할 특별한 이유가 없으면 **Active Directory 영역 복제 범위**에서 **이 도메인에 있는 도메인 컨트롤러에서 실행되는 모든 DNS 서버로**를 선택합니다. **다음**을 클릭합니다.

8.  첫 번째 **역방향 조회 영역 이름** 페이지에서 **IPv4 역방향 조회 영역**을 선택합니다. **다음**을 클릭합니다.

9. 두 번째 **역방향 조회 영역 이름** 페이지에서 다음 중 하나를 수행합니다.

    -   **네트워크 ID**에 IP 주소 범위의 네트워크 ID를 입력합니다. 예를 들어 IP 주소 범위가 10.0.0.1 - 10.0.0.254인 경우 **10.0.0**을 입력합니다.

    -   **역방향 조회 영역 이름**에 IPv4 역방향 조회 영역 이름이 자동으로 추가됩니다. **다음**을 클릭합니다.

10. **동적 업데이트**에서 허용할 동적 업데이트 형식을 선택합니다. **다음**을 클릭합니다.

11. **새 영역 마법사 완료**에서 선택 내용을 검토한 다음 **마침**을 클릭합니다.

#### <a name="joining-server-computers-to-the-domain-and-logging-on"></a><a name="BKMK_joinlogserver"></a>도메인에 서버 컴퓨터 가입 및 로그온
Active Directory Domain Services (AD DS)를 설치 하 고 컴퓨터를 도메인에 가입할 수 있는 권한이 있는 사용자 계정을 하나 이상 만든 후에는 핵심 네트워크 서버를 도메인에 가입 하 고 서버에 로그온 하 여 추가 설치를 수행할 수 있습니다. DHCP (Dynamic Host Configuration Protocol)와 같은 기술

AD DS를 실행 하는 서버를 제외 하 고 배포 하는 모든 서버에서 다음을 수행 합니다.

1.  [모든 서버 구성](#BKMK_configuringAll)에서 설명하는 절차를 완료합니다.

2.  다음 두 절차의 지침에 따라 도메인에 서버를 가입하고 서버에 로그온하여 추가 배포 작업을 수행합니다.

> [!NOTE]
> Windows PowerShell을 사용하여 이 절차를 수행하려면 PowerShell을 열고 다음 cmdlet을 입력한 후 Enter 키를 누릅니다. 도메인 이름을, 사용하려는 이름으로 바꾸는 작업도 수행해야 합니다.
>
> `Add-Computer -DomainName corp.contoso.com`
>
> 사용자 이름과 암호를 입력하라는 메시지가 표시되면 컴퓨터를 도메인에 가입할 수 있는 사용 권한을 갖춘 계정의 사용자 이름과 암호를 입력합니다. 컴퓨터를 다시 시작하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.
>
> `Restart-Computer`

###### <a name="to-join-computers-running--windows-server-2016--windows-server-2012-r2--and--windows-server-2012--to-the-domain"></a>Windows server 2016, Windows Server 2012 R2 및 Windows Server 2012를 실행 하는 컴퓨터를 도메인에 가입 시키려면

1.  서버 관리자에서 **로컬 서버**를 클릭합니다. 세부 정보 창에서 **작업 그룹**을 클릭합니다. **시스템 속성** 대화 상자가 열립니다.

2.  **시스템 속성** 대화 상자에서 **변경**을 클릭합니다. **컴퓨터 이름/도메인 변경** 대화 상자가 열립니다.

3.  **컴퓨터 이름**의 **소속 그룹**에서 **도메인**을 클릭한 다음 가입할 도메인 이름을 입력합니다. 예를 들어 도메인 이름이 corp.contoso.com이면 **corp.contoso.com**을 입력합니다.

4.  **확인**을 클릭합니다. **Windows 보안** 대화 상자가 열립니다.

5.  **컴퓨터 이름/도메인 변경**의 **사용자 이름**에 사용자 이름을 입력하고, **암호**에 암호를 입력한 다음 **확인**을 클릭합니다. **컴퓨터 이름/도메인 변경** 대화 상자가 열리고 도메인이 시작됩니다. **확인**을 클릭합니다.

6.  변경 내용을 적용하려면 컴퓨터를 다시 시작해야 한다는 메시지가 **컴퓨터 이름/도메인 변경** 대화 상자에 표시됩니다. **확인**을 클릭합니다.

7.  **시스템 속성** 대화 상자의 **컴퓨터 이름** 탭에서 **닫기**를 클릭합니다. **Microsoft Windows** 대화 상자가 열리고, 변경 내용을 적용하려면 컴퓨터를 다시 시작해야 한다는 메시지가 다시 표시됩니다. **지금 다시 시작**을 클릭합니다.

> [!NOTE]
> 다른 Microsoft 운영 체제를 실행 하는 컴퓨터를 도메인에 가입 하는 방법에 대 한 자세한 내용은 [부록 C-컴퓨터를 도메인에 가입](#BKMK_C)을 참조 하세요.

###### <a name="to-log-on-to-the-domain-using-computers-running-windows-server-2016"></a>Windows Server 2016를 실행 하는 컴퓨터를 사용 하 여 도메인에 로그온 하려면

1.  컴퓨터에서 로그오프하거나 컴퓨터를 다시 시작합니다.

2.  Ctrl+Alt+Del을 누릅니다. 로그온 화면이 표시됩니다.

3.  왼쪽 아래 모서리에서 **기타 사용자**를 클릭 합니다.

4.  **사용자 이름**에 사용자 이름을 입력 합니다.

5.  **암호**에 도메인 암호를 입력한 다음 화살표를 클릭하거나 Enter 키를 누릅니다.

> [!NOTE]
> 다른 Microsoft 운영 체제를 실행 하는 컴퓨터를 사용 하 여 도메인에 로그온 하는 방법에 대 한 자세한 내용은 [부록 D-도메인에 로그온](#BKMK_D)을 참조 하세요.

#### <a name="deploying-dhcp1"></a><a name="BKMK_deployDHCP01"></a>DHCP1 배포
핵심 네트워크의 이 구성 요소를 배포하기 전에 다음을 수행해야 합니다.

-   [모든 서버 구성](#BKMK_configuringAll) 섹션의 단계 수행

-   [도메인에 컴퓨터 가입 및 로그온](#BKMK_joinlogserver) 섹션의 단계 수행

DHCP(Dynamic Host Configuration Protocol) 서버 역할을 실행하는 컴퓨터인 DHCP1을 배포하려면 다음 단계를 순서대로 완료해야 합니다.

-   [DHCP (Dynamic Host Configuration Protocol) 설치](#BKMK_installDHCP)

-   [새 DHCP 범위 만들기 및 활성화](#BKMK_newscopeDHCP)

> [!NOTE]
> Windows PowerShell을 사용하여 이러한 절차를 수행하려면 PowerShell을 열고 별도의 행에 다음 cmdlet을 입력한 후 Enter 키를 누릅니다. 이 예제의 범위 이름, IP 주소 시작 및 끝 범위, 서브넷 마스크 및 기타 값을, 사용하려는 값으로 바꾸는 작업도 수행해야 합니다.
>
> `Install-WindowsFeature DHCP -IncludeManagementTools`
>
> `Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active`
>
> `Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15`
>
> `Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com`
>
> `Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active`
>
> `Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15`
>
> `Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com`
>
> `Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2`
>
> `Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com`

##### <a name="install-dynamic-host-configuration-protocol-dhcp"></a><a name="BKMK_installDHCP"></a>DHCP (Dynamic Host Configuration Protocol) 설치
다음 절차에 따라 역할 및 기능 추가 마법사를 사용하여 DHCP 서버 역할을 설치하고 구성할 수 있습니다.

이 절차를 수행하려면 최소한 **Domain Admins** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

###### <a name="to-install-dhcp"></a>DHCP를 설치하려면

1.  DHCP1의 서버 관리자에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 열립니다.

2.  **시작하기 전**에서 **다음**을 클릭합니다.

    > [!NOTE]
    > 이전에 역할 및 기능 추가 마법사를 실행할 때 **항상 이 페이지 건너뛰기**를 선택한 경우에는 역할 및 기능 추가 마법사의 **시작하기 전** 페이지가 표시되지 않습니다.

3.  **설치 유형 선택**에서 **역할 기반 또는 기능 기반 설치**가 선택되어 있는지 확인하고 **다음**을 클릭합니다.

4.  **대상 서버 선택**에서 **서버 풀에서 서버 선택**이 선택되어 있는지 확인합니다. **서버 풀**에서 로컬 컴퓨터가 선택되어 있는지 확인합니다. **다음**을 클릭합니다.

5.  **서버 역할 선택**의 **역할**에서 **DHCP 서버**를 선택 합니다. **DHCP 서버에 필요한 기능 추가**에서 **기능 추가**를 클릭합니다. **다음**을 클릭합니다.

6.  **기능 선택**에서 **다음**을 클릭하고 **DHCP 서버**에서 제공된 정보를 검토한 후 **다음**을 클릭합니다.

7.  **설치 선택 확인**에서 **필요한 경우 자동으로 대상 서버 다시 시작**을 클릭합니다. 이 선택을 확인하라는 메시지가 표시되면 **예**를 클릭한 다음 **설치**를 클릭합니다. 설치 **진행률** 페이지에는 설치 과정 중에 상태가 표시 됩니다. 프로세스가 완료 되 면 "구성이 필요 합니다. *Computername*에서 설치가 완료 되었습니다. "가 표시 됩니다. 여기서 *ComputerName* 은 DHCP 서버를 설치한 컴퓨터의 이름입니다. 메시지 창에서 **DHCP 구성 완료**를 클릭합니다. DHCP 설치 후 구성 마법사가 열립니다. **다음**을 클릭합니다.

8.  **권한 부여**에서 Active Directory Domain Services의 DHCP 서버에 대해 권한을 부여하는 데 사용할 자격 증명을 지정한 다음 **커밋**을 클릭합니다. 권한 부여가 완료되면 **닫기**를 클릭합니다.

##### <a name="create-and-activate-a-new-dhcp-scope"></a><a name="BKMK_newscopeDHCP"></a>새 DHCP 범위 만들기 및 활성화
다음 절차에 따라 DHCP MMC(Microsoft Management Console)를 사용하여 새 DHCP 범위를 만들 수 있습니다. 절차가 완료되면 범위가 활성화되고, 만든 제외 범위를 통해 고정 IP 주소가 필요한 서비스 및 기타 디바이스를 정적으로 구성하는 데 사용하는 IP 주소를 DHCP 서버에서 대여하지 않도록 할 수 있습니다.

이 절차를 수행하려면 최소한 **DHCP 관리자** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

###### <a name="to-create-and-activate-a-new-dhcp-scope"></a>새 DHCP 범위를 만들고 활성화하려면

1.  DHCP1의 서버 관리자에서 **도구**를 클릭한 다음 **DHCP**를 클릭합니다. DHCP MMC가 열립니다.

2.  **DHCP**에서 서버 이름을 확장 합니다. 예를 들어 DHCP 서버 이름이 DHCP1.corp.contoso.com 인 경우 **DHCP1.corp.contoso.com**옆에 있는 아래쪽 화살표를 클릭 합니다.

3.  서버 이름 아래에서 **IPv4**를 마우스 오른쪽 단추로 클릭 한 다음 **새 범위**를 클릭 합니다. 새 범위 마법사가 열립니다.

4.  **새 범위 마법사 시작**에서 **다음**을 클릭합니다.

5.  **범위 이름**의 **이름**에 범위 이름을 입력합니다. 예를 들어 **서브넷 1**을 입력합니다.

6.  **설명**에, 새 범위에 대한 설명을 입력하고 **다음**을 클릭합니다.

7.  **IP 주소 범위**에서 다음을 수행합니다.

    1.  **시작 IP 주소**에 범위의 첫 번째 IP 주소인 IP 주소를 입력합니다. 예를 들어 **10.0.0.1**를 입력합니다.

    2.  **끝 IP 주소**에 범위의 마지막 IP 주소인 IP 주소를 입력합니다. 예를 들어 **10.0.0.254**을 입력 합니다. **길이** 및 **서브넷 마스크** 값은 **시작 IP 주소**에 입력한 IP 주소를 바탕으로 자동으로 입력됩니다.

    3.  필요한 경우 주소 지정 구성에 맞게 **길이** 또는 **서브넷 마스크**의 값을 적절하게 수정합니다.

    4.  **다음**을 클릭합니다.

8.  **제외 주소 추가**에서 다음을 수행합니다.

    1.  **시작 IP 주소**에 제외 범위의 첫 번째 IP 주소인 IP 주소를 입력합니다. 예를 들어 **10.0.0.1**를 입력합니다.

    2.  **끝 IP 주소**에 제외 범위의 마지막 IP 주소인 IP 주소를 입력합니다. 예를 들어 **10.0.0.15**를 입력합니다.

9. **추가**를 클릭하고 **다음**을 클릭합니다.

10. **임대 기간**에서 **일**, **시간** 및 **분**의 기본값을 네트워크에 맞게 수정하고 **다음**을 클릭합니다.

11. **DHCP 옵션을 구성합니다.** 에서 **예, 지금 구성합니다.** 를 선택하고 **다음**을 클릭합니다.

12. **라우터(기본 게이트웨이)** 에서 다음 중 하나를 수행합니다.

    -   네트워크에 라우터가 없는 경우에는 **다음**을 클릭합니다.

    -   **IP 주소**에 라우터 또는 기본 게이트웨이의 IP 주소를 입력합니다. 예를 들어 **10.0.0.1**를 입력합니다. **추가**를 클릭하고 **다음**을 클릭합니다.

13. **도메인 이름 및 DNS 서버**에서 다음을 수행합니다.

    1.  **부모 도메인**에, 클라이언트가 이름을 확인하는 데 사용하는 DNS 도메인의 이름을 입력합니다. 예를 들어 **corp.contoso.com**을 입력합니다.

    2.  **서버 이름**에, 클라이언트가 이름을 확인하는 데 사용하는 DNS 컴퓨터의 이름을 입력합니다. 예를 들어 **DC1**을 입력합니다.

    3.  **해결**을 클릭합니다. DNS 서버의 IP 주소가 **IP 주소**에 추가됩니다. **추가**를 클릭하고 DNS 서버 IP 주소 유효성 검사가 완료될 때까지 기다린 후 **다음**을 클릭합니다.

14. 네트워크에 WINS 서버가 없으므로 **WINS 서버**에서 **다음**을 클릭합니다.

15. **범위 활성화**에서 **예, 지금 활성화합니다.** 를 선택합니다.

16. **다음**을 클릭하고 **마침**을 클릭합니다.

> [!IMPORTANT]
> 추가 서브넷에 대해 새 범위를 만들려면 위의 절차를 반복합니다. 배포하려는 각 서브넷에 대해 서로 다른 IP 주소를 사용하고 DHCP 메시지가 다른 서브넷으로 전달되도록, DHCP 메시지 전달이 모든 라우터에서 사용하도록 설정되어 있는지 확인합니다.

### <a name="joining-client-computers-to-the-domain-and-logging-on"></a><a name="BKMK_joinlogclients"></a>도메인에 클라이언트 컴퓨터 가입 및 로그온

> [!NOTE]
> Windows PowerShell을 사용하여 이 절차를 수행하려면 PowerShell을 열고 다음 cmdlet을 입력한 후 Enter 키를 누릅니다. 도메인 이름을, 사용하려는 이름으로 바꾸는 작업도 수행해야 합니다.
>
> `Add-Computer -DomainName corp.contoso.com`
>
> 사용자 이름과 암호를 입력하라는 메시지가 표시되면 컴퓨터를 도메인에 가입할 수 있는 사용 권한을 갖춘 계정의 사용자 이름과 암호를 입력합니다. 컴퓨터를 다시 시작하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.
>
> `Restart-Computer`

##### <a name="to-join-computers-running-windows-10-to-the-domain"></a>Windows 10을 실행 하는 컴퓨터를 도메인에 가입 시키려면

1.  로컬 Administrator 계정을 사용하여 컴퓨터에 로그온합니다.

2.  **웹 및 Windows 검색**에서 **System**을 입력 합니다. 검색 결과에서 **시스템 (제어판)** 을 클릭 합니다. **시스템** 대화 상자가 열립니다.

3.  **시스템**에서 **고급 시스템 설정**을 클릭 합니다. **시스템 속성** 대화 상자가 열립니다. **컴퓨터 이름** 탭을 클릭 합니다.

4.  **컴퓨터 이름**에서 **변경**을 클릭 합니다. **컴퓨터 이름/도메인 변경** 대화 상자가 열립니다.

5.  **컴퓨터 이름/도메인 변경** 의 **소속 그룹**에서 **도메인**을 클릭 한 다음 가입 하려는 도메인의 이름을 입력 합니다. 예를 들어 도메인 이름이 corp.contoso.com이면 **corp.contoso.com**을 입력합니다.

6.  **확인**을 클릭합니다. **Windows 보안** 대화 상자가 열립니다.

7.  **컴퓨터 이름/도메인 변경**의 **사용자 이름**에 사용자 이름을 입력하고, **암호**에 암호를 입력한 다음 **확인**을 클릭합니다. **컴퓨터 이름/도메인 변경** 대화 상자가 열리고 도메인이 시작됩니다. **확인**을 클릭합니다.

8.  변경 내용을 적용하려면 컴퓨터를 다시 시작해야 한다는 메시지가 **컴퓨터 이름/도메인 변경** 대화 상자에 표시됩니다. **확인**을 클릭합니다.

9. **시스템 속성** 대화 상자의 **컴퓨터 이름** 탭에서 **닫기**를 클릭합니다. **Microsoft Windows** 대화 상자가 열리고, 변경 내용을 적용하려면 컴퓨터를 다시 시작해야 한다는 메시지가 다시 표시됩니다. **지금 다시 시작**을 클릭합니다.

##### <a name="to-join-computers-running-windows-81-to-the-domain"></a>Windows 8.1를 실행 하는 컴퓨터를 도메인에 가입 시키려면

1.  로컬 Administrator 계정을 사용하여 컴퓨터에 로그온합니다.

2.  **시작**을 마우스 오른쪽 단추로 클릭 한 다음 **시스템**을 클릭 합니다. **시스템** 대화 상자가 열립니다.

3.  **시스템**에서 **고급 시스템 설정**을 클릭 합니다. **시스템 속성** 대화 상자가 열립니다. **컴퓨터 이름** 탭을 클릭 합니다.

4.  **컴퓨터 이름**에서 **변경**을 클릭 합니다. **컴퓨터 이름/도메인 변경** 대화 상자가 열립니다.

5.  **컴퓨터 이름/도메인 변경** 의 **소속 그룹**에서 **도메인**을 클릭 한 다음 가입 하려는 도메인의 이름을 입력 합니다. 예를 들어 도메인 이름이 corp.contoso.com이면 **corp.contoso.com**을 입력합니다.

6.  **확인**을 클릭합니다. **Windows 보안** 대화 상자가 열립니다.

7.  **컴퓨터 이름/도메인 변경**의 **사용자 이름**에 사용자 이름을 입력하고, **암호**에 암호를 입력한 다음 **확인**을 클릭합니다. **컴퓨터 이름/도메인 변경** 대화 상자가 열리고 도메인이 시작됩니다. **확인**을 클릭합니다.

8.  변경 내용을 적용하려면 컴퓨터를 다시 시작해야 한다는 메시지가 **컴퓨터 이름/도메인 변경** 대화 상자에 표시됩니다. **확인**을 클릭합니다.

9. **시스템 속성** 대화 상자의 **컴퓨터 이름** 탭에서 **닫기**를 클릭합니다. **Microsoft Windows** 대화 상자가 열리고, 변경 내용을 적용하려면 컴퓨터를 다시 시작해야 한다는 메시지가 다시 표시됩니다. **지금 다시 시작**을 클릭합니다.

##### <a name="to-log-on-to-the-domain-using-computers-running-windows-10"></a>Windows 10을 실행 하는 컴퓨터를 사용 하 여 도메인에 로그온 하려면

1.  컴퓨터에서 로그오프하거나 컴퓨터를 다시 시작합니다.

2.  Ctrl+Alt+Del을 누릅니다. 로그온 화면이 표시됩니다.

3.  왼쪽 아래에서 **기타 사용자**를 클릭 합니다.

4.  **사용자 이름**에, 도메인과 사용자 이름을 *도메인\사용자* 형식으로 입력합니다. 예를 들어 **User-01**이라는 계정을 사용하여 도메인 corp.contoso.com에 로그온하려면 **CORP\User-01**을 입력합니다.

5.  **암호**에 도메인 암호를 입력한 다음 화살표를 클릭하거나 Enter 키를 누릅니다.

### <a name="deploying-optional-features-for-network-access-authentication-and-web-services"></a><a name="BKMK_optionalfeatures"></a>네트워크 액세스 인증 및 웹 서비스에 대 한 선택적 기능 배포
핵심 네트워크를 설치한 후 무선 액세스 지점이 나 VPN 서버와 같은 네트워크 액세스 서버를 배포 하려는 경우 NPS와 웹 서버를 모두 배포 하는 것이 좋습니다. 네트워크 액세스 배포의 경우 보안 인증서 기반 인증 방법을 사용하는 것이 좋습니다. NPS를 사용하여 네트워크 액세스 정책을 관리하고 보안 인증 방법을 배포할 수 있습니다. 웹 서버를 사용하여 보안 인증에 대한 인증서를 제공하는 CA(인증 기관)의 CRL(인증서 해지 목록)을 게시할 수 있습니다.

> [!NOTE]
> 핵심 네트워크 부록 가이드를 사용하여 서버 인증서 및 기타 추가 기능을 배포할 수 있습니다. 자세한 내용은 [추가 기술 리소스](#BKMK_resources)를 참조하십시오.

다음 그림에서는 추가 된 NPS 및 웹 서버가 있는 Windows Server Core 네트워크 토폴로지를 보여 줍니다.

![추가 된 NPS 및 웹 서버가 포함 된 Windows Server Core 네트워크 토폴로지](../media/Core-Network-Guide/cng16_overview_2.jpg)

다음 섹션에는 네트워크에 NPS 및 웹 서버를 추가하는 방법에 대한 설명이 나와 있습니다.

-   [NPS1 배포](#BKMK_deployNPS1)

-   [WEB1 배포](#BKMK_IIS)

#### <a name="deploying-nps1"></a><a name="BKMK_deployNPS1"></a>NPS1 배포
NPS(네트워크 정책 서버) 서버는 VPN(가상 사설망) 서버, 무선 액세스 지점 및 802.1X 인증 스위치와 같은 다른 네트워크 액세스 기술을 배포하기 위한 준비 단계로 설치합니다.

NPS (네트워크 정책 서버)를 사용 하면 다음 기능을 사용 하 여 네트워크 정책을 중앙에서 구성 하 고 관리할 수 있습니다. RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 서버 및 RADIUS 프록시.

NPS는 핵심 네트워크의 선택적 구성 요소이지만 다음 중 한 가지라도 해당하는 경우에는 NPS를 설치해야 합니다.

-   RADIUS 프로토콜과 호환 되는 원격 액세스 서버 (예: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행 하는 컴퓨터)를 포함 하도록 네트워크를 확장할 계획입니다. 라우팅 및 원격 액세스 서비스, 터미널 서비스 게이트웨이 또는 원격 데스크톱 게이트웨이 합니다.


-   유선 또는 무선 액세스에 대해 802.1 X 인증을 배포할 계획입니다.

이 역할 서비스를 배포 하기 전에 NPS로 구성 하는 컴퓨터에서 다음 단계를 수행 해야 합니다.

-   [모든 서버 구성](#BKMK_configuringAll) 섹션의 단계 수행

-   [도메인에 컴퓨터 가입 및 로그온](#BKMK_joinlogserver) 섹션의 단계 수행

네트워크 정책 및 액세스 서비스 서버 역할의 NPS(네트워크 정책 서버) 역할 서비스를 실행하는 컴퓨터인 NPS1을 배포하려면 다음 단계를 완료해야 합니다.

-   [NPS1 배포 계획](#bkmk_NetFndtn_Pln_NPS-01)

-   [NPS (네트워크 정책 서버) 설치](#BKMK_installNPS)

-   [기본 도메인에 NPS 등록](#BKMK_registerNPS)

> [!NOTE]
> 이 가이드에서는 독립 실행형 서버 또는 NPS1 이라는 VM에 NPS를 배포 하기 위한 지침을 제공 합니다.  또 다른 권장 되는 배포 모델은 도메인 컨트롤러에 NPS를 설치 하는 것입니다. 독립 실행형 서버 대신 도메인 컨트롤러에 NPS를 설치 하려는 경우에는 d c 1에 NPS를 설치 합니다.

##### <a name="planning-the-deployment-of-nps1"></a><a name="bkmk_NetFndtn_Pln_NPS-01"></a>NPS1 배포 계획
핵심 네트워크 설치 후 무선 액세스 지점이나 VPN 서버와 같은 네트워크 액세스 서버를 배포하려는 경우에는 NPS를 배포하는 것이 좋습니다.

NPS를 RADIUS(Remote Authentication Dial-In User Service) 서버로 사용하는 경우 NPS에서 네트워크 액세스 서버를 통해 연결 요청을 인증하고 권한 부여합니다. 또한 NPS를 사용하면 네트워크에 액세스할 수 있는 사용자, 네트워크에 액세스할 수 있는 방법 및 네트워크에 액세스할 수 있는 시기를 결정하는 네트워크 정책을 중앙에서 구성하고 관리할 수 있습니다.

다음은 NPS를 설치하기 전에 주요 계획 단계입니다.

- 사용자 계정 데이터베이스 계획을 세웁니다. 기본적으로 NPS를 실행 하는 서버를 Active Directory 도메인에 가입 하면 NPS는 AD DS 사용자 계정 데이터베이스를 사용 하 여 인증 및 권한 부여를 수행 합니다. NPS를 RADIUS 프록시로 사용하여 연결 요청을 다른 RADIUS 서버로 전달하는 대규모 네트워크와 같은 경우에는 도메인 구성원이 아닌 컴퓨터에 NPS를 설치할 수 있습니다.

- RADIUS 계정 구성을 계획합니다. NPS에서는 계정 데이터를 SQL Server 데이터베이스 또는 로컬 컴퓨터의 텍스트 파일로 기록할 수 있습니다. SQL Server 로깅을 사용하려는 경우에는 SQL Server를 실행하는 서버의 설치와 구성을 계획합니다.

##### <a name="install-network-policy-server-nps"></a><a name="BKMK_installNPS"></a>NPS (네트워크 정책 서버) 설치
역할 및 기능 추가 마법사를 사용 하 여 NPS (네트워크 정책 서버)를 설치 하려면이 절차를 사용할 수 있습니다. NPS는 네트워크 정책 및 액세스 서비스 서버 역할의 역할 서비스입니다.

> [!NOTE]
> 기본적으로 NPS는 설치된 모든 네트워크 어댑터의 포트 1812, 1813, 1645 및 1646에서 RADIUS 트래픽을 수신 대기합니다. NPS를 설치할 때 고급 보안이 포함 된 Windows 방화벽을 사용 하는 경우 인터넷 프로토콜 버전 6 \(IPv6\)와 IPv4 트래픽 모두에 대 한 설치 프로세스 중에 이러한 포트에 대 한 방화벽 예외가 자동으로 생성 됩니다. 네트워크 액세스 서버가 이러한 기본값 이외의 포트를 통해 RADIUS 트래픽을 보내도록 구성 된 경우에는 NPS 설치 중에 고급 보안이 설정 된 Windows 방화벽에서 생성 된 예외를 제거 하 고에서 사용 하는 포트에 대 한 예외를 만듭니다. RADIUS 트래픽

**관리 자격 증명**

이 절차를 완료하려면 **Domain Admins** 그룹의 구성원이어야 합니다.

> [!NOTE]
> Windows PowerShell을 사용하여 이 절차를 수행하려면 PowerShell을 열고 다음을 입력한 후 Enter 키를 누릅니다.
>
> `Install-WindowsFeature NPAS -IncludeManagementTools`

###### <a name="to-install-nps"></a>NPS를 설치하려면

1.  NPS1의 서버 관리자에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 열립니다.

2.  **시작하기 전**에서 **다음**을 클릭합니다.

    > [!NOTE]
    > 이전에 역할 및 기능 추가 마법사를 실행할 때 **항상 이 페이지 건너뛰기**를 선택한 경우에는 역할 및 기능 추가 마법사의 **시작하기 전** 페이지가 표시되지 않습니다.

3.  **설치 유형 선택**에서 **역할 기반 또는 기능 기반 설치**가 선택되어 있는지 확인하고 **다음**을 클릭합니다.

4.  **대상 서버 선택**에서 **서버 풀에서 서버 선택**이 선택되어 있는지 확인합니다. **서버 풀**에서 로컬 컴퓨터가 선택되어 있는지 확인합니다. **다음**을 클릭합니다.

5.  **서버 역할 선택**의 **역할**에서 **네트워크 정책 및 액세스 서비스**를 선택 합니다. 네트워크 정책 및 액세스 서비스에 필요한 기능을 추가 해야 하는지 여부를 묻는 대화 상자가 열립니다. **기능 추가**를 클릭한 후 **다음**을 클릭합니다.

6.  **기능 선택**에서 **다음**을 클릭하고 **네트워크 정책 및 액세스 서비스**에서 제공된 정보를 검토한 후 **다음**을 클릭합니다.

7.  **역할 서비스 선택**에서 **네트워크 정책 서버**를 클릭합니다.  **네트워크 정책 서버에 필요한 기능 추가**에서 **기능 추가**를 클릭합니다. **다음**을 클릭합니다.

8.  **설치 선택 확인**에서 **필요한 경우 자동으로 대상 서버 다시 시작**을 클릭합니다. 이 선택을 확인하라는 메시지가 표시되면 **예**를 클릭한 다음 **설치**를 클릭합니다. 설치 프로세스가 진행되는 동안 설치 진행률 페이지에 상태가 표시됩니다. 프로세스가 완료 되 면 " *computername*에서 설치가 완료 되었습니다." 라는 메시지가 표시 됩니다. 여기서 *Computername* 은 네트워크 정책 서버를 설치한 컴퓨터의 이름입니다. **닫기**를 클릭합니다.

##### <a name="register-the-nps-in-the-default-domain"></a><a name="BKMK_registerNPS"></a>기본 도메인에 NPS 등록
이 절차를 사용 하 여 서버가 도메인 구성원 인 도메인에 NPS를 등록할 수 있습니다.

NPSs는 권한 부여 프로세스 동안 사용자 계정의 전화 접속 속성을 읽을 수 있는 권한을 갖도록 Active Directory에 등록 되어야 합니다. NPS를 등록 하면 서버가 Active Directory의 **RAS 및 IAS 서버** 그룹에 추가 됩니다.

**관리 자격 증명**

이 절차를 완료하려면 **Domain Admins** 그룹의 구성원이어야 합니다.

> [!NOTE]
> Windows PowerShell 내에서 Netsh (네트워크 셸) 명령을 사용 하 여이 절차를 수행 하려면 PowerShell을 열고 다음을 입력 한 다음 ENTER 키를 누릅니다.
>
> `netsh nps add registeredserver domain=corp.contoso.com server=NPS1.corp.contoso.com`

###### <a name="to-register-an-nps-in-its-default-domain"></a>기본 도메인에 NPS를 등록 하려면

1.  NPS1의 서버 관리자에서 도구를 클릭한 다음 **네트워크 정책 서버**를 클릭합니다. 네트워크 정책 서버 MMC가 열립니다.

2.  **NPS(로컬)** 를 마우스 오른쪽 단추로 클릭한 다음 **Active Directory에 서버 등록**을 클릭합니다. **네트워크 정책 서버** 대화 상자가 열립니다.

3.  **네트워크 정책 서버**에서 **확인**을 클릭한 다음 **확인**을 다시 클릭합니다.

네트워크 정책 서버에 대 한 자세한 내용은 [NPS (네트워크 정책 서버)](../technologies/nps/nps-top.md)를 참조 하세요.

#### <a name="deploying-web1"></a><a name="BKMK_IIS"></a>WEB1 배포

Windows Server 2016의 웹 서버 (IIS) 역할은 웹 사이트, 서비스 및 응용 프로그램을 안정적으로 호스팅하기 위한 안전 하 고 확장 가능 하며 관리 하기 쉬운 모듈식 플랫폼을 제공 합니다. 인터넷 정보 서비스 (IIS)를 사용 하 여 인터넷, 인트라넷 또는 엑스트라넷의 사용자와 정보를 공유할 수 있습니다. IIS는 IIS, ASP.NET, FTP 서비스, PHP 및 WCF (Windows Communication Foundation)를 통합 하는 통합 웹 플랫폼입니다.

웹 서버 (IIS) 서버 역할을 사용 하 여 도메인 구성원 컴퓨터에서 액세스할 수 있도록 CRL을 게시 하는 것 외에도 웹 서버 (IIS) 서버 역할을 사용 하면 여러 웹 사이트, 웹 응용 프로그램 및 FTP 사이트를 설정 하 고 관리할 수 있습니다. 또한 IIS는 다음과 같은 이점을 제공 합니다.

-   서버 공간 감소 및 자동 애플리케이션 격리를 통해 웹 보안을 최대화할 수 있습니다.

-   ASP.NET, 클래식 ASP 및 PHP 웹 애플리케이션을 같은 서버에서 쉽게 배포 및 실행할 수 있습니다.

-   작업자 프로세스에 고유한 ID 및 샌드박스 구성을 기본적으로 제공하여 애플리케이션을 격리함으로써 보안 위험을 더욱 줄입니다.

-   고객의 요구 사항에 적합한 사용자 지정 모듈을 통해 기본 제공 IIS 구성 요소를 쉽게 추가, 제거 및 교체할 수 있습니다.

-   기본 제공되는 동적 캐싱 및 향상된 압축 기능을 통해 웹 사이트의 속도를 높일 수 있습니다.

웹 서버(IIS) 서버 역할을 실행하는 컴퓨터인 WEB1을 배포하려면 다음을 수행해야 합니다.

-   [모든 서버 구성](#BKMK_configuringAll) 섹션의 단계 수행

-   [도메인에 컴퓨터 가입 및 로그온](#BKMK_joinlogserver) 섹션의 단계 수행

-   [웹 서버 (IIS) 서버 역할을 설치 합니다.](#BKMK_install_IIS)

##### <a name="install-the-web-server-iis-server-role"></a><a name="BKMK_install_IIS"></a>웹 서버 (IIS) 서버 역할을 설치 합니다.
이 절차를 완료하려면 **Administrators** 그룹의 구성원이어야 합니다.

> [!NOTE]
> Windows PowerShell을 사용하여 이 절차를 수행하려면 PowerShell을 열고 다음을 입력한 후 Enter 키를 누릅니다.
>
> `Install-WindowsFeature Web-Server -IncludeManagementTools`

1.  **서버 관리자**에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 열립니다.

2.  **시작하기 전**에서 **다음**을 클릭합니다.

    > [!NOTE]
    > 이전에 역할 및 기능 추가 마법사를 실행할 때 **항상 이 페이지 건너뛰기**를 선택한 경우에는 역할 및 기능 추가 마법사의 **시작하기 전** 페이지가 표시되지 않습니다.

3.  **설치 유형 선택** 페이지에서 **다음**을 클릭 합니다.

4.  **대상 서버 선택** 페이지에서 로컬 컴퓨터가 선택 되어 있는지 확인 하 고 **다음**을 클릭 합니다.

5.  **서버 역할 선택** 페이지에서를 스크롤하고 **웹 서버 (IIS)** 를 선택 합니다. **웹 서버 (IIS)에 필요한 기능 추가** 대화 상자가 열립니다. **기능 추가**를 클릭한 후 **다음**을 클릭합니다.

6.  기본 웹 서버 설정이 모두 적용될 때까지 **다음**을 클릭한 후 **설치**를 클릭합니다.

7.  모든 설치가 완료되었는지 확인한 다음 **닫기**를 클릭합니다.

## <a name="additional-technical-resources"></a><a name="BKMK_resources"></a>추가 기술 리소스
이 가이드의 기술에 대한 자세한 내용은 다음 리소스를 참조하십시오.

 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012 기술 라이브러리 리소스

-   [Windows Server 2016에 Active Directory Domain Services (AD DS)의 새로운 기능](https://technet.microsoft.com/library/mt163897.aspx)

-   https://technet.microsoft.com/library/hh831484.aspx[개요를 Active Directory Domain Services](https://technet.microsoft.com/library/hh831484.aspx) 합니다.

-   https://technet.microsoft.com/library/hh831667.aspx[DNS (Domain Name System) 개요](https://technet.microsoft.com/library/hh831667.aspx)

-   [DNS 관리자 역할 구현](https://technet.microsoft.com/library/cc756152(WS.10).aspx)

-   [DHCP (Dynamic Host Configuration Protocol) 개요](https://technet.microsoft.com/library/hh831825.aspx) https://technet.microsoft.com/library/hh831825.aspx.

-   https://technet.microsoft.com/library/hh831683.aspx에서 [네트워크 정책 및 액세스 서비스 개요](https://technet.microsoft.com/library/hh831683.aspx) 를 사용 합니다.

-   [웹 서버 (IIS) 개요](https://technet.microsoft.com/library/hh831725.aspx) https://technet.microsoft.com/library/hh831725.aspx.

## <a name="appendices-a-through-e"></a><a name="BKMK_appendix"></a>부록 A ~ E
다음 섹션에는 Windows Server 2016, Windows 10, Windows Server 2012 및 Windows 8이 아닌 다른 운영 체제를 실행 하는 컴퓨터에 대 한 추가 구성 정보가 포함 되어 있습니다. 또한 배포를 지원 하기 위한 네트워크 준비 워크시트도 제공 됩니다.

1.  [부록 A-컴퓨터 이름 바꾸기](#BKMK_A)

2.  [부록 B-고정 IP 주소 구성](#BKMK_B)

3.  [부록 C-도메인에 컴퓨터 가입](#BKMK_C)

4.  [부록 D-도메인에 로그온](#BKMK_D)

5.  [부록 E-핵심 네트워크 계획 준비 시트](#BKMK_E)

## <a name="appendix-a---renaming-computers"></a><a name="BKMK_A"></a>부록 A-컴퓨터 이름 바꾸기
이 섹션의 절차를 사용 하 여 Windows Server 2008 R2, Windows 7, Windows Server 2008 및 Windows Vista를 실행 하는 컴퓨터에 다른 컴퓨터 이름을 제공할 수 있습니다.

-   [Windows Server 2008 R2 및 Windows 7](#bkmk_NetFndtn_Pln_rename_R2)

-   [Windows Server 2008 및 Windows Vista](#bkmk_NetFndtn_Pln_Renam08)

### <a name="windows-server-2008-r2-and-windows-7"></a><a name="bkmk_NetFndtn_Pln_rename_R2"></a>Windows Server 2008 R2 및 Windows 7
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

##### <a name="to-rename-computers-running-windows-server-2008-r2-and-windows-7"></a>Windows Server 2008 R2 및 Windows 7을 실행하는 컴퓨터의 이름을 바꾸려면

1.  **시작**을 클릭하고 **컴퓨터**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. **시스템** 대화 상자가 열립니다.

2.  **컴퓨터 이름, 도메인 및 작업 그룹 설정**에서 **설정 변경**을 클릭합니다. **시스템 속성** 대화 상자가 열립니다.

    > [!NOTE]
    > Windows 7을 실행 하는 컴퓨터에서 **시스템 속성** 대화 상자가 열리기 전에 **사용자 계정 컨트롤** 대화 상자가 열리고 계속할 수 있는 권한을 요청 합니다. 계속하려면 **계속**을 클릭합니다.

3.  **변경**을 클릭합니다. **컴퓨터 이름/도메인 변경** 대화 상자가 열립니다.

4.  **컴퓨터 이름**에 컴퓨터 이름을 입력합니다. 예를 들어 컴퓨터 이름을 DC1로 지정하려면 **DC1**을 입력합니다.

5.  **확인**을 차례로 두 번 클릭하고 **닫기**를 클릭한 다음 **지금 다시 시작**을 클릭하여 컴퓨터를 다시 시작합니다.

### <a name="windows-server-2008-and-windows-vista"></a><a name="bkmk_NetFndtn_Pln_Renam08"></a>Windows Server 2008 및 Windows Vista
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

##### <a name="to-rename-computers-running-windows-server-2008-and-windows-vista"></a>Windows Server 2008 및 Windows Vista를 실행 하는 컴퓨터의 이름을 바꾸려면

1.  **시작**을 클릭하고 **컴퓨터**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. **시스템** 대화 상자가 열립니다.

2.  **컴퓨터 이름, 도메인 및 작업 그룹 설정**에서 **설정 변경**을 클릭합니다. **시스템 속성** 대화 상자가 열립니다.

    > [!NOTE]
    > Windows Vista를 실행 하는 컴퓨터에서 **시스템 속성** 대화 상자가 열리기 전에 **사용자 계정 컨트롤** 대화 상자가 열리고 계속할 수 있는 권한을 요청 합니다. 계속하려면 **계속**을 클릭합니다.

3.  **변경**을 클릭합니다. **컴퓨터 이름/도메인 변경** 대화 상자가 열립니다.

4.  **컴퓨터 이름**에 컴퓨터 이름을 입력합니다. 예를 들어 컴퓨터 이름을 DC1로 지정하려면 **DC1**을 입력합니다.

5.  **확인**을 차례로 두 번 클릭하고 **닫기**를 클릭한 다음 **지금 다시 시작**을 클릭하여 컴퓨터를 다시 시작합니다.

## <a name="appendix-b---configuring-static-ip-addresses"></a><a name="BKMK_B"></a>부록 B-고정 IP 주소 구성
이 항목에서는 다음 운영 체제를 실행하는 컴퓨터에 대해 고정 IP 주소를 구성하는 절차를 설명합니다.

-   [Windows Server 2008 R2](#bkmk_R2Cng_WS08R2IP)

-   [Windows Server 2008](#bkmk_NetFndtn_Pln_CfgStatic08)

### <a name="windows-server-2008-r2"></a><a name="bkmk_R2Cng_WS08R2IP"></a>Windows Server 2008 R2
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.

##### <a name="to-configure-a-static-ip-address-on-a-computer-running-windows-server-2008-r2"></a>Windows Server 2008 R2를 실행하는 컴퓨터에 대해 고정 IP 주소를 구성하려면

1.  **시작**을 클릭하고 **제어판**을 클릭합니다.

2.  **제어판**에서 **네트워크 및 인터넷**을 클릭합니다. **네트워크 및 인터넷**이 열립니다.

    **네트워크 및 인터넷**에서 **네트워크 및 공유 센터**를 클릭합니다. **네트워크 및 공유 센터**가 열립니다.

3.  **네트워크 및 공유 센터**에서 **어댑터 설정 변경**을 클릭합니다. **네트워크 연결**이 열립니다.

4.  **네트워크 연결**에서 구성할 네트워크 연결을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

5.  **로컬 영역 연결 속성**의 **이 연결에 다음 항목 사용**에서 **Internet Protocol Version 4(TCP/IPv4)** 를 선택하고 **속성**을 클릭합니다. **Internet Protocol Version 4(TCP/IPv4) 속성** 대화 상자가 열립니다.

6.  **Internet Protocol Version 4(TCP/IPv4) 속성**의 **일반** 탭에서 **다음 IP 주소 사용**을 클릭합니다. **IP 주소**에, 사용할 IP 주소를 입력합니다.

7.  Tab 키를 눌러 **서브넷 마스크**에 커서를 놓습니다. 서브넷 마스크의 기본값이 자동으로 입력됩니다. 기본 서브넷 마스크를 그대로 사용하거나 사용할 서브넷 마스크를 입력합니다.

8.  **기본 게이트웨이**에 기본 게이트웨이의 IP 주소를 입력합니다.

9. **기본 설정 DNS 서버**에 DNS 서버의 IP 주소를 입력합니다. 로컬 컴퓨터를 기본 설정 DNS 서버로 사용하려는 경우 로컬 컴퓨터의 IP 주소를 입력합니다.

10. **대체 DNS 서버**에 대체 DNS 서버(있는 경우)의 IP 주소를 입력합니다. 로컬 컴퓨터를 대체 DNS 서버로 사용하려는 경우 로컬 컴퓨터의 IP 주소를 입력합니다.

11. **확인**을 클릭한 다음 **닫기**를 클릭합니다.

### <a name="windows-server-2008"></a><a name="bkmk_NetFndtn_Pln_CfgStatic08"></a>Windows Server 2008
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

##### <a name="to-configure-a-static-ip-address-on-a-computer-running-windows-server-2008"></a>Windows Server 2008을 실행하는 컴퓨터에 대해 고정 IP 주소를 구성하려면

1.  **시작**을 클릭하고 **제어판**을 클릭합니다.

2.  **제어판**에서 **클래식 보기**가 선택되었는지 확인한 다음 **네트워크 및 공유 센터**를 두 번 클릭합니다.

3.  **네트워크 및 공유 센터**의 **작업**에서 **네트워크 연결 관리**를 클릭합니다.

4.  **네트워크 연결**에서 구성할 네트워크 연결을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

5.  **로컬 영역 연결 속성**의 **이 연결에 다음 항목 사용**에서 **Internet Protocol Version 4(TCP/IPv4)** 를 선택하고 **속성**을 클릭합니다. **Internet Protocol Version 4(TCP/IPv4) 속성** 대화 상자가 열립니다.

6.  **Internet Protocol Version 4(TCP/IPv4) 속성**의 **일반** 탭에서 **다음 IP 주소 사용**을 클릭합니다. **IP 주소**에, 사용할 IP 주소를 입력합니다.

7.  Tab 키를 눌러 **서브넷 마스크**에 커서를 놓습니다. 서브넷 마스크의 기본값이 자동으로 입력됩니다. 기본 서브넷 마스크를 그대로 사용하거나 사용할 서브넷 마스크를 입력합니다.

8.  **기본 게이트웨이**에 기본 게이트웨이의 IP 주소를 입력합니다.

9. **기본 설정 DNS 서버**에 DNS 서버의 IP 주소를 입력합니다. 로컬 컴퓨터를 기본 설정 DNS 서버로 사용하려는 경우 로컬 컴퓨터의 IP 주소를 입력합니다.

10. **대체 DNS 서버**에 대체 DNS 서버(있는 경우)의 IP 주소를 입력합니다. 로컬 컴퓨터를 대체 DNS 서버로 사용하려는 경우 로컬 컴퓨터의 IP 주소를 입력합니다.

11. **확인**을 클릭한 다음 **닫기**를 클릭합니다.

## <a name="appendix-c---joining-computers-to-the-domain"></a><a name="BKMK_C"></a>부록 C-도메인에 컴퓨터 가입
이러한 절차를 사용 하 여 Windows Server 2008 R2, Windows 7, Windows Server 2008 및 Windows Vista를 실행 하는 컴퓨터를 도메인에 조인할 수 있습니다.

-   [Windows Server 2008 R2 및 Windows 7](#BKMK_c1)

-   [Windows Server 2008 및 Windows Vista](#BKMK_c2)

> [!IMPORTANT]
> 도메인에 컴퓨터를 가입하려면 로컬 Administrator 계정으로 컴퓨터에 로그온하거나, 로컬 컴퓨터 관리 자격 증명이 없는 사용자 계정으로 컴퓨터에 로그온한 경우 도메인에 컴퓨터를 가입하는 중에 로컬 Administrator 계정의 자격 증명을 제공해야 합니다. 또한 컴퓨터를 가입할 도메인에 사용자 계정이 있어야 합니다. 도메인에 컴퓨터를 가입하는 중에 도메인 계정 자격 증명(사용자 이름 및 암호)을 확인하는 메시지가 표시됩니다.

### <a name="windows-server-2008-r2-and-windows-7"></a><a name="BKMK_c1"></a>Windows Server 2008 R2 및 Windows 7
이 절차를 수행하려면 최소한 **Domain Users** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

##### <a name="to-join-computers-running-windows-server-2008-r2-and-windows-7-to-the-domain"></a>Windows Server 2008 R2 및 Windows 7을 실행 하는 컴퓨터를 도메인에 가입 시키려면

1.  로컬 Administrator 계정을 사용하여 컴퓨터에 로그온합니다.

2.  **시작**을 클릭하고 **컴퓨터**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. **시스템** 대화 상자가 열립니다.

3.  **컴퓨터 이름, 도메인 및 작업 그룹 설정**에서 **설정 변경**을 클릭합니다. **시스템 속성** 대화 상자가 열립니다.

    > [!NOTE]
    > Windows 7을 실행 하는 컴퓨터에서 **시스템 속성** 대화 상자가 열리기 전에 **사용자 계정 컨트롤** 대화 상자가 열리고 계속할 수 있는 권한을 요청 합니다. 계속하려면 **계속**을 클릭합니다.

4.  **변경**을 클릭합니다. **컴퓨터 이름/도메인 변경** 대화 상자가 열립니다.

5.  **컴퓨터 이름**의 **소속 그룹**에서 **도메인**을 선택한 다음 가입할 도메인 이름을 입력합니다. 예를 들어 도메인 이름이 corp.contoso.com이면 **corp.contoso.com**을 입력합니다.

6.  **확인**을 클릭합니다. **Windows 보안** 대화 상자가 열립니다.

7.  **컴퓨터 이름/도메인 변경**의 **사용자 이름**에 사용자 이름을 입력하고, **암호**에 암호를 입력한 다음 **확인**을 클릭합니다. **컴퓨터 이름/도메인 변경** 대화 상자가 열리고 도메인이 시작됩니다. **확인**을 클릭합니다.

8.  변경 내용을 적용하려면 컴퓨터를 다시 시작해야 한다는 메시지가 **컴퓨터 이름/도메인 변경** 대화 상자에 표시됩니다. **확인**을 클릭합니다.

9. **시스템 속성** 대화 상자의 **컴퓨터 이름** 탭에서 **닫기**를 클릭합니다. **Microsoft Windows** 대화 상자가 열리고, 변경 내용을 적용하려면 컴퓨터를 다시 시작해야 한다는 메시지가 다시 표시됩니다. **지금 다시 시작**을 클릭합니다.

### <a name="windows-server-2008-and-windows-vista"></a><a name="BKMK_c2"></a>Windows Server 2008 및 Windows Vista
이 절차를 수행하려면 최소한 **Domain Users** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

##### <a name="to-join-computers-running-windows-server-2008-and-windows-vista-to-the-domain"></a>Windows Server 2008 및 Windows Vista를 실행 하는 컴퓨터를 도메인에 가입 시키려면

1.  로컬 Administrator 계정을 사용하여 컴퓨터에 로그온합니다.

2.  **시작**을 클릭하고 **컴퓨터**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. **시스템** 대화 상자가 열립니다.

3.  **컴퓨터 이름, 도메인 및 작업 그룹 설정**에서 **설정 변경**을 클릭합니다. **시스템 속성** 대화 상자가 열립니다.

4.  **변경**을 클릭합니다. **컴퓨터 이름/도메인 변경** 대화 상자가 열립니다.

5.  **컴퓨터 이름**의 **소속 그룹**에서 **도메인**을 선택한 다음 가입할 도메인 이름을 입력합니다. 예를 들어 도메인 이름이 corp.contoso.com이면 **corp.contoso.com**을 입력합니다.

6.  **확인**을 클릭합니다. **Windows 보안** 대화 상자가 열립니다.

7.  **컴퓨터 이름/도메인 변경**의 **사용자 이름**에 사용자 이름을 입력하고, **암호**에 암호를 입력한 다음 **확인**을 클릭합니다. **컴퓨터 이름/도메인 변경** 대화 상자가 열리고 도메인이 시작됩니다. **확인**을 클릭합니다.

8.  변경 내용을 적용하려면 컴퓨터를 다시 시작해야 한다는 메시지가 **컴퓨터 이름/도메인 변경** 대화 상자에 표시됩니다. **확인**을 클릭합니다.

9. **시스템 속성** 대화 상자의 **컴퓨터 이름** 탭에서 **닫기**를 클릭합니다. **Microsoft Windows** 대화 상자가 열리고, 변경 내용을 적용하려면 컴퓨터를 다시 시작해야 한다는 메시지가 다시 표시됩니다. **지금 다시 시작**을 클릭합니다.

## <a name="appendix-d---log-on-to-the-domain"></a><a name="BKMK_D"></a>부록 D-도메인에 로그온
이러한 절차를 사용 하 여 Windows Server 2008 R2, Windows 7, Windows Server 2008 및 Windows Vista를 실행 하는 컴퓨터를 사용 하 여 도메인에 로그온 할 수 있습니다.

-   [Windows Server 2008 R2 및 Windows 7](#BKMK_d1)

-   [Windows Server 2008 및 Windows Vista](#BKMK_d2)

### <a name="windows-server-2008-r2-and-windows-7"></a><a name="BKMK_d1"></a>Windows Server 2008 R2 및 Windows 7
이 절차를 수행하려면 최소한 **Domain Users** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

##### <a name="log-on-to-the-domain-using-computers-running-windows-server-2008-r2-and-windows-7"></a>Windows Server 2008 R2 및 Windows 7을 실행 하는 컴퓨터를 사용 하 여 도메인에 로그온

1.  컴퓨터에서 로그오프하거나 컴퓨터를 다시 시작합니다.

2.  Ctrl+Alt+Del을 누릅니다. 로그온 화면이 표시됩니다.

3.  **사용자 전환**을 클릭한 다음 **기타 사용자**를 클릭합니다.

4.  **사용자 이름**에, 도메인과 사용자 이름을 *도메인\사용자* 형식으로 입력합니다. 예를 들어 **User-01**이라는 계정을 사용하여 도메인 corp.contoso.com에 로그온하려면 **CORP\User-01**을 입력합니다.

5.  **암호**에 도메인 암호를 입력한 다음 화살표를 클릭하거나 Enter 키를 누릅니다.

### <a name="windows-server-2008-and-windows-vista"></a><a name="BKMK_d2"></a>Windows Server 2008 및 Windows Vista
이 절차를 수행하려면 최소한 **Domain Users** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

##### <a name="log-on-to-the-domain-using-computers-running-windows-server-2008-and-windows-vista"></a>Windows Server 2008 및 Windows Vista를 실행 하는 컴퓨터를 사용 하 여 도메인에 로그온

1.  컴퓨터에서 로그오프하거나 컴퓨터를 다시 시작합니다.

2.  Ctrl+Alt+Del을 누릅니다. 로그온 화면이 표시됩니다.

3.  **사용자 전환**을 클릭한 다음 **기타 사용자**를 클릭합니다.

4.  **사용자 이름**에, 도메인과 사용자 이름을 *도메인\사용자* 형식으로 입력합니다. 예를 들어 **User-01**이라는 계정을 사용하여 도메인 corp.contoso.com에 로그온하려면 **CORP\User-01**을 입력합니다.

5.  **암호**에 도메인 암호를 입력한 다음 화살표를 클릭하거나 Enter 키를 누릅니다.

## <a name="appendix-e---core-network-planning-preparation-sheet"></a><a name="BKMK_E"></a>부록 E-핵심 네트워크 계획 준비 시트
이 네트워크 계획 준비 시트를 사용하여 핵심 네트워크 설치에 필요한 정보를 수집할 수 있습니다. 이 항목에서는 설치 또는 구성 프로세스 도중 정보나 특정 값을 제공해야 하는 각 서버 컴퓨터에 대한 개별 구성 항목이 포함된 표를 제공합니다. 각 구성 항목에 대한 예제 값을 제공합니다.

계획 및 추적을 위해, 각 표에는 자신의 배포에 사용한 값을 입력할 수 있는 공간이 있습니다. 이 표를 사용하여 보안 관련 값을 기록하는 경우에는 정보를 안전한 위치에 보관해야 합니다.

다음 링크는 이 가이드에 나오는 배포 절차와 관련된 구성 항목과 예제 값이 있는 본 항목의 섹션으로 연결됩니다.

1.  [Active Directory Domain Services 및 DNS 설치](#BKMK_FndtnPrep_InstallAD)

    -   [DNS 역방향 조회 영역 구성](#BKMK_FndtnPrep_DNSRevrsLook)

2.  [DHCP 설치](#BKMK_FndtnPrep_InstallDHCP)

    -   [DHCP에서 제외 범위 만들기](#BKMK_FndtnPrep_DHCP_Exclusn)

    -   [새 DHCP 범위 만들기](#bkmk_NetFndtn_Pln_DHCP_NewScope)

3.  [네트워크 정책 서버 설치 (선택 사항)](#BKMK_FndtnPrep_InstallNPS)

### <a name="installing-active-directory-domain-services-and-dns"></a><a name="BKMK_FndtnPrep_InstallAD"></a>Active Directory Domain Services 및 DNS 설치
이 섹션의 표에는 Active Directory Domain Services (AD DS) 및 DNS의 사전 설치 및 설치에 대 한 구성 항목이 나열 되어 있습니다.

##### <a name="pre-installation-configuration-items-for-ad-ds-and-dns"></a>AD DS 및 DNS에 대 한 사전 설치 구성 항목
다음 표에서는 [모든 서버 구성](#BKMK_configuringAll)에 설명되어 있는 사전 설치 구성 항목을 보여 줍니다.

-   [고정 IP 주소 구성](#BKMK_ip)

|구성 항목|예제 값|값|
|-----------------------|------------------|----------|
|IP 주소|10.0.0.2||
|서브넷 마스크|255.255.255.0||
|기본 게이트웨이|10.0.0.1||
|기본 설정 DNS 서버|127.0.0.1||
|대체 DNS 서버|10.0.0.15||

-   [컴퓨터 이름 바꾸기](#BKMK_rename)

|구성 항목|예제 값|값|
|----------------------|-----------------|---------|
|컴퓨터 이름|DC1||

##### <a name="ad-ds-and-dns-installation-configuration-items"></a>AD DS 및 DNS 설치 구성 항목
Windows Server 핵심 네트워크 배포 절차 [새 포리스트에 대한 AD DS 및 DNS 설치](#BKMK_installAD-DNS)에 대한 구성 항목

|구성 항목|예제 값|값|
|-----------------------|------------------|----------|
|전체 DNS 이름|corp.contoso.com||
|포리스트 기능 수준|Windows Server 2003||
|Active Directory Domain Services 데이터베이스 폴더 위치|E:\Configuration\\<br /><br />또는 기본 위치를 적용합니다.||
|Active Directory Domain Services 로그 파일 폴더 위치|E:\Configuration\\<br /><br />또는 기본 위치를 적용합니다.||
|Active Directory Domain Services SYSVOL 폴더 위치|E:\Configuration\\<br /><br />또는 기본 위치를 적용합니다.||
|디렉터리 복원 모드 관리자 암호|J*p2leO4$F||
|응답 파일 이름(옵션)|AD DS_AnswerFile||

#### <a name="configuring-a-dns-reverse-lookup-zone"></a><a name="BKMK_FndtnPrep_DNSRevrsLook"></a>DNS 역방향 조회 영역 구성

|구성 항목|예제 값|값|
|-----------------------|------------------|----------|
|영역 종류:|-주 영역<br />-보조 영역<br />-스텁 영역||
|영역 종류<br /><br />**영역을 Active Directory에 저장 합니다.**|-선택 됨<br />-선택 하지 않음||
|Active Directory 영역 복제 범위|-이 포리스트의 모든 DNS 서버에<br />-이 도메인의 모든 DNS 서버로<br />-이 도메인의 모든 도메인 컨트롤러에<br />-이 디렉터리 파티션의 범위에 지정 된 모든 도메인 컨트롤러||
|역방향 조회 영역 이름<br /><br />(IP 유형)|-IPv4 역방향 조회 영역<br />-IPv6 역방향 조회 영역||
|역방향 조회 영역 이름<br /><br />(네트워크 ID)|10.0.0||

### <a name="installing-dhcp"></a><a name="BKMK_FndtnPrep_InstallDHCP"></a>DHCP 설치
이 섹션의 표에는 DHCP의 사전 설치 및 설치에 대한 구성 항목이 나열되어 있습니다.

##### <a name="pre-installation-configuration-items-for-dhcp"></a>DHCP에 대한 사전 설치 구성 항목
다음 표에서는 [모든 서버 구성](#BKMK_configuringAll)에 설명되어 있는 사전 설치 구성 항목을 보여 줍니다.

-   [고정 IP 주소 구성](#BKMK_ip)

|구성 항목|예제 값|값|
|-----------------------|------------------|----------|
|IP 주소|10.0.0.3||
|서브넷 마스크|255.255.255.0||
|기본 게이트웨이|10.0.0.1||
|기본 설정 DNS 서버|10.0.0.2||
|대체 DNS 서버|10.0.0.15||

-   [컴퓨터 이름 바꾸기](#BKMK_rename)

|구성 항목|예제 값|값|
|----------------------|-----------------|---------|
|컴퓨터 이름|DHCP1||

##### <a name="dhcp-installation-configuration-items"></a>DHCP 설치 구성 항목
Windows Server 핵심 네트워크 배포 절차 [DHCP(Dynamic Host Configuration Protocol) 설치](#BKMK_installDHCP)에 대한 구성 항목

|구성 항목|예제 값|값|
|-----------------------|------------------|----------|
|네트워크 연결 바인딩|이더넷||
|DNS 서버 설정|DC1||
|기본 설정 DNS 서버 IP 주소|10.0.0.2||
|대체 DNS 서버 IP 주소|10.0.0.15||
|범위 이름|Corp1||
|시작 IP 주소|10.0.0.1||
|끝 IP 주소|10.0.0.254||
|서브넷 마스크|255.255.255.0||
|기본 게이트웨이(옵션)|10.0.0.1||
|임대 기간|8일||
|IPv6 DHCP 서버 작동 모드|사용 안 함||

#### <a name="creating-an-exclusion-range-in-dhcp"></a><a name="BKMK_FndtnPrep_DHCP_Exclusn"></a>DHCP에서 제외 범위 만들기
DHCP에서 범위를 만드는 동안 제외 범위를 만들기 위한 구성 항목입니다.

|구성 항목|예제 값|값|
|-----------------------|------------------|----------|
|범위 이름|Corp1||
|범위 설명|본사 서브넷 1||
|제외 범위 시작 IP 주소|10.0.0.1||
|제외 범위 끝 IP 주소|10.0.0.15||

#### <a name="creating-a-new-dhcp-scope"></a><a name="bkmk_NetFndtn_Pln_DHCP_NewScope"></a>새 DHCP 범위 만들기
Windows Server 핵심 네트워크 배포 절차 [새 DHCP 범위 만들기 및 활성화](#BKMK_newscopeDHCP)에 대한 구성 항목

|구성 항목|예제 값|값|
|-----------------------|------------------|----------|
|새 범위 이름|Corp2||
|범위 설명|본사 서브넷 2||
|(IP 주소 범위)<br /><br />시작 IP 주소|10.0.1.1||
|(IP 주소 범위)<br /><br />끝 IP 주소|10.0.1.254||
|길이|8||
|서브넷 마스크|255.255.255.0||
|(제외 범위) 시작 IP 주소|10.0.1.1||
|제외 범위 끝 IP 주소|10.0.1.15||
|임대 기간<br /><br />요일<br /><br />Hours<br /><br />분|-8<br />-   0<br />-   0||
|라우터(기본 게이트웨이)<br /><br />IP 주소|10.0.1.1||
|DNS 부모 도메인|corp.contoso.com||
|DNS 서버<br /><br />IP 주소|10.0.0.2||

### <a name="installing-network-policy-server-optional"></a><a name="BKMK_FndtnPrep_InstallNPS"></a>네트워크 정책 서버 설치 (선택 사항)
이 섹션의 표에서는 NPS의 사전 설치 및 설치에 대한 구성 항목을 보여 줍니다.

##### <a name="pre-installation-configuration-items"></a>사전 설치 구성 항목
다음 세 개 표에서는 [모든 서버 구성](#BKMK_configuringAll)에 설명되어 있는 사전 설치 구성 항목을 보여 줍니다.

-   [고정 IP 주소 구성](#BKMK_ip)

|구성 항목|예제 값|값|
|-----------------------|------------------|----------|
|IP 주소|10.0.0.4||
|서브넷 마스크|255.255.255.0||
|기본 게이트웨이|10.0.0.1||
|기본 설정 DNS 서버|10.0.0.2||
|대체 DNS 서버|10.0.0.15||

-   [컴퓨터 이름 바꾸기](#BKMK_rename)

|구성 항목|예제 값|값|
|----------------------|-----------------|---------|
|컴퓨터 이름|NPS1||

##### <a name="network-policy-server-installation-configuration-items"></a>네트워크 정책 서버 설치 구성 항목
Windows Server Core 네트워크 NPS 배포 절차에 대 한 구성 항목 nps [(네트워크 정책 서버)를 설치](#BKMK_installNPS) 하 고 [기본 도메인에 nps를 등록](#BKMK_registerNPS)합니다.

-   NPS 설치 및 등록에는 추가적인 구성 항목이 필요하지 않습니다.

