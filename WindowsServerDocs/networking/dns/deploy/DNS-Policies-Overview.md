---
title: DNS 정책 개요
description: 이 항목은 DNS 정책 시나리오 가이드에 대 한 Windows Server 2016의 일부
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 566bc270-81c7-48c3-a904-3cba942ad463
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ad8fa904f43bb51871e5063eaddedd0762d54d95
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814304"
---
# <a name="dns-policies-overview"></a>DNS 정책 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Windows Server 2016의 새로운 DNS 정책에 알아보려면이 항목에서는 사용할 수 있습니다. 지리적 위치 기반 트래픽 관리를 단일 분할에 대해 구성 된 DNS 서버를 관리 하려면, 하루 중 시간을 기준으로 지능형 DNS 응답에 대 한 DNS 정책을 사용 하 여\-브레인 배포, DNS 쿼리 및 기타 정보에 필터를 적용 합니다. 다음 항목을 이러한 기능에 대해 자세히 설명 합니다.

-   **응용 프로그램 부하를 분산 합니다.** 다른 위치에 있는 응용 프로그램의 여러 인스턴스를 배포한 경우 응용 프로그램에 대 한 트래픽 부하를 동적으로 할당 된 다른 응용 프로그램 인스턴스 간에 트래픽 부하를 분산 DNS 정책을 사용할 수 있습니다.

-   **지역\-위치 기반 트래픽 관리 합니다.** 클라이언트를 제공 하는 가장 가까운의 IP 주소를 사용 하 여 기본 및 보조 DNS 서버는 클라이언트와 연결을 시도 하는 클라이언트는 리소스의 지리적 위치 기반 DNS 클라이언트 쿼리에 응답할 수 있도록 DNS 정책의 사용할 수 있습니다. 리소스입니다. 

-   **분할 DNS 두뇌입니다.** 분할을 사용 하 여\-머리 DNS 클라이언트 내부 또는 외부 클라이언트를 지 여부에 따라 응답을 수신 하는 DNS 클라이언트 및 DNS 레코드는 동일한 DNS 서버에서 다른 영역 범위도 분할 됩니다. 분할을 구성할 수 있습니다\-Active Directory 통합 영역에 대 한 또는 독립 실행형 DNS 서버 영역에 대 한 DNS 머리.

-   **필터링합니다.** 제공 하는 조건을 기반으로 하는 쿼리 필터를 만드는 DNS 정책을 구성할 수 있습니다. DNS 정책에서 쿼리 필터를 사용 하는 DNS 쿼리 및 DNS 쿼리를 보내는 DNS 클라이언트에 따라 사용자 지정 방식으로 응답 하도록 DNS 서버를 구성할 수 있습니다. 
-   **법정 분석 합니다.** DNS 정책을 사용 하 여 비 DNS는 악의적인 클라이언트가 리디렉션할\-연결 하려는 컴퓨터에 연결 하는 대신 기존 IP 주소입니다.

-   **하루 중 시간 기반 리디렉션.** 하루 중 시간을 기반으로 하는 DNS 정책을 사용 하 여 응용 프로그램의 서로 다른 지리적으로 분산 된 인스턴스 응용 프로그램 트래픽을 분산 DNS 정책을 사용할 수 있습니다.

## <a name="new-concepts"></a>새로운 개념  
위에 나열 된 시나리오를 지원 하기 위해 정책을 만들려면 영역에 그룹의 다른 요소 간에 네트워크에서 클라이언트의 레코드 그룹을 식별할 수 있어야 하는 데 필요한 됩니다. 이러한 요소는 다음 새 DNS 개체에 의해 표시 됩니다.  

- **클라이언트 서브넷:** 클라이언트 서브넷 개체는 쿼리는 DNS 서버에 전송 됩니다 IPv4 또는 IPv6 서브넷을 나타냅니다. 나중에 요청에서 제공 하는 서브넷에 따라 적용 하는 정책을 정의 하는 서브넷을 만들 수 있습니다. 분할 브레인 DNS 시나리오와 같이 이름에 대 한 해결 방법에 대 한 요청에서 예를 들어 *www.microsoft.com* 내부 서브넷의 클라이언트에 내부 IP 주소 및 외부의 클라이언트에 다른 IP 주소를 사용 하 여 응답할 수 있습니다 서브넷입니다.

- **재귀 범위:** 재귀 범위는 재귀 DNS 서버에서 제어 하는 설정 그룹의 고유 인스턴스입니다. 재귀 범위 전달자의 목록을 포함 하 고 재귀 사용 되는지 여부를 지정 합니다. DNS 서버는 여러 재귀 범위를 가질 수 있습니다. DNS 서버 재귀 정책 쿼리 집합에 대 한 재귀 범위를 선택 하는 것과 할 수 있습니다. DNS 서버를 신뢰할 수 없는 경우 특정, DNS 서버 재귀 정책 쿼리인 경우에 이러한 쿼리를 해결 하는 방법을 제어할 수 있습니다. 전달자는 사용 및 재귀 사용 여부를 지정할 수 있습니다.

- **영역 범위:** DNS 영역은 자체 DNS 레코드 집합이 포함 된 각 영역 범위를 사용 하 여 여러 영역 범위를 가질 수 있습니다. 동일한 레코드는 서로 다른 IP 주소를 사용 하 여 여러 범위에 있을 수 있습니다. 또한 영역 전송 영역 범위 수준에서 수행 됩니다. 즉, 기본 영역에서 영역 범위에서 레코드는 보조 영역에 있는 동일한 영역 범위에 전송 됩니다.

## <a name="types-of-policy"></a>정책 유형

DNS 정책 수준 및 형식에 따라 구분 됩니다. 쿼리 해결 정책 쿼리 처리 되는 방법을 정의 하 고 영역 전송을 수행 하는 방법을 정의 하려면 영역 전송 정책을 사용할 수 있습니다. 서버 수준 또는 영역 수준에서 각 정책 형식에 적용할 수 있습니다.
  
### <a name="query-resolution-policies"></a>쿼리 해결 정책

DNS 서버에서 쿼리 처리는 수신 하는 방법을 해결 수준을 지정 하는 DNS 쿼리 해결 정책을 사용할 수 있습니다. 모든 DNS 쿼리 해결 정책에는 다음 요소가 포함 됩니다.  
  
|필드|설명|가능한 값|  
|---------|---------------|-------------------|  
|**이름**|정책 이름|-최대 256 자<br />-파일 이름에 유효한 모든 문자를 포함할 수 있습니다.|  
|**State**|정책 상태|--(기본값)를 사용 하는 중<br />-사용 안 함|  
|**Level**|정책 수준|-   Server<br />영역|  
|**처리 순서**|서버 쿼리 조건과 일치 및 쿼리를 적용 하는 첫 번째 정책을 찾습니다 쿼리 수준에 따라 분류 됩니다에 적용 되 고|-숫자 값<br />동일한 수준 및 값에 적용 되 정책 포함 된 당 고유 값|  
|**동작**|DNS 서버에서 수행할 작업|---(영역 수준에 대 한 기본값)를 허용 하는 중<br />-(서버 수준에서 기본값)을 거부 합니다.<br />-   Ignore|  
|**조건**|정책 조건 (및/또는) 정책을 적용 하기 위해 충족 해야 하는 조건 목록 및|조건 연산자 (및/또는)<br />-조건의 목록입니다 (아래 조건 표 참조)|  
|**범위**|영역 범위 및 범위 별로 가중치가 적용 된 값 목록입니다. 가중치는 부하 분산 배포에 사용 됩니다. 예를 들어 datacenter1 가중치가 3 인 및 datacenter2 5의 가중치를 사용 하 여이 목록에 포함 된 경우 서버 응답할 레코드를 사용 하 여 요청을 8 개에서 세 번 datacentre1에서|목록 이름 사용 하 여 영역 범위 및 가중치|  

> [!NOTE]
> 서버 수준 정책 값을 하나만 사용할 수 있습니다 **Deny** 하거나 **무시** 는 동작입니다.

DNS 정책 조건 필드 두 요소로 구성 됩니다.

|이름|설명|샘플 값|
|--------|---------------|-----------------|
|**클라이언트 서브넷**|미리 정의 된 클라이언트 서브넷의 이름입니다. 쿼리를 전송한 서브넷을 확인 하는 데 사용 합니다.|-   **EQ, 스페인, 프랑스** -서브넷 스페인 또는 프랑스로 식별 되 면 true로 확인<br />-   **NE, 캐나다, 멕시코** -클라이언트 서브넷 캐나다와 멕시코 이외의 모든 서브넷에 있으면 true로 확인|  
|**전송 프로토콜**|쿼리에 사용 되는 프로토콜을 전송 합니다. 가능한 항목은 **UDP** 고 **TCP**|-   **EQ,TCP**<br />-   **EQ,UDP**|  
|**인터넷 프로토콜**|쿼리에서 사용 되는 네트워크 프로토콜입니다. 가능한 항목은 **IPv4** 고 **IPv6**|-   **EQ,IPv4**<br />-   **EQ,IPv6**|  
|**서버 인터페이스 IP 주소**|들어오는 DNS 서버 네트워크 인터페이스에 대 한 IP 주소|-   **EQ,10.0.0.1**<br />-   **EQ,192.168.1.1**|  
|**FQDN**|와일드 카드를 사용 하 여 가능성이 있는 쿼리에서 레코드의 FQDN|-   **EQ, www.contoso.com** -확인 총 조각 수 rue는 경우에만 쿼리 확인 하려고 시도 합니다 *www.contoso.com* FQDN<br />-   **EQ,\*. contoso.com\*. woodgrove.com** -끝나는 모든 레코드에 대 한 쿼리는 true로 확인 되 *contoso.com***또는***woodgrove.com*|  
|**쿼리 유형**|형식의 레코드 쿼리 중인 (A, SVR, TXT)|-   **EQ, TXT, SRV** -쿼리 TXT 요청 하는 경우 true로 확인 **또는** SRV 레코드<br />-   **EQ, MX** -쿼리 MX 레코드를 요청 하는 경우 true로 확인|  
|**하루 중 시간**|쿼리가 수신 되는 시간|-   **EQ, 오전 10:00-12시 22시-23시** -쿼리 오전 10 시와 정오 사이 수신 되 면 true로 확인 **또는** 오후 10 시에서 오후 11 시 사이|  
  
위 표를 사용 하 여 시작 지점으로, 아래 표에서 사용할 수 있습니다 레코드 8 사이 통해 오후 10 10.0.0.0/24 서브넷의 클라이언트에서 TCP를 통해 들어오는 contoso.com 도메인의 SRV 레코드의 모든 형식에 대 한 쿼리와 일치 하는 데 사용 되는 조건을 정의할 수 있습니까 인터페이스 10.0.0.3 합니다.  
  
|이름|값|  
|--------|---------|  
|클라이언트 서브넷|EQ,10.0.0.0/24|  
|전송 프로토콜|EQ, TCP|  
|서버 인터페이스 IP 주소|EQ,10.0.0.3|  
|FQDN|EQ,*.contoso.com|  
|쿼리 유형|NE, SRV|  
|하루 중 시간|EQ, 20시-22:00|  
  
처리 순서에 다른 값을 갖고 있다면 동일한 수준 확인 정책 여러 쿼리를 만들 수 있습니다. 여러 정책을 사용할 수 있는 경우 다음과 같은 방식으로 들어오는 쿼리를 처리 하는 DNS 서버:  
  
![DNS 정책 처리](../../media/DNS-Policies-Overview/DNSQueryResolutionPolicyFlowchart.png)  
  
### <a name="recursion-policies"></a>재귀 정책  
재귀 정책은 특수 **형식** 서버 수준 정책입니다. 재귀 정책을 DNS 서버가 쿼리에 대 한 재귀를 수행 하는 방법을 제어 합니다. 재귀 정책 쿼리 처리 재귀 경로 도달 하면 적용 됩니다. 재귀 쿼리의 집합에 대 한 DENY 또는 무시의 값을 선택할 수 있습니다. 또는 쿼리 집합에 대 한 전달자의 집합을 선택할 수 있습니다.  
  
재귀 정책을 DNS Split-brain 구성을 구현 하려면 사용할 수 있습니다. 이 구성에서는 DNS 서버가 해당 쿼리에 대 한 다른 클라이언트에 대 한 재귀 DNS 서버에 수행 하지 않습니다 하는 동안 쿼리를 위해 클라이언트 집합에 대 한 재귀를 수행 합니다.  
  
아래 표에 요소와 함께 일반 DNS 쿼리 해결 정책을 포함 같은 요소를 포함 하는 재귀 정책:  
  
|이름|설명|  
|--------|---------------|  
|**재귀에 적용**|이 정책은 재귀만 사용 해야 지정 합니다.|  
|**재귀 범위**|재귀 범위의 이름입니다.|  
  
> [!NOTE]  
> 재귀 정책은 서버 수준 에서만 만들 수 있습니다.  
  
### <a name="zone-transfer-policies"></a>영역 전송 정책  
영역 전송 정책을 영역 전송이 허용 되는지 여부 또는 DNS 서버가 아니라 제어 합니다. 서버 수준 또는 영역 수준에서 영역 전송에 대 한 정책을 만들 수 있습니다. 서버 수준 정책을 DNS 서버에서 발생 하는 모든 영역 전송 쿼리에 적용 됩니다. 영역 수준 정책은 DNS 서버에 호스트 된 영역에 대 한 쿼리에만 적용 됩니다. 영역 수준 정책에 대 한 가장 일반적인 사용 차단 또는 안전한 목록을 구현 하는 것입니다.  
  
> [!NOTE]  
> 영역 전송 정책을 무시 또는 거부 작업으로만 사용할 수 있습니다.  
  
지정된 된 서브넷에서 contoso.com 도메인에 대 한 영역 전송을 거부 하도록 서버 수준 영역 전송 정책 아래에 사용할 수 있습니다.  
  
```  
Add-DnsServerZoneTransferPolicy -Name DenyTransferOfContosoToFabrikam -Zone contoso.com -Action DENY -ClientSubnet "EQ,192.168.1.0/24"  
```  
  
처리 순서에 대 한 다른 값이 있는으로 동일한 수준의 정책을 여러 영역 전송을 만들 수 있습니다. 여러 정책을 사용할 수 있는 경우 다음과 같은 방식으로 들어오는 쿼리를 처리 하는 DNS 서버:  
  
![여러 영역 전송 정책에 대 한 DNS 프로세스](../../media/DNS-Policies-Overview/DNSPolicyZone.png)  
  
## <a name="managing-dns-policies"></a>DNS 정책 관리  
만들기 및 PowerShell을 사용 하 여 DNS 정책을 관리할 수 있습니다. 아래 예제에서는 DNS 정책을 통해 구성할 수 있는 다른 샘플 시나리오를 통해 이동 합니다.  
  
### <a name="traffic-management"></a>Traffic Management  
DNS 클라이언트의 위치에 따라 서로 다른 서버를 FQDN에 따라 트래픽을 보낼 수 있습니다. 아래 예제에서는 트래픽을 북아메리카 데이터 센터는 특정 서브넷에서 다른 서브넷은 유럽 데이터 센터에서 고객에 게 직접 관리 정책을 만드는 방법을 보여 줍니다.  
  
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
  
스크립트의 처음 두 줄은 클라이언트 North America 및 Europe에 대 한 서브넷 개체를 만듭니다. 그런 다음 두 줄에는 각 지역별로 하나씩 contoso.com 도메인 내에서 영역 범위를 만듭니다. 그런 다음 두 줄을 다른 IP 주소, 유럽에 대 한, North America의 다른 ww.contoso.com를 연결 하는 각 영역에서 레코드를 만듭니다. 마지막으로 스크립트의 마지막 줄에는 두 개의 DNS 쿼리 해결 정책, 유럽 서브넷에 다른 North America 서브넷에 적용할 하나 만듭니다.  
  
### <a name="block-queries-for-a-domain"></a>도메인에 대 한 쿼리를 차단  
쿼리를 차단 하는 DNS 쿼리 해결 정책을 도메인에 사용할 수 있습니다. 아래 예제에서는 모든 쿼리를 treyresearch.net 차단:  
  
```  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicy" -Action IGNORE -FQDN "EQ,*.treyresearch.com"  
```  
  
### <a name="block-queries-from-a-subnet"></a>서브넷에서 쿼리를 차단  
또한 특정 서브넷에서 들어오는 쿼리를 차단할 수 있습니다. 아래 스크립트 172.0.33.0/24에 대 한 서브넷을 만들고 해당 서브넷에서 들어오는 모든 쿼리를 무시 하는 정책을 만듭니다.  
  
```  
Add-DnsServerClientSubnet -Name "MaliciousSubnet06" -IPv4Subnet 172.0.33.0/24  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06"  
```  
  
### <a name="allow-recursion-for-internal-clients"></a>내부 클라이언트에 대 한 재귀를 허용 합니다.  
재귀 DNS 쿼리 해결 정책을 사용 하 여 제어할 수 있습니다. 분할 브레인 시나리오에서 외부 클라이언트에 대 한 사용 하지 않도록 설정 하는 동안 내부 클라이언트에 대 한 재귀를 사용 하도록 설정 하려면 아래 샘플을 사용할 수 있습니다.  
  
```  
Set-DnsServerRecursionScope -Name . -EnableRecursion $False   
Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True  
Add-DnsServerQueryResolutionPolicy -Name "SplitBrainPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP  "EQ,10.0.0.34"  
```  
  
스크립트의 첫 번째 줄으로 간단히 명명 된 기본 재귀 범위를 변경 "." (점) 재귀를 사용 하지 않도록 설정 합니다. 두 번째 줄은 명명 된 재귀 범위를 만듭니다 *InternalClients* 사용 하도록 설정 합니다. 세 번째 줄에 적용 하는 정책을 만들고는 재귀 범위를 IP 주소로 10.0.0.34 있는 서버 인터페이스를 통해 들어오는 모든 쿼리를 새로 만듭니다.  
  
### <a name="create-a-server-level-zone-transfer-policy"></a>서버 수준 영역 전송 정책을 만들려면  
DNS 영역 전송 정책을 사용 하 여 보다 세분화 된 양식에서 영역 전송을 제어할 수 있습니다. 아래 샘플 스크립트는 모든 서버의 지정된 된 서브넷에 대 한 영역 전송 수 있도록 사용할 수 있습니다.  
  
```  
Add-DnsServerClientSubnet -Name "AllowedSubnet" -IPv4Subnet 172.21.33.0/24  
Add-DnsServerZoneTransferPolicy -Name "NorthAmericaPolicy" -Action IGNORE -ClientSubnet "ne,AllowedSubnet"  
```  
  
스크립트의 첫 번째 줄에는 명명 된 서브넷 개체를 만듭니다 *AllowedSubnet* IP를 사용 하 여 172.21.33.0/24를 차단 합니다. 두 번째 줄에는 이전에 만든 서브넷에 있는 DNS 서버 영역 전송 수 있도록 영역 전송 정책을 만듭니다.  
  
### <a name="create-a-zone-level-zone-transfer-policy"></a>영역 수준 영역 전송 정책 만들기  
또한 영역 수준 영역 전송 정책을 만들 수 있습니다. 아래 예제에서는 10.0.0.33의 IP 주소가 있는 서버 인터페이스에서 제공 하는 contoso.com에 대 한 영역 전송 요청을 무시:  
  
```  
Add-DnsServerZoneTransferPolicy -Name "InternalTransfers" -Action IGNORE -ServerInterfaceIP "ne,10.0.0.33" -PassThru -ZoneName "contoso.com"  
```  
  
## <a name="dns-policy-scenarios"></a>DNS 정책 시나리오

특정 시나리오에 대 한 DNS 정책을 사용 하는 방법에 대 한 자세한 내용은이 가이드의 다음 항목을 참조 하세요.

- [지리적 위치에 대 한 DNS 정책을 사용 하 여 기반 주 서버를 사용 하 여 트래픽 관리](primary-geo-location.md)  
- [지리적 위치 기반 기본 보조 배포를 사용 하 여 트래픽 관리에 대 한 DNS 정책을 사용 하 여](primary-secondary-geo-location.md)  
- [하루 중 시간에 따라 지능형 DNS 응답에 대 한 DNS 정책을 사용 하 여](dns-tod-intelligent.md)
- [Azure 사용 하 여 하루 중 시간에 따라 DNS 응답 클라우드 앱 서버](dns-tod-azure-cloud-app-server.md)
- [스플릿 브레인 DNS 배포에 대 한 DNS 정책을 사용 하 여](split-brain-DNS-deployment.md)
- [스플릿 브레인 DNS Active Directory에 대 한 DNS 정책을 사용 하 여](dns-sb-with-ad.md)
- [DNS 쿼리에 필터를 적용 하는 것에 대 한 DNS 정책 사용](apply-filters-on-dns-queries.md)
- [응용 프로그램 부하 분산에 대 한 DNS 정책을 사용 하 여](app-lb.md)
- [지리적 위치 인식 기능을 사용 하 여 분산 응용 프로그램에 대 한 DNS 정책을 사용 하 여](app-lb-geo.md)

## <a name="using-dns-policy-on-read-only-domain-controllers"></a>읽기 전용 도메인 컨트롤러에 DNS 정책 사용

DNS 정책 읽기 전용 도메인 컨트롤러와 호환 됩니다. DNS 서버 서비스를 다시 시작이 읽기 전용 도메인 컨트롤러에서 로드 되도록 새 DNS 정책을 반드시 note 수행 합니다. 이 쓰기 가능한 도메인 컨트롤러에서 필요 하지 않습니다.
