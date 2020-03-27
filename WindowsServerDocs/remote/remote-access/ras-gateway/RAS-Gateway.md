---
title: RAS 게이트웨이
description: IT (정보 기술) 전문가를 위한이 항목에서는 ras gateway 배포 모드 및 Windows Server 2016의 기능을 비롯 한 RAS 게이트웨이에 대 한 개요 정보를 제공 합니다.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: acaa46b7-09b1-4707-9562-116df8db17eb
ms.author: lizross
author: eross-msft
ms.date: 05/23/2018
ms.openlocfilehash: 762ba98a57db1411098c6ae6a8394e9a9b063181
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308531"
---
# <a name="ras-gateway"></a>RAS 게이트웨이

>적용 대상: Windows Server(반기 채널), Windows Server 2016

RAS 게이트웨이는 단일 테 넌 트 모드 또는 다중 테 넌 트 모드에서 사용할 수 있는 소프트웨어 라우터 및 게이트웨이입니다.  
  
- **단일 테 넌 트** 모드를 사용 하면 모든 규모의 조직이 외부 또는 인터넷 연결에 지 VPN (가상 사설망) 및 DirectAccess 서버로 게이트웨이를 배포할 수 있습니다. 단일 테 넌 트 모드에서 Windows Server 2016를 실행 하는 물리적 서버 또는 VM (가상 머신)에 RAS 게이트웨이를 배포할 수 있습니다.  
  
- **다중 테 넌 트 모드** 에서는 Csp (클라우드 서비스 공급자) 및 기업이 RAS Gateway를 사용 하 여 인터넷을 포함 하 여 가상 네트워크와 실제 네트워크 간에 데이터 센터 및 클라우드 네트워크 트래픽을 라우팅할 수 있습니다. 다중 테 넌 트 모드의 경우 Windows Server 2016를 실행 하는 Vm에 RAS 게이트웨이를 배포 하는 것이 좋습니다.  
  
> [!NOTE]  
> RAS 게이트웨이는 ipv4 및 IPv6 (IPv4 및 IPv6 전달 포함)을 지원 합니다. NAT (Network Address Translation)를 사용 하 여 RAS 게이트웨이를 구성 하는 경우 NAT44만 지원 됩니다.  
  
## <a name="who-will-be-interested-in-ras-gateway"></a>RAS 게이트웨이에 관심이 있는 사용자는 누구 인가요?
  
시스템 관리자, 네트워크 설계자 또는 기타 IT 전문가 라면 RAS 게이트웨이는 다음과 같은 상황 중 하나 이상에 관심을 가질 수 있습니다.  
  
-   가상 네트워크에 VM(가상 컴퓨터)을 배포하는 데 Hyper-V를 사용하거나 사용할 계획인 조직의 IT 인프라를 설계하거나 지원하는 경우  
  
-   클라우드 기술을 배포했거나 배포할 계획인 조직의 IT 인프라를 설계하거나 지원하는 경우  
  
-   실제 네트워크와 가상 네트워크 간의 완벽한 네트워크 연결을 제공하려는 경우  
  
-   조직의 고객에 게 인터넷을 통해 가상 네트워크에 대 한 액세스 권한을 제공 하려고 합니다.  
  
-   조직의 직원에 게 조직 네트워크에 대 한 원격 액세스를 제공 하려고 합니다.  
  
-   인터넷을 통해 서로 다른 물리적 위치에 있는 사무실을 연결 하려고 합니다.  
 
IT (정보 기술) 전문가를 위한이 항목에서는 ras gateway 배포 모드 및 기능을 비롯 한 RAS 게이트웨이에 대 한 개요 정보를 제공 합니다. 
  
이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
  
-   [RAS 게이트웨이 배포 모드](#bkmk_modes)  
  
-   [고가용성을 위해 RAS 게이트웨이 클러스터링](#bkmk_clustering)  
  
-   [RAS 게이트웨이 기능](#bkmk_features)  
  
-   [RAS 게이트웨이 배포 시나리오](#bkmk_deploy)  
  
-   [RAS 게이트웨이 관리 도구](#bkmk_manage)  
  


  
## <a name="ras-gateway-deployment-modes"></a><a name="bkmk_modes"></a>RAS 게이트웨이 배포 모드  
RAS 게이트웨이는 다음과 같은 배포 모드를 포함 합니다.  
  
### <a name="single-tenant-mode"></a>단일 테 넌 트 모드  
대부분의 조직에서는 단일 테 넌 트 모드에서 RAS 게이트웨이를 사용 하는 것이 일반적인 구성입니다. 단일 테 넌 트 모드에서 RAS 게이트웨이를에 지 VPN 서버,에 지 DirectAccess 서버 또는 둘 다 동시에 배포할 수 있습니다. 이 구성에서 RAS 게이트웨이는 VPN 또는 DirectAccess 연결을 사용 하 여 원격 직원에 게 네트워크에 대 한 연결을 제공 합니다. 또한 단일 테 넌 트 모드를 사용 하면 인터넷을 통해 서로 다른 물리적 위치에 있는 사무실을 연결할 수 있습니다.  
  
### <a name="multitenant-mode"></a>다중 테 넌 트 모드  
조직이 여러 테 넌 트가 있는 CSP 또는 엔터프라이즈 인 경우 다중 테 넌 트 모드에서 RAS 게이트웨이를 배포 하 여 가상 네트워크와 실제 네트워크 간에 트래픽을 라우팅하는 네트워크 트래픽을 제공할 수 있습니다.  
  
배포할지에은 여러 테 넌 트의 가상 컴퓨터 워크 로드를 지원 하 고, 모든 워크 로드를 동일한 인프라에서 실행 하는 클라우드 인프라의 기능입니다. 개별 테넌트의 여러 작업을 상호 연결하고 원격으로 관리할 수는 있지만, 이러한 시스템이 다른 테넌트의 작업과 서로 연결되거나 다른 테넌트에서 이러한 시스템을 원격으로 관리하지는 않습니다.  
  
예를 들어 기업에는 각각 연구 개발 또는 회계와 같은 특정 부서를 지원하는 데 전용되는 여러 가상 서브넷이 있을 수 있습니다. 또 다른 예로, CSP에는 동일한 실제 데이터 센터에서 격리된 상태로 존재하는 가상 서브넷을 가진 많은 테넌트가 있습니다. 두 경우 모두 RAS 게이트웨이는 각 테 넌 트의 설계 된 격리를 유지 하면서 각 테 넌 트 간에 트래픽을 라우팅할 수 있습니다. 이 기능을 통해 RAS 게이트웨이는 다중 테 넌 트를 인식 합니다.  
  
가상 네트워크는 Windows Server 2012에 도입 된 기술인 Hyper-v 네트워크 가상화를 사용 하 여 생성 되며 Windows Server 2016에서 개선 되었습니다. RAS 게이트웨이는 Hyper-v 네트워크 가상화와 통합 되며 여러 고객 또는 테 넌 트가 동일한 데이터 센터에 격리 된 가상 네트워크를 보유 하는 환경에서 네트워크 트래픽을 효과적으로 라우팅할 수 있습니다.  
  
Hyper-v 네트워크 가상화는 기본 실제 네트워크와 무관 한 VM (가상 컴퓨터) 네트워크를 배포 하는 기능을 제공 합니다. 하나 이상의 가상 서브넷으로 구성 된 VM 네트워크를 사용 하는 경우 IP 서브넷의 정확한 실제 위치는 가상 네트워크 토폴로지에서 분리 됩니다. 따라서 클라우드에서 기존 IP 주소와 토폴로지를 유지 하면서 온-프레미스 서브넷을 클라우드로 쉽게 이동할 수 있습니다. 인프라를 유지할 수 있으므로 서브넷의 실제 위치를 몰라도 기존 서비스가 계속 작동합니다. 즉, Hyper-V 네트워크 가상화를 통해 원활한 하이브리드 클라우드가 가능해집니다.  
  
> [!NOTE]  
> Hyper-v 네트워크 가상화는 테 넌 트가 고유한 주소 공간을 가져오고 Csp가 테 넌 트 격리에 Vlan을 사용 하 여 확장성을 향상 시킬 수 있도록 하는 네트워크 가상화[NVGRE](https://tools.ietf.org/html/draft-sridharan-virtualization-nvgre-00)(제네릭 라우팅 캡슐화)를 사용 하는 네트워크 오버레이 기술입니다.  
  
Windows Server 2016에서 RAS 게이트웨이는 리소스가 있는 위치에 관계 없이 실제 네트워크 리소스와 VM 네트워크 리소스 간에 네트워크 트래픽을 라우팅합니다. RAS 게이트웨이를 사용 하 여 실제 네트워크와 가상 네트워크 간에 네트워크 트래픽을 라우팅할 수 있습니다.  
  
예를 들어 실제 네트워크와 가상 네트워크가 동일한 실제 위치에 있는 경우에는 RAS 게이트웨이 VM으로 구성 된 Hyper-v를 실행 하는 컴퓨터를 배포 하 여 전달 게이트웨이의 역할을 수행 하 고 가상 및 실제 간에 트래픽을 라우팅할 수 있습니다. 사설망.  
  
또 다른 예로, 가상 네트워크가 클라우드에 있는 경우 CSP는 VPN 서버와 CSP의 RAS 게이트웨이 간에 VPN (가상 사설망) 사이트 간 연결을 만들 수 있도록 RAS 게이트웨이를 배포할 수 있습니다. 이 링크가 설정 되 면 VPN 연결을 통해 클라우드의 가상 리소스에 연결할 수 있습니다.  
  
자세한 내용은 참조 [RAS 게이트웨이 고가용성](../../../networking/sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)합니다.  
  
## <a name="clustering-ras-gateway-for-high-availability"></a><a name="bkmk_clustering"></a>고가용성을 위해 RAS 게이트웨이 클러스터링  
RAS 게이트웨이는 Hyper-v를 실행 하 고 하나의 VM으로 구성 된 전용 컴퓨터에 배포 됩니다. 그러면 VM이 RAS 게이트웨이로 구성 됩니다.  
  
네트워크 리소스의 고가용성을 위해 Hyper-v를 실행 하는 두 대의 실제 호스트 서버를 사용 하 여 장애 조치 (failover)를 통해 RAS 게이트웨이를 배포할 수 있습니다 .이는 각각 게이트웨이로 구성 된 VM (가상 머신)도 실행 합니다. 그러면 이 게이트웨이 VM이 클러스터로 구성되어 네트워크 중단 및 하드웨어 오류로부터 장애 조치(failover) 보호를 제공합니다.  
  
예를 들어 조직이 사설 클라우드 배포를 사용 하는 엔터프라이즈 인 경우 각각 Hyper-v를 실행 하는 다른 컴퓨터에 설치 되는 RAS 게이트웨이 Vm이 두 개만 필요할 수 있습니다. 이 시나리오에서 RAS 게이트웨이 Vm은 고가용성을 제공 하기 위해 클러스터에 추가 됩니다.  
  
또 다른 예로, 조직이 데이터 센터에서 200 테 넌 트를 사용 하는 CSP (클라우드 서비스 공급자) 인 경우 8 개의 RAS 게이트웨이 Vm 50을 사용할 수 있습니다. 이 시나리오에서는 Hyper-v를 실행 하는 두 대의 컴퓨터에 모두 RAS 게이트웨이로 구성 된 4 개의 Vm이 있습니다. 그런 다음, Hyper-v를 실행 하는 각 컴퓨터에서 하나의 VM을 포함 하는 4 개의 RAS 게이트웨이 VM 클러스터를 구성 합니다.  
  
RAS 게이트웨이를 배포 하는 경우 Hyper-v를 실행 하는 호스트 서버와 게이트웨이로 구성 하는 Vm은 Windows Server 2012 R2 또는 Windows Server 2016를 실행 해야 합니다.  
  
## <a name="ras-gateway-features"></a><a name="bkmk_features"></a>RAS 게이트웨이 기능  
RAS 게이트웨이는 다음과 같은 기능을 포함 합니다.  
  
-   **사이트 간 VPN**. 이 RAS 게이트웨이 기능을 사용 하면 사이트 간 VPN 연결을 사용 하 여 인터넷을 통해 서로 다른 물리적 위치에 있는 두 네트워크를 연결할 수 있습니다. 본사와 지점이 여러 개인 경우 각 위치에 edge RAS 게이트웨이를 배포 하 고 사이트 간 연결을 만들어 위치 간에 네트워크 트래픽 흐름을 제공할 수 있습니다. 데이터 센터에서 많은 테 넌 트를 호스팅하는 Csp의 경우, RAS 게이트웨이는 테 넌 트가 원격 사이트에서 사이트 간 VPN 연결을 통해 리소스를 액세스 및 관리할 수 있도록 하 고 네트워크 트래픽 흐름을 허용 하는 다중 테 넌 트 게이트웨이 솔루션을 제공 합니다. 데이터 센터의 가상 리소스와 실제 네트워크  
  
-   **지점 및 사이트 간 VPN**. 이 RAS 게이트웨이 기능을 통해 조직 직원 또는 관리자는 원격 위치에서 조직의 네트워크에 연결할 수 있습니다. RAS 게이트웨이의 단일 테 넌 트 배포의 경우 원격 직원은 VPN 연결을 사용 하 여 조직 네트워크에 연결할 수 있습니다. 이 연결을 통해 인트라넷 웹 사이트 및 파일 서버와 같은 내부 네트워크 리소스를 사용할 수 있습니다. 다중 테 넌 트 배포의 경우, 테 넌 트 네트워크 관리자는 지점 및 사이트 간 VPN 연결을 사용 하 여 CSP 데이터 센터의 가상 네트워크 리소스에 액세스할 수 있습니다.  
  
-   **BGP (Border Gateway Protocol)를 사용 하는 동적 라우팅** BGP는 동적 라우팅 프로토콜이기 때문에 라우터에서 수동으로 경로를 구성할 필요성이 줄어들고 사이트 간 VPN 연결을 사용하여 연결된 사이트 간 경로를 자동으로 알아냅니다. 조직에 RAS 게이트웨이와 같은 BGP 사용 라우터를 사용 하 여 연결 된 여러 사이트가 있는 경우 BGP를 사용 하면 네트워크 중단 또는 실패가 발생할 경우 라우터가 자동으로 유효한 경로를 계산 하 고 사용할 수 있습니다. 자세한 내용은 [RFC 4271](https://tools.ietf.org/html/rfc4271)을 참조 하세요.  
  
-   **NAT (Network Address Translation)** . NAT (네트워크 주소 변환)를 사용 하면 단일 공용 IP 주소를 사용 하는 단일 인터페이스를 통해 공용 인터넷에 대 한 연결을 공유할 수 있습니다. 개인 네트워크의 컴퓨터는 라우팅 불가능 한 개인 주소를 사용 합니다. NAT는 개인 주소를 공용 주소로 매핑합니다. 이 RAS 게이트웨이 기능을 통해 조직 직원은 단일 테 넌 트 배포를 통해 게이트웨이 뒤에서 인터넷 리소스에 액세스할 수 있습니다. Csp의 경우이 기능을 사용 하면 테 넌 트 Vm에서 실행 되는 응용 프로그램이 인터넷에 액세스할 수 있습니다. 예를 들어 웹 서버로 구성 된 테 넌 트 VM은 신용 카드 거래를 처리 하기 위해 외부 금융 리소스에 연결할 수 있습니다.  

  
## <a name="ras-gateway-deployment-scenarios"></a><a name="bkmk_deploy"></a>RAS 게이트웨이 배포 시나리오  
다음은 RAS Gateway에 권장 되는 배포 시나리오입니다.  
  
-   **Enterprise Edge-단일 테 넌 트 배포**. 단일 테 넌 트 엔터프라이즈 배포를 사용 하 여 사이트 간 VPN 기능을 사용 하 여 인터넷을 통해 물리적으로 물리적 위치 하나를 연결 하 고, BGP (Border Gateway Protocol)를 사용 하 여 동적 라우팅을 사용할 수 있습니다. 지점 및 사이트 간 VPN 연결 및 DirectAccess 연결을 모두 사용 하 여 원격 직원에 게 조직 네트워크에 대 한 액세스를 제공할 수도 있습니다. DirectAccess 연결은 항상 설정 되어 있으며 DirectAccess를 사용 하 여 연결 된 컴퓨터를 설정 하 고 인터넷에 연결할 때마다 연결 되므로이를 쉽게 관리할 수 있는 이점도 제공 합니다. 인트라넷의 컴퓨터가 인터넷과 쉽게 통신할 수 있도록 NAT를 사용 하 여 단일 테 넌 트 엔터프라이즈 RAS 게이트웨이를 구성할 수도 있습니다.  
  
-   **클라우드 서비스 공급자에 지-다중 테 넌 트 배포**. Csp에 대 한 RAS 게이트웨이 다중 테 넌 트 배포를 사용 하면 엔터프라이즈에 지 단일 테 넌 트 배포에서 사용할 수 있는 모든 기능을 테 넌 트에 제공할 수 있습니다. 데이터 센터에 있는 테 넌 트 가상 네트워크와 인터넷을 통한 테 넌 트 네트워크 위치 간의 사이트 간 VPN 연결을 통해 테 넌 트가 항상 클라우드 리소스에 원활 하 게 액세스할 수 있습니다. 테 넌 트에 대 한 지점 및 사이트 간 VPN 액세스는 테 넌 트 관리자가 항상 데이터 센터의 가상 네트워크에 연결 하 여 리소스를 관리할 수 있음을 의미 합니다. BGP는 인터넷에서 네트워크 문제가 발생 하는 경우에도 동적 라우팅을 제공 하 고 테 넌 트가 자산에 연결 된 상태로 유지 합니다. 및 NAT를 통해 테 넌 트 Vm은 신용 카드 처리 리소스와 같은 인터넷의 리소스에 연결할 수 있습니다.  
  
## <a name="ras-gateway-management-tools"></a><a name="bkmk_manage"></a>RAS 게이트웨이 관리 도구  
RAS 게이트웨이에 대 한 관리 도구는 다음과 같습니다.  
  
-   Windows Server 2016에서 RAS 게이트웨이 라우터를 배포 하려면 Windows PowerShell 명령을 사용 해야 합니다. 자세한 내용은 Windows Server 2016 및 Windows 10 용 [원격 액세스 cmdlet](https://docs.microsoft.com/powershell/module/remoteaccess) 을 참조 하세요.  
  
-   System Center 2012 R2 Virtual Machine Manager (VMM)에서 RAS 게이트웨이의 이름은 Windows Server Gateway입니다. **로컬 BGP IP 주소** 와 **Asn (자치 시스템 번호)** , **bgp 피어 IP 주소 목록**및 **asn 값**등 VMM 소프트웨어 인터페이스에서 제한 된 bgp (Border Gateway Protocol) 구성 옵션을 사용할 수 있습니다. 그러나 원격 액세스 Windows PowerShell BGP 명령을 사용하여 Windows Server 게이트웨이의 다른 모든 기능을 구성할 수 있습니다. 자세한 내용은 [Virtual Machine Manager (VMM)](https://technet.microsoft.com/system-center-docs/vmm/vmm) 및 windows Server 2016 및 windows 10 용 [원격 액세스 cmdlet](https://technet.microsoft.com/library/hh918399.aspx) 을 참조 하세요.  
  
## <a name="related-topics"></a>관련 항목
- [RAS 게이트웨이 고가용성](../../../networking/sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)  
- [Windows Server의 GRE 터널링](gre-tunneling-windows-server.md)
- [RAS 게이트웨이 GRE 터널 처리량 및 성능](RAS-Gateway-GRE-Perf.md)
