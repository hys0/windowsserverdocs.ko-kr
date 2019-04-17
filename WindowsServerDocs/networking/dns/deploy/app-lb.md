---
title: DNS 정책을 사용 하 여 응용 프로그램 부하 분산에 대 한
description: 이 항목은 Windows Server 2016 용 DNS 정책 시나리오 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9c313ac-bb86-4e48-b9b9-de5004393e06
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d156c258b971c45bf1c4c20739440bd5cc9e239f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-application-load-balancing"></a>DNS 정책을 사용 하 여 응용 프로그램 부하 분산에 대 한

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 부하 분산 응용 프로그램을 수행 하도록 DNS 정책을 구성 하는 방법을 알아보려면 사용할 수 있습니다.

이전 버전의 Windows Server DNS 차례로 응답;를 사용 하 여 부하 분산만 제공 하지만, Windows Server 2016에 dns 부하 분산 응용 프로그램에 대 한 정책을 DNS 구성할 수 있습니다.

여러 개 응용 프로그램을 배포 하는 경우 DNS 정책 응용 프로그램에 대 한 교통량 로드 동적으로 함으로써 할당 다른 응용 프로그램이 인스턴스 간에 교통 부하 분산을 사용할 수 있습니다.

## <a name="example-of-application-load-balancing"></a>응용 프로그램 부하 분산 예제

다음은 예 부하 분산 응용 프로그램에 대 한 DNS 정책을 사용 하는 방법입니다.

사용 하 여 한 가상 회사-Contoso 선물 서비스-gifing 온라인 서비스를 제공 하는 및 라는 웹 사이트가 되어 있는이 예제 **contosogiftservices.com**합니다.

Contosogiftservices.com 웹 사이트가 다른 IP 주소를 포함 하는 여러 데이터 센터에 호스트 합니다.

Contoso 선물 서비스에 대 한 주요 지역/국가 북미 지역에서 웹 사이트 세 데이터 센터에 호스트: 시카고, IL, 댈러스 텍사스주 및 워싱턴 주 시애틀 합니다.

시애틀 웹 서버 최상의 하드웨어 구성에 및 두 가지 다른 사이트와 배가 로드 처리할 수 있습니다. Contoso 선물 서비스 응용 프로그램 교통 다음과 같은 방법으로 전달 하려고 합니다.

- 시애틀 웹 서버에 더 많은 리소스를 있기 때문에이 서버에 매핑됩니다 절반 응용 프로그램의 클라이언트
- 댈러스 텍사스주 datacenter 리디렉션되는 4 분의 응용 프로그램의 클라이언트
- 응용 프로그램의 클라이언트 4 분의 1 시카고, IL datacenter 리디렉션되는

다음 그림에서는이 시나리오를 보여 줍니다.

![DNS 응용 프로그램 부하 분산 DNS 정책](../../media/Dns-App-Lb/dns-app-lb.jpg)


### <a name="how-application-load-balancing-works"></a>응용 프로그램 균형 작동

구성한 경우 응용 프로그램에 대 한 DNS 정책 사용 하 여 DNS 서버 로드이 예제 시나리오를 사용 하 여 균형 조정 DNS 서버가 응답 50% 비율로 25% 댈러스 웹 서버 주소를 사용 시간 및 시카고 웹 서버 주소를 사용 시간 25% 시애틀 웹 서버 주소를 사용 합니다.

따라서 DNS 서버를 받는 모든 4 쿼리를에 대 한 응답으로 두 응답 시애틀 및 각에 대 한 댈러스 및 시카고.

가능한 한 문제가 부하 분산 DNS 정책을 사용 하 여 DNS 클라이언트와 부하 분산 클라이언트 또는 확인자 수행 보내지 쿼리 DNS 서버를 방해할 수 있는 해결/LDNS, DNS 레코드 캐싱입니다.

낮은 Time\ to\ 라이브 \(TTL\) 값 부하가 되어야 하는 DNS 레코드에 대 한 사용 하 여이 문제의 영향을 줄일 수 있습니다.

### <a name="how-to-configure-application-load-balancing"></a>응용 프로그램 부하 분산 구성 하는 방법

다음 섹션 DNS 정책을 부하 분산 응용 프로그램에 대 한 구성 하는 방법을 보여 줍니다.

#### <a name="create-the-zone-scopes"></a>영역 범위가 만들기

먼저의 범위 영역 contosogiftservices.com 데이터 센터에 대 한 호스트 되는 위치 만들어야 합니다.

영역 범위 영역의 고유한 인스턴스입니다. DNS 영역 고유한 DNS 레코드에 포함 된 각 영역 범위와의 여러 영역 범위에 있을 수 있습니다. 동일한 기록 IP 주소가 서로 다른 여러 범위 또는 동일한 IP 주소에서 사용할 수 있습니다.

>[!NOTE]
>기본적으로 영역 범위 DNS 영역에 있습니다. 해당 영역 같은 이름이이 영역 범위 및이 범위 레거시 DNS 작업 작업 합니다.

다음 Windows PowerShell 명령을 영역 범위가 만드는 사용할 수 있습니다.
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DallasZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "ChicagoZoneScope"

자세한 내용은 참조 [DnsServerZoneScope 추가](https://technet.microsoft.com/library/mt126267.aspx)

####<a name="bkmk_records"></a>레코드 영역 범위에 추가

이제 영역 범위에는 웹 서버 호스트 나타내는 레코드를 추가 해야 합니다.

**SeattleZoneScope**, 시애틀 데이터 센터에 있는 192.0.0.1, IP 주소를 가진 녹화 www.contosogiftservices.com 추가할 수 있습니다.

**ChicagoZoneScope**, 182.0.0.1 IP 주소와 동일한 녹화 \(www.contosogiftservices.com\) 시카고 데이터 센터에 추가할 수 있습니다.

마찬가지로 내에 **DallasZoneScope**, IP 주소 162.0.0.1 기록 \(www.contosogiftservices.com\) 시카고 데이터 센터에 추가할 수 있습니다.

기록 영역 범위에 추가 하는 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "182.0.0.1" -ZoneScope "ChicagoZoneScope"
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "162.0.0.1" -ZoneScope "DallasZoneScope"
    

자세한 내용은 참조 [추가 DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx)합니다.

####<a name="bkmk_policies"></a>DNS 정책 만들기

파티션 (영역 범위가) 만든 기록 추가한 후 50 %contosogiftservices.com 대 한 쿼리가의 IP 주소가 시애틀 데이터 센터의 웹 서버에 대 한 응답 하 고 나머지 시카고 및 댈러스 데이터 센터 간에 동일 하 게 배포 이러한 범위 들어오는 쿼리 분산 DNS 정책 만들어야 합니다.

다음 세 가지 데이터 센터 응용 프로그램 교통 너무 DNS 정책을 만들려면 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.

>[!NOTE]
>예 명령 식 아래에서 – ZoneScope "SeattleZoneScope, 2; ChicagoZoneScope 1; 매개 조합이 포함 배열을 사용 하 여 DNS 서버, DallasZoneScope 1"구성 \ < ZoneScope\ > \ < weight\ > 합니다.
    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW – -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1;DallasZoneScope,1" -ZoneName "contosogiftservices.com"
    

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx)합니다.  

이제 응용 프로그램 부하 분산 웹 서버 세 가지 다른 데이터 센터에서 제공 하는 DNS 정책을 만든 했습니다.

관리 요구 사항에 교통에 따라 DNS 정책 수천을 만들 수 있습니다 고-들어오는 쿼리에서 DNS 서버를 다시 시작 하지 않고 모든 새로운 정책 동적-적용 됩니다.