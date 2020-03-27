---
title: 2 단계 고급 DirectAccess 배포 계획
description: 이 항목은 Windows Server 2016에 대 한 고급 설정을 사용 하 여 단일 DirectAccess 서버 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3bba28d4-23e2-449f-8319-7d2190f68d56
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8269fee952e60aa53facec95ab3070b906383ad2
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309057"
---
# <a name="step-2-plan-advanced-directaccess-deployments"></a>2 단계 고급 DirectAccess 배포 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IPv4 및 IPv6을 사용하는 단일 서버에 고급 DirectAccess를 배포하는 단계에서 DirectAccess 인프라를 계획한 후에는 원격 액세스 설치 마법사에 대한 설정을 계획해야 합니다.  
  
|작업|설명|  
|----|--------|  
|[2.1 클라이언트 배포 계획](#21-plan-for-client-deployment)|클라이언트 컴퓨터에서 DirectAccess를 사용하여 연결하도록 허용할 방법을 계획합니다. DirectAccess 클라이언트로 구성할 관리되는 컴퓨터를 결정하고, 클라이언트 컴퓨터에 네트워크 연결 길잡이를 배포할지 또는 DirectAccess 연결 길잡이를 배포할지 계획합니다.|  
|[2.2 DirectAccess 서버 배포 계획](#22-plan-for-directaccess-server-deployment)|DirectAccess 서버를 배포할 방법을 계획합니다.|  
|[2.3 인프라 서버 계획](#23-plan-infrastructure-servers)|DirectAccess 네트워크 위치 서버, DNS(Domain Name System) 서버, DirectAccess 관리 서버 등 DirectAccess 배포를 위한 인프라 서버를 계획합니다.|  
|[2.4 응용 프로그램 서버 계획](#24-plan-application-servers)|IPv4/IPv6 애플리케이션 서버를 계획하고 선택적으로 DirectAccess 클라이언트 컴퓨터와 내부 애플리케이션 서버 사이에 엔드투엔드 인증이 필요한지를 고려합니다.|  
|[2.5 DirectAccess 및 타사 VPN 클라이언트 계획](#25-plan-directaccess-and-third-party-vpn-clients)|타사 VPN 클라이언트와 함께 DirectAccess를 배포하려면 두 원격 액세스 솔루션의 원활한 공존을 지원하도록 레지스트리 값을 설정해야 할 수 있습니다.|  
  
## <a name="21-plan-for-client-deployment"></a>2.1 클라이언트 배포 계획  
클라이언트 배포를 계획할 때 결정해야 하는 세 가지 사항이 있습니다.  
  
1.  DirectAccess를 이동 컴퓨터에서만 사용할 수 있나요, 아니면 모든 컴퓨터에서 사용할 수 있나요?  
  
    DirectAccess 클라이언트 설치 마법사에서 DirectAccess 클라이언트를 구성할 때 지정된 보안 그룹의 이동 컴퓨터에서만 DirectAccess를 사용하여 연결하도록 허용할 수 있습니다. 액세스를 이동 컴퓨터로 제한하면 원격 액세스에서 DirectAccess 클라이언트 GPO가 지정된 보안 그룹의 이동 컴퓨터에만 적용되도록 WMI 필터를 자동으로 구성합니다. 이 설정을 사용하려면 원격 액세스 관리자에게 GPO(그룹 정책 개체) WMI 필터를 만들거나 수정할 수 있는 보안 만들기 또는 수정 권한이 있어야 합니다.  
  
2.  DirectAccess 클라이언트 컴퓨터가 어떤 보안 그룹에 포함되나요?  
  
    DirectAccess 클라이언트 설정은 DirectAccess 클라이언트 GPO에 포함됩니다. 이 GPO는 DirectAccess 클라이언트 설치 마법사에서 지정한 보안 그룹에 속한 컴퓨터에 적용됩니다. 지원되는 모든 도메인에 보안 그룹이 포함되도록 지정할 수 있습니다. 자세한 내용은 [Active Directory Domain Services 1.7 계획](da-adv-plan-s1-infrastructure.md#17-plan-active-directory-domain-services)섹션을 참조 하세요.  
  
    DirectAccess를 구성하기 전에 보안 그룹을 만들어야 합니다. DirectAccess 배포를 완료한 후 보안 그룹에 컴퓨터를 추가할 수 있지만 보안 그룹과 다른 도메인에 상주하는 클라이언트 컴퓨터를 추가한 경우 해당 클라이언트에는 클라이언트 GPO가 적용되지 않습니다. 예를 들어 도메인 A에 DirectAccess 클라이언트에 대한 SG1을 만들고 나중에 도메인 B의 클라이언트를 이 그룹에 추가하는 경우 도메인 B의 클라이언트에는 클라이언트 GPO가 적용되지 않습니다. 이 문제를 방지하려면 DirectAccess 클라이언트 컴퓨터가 포함된 각 도메인에 대한 새 클라이언트 보안 그룹을 만들어야 합니다. 또는 새 보안 그룹을 만들지 않으려면 새 도메인의 새 GPO 이름으로 Windows PowerShell cmdlet **Add-DAClient**를 실행합니다.  
  
3.  네트워크 연결 길잡이에 대해 구성할 설정이 무엇인가요?  
  
    네트워크 연결 길잡이는 클라이언트 컴퓨터에서 실행되며 최종 사용자에게 DirectAccess 연결에 대한 추가 정보를 제공합니다. DirectAccess 클라이언트 설치 마법사에서 다음을 구성할 수 있습니다.  
  
    -   **연결 검증 도구**  
  
        클라이언트에서 내부 네트워크 연결의 유효성을 검사하는 데 사용하는 기본 웹 검색이 만들어집니다. 기본 이름은 다음과 같습니다.  
  
        https://directaccess-WebProbeHost.<domain_name>  
  
        DNS에 이름을 수동으로 등록해야 합니다. HTTP 또는 **ping**을 통해 다른 웹 주소를 사용하여 다른 연결 검증 도구를 만들 수 있습니다. 각 연결 검증 도구에 대한 DNS 항목이 있어야 합니다.  
  
    -   **지원 센터 전자 메일 주소**  
  
        DirectAccess 연결 문제가 발생한 경우 최종 사용자는 DirectAccess 관리자에게 진단 정보가 포함된 전자 메일을 보내 문제를 해결할 수 있습니다.  
  
    -   **DirectAccess 연결 이름**  
  
        최종 사용자가 자신의 컴퓨터에서 DirectAccess 연결을 식별할 수 있는 DirectAccess 연결 이름을 지정합니다.  
  
    -   **DirectAccess 클라이언트에서 로컬 이름 확인을 사용 하도록 허용**  
  
        클라이언트에 이름을 로컬로 확인할 방법이 필요합니다. DirectAccess 클라이언트에서 로컬 이름 확인을 사용하도록 허용하면 최종 사용자가 로컬 DNS 서버를 사용하여 이름을 확인할 수 있습니다. 최종 사용자가 이름 확인에 DNS 서버를 사용하도록 선택한 경우 DirectAccess는 회사 내부 DNS 서버로 단일 레이블 이름에 대한 확인 요청을 보내지 않습니다. 대신 LLMNR(링크-로컬 멀티 캐스트 이름 확인) 및 NetBIOS over TCP/IP 프로토콜을 통해 로컬 이름 확인을 사용합니다.  
  
## <a name="22-plan-for-directaccess-server-deployment"></a>2.2 DirectAccess 서버 배포 계획  
DirectAccess 서버 배포를 계획할 때 다음 결정할 사항은 다음과 같습니다.  
  
-   **네트워크 토폴로지**  
  
    DirectAccess 서버를 배포할 때 사용할 수 있는 토폴로지에는 다음 두 가지가 있습니다.  
  
    -   **네트워크 어댑터 2개**. 네트워크 어댑터 2개를 사용하면 인터넷에 직접 연결되는 네트워크 어댑터와 내부 네트워크에 연결되는 네트워크 어댑터로 DirectAccess를 구성할 수 있습니다. 또는 방화벽이나 라우터와 같은 에지 장치 뒤에 서버가 설치됩니다. 이 구성에서는 네트워크 어댑터가 경계 네트워크와 내부 네트워크에 각각 하나씩 연결됩니다.  
  
    -   **네트워크 어댑터 1 개**합니다. 이 구성에서는 방화벽이나 라우터와 같은 에지 장치 뒤에 DirectAccess 서버가 설치됩니다. 네트워크 어댑터는 내부 네트워크에 연결됩니다.  
  
    배포에 대 한 토폴로지를 선택 하는 방법에 대 한 자세한 내용은 [1.1 네트워크 토폴로지 및 설정 계획](da-adv-plan-s1-infrastructure.md#11-plan-network-topology-and-settings)을 참조 하세요.  
  
-   **ConnectTo 주소**  
  
    클라이언트 컴퓨터에서는 ConnectTo 주소를 사용하여 DirectAccess 서버에 연결합니다. 선택한 주소는 IP-HTTPS 연결을 위해 배포할 IP-HTTPS 인증서의 주체 이름과 일치해야 하며 공용 DNS에서 사용할 수 있어야 합니다.  
  
-   **네트워크 어댑터**  
  
    원격 액세스 서버 설치 마법사가 DirectAccess 서버에 구성된 네트워크 어댑터를 자동으로 검색합니다. 올바른 어댑터를 선택해야 합니다.  
  
-   **IP-HTTPS 인증서**  
  
    원격 액세스 서버 설치 마법사가 IP-HTTPS 연결에 적합한 인증서를 자동으로 검색합니다. 선택한 인증서의 주체 이름이 ConnectTo 주소와 일치해야 합니다. 자체 서명된 인증서를 사용하는 경우 원격 액세스 서버에서 자동으로 만들어진 인증서를 사용하도록 선택할 수 있습니다.  
  
-   **IPv6 접두사**  
  
    원격 액세스 서버 설치 마법사가 네트워크 어댑터에 배포된 IPv6을 검색하며, 내부 네트워크의 IPv6 접두사, DirectAccess 클라이언트 컴퓨터에 할당할 IPv6 접두사 및 VPN 클라이언트 컴퓨터에 할당할 IPv6 접두사를 자동으로 채웁니다. 자동으로 생성된 접두사가 기본 IPv6 인프라에 올바르지 않은 경우 수동으로 변경해야 합니다. 자세한 내용은 [1.1 네트워크 토폴로지 및 설정 계획](da-adv-plan-s1-infrastructure.md#11-plan-network-topology-and-settings)을 참조 하세요.  
  
-   **인증**  
  
    DirectAccess 클라이언트가 DirectAccess 서버의 인증을 받는 방법을 결정합니다.  
  
    -   **사용자 인증**. 사용자가 Active Directory 자격 증명 또는 2단계 인증을 통해 인증을 받도록 설정할 수 있습니다. 2 단계 인증을 사용 하 여 인증 하는 방법에 대 한 자세한 내용은 [OTP 인증을 사용 하 여 원격 액세스 배포](https://technet.microsoft.com/library/hh831379.aspx)를 참조 하세요.  
  
    -   **컴퓨터 인증**. 인증서를 사용하거나 클라이언트 대신해 DirectAccess 서버를 Kerberos 프록시로 사용하도록 컴퓨터 인증을 구성할 수 있습니다. 자세한 내용은 [1.3 인증서 요구 사항 계획](da-adv-plan-s1-infrastructure.md#13-plan-certificate-requirements)을 참조 하세요.  
  
    -   **Windows 7 클라이언트**. 기본적으로 Windows 7을 실행 하는 클라이언트 컴퓨터는 Windows Server 2012 R2 또는 Windows Server 2012 DirectAccess 배포에 연결할 수 없습니다. 조직에 Windows 7을 실행 하는 클라이언트가 있고 내부 리소스에 대 한 원격 액세스 권한이 필요한 경우 연결 하도록 허용할 수 있습니다. 내부 리소스에 대한 액세스를 허용할 클라이언트 컴퓨터는 DirectAccess 클라이언트 설치 마법사에서 지정한 보안 그룹의 구성원이어야 합니다.  
  
        > [!NOTE]  
        > Windows 7을 실행 하는 클라이언트가 DirectAccess를 사용 하 여 연결 하도록 허용 하려면 컴퓨터 인증서 인증을 사용 해야 합니다.  
  
-   **VPN 구성**  
  
    DirectAccess를 구성하기 전에 DirectAccess를 지원하지 않는 원격 클라이언트에 대한 VPN 액세스를 제공할지 여부를 결정합니다. 관리되지 않거나 DirectAccess가 지원되지 않는 운영 체제를 실행하기 때문에 DirectAccess 연결을 지원하지 않는 클라이언트 컴퓨터가 조직에 있는 경우 VPN 액세스를 제공해야 합니다. 원격 액세스 서버 설치 마법사를 통해 IP 주소 할당 방법(DHCP를 사용하여 할당하거나 고정 주소 풀에서 할당) 및 VPN 클라이언트 인증 방법(Active Directory 또는 RADIUS(Remote Authentication Dial-Up Service) 서버 사용)을 구성할 수 있습니다.  
  
## <a name="23-plan-infrastructure-servers"></a>2.3 인프라 서버 계획  
DirectAccess에는 다음 세 가지 유형의 인프라 서버가 필요합니다.  
  
-   **DNS 서버**. 자세한 내용은 [1.4 DNS 요구 사항 계획](da-adv-plan-s1-infrastructure.md#14-plan-dns-requirements)을 참조하세요.  
  
-   **네트워크 위치 서버**. 자세한 내용은 [1.5 네트워크 위치 서버 계획](da-adv-plan-s1-infrastructure.md#15-plan-the-network-location-server)을 참조하세요.  
  
-   **관리 서버**. 자세한 내용은 [1.6 관리 서버 계획](da-adv-plan-s1-infrastructure.md#16-plan-management-servers)을 참조하세요.  
  
## <a name="24-plan-application-servers"></a>2.4 응용 프로그램 서버 계획  
응용 프로그램 서버는 클라이언트 컴퓨터에서 DirectAccess 연결을 통해 액세스할 수 있는 회사 네트워크의 서버입니다. 응용 프로그램 서버를 식별하려면 보안 그룹에 추가해야 합니다. 그러면 응용 프로그램 서버 GPO가 해당 그룹의 서버에 적용됩니다.  
  
> [!NOTE]  
> 엔드투엔드 인증 및 암호화를 요구하려는 경우에만 애플리케이션 서버를 보안 그룹에 추가하면 됩니다.  
  
DirectAccess 클라이언트와 선택한 내부 애플리케이션 서버 간에 선택적으로 엔드투엔드 인증 및 암호화를 요구할 수 있습니다. 엔드투엔드 인증을 구성하면 DirectAccess 클라이언트에서 IPsec 전송 정책을 사용합니다. 이 정책에서는 IPsec 세션의 인증 및 트래픽 보호가 지정된 응용 프로그램 서버에서 종료되도록 요구합니다. 이 경우 원격 액세스 서버는 인증 및 보호된 IPsec 세션을 응용 프로그램 서버로 전달합니다.  
  
응용 프로그램 서버로 인증을 확장한 경우 기본적으로 DirectAccess 클라이언트와 응용 프로그램 서버 간에 데이터 페이로드가 암호화됩니다. 트래픽을 암호화하지 않고 인증만 사용하도록 선택할 수 있습니다. 그러나이는 인증 및 암호화를 사용 하는 것 보다 안전 하지 않으며, Windows Server 2008 R2 또는 Windows Server 2012 운영 체제를 실행 하는 응용 프로그램 서버에 대해서만 지원 됩니다.  
  
## <a name="25-plan-directaccess-and-third-party-vpn-clients"></a>2.5 DirectAccess 및 타사 VPN 클라이언트 계획  
일부 타사 VPN 클라이언트는 네트워크 연결 폴더에 연결을 만들지 않습니다. 이로 인해 VPN 연결이 설정되고 인트라넷 연결이 존재할 때 DirectAccess에서 인트라넷 연결이 없는 것으로 확인할 수 있습니다. 이는 타사 VPN 클라이언트가 자체를 NDIS(네트워크 장치 인터페이스 규격) 끝점 형식으로 정의하여 해당 인터페이스를 등록한 경우에 발생합니다. DirectAccess 클라이언트에서 다음 레지스트리 값을 1로 설정하여 이러한 유형의 VPN 클라이언트와의 공존을 지원할 수 있습니다.  
  
**HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\services\NlaSvc\Parameters\ShowDomainEndpointInterfaces (REG_DWORD)**  
  
일부 타사 VPN 클라이언트는 VPN 클라이언트 컴퓨터에서 VPN 연결을 통해 인트라넷으로 트래픽을 보낼 필요 없이 인터넷에 직접 액세스하도록 허용하는 분할 터널링 구성을 사용합니다.  
  
분할 터널 구성은 일반적으로 VPN 클라이언트의 기본 게이트웨이 설정을 구성되지 않거나 모두 0(0.0.0.0)인 상태로 그대로 둡니다. 이는 인트라넷에 대한 VPN 연결 설정 및 Ipconfig.exe 명령줄 도구의 결과 구성 확인을 통해 확인할 수 있습니다.  
  
VPN 연결에 해당 기본 게이트웨이가 비어 있거나 모두 0(0.0.0.0)인 것으로 나열되면 VPN 클라이언트가 이 방식으로 구성된 것입니다. 기본적으로 DirectAccess 클라이언트는 분할 터널링 구성을 식별하지 않습니다. 이러한 유형의 VPN 클라이언트 구성을 검색하고 함께 사용되도록 DirectAccess 클라이언트를 구성하려면 다음 레지스트리 설정을 1로 설정합니다.  
  
**REG_DWORD (HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\services\NlaSvc\Parameters\Internet\ EnableNoGatewayLocationDetection)**  
  
## <a name="previous-step"></a>이전 단계  
  
-   [1 단계: DirectAccess 인프라 계획](da-adv-plan-s1-infrastructure.md)  
  


