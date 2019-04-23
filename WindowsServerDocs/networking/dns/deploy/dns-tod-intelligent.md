---
title: 시간 기반 지능형 DNS 응답에 DNS 정책 사용
description: 이 항목은 DNS 정책 시나리오 가이드에 대 한 Windows Server 2016의 일부
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 161446ff-a072-4cc4-b339-00a04857ff3a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 33fd9447a79346127714a5e5e73977611eba483c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829474"
---
# <a name="use-dns-policy-for-intelligent-dns-responses-based-on-the-time-of-day"></a>시간 기반 지능형 DNS 응답에 DNS 정책 사용

>적용 대상: Windows Server (반기 채널), Windows Server 2016

하루 중 시간을 기반으로 하는 DNS 정책을 사용 하 여 응용 프로그램의 서로 다른 지리적으로 분산 된 인스턴스 응용 프로그램 트래픽을 분산 하는 방법에 알아보려면이 항목을 사용할 수 있습니다.  
  
이 시나리오는 다른 표준 시간대에 있는 웹 서버와 같은 다른 응용 프로그램 서버에 한 표준 시간대에 트래픽을 전달 하려는 경우에 유용 합니다. 사용량이 많은 기간 중 응용 프로그램 인스턴스 간에 트래픽의 부하를 분산 하면 트래픽이 주 서버는 오버 로드 하는 경우 기간입니다.   
  
### <a name="bkmk_example1"></a>하루 중 시간을 기준으로 지능형 DNS 응답의 예  
다음은 하루 중 시간에 따라 응용 프로그램 트래픽 분산을 DNS 정책 사용 방법의 예입니다.  
  
이 예제에서는 가상의 회사를 해당 웹 사이트를 통해 전 세계에 걸쳐 온라인 gifting 솔루션에서 제공 하는 Contoso 선물 서비스를 사용 하 여 contosogiftservices.com 합니다.   
  
Contosogiftservices.com 웹 사이트는 두 데이터 센터, seattle (북미 지역)와 더블린 (유럽)에서 호스팅됩니다. DNS 서버는 응답을 보낼 지리적 위치 인식 DNS 정책을 사용 하 여 구성 됩니다. 비즈니스에서에 최근 서 지 contosogiftservices.com 방문자 수가 높을수록 매일 있으며 일부 고객의 서비스 가용성 문제는 보고 합니다.  
  
Contoso 선물 서비스는 사이트 분석을 수행 하 고 현지 시간으로 오후 6 시와 오후 9 시 사이의 매일 저녁 급증 함에에서는 웹 서버에 대 한 트래픽을 검색 합니다. 웹 서버 고객에 게 서비스 거부가 발생 하는 이러한 피크 시간에 늘어난된 트래픽을 처리 하도록 확장할 수 없습니다. 동일한 피크 시간 트래픽 오버 로드는 미국 및 유럽 데이터 센터에서 발생합니다. 다른 시간에 서버 최대 기능 보다 훨씬 아래에 있는 트래픽 볼륨을 처리 합니다.  
  
Contosogiftservices.com 고객 웹 사이트에서 응답성이 뛰어난 환경을 얻을 수 있도록, 하려면 Contoso 선물 서비스 더블린; 오후 6 시와 오후 9 시 사이의 시애틀 응용 프로그램 서버에 일부 더블린 트래픽을 리디렉션할 하려는 와 오후 6 시와 시애틀의 오후 9 시 사이의 더블린 응용 프로그램 서버에 일부 시애틀 트래픽을 리디렉션할 수 있습니다.  
  
다음 그림에서는이 시나리오를 보여 줍니다.  
  
![하루 DNS 정책의 예의 시간](../../media/DNS-Policy-Tod1/dns_policy_tod1.jpg)  
  
### <a name="bkmk_works1"></a>일의 작동 시간에 따라 어떻게 지능형 DNS 응답  
  
DNS 서버가 시간 오후 6 시와 각각의 지리적 위치에서 오후 9 시 사이의 일 DNS 정책으로 구성 된 경우 DNS 서버는 다음을 수행 합니다.  
  
- 로컬 데이터 센터의 웹 서버 IP 주소와 받은 처음 네 개의 쿼리에 응답 합니다.  
- 원격 데이터 센터에서 웹 서버의 IP 주소를 가진 수신 다섯 번째 쿼리에 응답 합니다.   
  
이 정책에 따라 동작에는 로컬 응용 프로그램 서버에 대 한 부담을 간소화 하 고 고객에 대 한 사이트 성능을 향상 원격 웹 서버에 로컬 웹 서버 트래픽 부하의 20% 오프 로드 합니다.  
  
사용량이 적은 시간에 DNS 서버를 기반으로 일반적인 지리적 위치 트래픽 관리를 수행합니다. 또한 북미 또는 유럽 이외의 위치에서 쿼리를 전송 하는 DNS 클라이언트가 DNS 서버 부하 분산 트래픽을 시애틀 및 더블린 데이터 센터 합니다.  
  
DNS에 여러 DNS 정책이 구성 되 면 규칙의 정렬된 된 집합 않으며 우선 순위가 가장 높은 우선 순위에서 DNS에 의해 처리 됩니다. DNS는 하루 중 시간을 포함 하는 상황에 맞는 첫 번째 정책을 사용 합니다. 이러한 이유 때문에 대 한 보다 구체적인 정책을 더 높은 우선 순위가 있어야 합니다. 정책 하루 중 시간을 만들고 정책 목록에서 높은 우선 순위를 부여 하는 경우 DNS를 처리 및 DNS 클라이언트 쿼리 및 정책에 정의 된 기준의 매개 변수를 일치 하는 경우 먼저 이러한 정책을 사용 합니다. 일치 하지 않으면 기본 정책이 일치 항목을 찾으면를 처리 하기 위해 DNS 정책 목록 아래로 이동 합니다.  
  
정책 형식 및 조건에 대 한 자세한 내용은 참조 [DNS 정책 개요](../../dns/deploy/DNS-Policies-Overview.md)합니다.  
  
### <a name="bkmk_how1"></a>하루 중 시간에 따라 지능형 DNS 응답에 대 한 DNS 정책을 구성 하는 방법  
시간 기반 일 응용 프로그램 부하 분산의 쿼리 응답에 대 한 DNS 정책을 구성 하려면 다음 단계를 수행 해야 합니다.  
  
- [DNS 클라이언트 서브넷 만들기](#bkmk_subnets)  
- [영역 범위 만들기](#bkmk_zscopes)  
- [영역 범위에 레코드 추가](#bkmk_records)  
- [DNS 정책 만들기](#bkmk_policies)  
  
>[!NOTE]
>구성할 영역에 대 한 권한이 있는 DNS 서버에서 이러한 단계를 수행 해야 합니다. 멤버 자격이 **DnsAdmins**, 또는 이와 동등한 다음 절차를 수행 해야 합니다.  
  
다음 섹션에서는 자세한 구성 지침을 제공 합니다.  
  
>[!IMPORTANT]
>다음 섹션에서는 예제 많은 매개 변수 값이 포함 된 예제 Windows PowerShell 명령을 포함 합니다. 이러한 명령에 대 한 예제 값은 다음이 명령을 실행 하기 전에 배포에 적합 한 값으로 바꾸는 것을 확인 합니다.  
  
#### <a name="bkmk_subnets"></a>DNS 클라이언트 서브넷 만들기  
첫 번째 단계 서브넷 또는 IP 주소 공간 트래픽을 리디렉션할 하려는 영역을 식별 하는 것입니다. 예를 들어 미국 및 유럽에 대 한 트래픽을 리디렉션할 하려면 서브넷 또는 IP 주소 공간 이러한 영역의 식별 해야 합니다.  
  
지역-IP 지도에서이 정보를 얻을 수 있습니다. 이러한 IP 지리적 분포에 따라, 만들어야 "DNS 클라이언트 서브넷." DNS 클라이언트 서브넷은 DNS 서버에 전송 되는 쿼리는 IPv4 또는 IPv6 서브넷의 논리적 그룹화입니다.  
  
DNS 클라이언트 서브넷을 만드는 다음 Windows PowerShell 명령을 사용할 수 있습니다.  
  
```  
Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet "192.0.0.0/24, 182.0.0.0/24"  
  
Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24, 151.1.0.0/24"  
  
```  
자세한 내용은 참조 [추가 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)합니다.  
  
#### <a name="bkmk_zscopes"></a>영역 범위 만들기  
클라이언트 서브넷 구성 요소를 두 개의 다른 영역 범위로 리디렉션할 트래픽을 각 사용자가 구성한 DNS 클라이언트 서브넷에 대 한 하나의 범위 영역을 분할 해야 합니다.  
  
예를 들어, DNS 이름 www.contosogiftservices.com에 대 한 트래픽을 리디렉션할 하려는 경우에 만들어야 합니다 두 개의 다른 영역 범위가 미국 및 유럽 contosogiftservices.com 영역입니다.  
  
영역 범위는 영역의 고유 인스턴스입니다. DNS 영역은 자체 DNS 레코드 집합이 포함 된 각 영역 범위를 갖는 여러 영역 범위를 가질 수 있습니다. 동일한 레코드는 동일한 IP 주소 또는 IP 주소가 다른 여러 범위에 있을 수 있습니다.  
  
>[!NOTE]
>기본적으로 영역 범위 DNS 영역에 있습니다. 영역을 같은 이름의이 영역 범위 및 레거시 DNS 작업은이 범위에서 작동 합니다.  
  
다음 Windows PowerShell 명령을 사용 하 여 영역 범위를 만들 수 있습니다.  
  
```  
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"  
  
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"  
  
```  
자세한 내용은 참조 [추가 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)합니다.  
  
#### <a name="bkmk_records"></a>영역 범위에 레코드 추가  
이제 두 영역 범위에는 웹 서버 호스트를 나타내는 레코드를 추가 해야 합니다.  
  
예를 들어 **SeattleZoneScope**, 레코드 **www.contosogiftservices.com** 시애틀 데이터 센터에 있는 IP 주소 192.0.0.1 함께 추가 됩니다. 마찬가지로,에서 **DublinZoneScope**, 레코드 **www.contosogiftservices.com** 더블린 데이터 센터에서 141.1.0.3 IP 주소로 추가  
  
레코드를 추가 하려면 영역 범위에는 다음 Windows PowerShell 명령을 사용할 수 있습니다.  
  
```  
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope  
  
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.3" -ZoneScope "DublinZoneScope"  
  
```  
기본 범위에서 레코드를 추가할 때 ZoneScope 매개 변수가 포함 되지 않습니다. 표준 DNS 영역에 레코드를 추가 하는와 같습니다.  
  
자세한 내용은 참조 [추가 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)합니다.  
  
#### <a name="bkmk_policies"></a>DNS 정책 만들기  
서브넷을 만든 후 (영역 범위), 파티션 및 사용자 레코드를 추가 했습니다, 그리고 영역의 올바른 범위 내에서 쿼리 응답의 DNS 클라이언트 서브넷 중 하나의 소스에서 쿼리 되 면 반환 되도록 서브넷과 파티션, 연결 하는 정책을 만들어야 합니다. 정책이 기본 영역 범위 매핑을 지정 해야 합니다.  
  
이러한 DNS 정책을 구성한 후 DNS 서버 문제는 다음과 같습니다.  
  
1. 유럽 DNS 클라이언트의 DNS 쿼리 응답에 더블린 데이터 센터에서 웹 서버의 IP 주소를 수신합니다.  
2. American DNS 클라이언트의 DNS 쿼리 응답에 시애틀 데이터 센터에서 웹 서버의 IP 주소를 수신합니다.  
3. 오후 6 시와 더블린에서 오후 9 시 사이의 20%의 유럽 클라이언트에서 쿼리는 해당 DNS 쿼리 응답에 시애틀 데이터 센터에서 웹 서버의 IP 주소를 받습니다.  
4. 오후 6 시와 시애틀의 오후 9 시 사이의 20%의 미국 클라이언트에서 쿼리는 해당 DNS 쿼리 응답에 더블린 데이터 센터에서 웹 서버의 IP 주소를 받습니다.  
5. 시애틀 데이터 센터의 IP 주소를 수신 하는 전 세계의 나머지 부분에서 쿼리의 절반 송수신 나머지 절반 더블린 데이터 센터의 IP 주소입니다.  
  
  
DNS 클라이언트 서브넷에 연결 되 고 영역 범위가 DNS 정책을 만들려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.  
  
>[!NOTE]
>이 예제에서는 DNS 서버는 GMT 표준 시간대 때문 사용량이 가장 많은 시간에 해당 GMT 시간 기간 표시 해야 합니다.  
  
```  
Add-DnsServerQueryResolutionPolicy -Name "America6To9Policy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,4;DublinZoneScope,1" -TimeOfDay "EQ,01:00-04:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 1  
  
Add-DnsServerQueryResolutionPolicy -Name "Europe6To9Policy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "SeattleZoneScope,1;DublinZoneScope,4" -TimeOfDay "EQ,17:00-20:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 2  
  
Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3  
  
Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 4  
  
Add-DnsServerQueryResolutionPolicy -Name "RestOfWorldPolicy" -Action ALLOW --ZoneScope "DublinZoneScope,1;SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 5  
  
```  
자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다.  
  
이제는 DNS 서버는 지리적 위치 및 하루 중 시간에 따라 트래픽을 리디렉션할 수 필요한 DNS 정책을 사용 하 여 구성 됩니다.  
  
DNS 서버 이름 확인 쿼리를 받으면 DNS 서버는 구성 된 DNS 정책에 대 한 DNS 요청에 있는 필드를 평가 합니다. 이름 확인 요청에서 원본 IP 주소를 일치 하는 정책 면 관련된 영역 범위 하는 데는 쿼리에 응답 하 고 사용자 지리적으로 가장 가까운 하는 리소스에 전달 됩니다.  
  
관리 요구 사항을 트래픽이 따라 DNS 정책의 수천을 만들 수 있습니다 하 고 들어오는 쿼리-DNS 서버를 다시 시작 하지 않고 모든 새 정책-동적으로 적용 됩니다.


