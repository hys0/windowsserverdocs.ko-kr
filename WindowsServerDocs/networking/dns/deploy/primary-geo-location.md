---
title: 지리적 위치를 사용 하 여 DNS 정책 기반 기본 서버와 함께 교통 체증 관리
description: 이 항목은 Windows Server 2016 용 DNS 정책 시나리오 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: ef9828f8-c0ad-431d-ae52-e2065532e68f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bd72e13cd3d2d7f3ca886afcdcf97e824ef227f5
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers"></a>지리적 위치를 사용 하 여 DNS 정책 기반 기본 서버와 함께 교통 체증 관리

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

클라이언트 가까운 리소스의 IP 주소를 제공 주 DNS 서버 DNS 클라이언트 쿼리가 클라이언트 및, 연결을 시도 하는 클라이언트를 리소스 지리적 위치에 따라에 응답할 수 있도록 DNS 정책 구성 하는 방법을 알아보려면이 항목을 사용할 수 있습니다.  
  
>[!IMPORTANT]  
>이 시나리오 주 DNS 서버를 사용할 때 지리적 위치를 기반으로 교통 관리에 대 한 정책을 DNS 배포 하는 방법을 보여 줍니다. 기본 및 보조 DNS 서버를 있는 경우에 지리적 위치를 기반으로 교통 관리를 수행할 수 있습니다. 주 보조 배포를 사용 하는 경우 먼저이 항목의 단계를 완료 한 다음 항목에서 제공 되는 단계를 완료 [주 보조 배포와 지리적 위치를 기반 교통 관리에 대 한 사용 하 여 DNS 정책을](primary-secondary-geo-location.md)합니다.

새 DNS 정책, DNS 서버 클라이언트 쿼리가 IP 주소 웹 서버에 대 한 요청에 응답할 수 있도록 해 주는 DNS 정책을 만들 수 있습니다. 인스턴스 웹 서버 서로 다른 위치에서 다른 데이터 센터에 남아 있을 수 있습니다. DNS는 클라이언트 및 웹 서버 위치 평가 하는 다음을 제공 하 여 클라이언트 웹 서버에 IP 주소는 실제로 더 가까이 클라이언트 하는 웹 서버에 대 한 클라이언트 요청에 응답할 수 있습니다.  

DNS 클라이언트에서 DNS 서버 응답 쿼리를 제어 하는 다음 DNS 정책 매개 변수를 사용할 수 있습니다. 

- **클라이언트 서브넷**합니다. 미리 정의 된 클라이언트 서브넷의 이름입니다. 쿼리를 보낸 서브넷 확인할 수 있습니다.
- **프로토콜 전송**합니다. 프로토콜 쿼리에 사용 되는 전송 합니다. 가능한 한 항목은 **UDP** 및 **TCP**합니다.
- **인터넷 프로토콜**합니다. 네트워크 프로토콜 쿼리에 사용 합니다. 가능한 한 항목은 **IPv4** 및 **IPv6**합니다.
- **서버 인터페이스 IP 주소**합니다. IP 주소 DNS 요청을 받은 DNS 서버 네트워크 인터페이스입니다.
- **FQDN**합니다. 된 적격 도메인 이름 (FQDN) 쿼리에 기록의 가능성을 와일드 카드를 사용 하 여 사용 합니다.
- **쿼리 유형**합니다. 기록 쿼리 중인 (A, SRV, TXT 등) 형식 있습니다.
- **하루 중 시간**합니다. 쿼리 수신 하는 하루 중 시간입니다. 
  
다음 기준을 논리 통신사와 (및/또는)을 정책 식 수립 결합할 수 있습니다. 이러한 식 일치 하는 경우 다음 중 하나를 수행 하려면 정책은 예상 됩니다.
 
- **무시**합니다. DNS 서버 쿼리를 자동으로 삭제합니다.          
- **거부**합니다. DNS 서버가 응답을 오류와 해당 쿼리를 응답합니다.          
- **허용**합니다. DNS 서버가 응답에 관리 하는 교통 응답 합니다.          
  
##  <a name="bkmk_example"></a>지리적 위치 기반 교통 관리 예

다음은 DNS 정책 DNS 쿼리를 수행 하는 클라이언트의 실제 위치를 기반으로 교통 리디렉션을 달성 하기 위해 사용 하는 방법을의 예입니다.   
  
사용 하 여 웹 및 솔루션; 호스팅 도메인을 제공 하는 클라우드 서비스를 Contoso 두 가상 회사-이 예제 하 고 Woodgrove 음식 서비스 세계 여러 도시에서 다양 한 음식 배달 서비스를 제공 하는 웹 사이트 woodgrove.com 라는 되어 있는.  
  
Contoso 클라우드 서비스는 미국에서 크기 조정 설정과 유럽의 두 개의 데이터 센터를 있습니다. 유럽 datacenter 호스트 woodgrove.com 포털 주문 음식 합니다.   
  
woodgrove.com 고객이 해당 웹 사이트에서 응답 경험을 가져올 되도록 Woodgrove 유럽 유럽 데이터 센터에 게 연락 하는 클라이언트와 미국 클라이언트 미국 데이터 센터에 게 연락 하려고 합니다. 다른 곳에서 전 세계에 있는 고객 데이터 센터 중 하나를 보낼 수 있습니다.   
  
다음 그림에서는이 시나리오를 보여 줍니다.  
  
![지리적 위치 기반 교통 관리 예](../../media/DNS-Policy-Geo1/dns_policy_geo1.png)  
  
##  <a name="bkmk_works"></a>DNS 해상도 프로세스 이름을 어떻게 작동  
  
이름 해상도 과정에서 사용자가 www.woodgrove.com에 연결 하려고 합니다. 이 인해 사용자의 컴퓨터에서 네트워크 연결 속성에서 구성 된 DNS 서버에 전송 된 DNS 이름 해상도 요청 합니다. 일반적으로 역할을 캐싱 확인자 ISP 지역에서 제공 되는 DNS 서버 이며 고 LDNS 라고도 합니다.   
  
DNS 이름 없는 경우에 로컬 캐시 LDNS의, LDNS 서버 쿼리 woodgrove.com를 신뢰할 수 있는 DNS 서버를 전달 됩니다. 정식 DNS 서버 결과적 기록 사용자의 컴퓨터에 보내기 전에 로컬 캐시 LDNS 서버에 요청된 레코드 (www.woodgrove.com)로 응답 합니다.  
  
정책 DNS 서버를 사용 하는 클라우드 서비스 Contoso 때문에 호스트 contoso.com 지리적 위치를 반환 하도록 구성 되어 정식 DNS 서버 관리 교통 응답 기반으로 합니다. 따라서 유럽 클라이언트의 방향을를 유럽 datacenter, 미국 데이터 센터에 미국 클라이언트의 방향을 그림에서 표시 된 대로 수 있습니다.  
  
이 경우 정식 DNS 서버 일반적으로 출시 LDNS 서버 및, 자주에서 사용자의 컴퓨터 이름을 확인 요청을 볼 수 있습니다. 이 때문 원본 IP 주소를 볼 수 있는 권한이 DNS 서버 이름 해상도 요청에서 LDNS 서버 하 고 사용자의 컴퓨터의 하는 것입니다. 그러나 지리적 위치를 구성할 때 LDNS 서버의 IP 주소를 사용 하 여 사용자의 로컬 ISP DNS 서버에 쿼리 때문에 응답 특히 예측의는 사용자의 지리적 위치를 제공 쿼리를 기반 합니다.  
  
>[!NOTE]  
>DNS 정책에 포함 되어 DNS 쿼리에 UDP/TCP 패킷 보낸 사람에 게 IP 활용 합니다. 쿼리 여러 확인자/LDNS 홉 통해 기본 서버에 도달 하면 정책을 DNS 서버를 쿼리를 받고 마지막 확인자 IP 고려 합니다.  
  
##  <a name="bkmk_config"></a>DNS 정책 기반 쿼리 응답 지리적 위치에 대 한 구성 하는 방법  
DNS 쿼리에 응답 지리적 위치를 기반 정책, 구성 하려면 다음 단계를 수행 해야 합니다.  
  
1. [DNS 클라이언트 서브넷 만들기](#bkmk_subnets)  
2. [영역 범위 만들기](#bkmk_scopes)  
3. [레코드 영역 범위에 추가](#bkmk_records)  
4. [정책은 만들기](#bkmk_policies)  
  
>[!NOTE]  
>DNS 서버를 구성할 영역에 대 한 권한이 있는에서 다음이 단계를 수행 해야 합니다. 회원 **DnsAdmins**, 다음 절차를 수행 하는 데 필요한는 오른쪽 단추를 클릭 합니다.  
  
다음 섹션 자세한 구성 지침을 제공 합니다.  
  
>[!IMPORTANT]  
>다음 섹션에 대 한 많은 매개 예 값 포함 된 예제 Windows PowerShell 명령 포함 됩니다. 다음이 명령을 실행 하기 전에 배포에 대 한 적절 한 값으로 들어 값이 명령에서를 교체 해야 합니다.  
  
### <a name="bkmk_subnets"></a>DNS 클라이언트 서브넷 만들기  
  
첫 번째 단계 서브넷 또는 교통량 이동 하려는 지역의 IP 주소 공간을 확인 하는 것입니다. 예를 들어, 미국과 유럽 풍경에 대 한 교통량을 이동 하려면 서브넷 또는 해당이 지역의 IP 주소 공간을 확인 해야 합니다.  
  
지리적 IP 지도에서이 정보를 얻을 수 있습니다. 이러한 지리적 IP 배포 시에 따라, 만들어야 "DNS 클라이언트 서브넷." DNS 클라이언트 서브넷 DNS 서버에 전송 되어 쿼리를 V4 또는 IPv6 서브넷 논리 그룹입니다.  
  
DNS 클라이언트 서브넷 만들 수는 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.  
  
      
    Add-DnsServerClientSubnet -Name "USSubnet" -IPv4Subnet "192.0.0.0/24"  
      
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24"  
      
  
자세한 내용은 참조 [추가 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)합니다.  
  
### <a name="bkmk_scopes"></a>영역 범위가 만들기  
구성 요소를 클라이언트 서브넷 하나의 범위 구성 된 DNS 클라이언트 서브넷 각 영역 두 가지 영역 범위로 이동 하 고 싶은 트래픽을 분할 해야 합니다.   
  
예를 들어, www.woodgrove.com DNS 이름에 대 한 교통량을 이동 하려면 만들어야 두 서로 다른 영역 범위가 미국 및 유럽 woodgrove.com 영역에서 합니다.  
  
영역 범위 영역의 고유한 인스턴스입니다. DNS 영역 고유한 DNS 레코드에 포함 된 각 영역 범위와의 여러 영역 범위에 있을 수 있습니다. 동일한 기록 IP 주소가 서로 다른 여러 범위 또는 동일한 IP 주소에서 사용할 수 있습니다.  
  
>[!NOTE]  
>기본적으로 영역 범위 DNS 영역에 있습니다. 영역 같은 이름이이 영역 범위 및이 범위에 레거시 DNS 작업 작동 합니다.   
  
다음 Windows PowerShell 명령을 영역 범위가 만드는 사용할 수 있습니다.  
  
      
    Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "USZoneScope"  
      
    Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "EuropeZoneScope"  

자세한 내용은 참조 [추가 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)합니다.  
  
### <a name="bkmk_records"></a>레코드 영역 범위에 추가  
이제 두 영역 범위가에 웹 서버 호스트 나타내는 레코드를 추가 해야 합니다.   
  
예를 들어, **USZoneScope** 및 **EuropeZoneScope**합니다. USZoneScope, 미국, 데이터 센터에 있는 192.0.0.1 IP 주소와 기록 www.woodgrove.com 추가할 수 있습니다. 및 EuropeZoneScope에서 유럽 데이터 센터에 141.1.0.1 IP 주소와 동일한 기록 (www.woodgrove.com)를 추가할 수 있습니다.   
  
기록 영역 범위에 추가 하는 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.  
  
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "USZoneScope  
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "EuropeZoneScope"  
  
  
  
이 예제도 이곳의 나머지 방식은 여전히 액세스는 woodgrove.com 웹 서버에서 두 개의 데이터 센터 중 하나를 기본 영역 범위에 레코드를 추가 하는 다음과 같은 Windows PowerShell 명령의 사용 해야 합니다.  
    
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1"   
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1"
      
 
**ZoneScope** 기록 기본 범위 내에 추가 하면 매개가 포함 되지 않습니다. 표준 시간대 DNS 레코드를 추가 하는 것 같습니다.  
  
자세한 내용은 참조 [추가 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)합니다.  
  
### <a name="bkmk_policies"></a>정책은 만들기  
기록 파티션 (영역 범위가) 및 사용자를 추가 서브넷 만든 후 쿼리에 응답 올바른 영역 범위에서 반환 되는 쿼리 DNS 클라이언트 서브넷 중 하나에 소스에서 상태가 되 면 되도록 서브넷 및 파티션, 연결 하는 정책을 만들어야 합니다. 정책이 영역 기본 범위 매핑 필요 합니다.   
  
DNS 클라이언트 서브넷 연결 되 고 영역 범위가 DNS 정책을 만들려면 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.   
  
      
    Add-DnsServerQueryResolutionPolicy -Name "USPolicy" -Action ALLOW -ClientSubnet "eq,USSubnet" -ZoneScope "USZoneScope,1" -ZoneName "woodgrove.com"  
      
    Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "EuropeZoneScope,1" -ZoneName "woodgrove.com"  
     
자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다.  
  
이제 DNS 서버를 리디렉션하여 교통 지리적 위치에 따라 필요한 DNS 정책으로 구성 됩니다.  
  
DNS 서버 이름 확인 쿼리 받으면 DNS 서버 평가 필드에서 구성 된 DNS 정책에 대 한 DNS 요청 합니다. 이름 해상도 요청에서 원본 IP 주소와 일치 하는 정책, 관련된 영역 범위 쿼리에 응답 하는 데 사용 되 고에서 리소스에 지리적 가까운 사용자가 이동 합니다.   
  
관리 요구 사항에 교통에 따라 DNS 정책 수천을 만들 수 있습니다 고-들어오는 쿼리에서 DNS 서버를 다시 시작 하지 않고 모든 새로운 정책 동적-적용 됩니다.  
  
  
