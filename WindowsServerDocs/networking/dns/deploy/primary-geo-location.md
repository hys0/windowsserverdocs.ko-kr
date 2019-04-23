---
title: 주 서버를 사용한 지리적 위치 기반 트래픽 관리에 DNS 정책 사용
description: 이 항목은 DNS 정책 시나리오 가이드에 대 한 Windows Server 2016의 일부
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: ef9828f8-c0ad-431d-ae52-e2065532e68f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 110014adf1e23be574f23efc01e8a4d69397e547
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831984"
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers"></a>주 서버를 사용한 지리적 위치 기반 트래픽 관리에 DNS 정책 사용

>적용 대상: Windows Server (반기 채널), Windows Server 2016

가장 가까운 리소스의 IP 주소로 클라이언트 제공 클라이언트와를 클라이언트에서 연결 하려는, 리소스의 지리적 위치에 따라 DNS 클라이언트 쿼리에 응답 하도록 DNS 서버를 주 수 있도록 DNS 정책을 구성 하는 방법에 알아보려면이 항목을 사용할 수 있습니다.  
  
>[!IMPORTANT]  
>이 시나리오에만 주 DNS 서버를 사용할 때 지리적 위치 기반 트래픽 관리에 대 한 DNS 정책을 배포 하는 방법을 보여 줍니다. 기본 및 보조 DNS 서버가 있는 경우에 지리적 위치 기반 트래픽 관리를 수행할 수 있습니다. 주-보조 배포가 있는 경우 먼저이 항목의 단계를 완료 하 고 다음 항목에서 제공 되는 단계를 완료 [기본보조배포와지리적위치기반트래픽관리에대한DNS정책을사용하여](primary-secondary-geo-location.md).

새 DNS 정책을 사용 하 여 클라이언트 쿼리 웹 서버의 IP 주소에 대 한 요청에 응답 하도록 DNS 서버를 허용 하는 DNS 정책을 만들 수 있습니다. 웹 서버 인스턴스는 서로 다른 물리적 위치에 있는 다른 데이터 센터에 있을 수 있습니다. DNS는 클라이언트 및 웹 서버 위치를 평가 하는 다음을 제공 하 여 클라이언트와 웹 서버 IP 주소는 클라이언트에 더 가까이 있는 물리적으로 웹 서버에 대 한 클라이언트 요청에 응답할 수 있습니다.  

DNS 클라이언트의 쿼리에 DNS 서버 응답을 제어 하는 다음 DNS 정책 매개 변수를 사용할 수 있습니다. 

- **클라이언트 서브넷**합니다. 미리 정의 된 클라이언트 서브넷의 이름입니다. 쿼리를 전송한 서브넷을 확인 하는 데 사용 합니다.
- **전송 프로토콜**합니다. 쿼리에 사용 되는 프로토콜을 전송 합니다. 가능한 항목은 **UDP** 및 **TCP**합니다.
- **인터넷 프로토콜**합니다. 쿼리에서 사용 되는 네트워크 프로토콜입니다. 가능한 항목은 **IPv4** 및 **IPv6**합니다.
- **서버 인터페이스 IP 주소**합니다. DNS 요청을 수신 하는 DNS 서버의 네트워크 인터페이스의 IP 주소입니다.
- **FQDN**합니다. 완전히 정규화 된 도메인 이름 (FQDN) 쿼리에서 레코드의 와일드 카드를 사용 하 여 가능성입니다.
- **쿼리 유형**합니다. 레코드 쿼리 중인 (A, SRV, TXT 등)의 형식입니다.
- **하루 중 시간**합니다. 쿼리가 수신 되는 날의 시간입니다. 
  
논리 연산자 (및/또는) 정책 식을 작성 하는 데는 다음과 같은 조건을 결합할 수 있습니다. 이러한 식은 일치 하는 경우 정책은 다음 작업 중 하나를 수행 해야 합니다.
 
- **무시**합니다. DNS 서버는 자동으로 쿼리를 삭제합니다.          
- **거부** DNS 서버는 해당 쿼리는 실패 응답으로 응답합니다.          
- **허용** DNS 서버가 트래픽 관리 되는 응답으로 다시 응답 합니다.          
  
##  <a name="bkmk_example"></a>지리적 위치 기반 트래픽 관리 예제

다음은 DNS 쿼리를 수행 하는 클라이언트의 실제 위치를 기준으로 트래픽 리디렉션은 달성 하기 위해 DNS 정책 사용 방법의 예입니다.   
  
이 예제에서는 두 가상의 회사-웹 및 도메인 호스팅 솔루션을 제공 하는 Contoso 클라우드 서비스 사용 및 Woodgrove 식품 서비스, 전 세계에 걸쳐 여러 도시에서 음식 배달 서비스를 제공 하 고 웹 사이트 (가) 라는 woodgrove.com 합니다.  
  
Contoso 클라우드 서비스에는 하나 미국에서 및 유럽에서 다른 두 데이터 센터를 있습니다. 유럽 데이터 센터는 식료품을 woodgrove.com에 대 한 포털 주문를 호스팅합니다.   
  
Woodgrove.com 고객 웹 사이트에서 응답성이 뛰어난 환경을 얻을 수 있도록, 하려면 Woodgrove 유럽 데이터 센터로 전송 된 유럽 클라이언트와 미국 데이터 센터에 전달 하는 미국 클라이언트 하려고 합니다. 다른 곳에 위치한 전 세계의 고객 데이터 센터 중 하나을 보낼 수 있습니다.   
  
다음 그림에서는이 시나리오를 보여 줍니다.  
  
![지리적 위치 기반 트래픽 관리 예제](../../media/DNS-Policy-Geo1/dns_policy_geo1.png)  
  
##  <a name="bkmk_works"></a>DNS 확인 프로세스 이름을 어떻게 작동  
  
이름 확인 프로세스 중 사용자 www.woodgrove.com에 연결 하려고 합니다. 그러면 사용자의 컴퓨터에서 네트워크 연결 속성에서 구성 된 DNS 서버에 전송 되는 DNS 이름 확인 요청 됩니다. 일반적으로 역할 캐싱 해결 프로그램을 로컬 ISP에서 제공 하는 DNS 서버 이며는 LDNS 라고 합니다.   
  
DNS 이름이 LDNS의 로컬 캐시에 없으면 LDNS 서버 woodgrove.com에 대 한 권한이 있는 DNS 서버에 쿼리를 전달 합니다. 권한 있는 DNS 서버 LDNS 서버로 다시 사용자의 컴퓨터에 전송 하기 전에 로컬로 레코드를 캐시 하는 요청된 된 레코드 (www.woodgrove.com)를 사용 하 여 응답 합니다.  
  
Contoso 클라우드 서비스 DNS 서버 정책에 사용 하므로 contoso.com을 호스팅하는 권한 있는 DNS 서버는 지리적 위치 기반 트래픽 관리 되는 응답을 반환 하도록 구성 됩니다. 이 때문에 유럽 클라이언트의 방향을 유럽 데이터 센터와 미국 데이터 센터를 미국 클라이언트의 방향에는 그림에 나와 있습니다.  
  
이 시나리오에서는 일반적으로 권한 있는 DNS 서버 LDNS 서버에서을, 거의 사용자의 컴퓨터에서 오는 이름 확인 요청에 게 표시 됩니다. 이 때문에 권한 있는 DNS 서버에서 인식 되는 이름 확인 요청에서 원본 IP 주소 이며 LDNS 서버 사용자의 컴퓨터 하는 것입니다. 그러나 지리적 위치를 구성할 때 LDNS 서버의 IP 주소를 사용 하 여 사용자가 로컬 ISP의 DNS 서버를 쿼리 하기 때문에 응답 한 사용자의 지리적 위치를 공정 하 게 예측할 제공 하는 쿼리를 기반 합니다.  
  
>[!NOTE]  
>DNS 정책 DNS 쿼리를 포함 하는 UDP/TCP 패킷의 보낸 IP를 사용 합니다. 쿼리에서 여러 확인자/LDNS 홉을 통해 주 서버에 도달 하면 정책이 DNS 서버가 있는 쿼리를 받으면 마지막 해결 프로그램의 IP만을 고려 합니다.  
  
##  <a name="bkmk_config"></a>지리적 위치 기반 쿼리 응답에 대 한 DNS 정책을 구성 하는 방법  
지리적 위치를 기반으로 쿼리 응답에 대 한 DNS 정책을 구성 하려면 다음 단계를 수행 해야 합니다.  
  
1. [DNS 클라이언트 서브넷 만들기](#bkmk_subnets)  
2. [영역 범위 만들기](#bkmk_scopes)  
3. [영역 범위에 레코드 추가](#bkmk_records)  
4. [정책 만들기](#bkmk_policies)  
  
>[!NOTE]  
>구성할 영역에 대 한 권한이 있는 DNS 서버에서 이러한 단계를 수행 해야 합니다. 멤버 자격이 **DnsAdmins**, 또는 이와 동등한 다음 절차를 수행 해야 합니다.  
  
다음 섹션에서는 자세한 구성 지침을 제공 합니다.  
  
>[!IMPORTANT]  
>다음 섹션에서는 예제 많은 매개 변수 값이 포함 된 예제 Windows PowerShell 명령을 포함 합니다. 이러한 명령에 대 한 예제 값은 다음이 명령을 실행 하기 전에 배포에 적합 한 값으로 바꾸는 것을 확인 합니다.  
  
### <a name="bkmk_subnets"></a>DNS 클라이언트 서브넷 만들기  
  
첫 번째 단계 서브넷 또는 IP 주소 공간 트래픽을 리디렉션할 하려는 영역을 식별 하는 것입니다. 예를 들어 미국 및 유럽에 대 한 트래픽을 리디렉션할 하려면 서브넷 또는 IP 주소 공간 이러한 영역의 식별 해야 합니다.  
  
지역-IP 지도에서이 정보를 얻을 수 있습니다. 이러한 IP 지리적 분포에 따라, 만들어야 "DNS 클라이언트 서브넷." DNS 클라이언트 서브넷은 DNS 서버에 전송 되는 쿼리는 IPv4 또는 IPv6 서브넷의 논리적 그룹화입니다.  
  
DNS 클라이언트 서브넷을 만드는 다음 Windows PowerShell 명령을 사용할 수 있습니다.  
  
      
    Add-DnsServerClientSubnet -Name "USSubnet" -IPv4Subnet "192.0.0.0/24"  
      
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24"  
      
  
자세한 내용은 참조 [추가 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)합니다.  
  
### <a name="bkmk_scopes"></a>영역 범위 만들기  
클라이언트 서브넷 구성 요소를 두 개의 다른 영역 범위로 리디렉션할 트래픽을 각 사용자가 구성한 DNS 클라이언트 서브넷에 대 한 하나의 범위 영역을 분할 해야 합니다.   
  
예를 들어, DNS 이름 www.woodgrove.com에 대 한 트래픽을 리디렉션할 하려는 경우에 만들어야 합니다 두 개의 다른 영역 범위가 미국 및 유럽 woodgrove.com 영역입니다.  
  
영역 범위는 영역의 고유 인스턴스입니다. DNS 영역은 자체 DNS 레코드 집합이 포함 된 각 영역 범위를 갖는 여러 영역 범위를 가질 수 있습니다. 동일한 레코드는 동일한 IP 주소 또는 IP 주소가 다른 여러 범위에 있을 수 있습니다.  
  
>[!NOTE]  
>기본적으로 영역 범위 DNS 영역에 있습니다. 이 영역 범위 영역으로 동일한 이름을 가진 및 레거시 DNS 작업은이 범위에서 작동 합니다.   
  
다음 Windows PowerShell 명령을 사용 하 여 영역 범위를 만들 수 있습니다.  
  
      
    Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "USZoneScope"  
      
    Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "EuropeZoneScope"  

자세한 내용은 참조 [추가 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)합니다.  
  
### <a name="bkmk_records"></a>영역 범위에 레코드 추가  
이제 두 영역 범위에는 웹 서버 호스트를 나타내는 레코드를 추가 해야 합니다.   
  
예를 들어 **USZoneScope** 및 **EuropeZoneScope**합니다. USZoneScope를 IP 주소로 192.0.0.1, 미국 데이터 센터;에 있는 레코드 www.woodgrove.com를 추가할 수 있습니다. 및 EuropeZoneScope에서 유럽 데이터 센터에서 141.1.0.1 IP 주소와 동일한 레코드 (www.woodgrove.com)를 추가할 수 있습니다.   
  
레코드를 추가 하려면 영역 범위에는 다음 Windows PowerShell 명령을 사용할 수 있습니다.  
  
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "USZoneScope  
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "EuropeZoneScope"  
  
  
  
이 예제에서는 또한 전 세계의 나머지 두 데이터 센터 중 하나에서 woodgrove.com 웹 서버를 액세스할 수 계속 하려면 기본 영역 범위에 레코드를 추가 하려면 다음 Windows PowerShell 명령을 사용 해야 합니다.  
    
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1"   
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1"
      
 
**ZoneScope** 매개 변수는 기본 범위에서 레코드를 추가 하 여 포함 되지 않습니다. 표준 DNS 영역에 레코드를 추가 하는와 같습니다.  
  
자세한 내용은 참조 [추가 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)합니다.  
  
### <a name="bkmk_policies"></a>정책 만들기  
서브넷을 만든 후 (영역 범위), 파티션 및 사용자 레코드를 추가 했습니다, 그리고 영역의 올바른 범위 내에서 쿼리 응답의 DNS 클라이언트 서브넷 중 하나의 소스에서 쿼리 되 면 반환 되도록 서브넷과 파티션, 연결 하는 정책을 만들어야 합니다. 정책이 기본 영역 범위 매핑을 지정 해야 합니다.   
  
DNS 클라이언트 서브넷에 연결 되 고 영역 범위가 DNS 정책을 만들려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.   
  
      
    Add-DnsServerQueryResolutionPolicy -Name "USPolicy" -Action ALLOW -ClientSubnet "eq,USSubnet" -ZoneScope "USZoneScope,1" -ZoneName "woodgrove.com"  
      
    Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "EuropeZoneScope,1" -ZoneName "woodgrove.com"  
     
자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다.  
  
이제는 DNS 서버는 지리적 위치에 따라 트래픽을 리디렉션할 수 필요한 DNS 정책을 사용 하 여 구성 됩니다.  
  
DNS 서버 이름 확인 쿼리를 받으면 DNS 서버는 구성 된 DNS 정책에 대 한 DNS 요청에 있는 필드를 평가 합니다. 이름 확인 요청에서 원본 IP 주소를 일치 하는 정책 면 관련된 영역 범위 하는 데는 쿼리에 응답 하 고 사용자 지리적으로 가장 가까운 하는 리소스에 전달 됩니다.   
  
관리 요구 사항을 트래픽이 따라 DNS 정책의 수천을 만들 수 있습니다 하 고 들어오는 쿼리-DNS 서버를 다시 시작 하지 않고 모든 새 정책-동적으로 적용 됩니다.  
  
  
