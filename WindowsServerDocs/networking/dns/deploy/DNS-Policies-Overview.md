---
title: DNS 정책 개요
description: 이 항목은 Windows Server 2016 용 DNS 정책 시나리오 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 566bc270-81c7-48c3-a904-3cba942ad463
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 06086bbd7edc2fa489805eb5075062332e002ab4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="dns-policies-overview"></a>DNS 정책 개요

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이것은 Windows Server 2016의 새로운 기능 DNS 정책에 대 한 자세한 내용은이 항목을 사용할 수 있습니다. 지리적 위치를 기반으로 교통 관리, 날짜, 시간에 따라 지능형 DNS 응답에 대 한 DNS 정책을 사용 하 여 DNS 쿼리에 등에서 필터를 적용 split\ 두뇌 배포를 위해 구성 되어 DNS 서버 관리 수 있습니다. 다음과 같은 항목에는 이러한 기능에 대 한 자세한 내용을 제공합니다.

-   **응용 프로그램 부하 분산 합니다.** 다른 위치에서 응용 프로그램을 여러 개를 배포한 때 DNS 정책 동적으로 응용 프로그램에 대 한 교통량 로드 할당 다른 응용 프로그램이 인스턴스 간에 교통 부하 분산를 사용할 수 있습니다.

-   **Geo\ 위치 기반 교통 관리 합니다.** 클라이언트 가까운 리소스의 IP 주소를 제공 하는 클라이언트와, 연결을 시도 하는 클라이언트를 리소스 지리적 위치에 따라 DNS 클라이언트 쿼리가 응답할 기본 및 보조 DNS 서버를 허용 하도록 DNS 정책을 사용할 수 있습니다. 

-   **DNS 두뇌를 분할 됩니다.** Split\ 두뇌 DNS DNS 레코드 동일한 DNS 서버에서 다양 한 영역 범위도 분할 및 DNS 클라이언트 클라이언트는 내장형 또는 외장형 클라이언트 있는지 여부에 따라 응답을 받습니다. 독립 실행형 DNS 서버에 통합 된 Active Directory 영역에 대 한 또는 영역에 대 한 split\ 두뇌 DNS 구성할 수 있습니다.

-   **필터링 합니다.** DNS 정책을를 제공 하는 조건에 따라 쿼리 필터 만드는 구성할 수 있습니다. DNS 정책에서 쿼리 필터를 사용 하 여 DNS 쿼리 및 DNS 쿼리에 보내는 DNS 클라이언트를 기반으로 사용자가 지정한 방식 응답 DNS 서버를 구성할 수 있습니다. 
-   **설명 합니다.** 연결 하려는 컴퓨터에 전송 하는 대신 non\ 존재 IP 주소를 악성 DNS 클라이언트 리디렉션합니다 DNS 정책을 사용할 수 있습니다.

-   **하루 중 시간 기반 전환 합니다.** DNS 정책을 사용 하 여 DNS 정책을 사용 하 여 하루 중 시간에 따라 다른 지리적 분산된 인스턴스 응용 프로그램의 응용 프로그램 교통 분산 수 있습니다.

## <a name="new-concepts"></a>새로운 개념이  
위에 나열 된 시나리오를 지원 하기 위해 정책을 만들기 위해 레코드 그룹에 네트워크에서 다른 요소 클라이언트 그룹 영역을 식별 하는 데 필요한입니다. 이러한 요소 다음과 같은 새로운 DNS 개체도 표시 됩니다.  

- **클라이언트 서브넷:** 클라이언트 서브넷 개체 쿼리 DNS 서버에 전송 되는 V4 또는 IPv6 서브넷 나타냅니다. 나중에 어떤 서브넷에서 제공 하 고 요청에 따라 적용 되도록 하기 정책을 정의할 서브넷 만들 수 있습니다. 예를 들어 분할 두뇌 DNS 시나리오 같은 이름에 대 한 해결 방법에 대 한 요청이에서 *www.microsoft.com* 내부 서브넷에서 클라이언트로 내부 IP 주소와 클라이언트로 서브넷 외부에 있는 다른 IP 주소를 대답할 수 있습니다.

- **재귀 범위:** 재귀 범위는 그룹 재귀 DNS 서버를 제어 하는 설정의 고유한 인스턴스 적용 됩니다. 재귀 범위 전달자 목록이 포함 되어 및 재귀가 사용할 수 있는지 여부를 지정 합니다. DNS 서버 많은 재귀 범위에 있을 수 있습니다. DNS 서버 재귀 정책 쿼리 집합에 대 한 재귀가 범위를 선택할 수 있습니다. DNS 서버를 신뢰할 수 없는 경우 특정 쿼리, DNS 서버 재귀 정책 조절할 수 있도록 이러한 쿼리 해결 하는 방법입니다. 재귀 사용 여부 등 사용 하는 전달자 지정할 수 있습니다.

- **범위 영역:** DNS 영역 자신의 설정 DNS 레코드에 포함 된 각 영역 범위와의 여러 영역 범위에 있을 수 있습니다. 동일한 기록 IP 주소가 서로 다른 여러 범위에 있을 수 있습니다. 또한 영역 전송 영역 범위 수준 수행 됩니다. 즉,의 주요 영역에서 영역 범위 레코드 보조 영역에서 동일한 영역 범위를 전송할 수 됩니다.

## <a name="types-of-policy"></a>종류의 정책

DNS 정책은 수준 및 형식으로 구분 됩니다. 쿼리 해상도 쿼리 처리 하는 방법을 정의 정책과 영역 전송 정책을 영역 전송 발생 하는 방법을 정의를 사용할 수 있습니다. 서버 수준 또는 영역 수준 정책 종류별로 적용할 수 있습니다.
  
### <a name="query-resolution-policies"></a>쿼리 해상도 정책

DNS 서버에서 쿼리를 처리 방법을 들어오는 해상도 지정 하려면 DNS 쿼리에 해상도 정책 사용할 수 있습니다. 모든 DNS 쿼리에 해결 정책 다음 요소를 포함 되어 있습니다.  
  
|들판|설명|가능한 한 값|  
|---------|---------------|-------------------|  
|**이름**|정책 이름|-최대 256 개의 문자<br />-파일 이름에 대해 잘못 된 문자 수 포함|  
|**상태가**|정책 상태|-(기본)를 사용 합니다.<br />-사용 안 함|  
|**수준**|정책 수준|서버<br />영역|  
|**처리 주문**|서버 쿼리와 일치 하는 기준 및 쿼리를 적용 하는 첫 번째 정책을 검색 쿼리 수준에 따라 분류에 적용 되 면|-숫자 값<br />별로 정책 동일한 수준 적용 하는 가치에 포함 된 고유 값|  
|**알림**|DNS 서버에서 수행할 작업|-허용 (수준 영역에 대 한 기본값)<br />-거부 (기본 서버 수준)<br />-무시|  
|**조건**|정책 조건 (또는) 및 조건의 적용 되도록 정책에 대 한 충족 목록|조건 통신사 (또는)<br />목록입니다 (아래 조건 표 참조) 하는 조건|  
|**범위**|영역 범위가 및 범위 마다가 값 목록입니다. 가 값 부하 분산 메일에 사용 됩니다. 예를 들어이 목록에 포함 3의 두께와 datacenter1 5의 두께와 datacenter2 서버로 응답 기록 세 번 8 요청 아웃 datacentre1에서|이름 사용 하 여 영역 범위가 및 무게 목록|  

> [!NOTE]
> 서버 수준 정책 수 값 하기만 **거부** 또는 **무시** 는 동작 합니다.

두 개의 요소 DNS 정책 조건과 필드 구성 됩니다.

|이름|설명|샘플 값|
|--------|---------------|-----------------|
|**클라이언트 서브넷**|프로토콜 쿼리에 사용 되는 전송 합니다. 가능한 한 항목은 **UDP** 및 **TCP**|-   **스페인, EQ 프랑스** -스페인 또는 프랑스 서브넷 식별 되 면 true 확인<br />-   **하나, 캐나다, 멕시코** -true 클라이언트 서브넷 캐나다와 멕시코 모든 서브넷 인지 확인|  
|**전송 프로토콜**|프로토콜 쿼리에 사용 되는 전송 합니다. 가능한 한 항목은 **UDP** 및 **TCP**|-   **TCP EQ**<br />-   **UDP EQ**|  
|**인터넷 프로토콜**|네트워크 프로토콜 쿼리에 사용 합니다. 가능한 한 항목은 **IPv4** 및 **IPv6**|-   **IPv4 EQ**<br />-   **IPv6 EQ**|  
|**서버 인터페이스 IP 주소**|IP 주소를 수신 DNS 서버 네트워크 인터페이스|-   **10.0.0.1 EQ**<br />-   **192.168.1.1 EQ**|  
|**FQDN**|쿼리에 기록의 사용 가능성 와일드 카드를 사용 하는 FQDN|-   **www.contoso.com EQ** -해결 tot rue 쿼리 확인 하려고 시도 있는 경우에만 있는 *www.contoso.com* FQDN<br />-   **EQ,\*.contoso.com,\*.woodgrove.com** -으로 끝나는 모든 기록에 대 한 쿼리가 경우 true 확인 *contoso.com***또는***woodgrove.com*|  
|**쿼리 유형**|기록 쿼리 중인 (A, SVR, TXT) 유형|-   **EQ TXT SRV** -쿼리를 TXT 요청 하는 경우 해결 tot rue **또는** SRV 기록<br />-   **EQ, MX** -해결 tot rue 쿼리 MX 기록 요청 하는 경우|  
|**하루 중 시간**|쿼리 수신 하는 하루 중 시간|-   **: 00 22-23시, 10시-12시 EQ** -10 오전 사이의 오후, 쿼리를 받은 경우 해결 tot rue **또는** 오후 10 오후 11과|  
  
위의 표를 사용 하 여 시작 지점으로을 아래 표에서를 정의할 모든 종류의 레코드 있지만에서 8 사이의 10.0.0.3 인터페이스를 통해 오후 10 TCP를 통해 10.0.0.0 월 24 서브넷에서 클라이언트에서 들어오는 contoso.com 도메인 SRV 레코드에 대 한 쿼리가 일치 하는 데 사용 하는 기준을 사용 수 있습니다.  
  
|이름|값|  
|--------|---------|  
|클라이언트 서브넷|10.0.0.0 월 24 EQ|  
|전송 프로토콜|TCP EQ|  
|서버 인터페이스 IP 주소|10.0.0.3 EQ|  
|FQDN|EQ, *. contoso.com|  
|쿼리 유형|새 SRV|  
|하루 중 시간|20시 22시 EQ|  
  
으로 처리 주문에 대 한 다른 유용 하 게 동일한 수준의 해상도 정책 여러 쿼리를 만들 수 있습니다. 사용할 수 있는 여러 정책, DNS 서버 다음과 같이 수신 쿼리를 처리:  
  
![DNS 정책 처리](../../media/DNS-Policies-Overview/DNSQueryResolutionPolicyFlowchart.png)  
  
### <a name="recursion-policies"></a>재귀 정책  
재귀가 정책은 특별 한 **종류** 서버 수준 정책입니다. 재귀가 정책은 제어 어떻게 DNS 서버 쿼리의 반복적으로 실행 합니다. 재귀가 정책은 쿼리 처리 재귀 경로 도달 적용 됩니다. 거부 또는 무시 재귀가 쿼리 집합에 대 한 값을 선택할 수 있습니다. 또는 쿼리 집합에 대 한 전달자 집합을 선택할 수 있습니다.  
  
재귀가 정책을 사용 하 여 구현 하는 Split-brain DNS 구성 합니다. 이 구성 DNS 서버 다른에 대 한 클라이언트 쿼리가 해당 재귀 DNS 서버를 수행 하지 않는 동안 쿼리를에 대 한 클라이언트 집합에 대 한 반복적으로 실행 합니다.  
  
아래 표에서 요소 함께 일반 DNS 쿼리에 해결 정책 포함 같은 요소를 포함 하는 재귀 정책:  
  
|이름|설명|  
|--------|---------------|  
|**재귀에 적용 합니다.**|이 정책 재귀가 사용 해야 지정 합니다.|  
|**재귀 범위**|재귀 범위의 이름입니다.|  
  
> [!NOTE]  
> 재귀 정책만 서버 수준 만들 수 있습니다.  
  
### <a name="zone-transfer-policies"></a>영역 전송 정책  
영역 전송 정책은 영역 전송 허용 하거나 하지 DNS 서버를 제어 합니다. 서버 수준 나 영역 수준 영역 전송에 대 한 정책을 만들 수 있습니다. DNS 서버에서 발생 하는 모든 영역 전송 쿼리에 서버 수준 정책이 적용 됩니다. 영역 수준 정책 DNS 서버에서 호스트 하는 영역에서 쿼리에만 적용 됩니다. 수준 정책 영역에 대 한 사용 되는 가장 일반적인 차단 또는 안전 하 게 목록 구현 하는 것입니다.  
  
> [!NOTE]  
> 영역 전송 정책 거부 또는 무시 동작으로만 사용할 수 있습니다.  
  
아래 서버 수준의 영역 전송 정책 영역 전송 contoso.com 도메인에 대 한 특정된 서브넷 거부할 사용할 수 있습니다.  
  
```  
Add-DnsServerZoneTransferPolicy -Name DenyTransferOfCOnsotostoFabrikam -Zone contoso.com -Action DENY -ClientSubnet "EQ,192.168.1.0/24"  
```  
  
으로 처리 주문에 대 한 다른 유용 하 게 동일한 수준의 정책 여러 영역 전송을 만들 수 있습니다. 사용할 수 있는 여러 정책, DNS 서버 다음과 같이 수신 쿼리를 처리:  
  
![DNS 프로세스에 대 한 여러 영역 전송 정책](../../media/DNS-Policies-Overview/DNSPolicyZone.png)  
  
## <a name="managing-dns-policies"></a>DNS 정책 관리  
만들 수 있으며 PowerShell를 사용 하 여 DNS 정책을 관리. 아래의 예제 DNS 정책을 통해 구성할 수 있는 다른 샘플 시나리오를 통과 다음과 같습니다.  
  
### <a name="traffic-management"></a>교통 관리  
DNS 클라이언트의 위치에 따라 다른 서버로 FQDN에 따라 교통을 보낼 수 있습니다. 아래의 예제 교통 관리 정책을 북아메리카 데이터 센터에 서브넷 및 다른 서브넷 유럽 데이터 센터에에서 고객에 게 직접 만들 수는 방법을 보여 줍니다.  
  
```  
Add-DnsServerClientSubnet -Name "NorthAmericaSubnet" -IPv4Subnet "172.21.33.0/24"  
Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "172.17.44.0/24"  
Add-DnsServerZoneScope -ZoneName "Contoso.com" -Name "NorthAmericaZoneScope"  
Add-DnsServerZoneScope -ZoneName "Contoso.com" -Name "EuropeZoneScope"  
Add-DnsServerResourceRecord -ZoneName "Contoso.com" -A -Name "www" -IPv4Address "172.17.97.97" -ZoneScope "EuropeZoneScope"  
Add-DnsServerResourceRecord -ZoneName "Contoso.com" -A -Name "www" -IPv4Address "172.21.21.21" -ZoneScope "NorthAmericaZoneScope"  
Add-DnsServerQueryResolutionPolicy -Name "NorthAmericaPolicy" -Action ALLOW -ClientSubnet "eq,NorthAmericaSubnet" -ZoneScope "NorthAmericaZoneScope,1" -ZoneName "Contoso.com"  
Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "EuropeZoneScope,1" -ZoneName contoso.com  
```  
  
처음 두 줄 스크립트 서브넷 개체 북미 지역 및 유럽 풍경에 대 한 클라이언트를 만듭니다. 두 줄 후에 각 영역에 대 한 contoso.com 도메인에 있는 영역 범위를 만듭니다. 두 줄 그 후 ww.contoso.com 다른 IP 주소, 유럽에 대 한 북미 지역에 대 한 다른 요금제를 연결 하는 각 영역에서 기록을 생성 합니다. 마지막으로, 스크립트 마지막 줄 두 DNS 쿼리 해상도 정책을 만든 하나을 위해 유럽 서브넷 다른 북미 지역 서브넷에 적용할 수 있습니다.  
  
### <a name="block-queries-for-a-domain"></a>도메인에 대 한 쿼리가 차단  
쿼리를 차단 하도록 DNS 쿼리에 해결 정책 도메인에 사용할 수 있습니다. 아래의 예제 모든 쿼리 treyresearch.net를 차단 합니다.  
  
```  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicy" -Action IGNORE -FQDN "EQ,*.treyresearch.com"  
```  
  
### <a name="block-queries-from-a-subnet"></a>차단 쿼리 서브넷에서  
또한 특정 서브넷에서 제공한 것임 쿼리를 차단할 수 있습니다. 아래의 스크립트 서브넷 172.0.33.0 월 24 만들고 모든 쿼리 해당 서브넷에서 제공한 것임을 무시 하도록 정책을 만듭니다.  
  
```  
Add-DnsServerClientSubnet -Name "MaliciousSubnet06" -IPv4Subnet 172.0.33.0/24  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06"  
```  
  
### <a name="allow-recursion-for-internal-clients"></a>내부 클라이언트 재귀 허용  
DNS 쿼리에 해상도 정책을 사용 하 여 재귀를 제어할 수 있습니다. 아래의 예제 외부 클라이언트 분할 두뇌 시나리오에서에 대 한 사용 하지 않도록 설정 하는 동안 반복 내부 클라이언트의 경우 설정에 사용할 수 있습니다.  
  
```  
Set-DnsServerRecursionScope -Name . -EnableRecursion $False   
Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True  
Add-DnsServerQueryResolutionPolicy -Name "SplitBrainPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP  "EQ,10.0.0.34"  
```  
  
스크립트 첫 번째 줄 변경로 간단 하 게 명명 된 기본 재귀 범위 "입니다." (점) 재귀 사용 안 함입니다. 두 번째 줄 라는 재귀 범위를 만들어 *InternalClients* 재귀 사용할 수 있습니다. 세 번째 줄 정책을 적용을 만들고는 재귀 범위에 IP 주소와 10.0.0.34 서버 인터페이스를 통해 수신 쿼리와를 새로 만들기.  
  
### <a name="create-a-server-level-zone-transfer-policy"></a>서버 수준의 영역 전송 정책 만들기  
DNS 영역 전송 정책을 사용 하 여 세분화 형태로 전송 영역을 제어할 수 있습니다. 아래의 예제 스크립트 영역 전송 될 수 있도록 지정 서브넷 모든 서버 사용할 수 있습니다.  
  
```  
Add-DnsServerClientSubnet -Name "AllowedSubnet" -IPv4Subnet 172.21.33.0/24  
Add-DnsServerZoneTransferPolicy -Name "NorthAmericaPolicy" -Action IGNORE -ClientSubnet "ne,AllowedSubnet"  
```  
  
스크립트 첫 번째 줄 라는 서브넷 개체를 만들어 *AllowedSubnet* IP와 함께 172.21.33.0 월 24 차단 합니다. 두 번째 줄 영역에서 이전에 만든 서브넷 DNS 서버를 전송할 수 있도록 영역 전송 정책을 만듭니다.  
  
### <a name="create-a-zone-level-zone-transfer-policy"></a>영역 수준의 영역 전송 정책 만들기  
영역 수준의 영역 전송 정책 만들 수 있습니다. 아래의 예제 무시 서버 인터페이스 10.0.0.33의 IP 주소를에서 들어오는 contoso.com 영역 전송에 대 한 요청 합니다.  
  
```  
Add-DnsServerZoneTransferPolicy -Name "InternalTransfers" -Action IGNORE -ServerInterfaceIP "ne,10.0.0.33" -PassThru -ZoneName "contoso.com"  
```  
  
## <a name="dns-policy-scenarios"></a>DNS 정책 시나리오

사용 하는 방법에 대 한 내용은 특정 시나리오에 대 한 정책을 DNS이이 가이드에 다음 항목을 참조 합니다.

- [지리적 위치를 사용 하 여 DNS 정책 기반 기본 서버와 함께 교통 체증 관리](primary-geo-location.md)  
- [지리적 위치를 사용 하 여 DNS 정책 기반 주 보조 배포 교통 관리](primary-secondary-geo-location.md)  
- [DNS 정책을 사용 하 여 지능형 DNS 응답 하루 중 시간에 따라에 대 한](dns-tod-intelligent.md)
- [DNS 응답은 Azure와 시간에 따라 클라우드 앱 서버](dns-tod-azure-cloud-app-server.md)
- [DNS 정책에 대 한 사용 하 여 Split-Brain DNS 배포](split-brain-DNS-deployment.md)
- [DNS 정책에 대 한 사용 하 여 Split-Brain DNS Active Directory에](dns-sb-with-ad.md)
- [DNS 정책을 DNS 쿼리에에서 필터를 적용 하는 데 사용 하 여](apply-filters-on-dns-queries.md)
- [DNS 정책을 사용 하 여 응용 프로그램 부하 분산에 대 한](app-lb.md)
- [DNS 정책을 사용 하 여 응용 프로그램 부하 분산와 지리적 위치 인식에 대 한](app-lb-geo.md)


