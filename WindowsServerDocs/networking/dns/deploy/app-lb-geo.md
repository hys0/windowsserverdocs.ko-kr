---
title: 응용 프로그램 부하를 분산 하는 지리적 위치 인식 기능을 위한 DNS 정책을 사용 하 여
description: 이 항목은 DNS 정책 시나리오 가이드에 대 한 Windows Server 2016의 일부
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: b6e679c6-4398-496c-88bc-115099f3a819
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 806c0cdeedb44db44fc0ec5218124f516a6f70e5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852554"
---
# <a name="use-dns-policy-for-application-load-balancing-with-geo-location-awareness"></a>응용 프로그램 부하를 분산 하는 지리적 위치 인식 기능을 위한 DNS 정책을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016

지리적 위치 인식 기능을 사용 하 여 분산 응용 프로그램을 로드 하는 DNS 정책을 구성 하는 방법을 알아보려면이 항목에서는 사용할 수 있습니다.

이 가이드에서는 이전 항목 [응용 프로그램 부하 분산에 대 한 DNS 정책을 사용 하 여](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb)온라인 선물을 제공 하는 가상 회사 Contoso 선물 서비스-의 예로 서비스를 사용 하 여, 및 라는 웹 사이트에는 contosogiftservices.com 합니다. Contoso 선물 서비스 부하 시애틀, WA, 시카고 및 달라스, TX 있는 북미 데이터 센터에서 서버 간에 온라인 웹 응용 프로그램을 분산 합니다.

>[!NOTE]
>항목을 사용 하 여 친숙 해지는 것이 좋습니다 [응용 프로그램 부하 분산에 대 한 DNS 정책을 사용 하 여](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb) 이 시나리오의 지침을 수행 하기 전에 합니다.

이 항목에서는 지리적 위치 인식 기능을 포함 하는 새 예제 배포에 대 한 기준으로 같은 가상의 회사 및 네트워크 인프라를 사용 합니다.

이 예제에서는 Contoso 선물 서비스 전 세계에 걸쳐 근무 성공적으로 확장 됩니다.

North America와 마찬가지로, 이제 회사는 유럽 데이터 센터에서 호스팅되는 웹 서버입니다.

Contoso 선물 서비스 DNS 관리자가 응용 프로그램 부하에 있는 웹 서버 간에 분산 하는 응용 프로그램 트래픽을 사용 하 여 미국에 DNS 정책 구현에 비슷한 방식으로 유럽 데이터 센터에 대 한 분산을 구성. 더블린, 아일랜드, 암스테르담, 네덜란드, 및 다른 곳입니다.

DNS 관리자는 또한 모든 데이터 센터 간에 균등 하 게 분산 전 세계의 다른 위치에서 모든 쿼리를 원합니다.

다음 섹션에서는 사용자 고유의 네트워크에 Contoso DNS 관리자의 유사한 목표를 달성 하는 방법에 알아보십시오.

## <a name="how-to-configure-application-load-balancing-with-geo-location-awareness"></a>지리적 위치 인식 기능을 사용 하 여 분산 응용 프로그램을 구성 하는 방법

다음 섹션은 지리적 위치 인식 기능을 사용 하 여 분산 응용 프로그램에 대 한 DNS 정책을 구성 하는 방법을 보여 줍니다.

>[!IMPORTANT]
>다음 섹션에서는 예제 많은 매개 변수 값이 포함 된 예제 Windows PowerShell 명령을 포함 합니다. 이러한 명령에 대 한 예제 값은 다음이 명령을 실행 하기 전에 배포에 적합 한 값으로 바꾸는 것을 확인 합니다.

###<a name="bkmk_clientsubnets"></a>DNS 클라이언트 서브넷 만들기

서브넷 또는 IP 주소 공간의 North America 및 Europe 지역을 먼저 식별 해야 합니다.

지역-IP 지도에서이 정보를 얻을 수 있습니다. 이러한 IP 지리적 분포에 따라 DNS 클라이언트 서브넷을 만들어야 합니다.

DNS 클라이언트 서브넷은 DNS 서버에 전송 되는 쿼리는 IPv4 또는 IPv6 서브넷의 논리적 그룹화입니다.

DNS 클라이언트 서브넷을 만드는 다음 Windows PowerShell 명령을 사용할 수 있습니다. 

    
    Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet 192.0.0.0/24,182.0.0.0/24
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet 141.1.0.0/24,151.1.0.0/24
    
자세한 내용은 참조 [추가 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)합니다.

###<a name="bkmk_zscopes2"></a>영역 범위 만들기

클라이언트 서브넷을 배치한 후에 각 데이터 센터에 대 한 다른 영역 범위도 영역 contosogiftservices.com를 분할 해야 합니다.

영역 범위는 영역의 고유 인스턴스입니다. DNS 영역은 자체 DNS 레코드 집합이 포함 된 각 영역 범위를 갖는 여러 영역 범위를 가질 수 있습니다. 동일한 레코드는 동일한 IP 주소 또는 IP 주소가 다른 여러 범위에 있을 수 있습니다.

>[!NOTE]
>기본적으로 영역 범위 DNS 영역에 있습니다. 영역을 같은 이름의이 영역 범위 및 레거시 DNS 작업은이 범위에서 작동 합니다.

응용 프로그램 부하 분산에 이전 시나리오에는 북미에서 데이터 센터에 대 한 세 가지 영역 범위를 구성 하는 방법을 보여 줍니다.

아래 명령을 사용 하 여 두 더 많은 영역 범위, 더블린 및 암스테르담 데이터 센터에 대해 각각 하나씩 만들 수 있습니다. 

동일한 영역에 세 가지 기존 North America 영역 범위를 변경 하지 않고 이러한 영역 범위를 추가할 수 있습니다. 또한 이러한 영역 범위를 만든 후 DNS 서버를 다시 시작할 필요가 없습니다.

다음 Windows PowerShell 명령을 사용 하 여 영역 범위를 만들 수 있습니다.

    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AmsterdamZoneScope"
    

자세한 내용은 참조 [DnsServerZoneScope 추가](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

###<a name="bkmk_records2"></a>영역 범위에 레코드 추가

이제 영역 범위에는 웹 서버 호스트를 나타내는 레코드를 추가 해야 합니다.

미국 데이터 센터에 대 한 레코드는 이전 시나리오에서 추가 되었습니다. 유럽 데이터 센터에 대 한 영역 범위에 레코드를 추가 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.
 
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "151.1.0.1" -ZoneScope "DublinZoneScope”
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "AmsterdamZoneScope"
    

자세한 내용은 참조 [추가 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)합니다.

###<a name="bkmk_policies2"></a>DNS 정책 만들기

파티션 (영역 범위)를 만든 후 레코드를 추가한 후에 이러한 범위 간에 들어오는 쿼리를 분산 하는 DNS 정책을 만들어야 합니다.

예를 들어 여러 데이터 센터에서 응용 프로그램 서버에서 쿼리 배포는 다음 조건을 충족 합니다.

1. 북아메리카 클라이언트 서브넷에 있는 원본에서 DNS 응답의 50% 시애틀 데이터 센터를 가리키도록 하는 DNS 쿼리를 받을 때 응답의 25% 시카고 데이터 센터를 가리키도록 하 고 응답의 나머지 25 %Dallas 데이터 센터를 가리킵니다.
2. 유럽 클라이언트 서브넷에 있는 원본에서 DNS 쿼리를 받으면 DNS 응답의 50% 더블린 데이터 센터를 가리키고 DNS 응답의 50% 암스테르담 데이터 센터를 가리킵니다.
3. 전 세계의 다른 위치에서 쿼리 상태가 되 면 DNS 응답을 모든 5 개 데이터 센터 간에 분산 됩니다.

이러한 DNS 정책을 구현 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.

    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaLBPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1; TexasZoneScope,1" -ZoneName "contosogiftservices.com" –ProcessingOrder 1
    
    Add-DnsServerQueryResolutionPolicy -Name "EuropeLBPolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 2
    
    Add-DnsServerQueryResolutionPolicy -Name "WorldWidePolicy" -Action ALLOW -FQDN "eq,*.contoso.com" -ZoneScope "SeattleZoneScope,1;ChicagoZoneScope,1; TexasZoneScope,1;DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3
    
    

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다.

이제 성공적으로 만든 여러 대륙에 5 개의 서로 다른 데이터 센터에 있는 웹 서버에 걸쳐 분산 응용 프로그램을 제공 하는 DNS 정책을 합니다.

관리 요구 사항을 트래픽이 따라 DNS 정책의 수천을 만들 수 있습니다 하 고 들어오는 쿼리-DNS 서버를 다시 시작 하지 않고 모든 새 정책-동적으로 적용 됩니다.
