---
title: 응용 프로그램 부하 분산에 대 한 DNS 정책을 사용 하 여
description: 이 항목은 Windows Server 2016에 대 한 DNS 정책 시나리오 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9c313ac-bb86-4e48-b9b9-de5004393e06
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 86ce83142cafe8ebe61aff2fb193e9b646172651
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317883"
---
# <a name="use-dns-policy-for-application-load-balancing"></a>응용 프로그램 부하 분산에 대 한 DNS 정책을 사용 하 여

>적용 대상: Windows Server(반기 채널), Windows Server 2016

애플리케이션 부하 분산을 수행 하는 DNS 정책을 구성 하는 방법에 알아보려면이 항목을 사용할 수 있습니다.

이전 버전의 Windows Server DNS 라운드 로빈 응답;를 사용 하 여 부하 분산만 제공 됩니다. 하지만 Windows Server 2016, dns 애플리케이션 부하 분산에 대 한 DNS 정책을 구성할 수 있습니다.

애플리케이션의 여러 인스턴스를 배포한 경우 애플리케이션에 대 한 트래픽 부하를 할당 하 여 동적으로, 다른 애플리케이션 인스턴스 간에 트래픽 부하를 분산 DNS 정책을 사용할 수 있습니다.

## <a name="example-of-application-load-balancing"></a>응용 프로그램 부하 분산의 예

다음은 애플리케이션 부하 분산에 대 한 DNS 정책 사용 방법의 예입니다.

이 예제에서는 하나의 가상 회사 Contoso 선물 서비스-온라인 gifing 서비스를 제공 하 고 (가) 라는 웹 사이트를 사용 하 여 **contosogiftservices.com**합니다.

Contosogiftservices.com 웹 사이트는 각각 서로 다른 IP 주소를 갖고 있는 여러 데이터 센터에서 호스팅됩니다.

세 개의 데이터 센터에서 호스팅되는 웹 사이트는 Contoso 선물 서비스에 대 한 기본 시장 북아메리카 지역에: 일리노이 주 시카고, 달라스, TX 및 미국 워싱턴주 시애틀 합니다.

시애틀 웹 서버에 가장 적합 한 하드웨어 구성을 두 개의 다른 사이트와 두 배 많은 부하를 처리할 수 있습니다. Contoso 선물 서비스는 다음과 같은 방식에서 보낸 애플리케이션 소통량을 하려고 합니다.

- 시애틀 웹 서버에서 더 많은 리소스를 포함 하기 때문에이 서버에 전달 되는 애플리케이션의 클라이언트의 절반
- 애플리케이션의 클라이언트의 1/4 Dallas 텍사스 데이터 센터에 매핑됩니다.
- 애플리케이션의 클라이언트의 1/4 주 시카고 데이터 센터에 매핑됩니다.

다음 그림에서는이 시나리오를 보여 줍니다.

![DNS 응용 프로그램 부하 DNS 정책을 사용 하 여 분산](../../media/Dns-App-Lb/dns-app-lb.jpg)


### <a name="how-application-load-balancing-works"></a>응용 프로그램 부하를 분산 작동

구성한 후 애플리케이션에 대 한 DNS 정책 사용 하 여 DNS 서버 로드이 예제 시나리오를 사용 하 여 분산 DNS 서버가 응답 하는 50%의 시간 Dallas 웹 서버 주소를 사용 하 여 시간의 25%에서 25% 시카고 웹 서버 주소를 사용 하 여 시간의 시애틀 웹 서버 주소를 사용 합니다.

따라서 DNS 서버가 받으면 마다 4 개의 쿼리에 대 한 응답을 보냅니다 두 응답 시애틀과 마다 하나씩 댈러스와 시카고에 대 한 합니다.

부하 분산 DNS 정책을 사용 하 여 가능한 한 가지 문제는 DNS 클라이언트와 클라이언트 또는 확인자를 전송 하지 마십시오 쿼리 DNS 서버에 때문에 부하 분산이 방해할 수 있는 확인자/LDNS, DNS 레코드를 캐시.

낮은 시간을 사용 하 여이 동작의 영향을 줄일 수 있습니다\-에\-Live \(TTL\) DNS 레코드는 부하를 분산할 수에 대 한 값입니다.

### <a name="how-to-configure-application-load-balancing"></a>응용 프로그램 부하 분산을 구성 하는 방법

다음 섹션에서는 애플리케이션 부하 분산에 대 한 DNS 정책을 구성 하는 방법을 보여 줍니다.

#### <a name="create-the-zone-scopes"></a>영역 범위를 만듭니다

범위 영역 contosogiftservices.com에 대 한 데이터 센터에서 호스팅되는 위치를 먼저 만들어야 합니다.

영역 범위는 영역의 고유 인스턴스입니다. DNS 영역은 자체 DNS 레코드 집합이 포함 된 각 영역 범위를 갖는 여러 영역 범위를 가질 수 있습니다. 동일한 레코드는 동일한 IP 주소 또는 IP 주소가 다른 여러 범위에 있을 수 있습니다.

>[!NOTE]
>기본적으로 영역 범위 DNS 영역에 있습니다. 영역을 같은 이름의이 영역 범위 및 레거시 DNS 작업은이 범위에서 작동 합니다.

다음 Windows PowerShell 명령을 사용 하 여 영역 범위를 만들 수 있습니다.
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DallasZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "ChicagoZoneScope"

자세한 내용은 참조 [DnsServerZoneScope 추가](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

#### <a name="add-records-to-the-zone-scopes"></a><a name="bkmk_records"></a>영역 범위에 레코드 추가

이제 영역 범위에는 웹 서버 호스트를 나타내는 레코드를 추가 해야 합니다.

**SeattleZoneScope**, 시애틀 데이터 센터에 있는 192.0.0.1, IP 주소를 가진 레코드 www.contosogiftservices.com를 추가할 수 있습니다.

**ChicagoZoneScope**, 동일한 레코드를 추가할 수 있습니다 \(www.contosogiftservices.com\) 을 IP 주소 182.0.0.1 시카고 데이터 센터에 있습니다.

마찬가지로 **DallasZoneScope**, 레코드를 추가할 수 \(www.contosogiftservices.com\) 을 IP 주소 162.0.0.1 시카고 데이터 센터에 있습니다.

레코드를 추가 하려면 영역 범위에는 다음 Windows PowerShell 명령을 사용할 수 있습니다.
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "182.0.0.1" -ZoneScope "ChicagoZoneScope"
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "162.0.0.1" -ZoneScope "DallasZoneScope"
    

자세한 내용은 참조 [추가 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)합니다.

#### <a name="create-the-dns-policies"></a><a name="bkmk_policies"></a>DNS 정책 만들기

파티션 (영역 범위)를 만든 후 레코드를 추가한 후 contosogiftservices.com에 대 한 쿼리의 50% 시애틀 데이터 센터의 웹 서버에 대 한 IP 주소를 가진 응답 하 고 나머지 시카고 및 Dallas 데이터 센터 간에 동일 하 게 배포 되도록 이러한 범위 간에 들어오는 쿼리를 분산 하는 DNS 정책을 만들어야 합니다.

이러한 세 개의 데이터 센터에서 애플리케이션 트래픽을 분산 하는 DNS 정책을 만들려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.

>[!NOTE]
>식 아래 예에서는 명령에서-ZoneScope "SeattleZoneScope, 2; ChicagoZoneScope, 1; DallasZoneScope, 1"DNS 서버를 구성 매개 변수 조합에 포함 된 배열을 사용 하 여 \<ZoneScope\>,\<가중치\>합니다.
    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1;DallasZoneScope,1" -ZoneName "contosogiftservices.com"
    

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다.  

이제 성공적으로 만든 세 가지 다른 데이터 센터의 웹 서버에 걸쳐 분산 애플리케이션 부하를 제공 하는 DNS 정책을 합니다.

관리 요구 사항을 트래픽이 따라 DNS 정책의 수천을 만들 수 있습니다 하 고 들어오는 쿼리-DNS 서버를 다시 시작 하지 않고 모든 새 정책-동적으로 적용 됩니다.
