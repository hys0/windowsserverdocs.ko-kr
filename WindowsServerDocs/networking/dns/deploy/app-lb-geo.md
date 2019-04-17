---
title: DNS 정책을 사용 하 여 응용 프로그램 부하 분산와 지리적 위치 인식에 대 한
description: 이 항목은 Windows Server 2016 용 DNS 정책 시나리오 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: b6e679c6-4398-496c-88bc-115099f3a819
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7637d927c7b22b83053e7f9100b07581c11bafc0
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-application-load-balancing-with-geo-location-awareness"></a>DNS 정책을 사용 하 여 응용 프로그램 부하 분산와 지리적 위치 인식에 대 한

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 DNS 정책을와 지리적 위치 인식 부하 분산 응용 프로그램을 구성 하는 방법을 알아보려면 사용할 수 있습니다.

이 가이드에서는 이전 항목 [부하 분산 응용 프로그램에 대 한 사용 하 여 DNS 정책을](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb), 사용 하 여 온라인 선물 제공 하는 가상 회사-Contoso 선물 서비스-의 예 서비스 및 되는 웹 사이트 이라는 contosogiftservices.com 합니다. Contoso 선물 서비스 로드 서버 워싱턴 주 시애틀, 시카고, IL 및 댈러스 텍사스주에는 북미 데이터 센터에 간 온라인 웹 응용 프로그램을 조정 합니다.

>[!NOTE]
>항목을 잘 알고 것이 좋습니다 [부하 분산 응용 프로그램에 대 한 사용 하 여 DNS 정책을](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb) 지침이 시나리오에서를 수행 하기 전에 합니다.

이 항목 지리적 위치 인식 포함 된 새 예 배포에 대 한 기본으로 동일한 가상 회사 및 네트워크 인프라를 사용 합니다.

여기에서 Contoso 선물 서비스 성공적으로 확장 자신의 존재 세계 합니다.

북미 지역와 마찬가지로, 이제 회사는 유럽 데이터 센터에서 호스트 하는 웹 서버 합니다.

Contoso 선물 서비스 DNS 관리자 응용 프로그램 균형 유럽 데이터 센터에 대 한를 미국에서 DNS 정책 구현 유사한 방식으로 응용 프로그램 교통 암스테르담, Dublin, 아일랜드, 네덜란드, 및 다른 곳에서 위치는 웹 서버에 분산 구성 해야 합니다.

DNS 관리자 모든 쿼리 데이터 센터의 모든 간에 동일 하 게 배포 하는 세계에서 다른 위치에서 수도 있습니다.

다음 섹션에는 사용자의 네트워크에 Contoso DNS 관리자 유사한 목표를 달성 하는 방법을 알아보십시오.

## <a name="how-to-configure-application-load-balancing-with-geo-location-awareness"></a>응용 프로그램 부하 분산 지리적 위치 인식을 구성 하는 방법

다음 섹션 DNS 정책 응용 프로그램 부하 분산와 지리적 위치 인식에 대 한 구성 하는 방법을 보여 줍니다.

>[!IMPORTANT]
>다음 섹션에 대 한 많은 매개 예 값 포함 된 예제 Windows PowerShell 명령 포함 됩니다. 다음이 명령을 실행 하기 전에 배포에 대 한 적절 한 값으로 들어 값이 명령에서를 교체 해야 합니다.

###<a name="bkmk_clientsubnets"></a>DNS 클라이언트 서브넷 만들기

먼저 서브넷 또는 유럽와 북미 지역의 IP 주소 공간 확인 해야 합니다.

지리적 IP 지도에서이 정보를 얻을 수 있습니다. 이러한 지리적 IP 배포 시에 따라, 만들어야 DNS 클라이언트 서브넷 합니다.

DNS 클라이언트 서브넷 DNS 서버에 전송 되어 쿼리를 V4 또는 IPv6 서브넷 논리 그룹입니다.

DNS 클라이언트 서브넷 만들 수는 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다. 

    
    Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet 192.0.0.0/24,182.0.0.0/24
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet 141.1.0.0/24,151.1.0.0/24
    
자세한 내용은 참조 [추가 DnsServerClientSubnet](https://technet.microsoft.com/library/mt126261.aspx)합니다.

###<a name="bkmk_zscopes2"></a>영역 범위가 만들기

후 클라이언트 서브넷 장소에는, 데이터 센터에 대 한 각 서로 다른 영역 범위로 영역 contosogiftservices.com을 분할 해야 합니다.

영역 범위 영역의 고유한 인스턴스입니다. DNS 영역 고유한 DNS 레코드에 포함 된 각 영역 범위와의 여러 영역 범위에 있을 수 있습니다. 동일한 기록 IP 주소가 서로 다른 여러 범위 또는 동일한 IP 주소에서 사용할 수 있습니다.

>[!NOTE]
>기본적으로 영역 범위 DNS 영역에 있습니다. 해당 영역 같은 이름이이 영역 범위 및이 범위 레거시 DNS 작업 작업 합니다.

응용 프로그램 부하 분산에 이전 시나리오 북미 지역에서 데이터 센터에 대해 세 가지 영역 범위 구성 하는 방법을 보여 줍니다.

다음 명령을 사용 하 여 두 더 많은 영역 범위가, Dublin 및 암스테르담 데이터 센터에 대 한 각 하나를 만들 수 있습니다. 

이러한 변경 없이 영역 범위 같은 영역에 세 개의 기존 북미 지역 영역 범위에 추가할 수 있습니다. 또한 이러한 영역 범위를 만든 후 DNS 서버를 다시 시작 필요가 없습니다.

다음 Windows PowerShell 명령을 영역 범위가 만드는 사용할 수 있습니다.

    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AmsterdamZoneScope"
    

자세한 내용은 참조 [DnsServerZoneScope 추가](https://technet.microsoft.com/library/mt126267.aspx)

###<a name="bkmk_records2"></a>레코드 영역 범위에 추가

이제 영역 범위에는 웹 서버 호스트 나타내는 레코드를 추가 해야 합니다.

아메리카 데이터 센터에 대 한 기록은 이전 시나리오에서 추가 되었습니다. 기록 유럽 데이터 센터에 대 한 영역 범위에 추가 하는 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.
 
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "151.1.0.1" -ZoneScope "DublinZoneScope”
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "AmsterdamZoneScope"
    

자세한 내용은 참조 [추가 DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx)합니다.

###<a name="bkmk_policies2"></a>DNS 정책 만들기

파티션 (영역 범위가) 만든 기록 추가한 후 이러한 범위 들어오는 쿼리 분산 DNS 정책 만들어야 합니다.

예를이 들어가 응용 서버 다른 데이터 센터에 배포 쿼리 다음 조건을 충족입니다.

1. 50%의 DNS 응답 가리킨 시애틀 데이터 센터에는 북미 클라이언트 서브넷 소스에서 DNS 쿼리에 받을 때 시카고 데이터 센터에 응답 25% 가리킨 하 고 응답 나머지 25% 댈러스 데이터 센터에 가리킵니다.
2. DNS 쿼리에 유럽 클라이언트 서브넷에서 소스에서 수신 하는 더블린 데이터 센터에 50%의 DNS 응답 가리키고 50%의 DNS 응답 암스테르담 datacenter 가리킵니다.
3. 쿼리 전 세계의 다른 곳에서 나옵니다, DNS 응답 모든 5 데이터 센터 분산 됩니다.

다음 Windows PowerShell 명령을 DNS 강화 하기 사용할 수 있습니다.

    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaLBPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1; TexasZoneScope,1" -ZoneName "contosogiftservices.com" –ProcessingOrder 1
    
    Add-DnsServerQueryResolutionPolicy -Name "EuropeLBPolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 2
    
    Add-DnsServerQueryResolutionPolicy -Name "WorldWidePolicy" -Action ALLOW -FQDN "eq,*.contoso.com" -ZoneScope "SeattleZoneScope,1;ChicagoZoneScope,1; TexasZoneScope,1;DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3
    
    

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx)합니다.

이제 응용 프로그램 부하 분산 여러 대륙에 5 개의 데이터 센터에 있는 웹 서버에서 제공 하는 DNS 정책을 만든 했습니다.

관리 요구 사항에 교통에 따라 DNS 정책 수천을 만들 수 있습니다 고-들어오는 쿼리에서 DNS 서버를 다시 시작 하지 않고 모든 새로운 정책 동적-적용 됩니다.
