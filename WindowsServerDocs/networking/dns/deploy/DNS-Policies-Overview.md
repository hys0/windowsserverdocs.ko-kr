---
title: DNS 정책 개요
description: 이 항목은 Windows Server 2016에 대 한 DNS 정책 시나리오 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: 566bc270-81c7-48c3-a904-3cba942ad463
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 613bb7f43b382389dc0db953a48668147cfaee88
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356048"
---
# <a name="dns-policies-overview"></a>DNS 정책 개요

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 Windows Server 2016의 새로운 DNS 정책에 대해 알아볼 수 있습니다. 지리적 위치 기반 트래픽 관리에 DNS 정책을 사용 하 고, 시간을 기준으로 지능형 DNS 응답을 사용 하 여 분할\-두뇌 배포를 위해 구성 된 단일 DNS 서버를 관리 하 고, DNS 쿼리에 필터를 적용 하는 등의 기능을 수행할 수 있습니다. 다음 항목은 이러한 기능에 대 한 자세한 정보를 제공 합니다.

-   **응용 프로그램 부하 분산.** 응용 프로그램의 여러 인스턴스를 서로 다른 위치에 배포한 경우에는 DNS 정책을 사용 하 여 응용 프로그램에 대 한 트래픽 부하를 동적으로 할당 하는 여러 응용 프로그램 인스턴스 간의 트래픽 부하를 분산할 수 있습니다.

-   **지리적\-위치 기반 트래픽 관리.** DNS 정책을 사용 하 여 클라이언트와 클라이언트가 연결 하려고 하는 리소스의 지리적 위치에 따라 DNS 클라이언트 쿼리에 응답 하도록 기본 및 보조 DNS 서버를 허용 하 고, 클라이언트에 가장 가까운 IP 주소를 제공 합니다. 리소스나. 

-   **두뇌 DNS를 분할 합니다.** 분할\-두뇌 DNS를 사용 하는 경우 DNS 레코드는 동일한 DNS 서버에서 다른 영역 범위로 분할 되 고, DNS 클라이언트는 내부 또는 외부 클라이언트 인지 여부에 따라 응답을 받습니다. 분할\-두뇌 DNS를 Active Directory 통합 영역에 대해 구성 하거나 독립 실행형 DNS 서버의 영역에 대해 구성할 수 있습니다.

-   **필터링.** 사용자가 제공 하는 조건을 기반으로 하는 쿼리 필터를 만들도록 DNS 정책을 구성할 수 있습니다. DNS 정책에서 쿼리 필터를 사용 하는 DNS 쿼리 및 DNS 쿼리를 보내는 DNS 클라이언트에 따라 사용자 지정 방식으로 응답 하도록 DNS 서버를 구성할 수 있습니다. 
-   **법률.** DNS 정책을 사용 하 여 악성 DNS 클라이언트를 연결 하려는 컴퓨터로 전달 하지 않고 존재\-하지 않는 IP 주소로 리디렉션할 수 있습니다.

-   **하루 기준 리디렉션 시간입니다.** DNS 정책을 사용 하 여 하루 중 시간을 기준으로 하는 DNS 정책을 사용 하 여 응용 프로그램의 여러 지리적으로 분산 된 인스턴스에 응용 프로그램 트래픽을 분산할 수 있습니다.

## <a name="new-concepts"></a>새 개념  
위에 나열 된 시나리오를 지원 하기 위한 정책을 만들려면 다른 요소 간의 영역, 네트워크에 있는 클라이언트 그룹의 레코드 그룹을 식별할 수 있어야 합니다. 이러한 요소는 다음과 같은 새 DNS 개체로 표시 됩니다.  

- **클라이언트 서브넷:** 클라이언트 서브넷 개체는 쿼리를 DNS 서버로 전송 하는 IPv4 또는 IPv6 서브넷을 나타냅니다. 나중에 서브넷을 만들어 요청이 발생 한 서브넷에 따라 적용할 정책을 정의할 수 있습니다. 예를 들어 분할 된 두뇌 DNS 시나리오에서 <em>www.microsoft.com</em> 와 같은 이름에 대 한 확인 요청은 내부 서브넷의 클라이언트에 대 한 내부 ip 주소와 외부 서브넷의 클라이언트에 대 한 다른 ip 주소를 사용 하 여 대답할 수 있습니다.

- **재귀 범위:** 재귀 범위는 DNS 서버에서 재귀를 제어 하는 설정 그룹의 고유한 인스턴스입니다. 재귀 범위 전달자의 목록을 포함 하 고 재귀 사용 되는지 여부를 지정 합니다. DNS 서버는 여러 재귀 범위를 가질 수 있습니다. DNS 서버 재귀 정책을 사용 하면 쿼리 집합에 대 한 재귀 범위를 선택할 수 있습니다. DNS 서버가 특정 쿼리에 대해 권한이 없는 경우 DNS 서버 재귀 정책을 통해 이러한 쿼리를 해결 하는 방법을 제어할 수 있습니다. 사용할 전달자와 재귀 사용 여부를 지정할 수 있습니다.

- **영역 범위:** dns 영역에는 여러 영역 범위가 있을 수 있으며, 각 영역 범위에는 자체 DNS 레코드 집합이 포함 됩니다. 서로 다른 IP 주소를 사용 하 여 여러 범위에 동일한 레코드가 있을 수 있습니다. 또한 영역 전송은 영역 범위 수준에서 수행 됩니다. 즉, 주 영역에 있는 영역 범위의 레코드는 보조 영역의 동일한 영역 범위에 전송 됩니다.

## <a name="types-of-policy"></a>정책 유형

DNS 정책은 수준 및 유형으로 구분 됩니다. 쿼리 확인 정책을 사용 하 여 쿼리가 처리 되는 방법 및 영역 전송 정책을 정의 하 여 영역 전송이 발생 하는 방식을 정의할 수 있습니다. 각 정책 유형은 서버 수준 또는 영역 수준에서 적용할 수 있습니다.

### <a name="query-resolution-policies"></a>쿼리 확인 정책

Dns 쿼리 확인 정책을 사용 하 여 DNS 서버에서 들어오는 확인 쿼리를 처리 하는 방법을 지정할 수 있습니다. 모든 DNS 쿼리 확인 정책에는 다음과 같은 요소가 포함 됩니다.  

|필드|설명|가능한 값|  
|---------|---------------|-------------------|  
|**이름**|정책 이름|-최대 256 문자<br />-파일 이름에 유효한 모든 문자를 포함할 수 있습니다.|  
|**상태**|정책 상태|-Enable (기본값)<br />-사용 안 함|  
|**Level**|정책 수준|-서버<br />-영역|  
|**처리 순서**|쿼리가 수준별로 분류 되 고에 적용 되 면 서버는 쿼리가 조건과 일치 하는 첫 번째 정책을 찾고 쿼리에 적용 합니다.|-숫자 값<br />-동일한 수준을 포함 하 고 값에 적용 되는 정책 당 고유한 값|  
|**동작**|DNS 서버에서 수행할 작업입니다.|-Allow (영역 수준에 대 한 기본값)<br />-Deny (서버 수준에서 기본값)<br />-무시|  
|**조건**|정책 조건 (및/또는) 및 정책을 적용 하기 위해 충족 해야 하는 조건 목록|-Condition 연산자 (AND/OR)<br />-조건 목록 (아래 조건 표 참조)|  
|**범위**|범위 당 영역 범위 및 가중치가 적용 된 값 목록입니다. 가중치가 적용 된 값은 부하 분산 배포에 사용 됩니다. 예를 들어,이 목록에 가중치가 3이 고 가중치가 5 인 datacenter1이 포함 된 경우 서버는 8 개의 요청에서 3 번 datacentre1의 레코드를 사용 하 여 응답 합니다.|-이름 및 가중치를 기준으로 영역 범위 목록|  

> [!NOTE]
> 서버 수준 정책에는 작업으로 **거부** 또는 **무시** 값만 사용할 수 있습니다.

DNS 정책 기준 필드는 다음 두 요소로 구성 됩니다.


|              이름               |                                         설명                                          |                                                                                                                               샘플 값                                                                                                                               |
|---------------------------------|----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        **클라이언트 서브넷**        | 미리 정의 된 클라이언트 서브넷의 이름입니다. 쿼리를 전송한 서브넷을 확인 하는 데 사용 합니다. |                             -   **EQ, 스페인, 프랑스** -서브넷이 스페인 또는 프랑스 중 하나로 식별 되는 경우 true로 확인 됩니다.<br />-   **NE, 캐나다, 멕시코** -클라이언트 서브넷이 캐나다 및 멕시코 이외의 서브넷 이면 true로 확인 됩니다.                             |
|     **전송 프로토콜**      |        쿼리에 사용 되는 프로토콜을 전송 합니다. 가능한 항목은 **UDP** 및 **TCP** 입니다.        |                                                                                                                    -   **EQ, TCP**<br />-   **EQ, UDP**                                                                                                                     |
|      **인터넷 프로토콜**      |        쿼리에서 사용 되는 네트워크 프로토콜입니다. 가능한 항목은 **IPv4** 및 **IPv6** 입니다.        |                                                                                                                   -   **EQ, IPv4**<br />-   **EQ, IPv6**                                                                                                                    |
| **서버 인터페이스 IP 주소** |                   들어오는 DNS 서버 네트워크 인터페이스의 IP 주소                   |                                                                                                              -   **EQ, 10.0.0.1**<br />-   **EQ, 192.168.1.1**                                                                                                              |
|            **일**             |            와일드 카드를 사용할 가능성이 있는 쿼리의 레코드 FQDN            | -   **EQ, www. .com** -쿼리가 <em>www.contoso.com</em> FQDN을 확인 하려고 시도 하는 경우에만 true로 확인 됩니다.<br />-   **EQ,\*\*, woodgrove.com** - *contoso.com***또는***woodgrove.com* 로 끝나는 모든 레코드에 대해 쿼리가 인 경우 true로 확인 됩니다. |
|         **쿼리 유형**          |                          쿼리 중인 레코드 유형 (A, SRV, TXT)                          |                                                  -   **EQ, txt, srv** -쿼리에서 TXT **또는** SRV 레코드를 요청 하는 경우 true로 확인 됩니다.<br />-   **EQ, mx** -쿼리가 MX 레코드를 요청 하는 경우 true로 확인 됩니다.                                                   |
|         **하루 중 시간**         |                              쿼리가 수신 된 시간                               |                                                                    -   **EQ, 10:00-12:00, 22:00-23:00** -쿼리가 오전 10 시와 정오 사이에 수신 되는 경우 true로 **, 오전** 10 시에서 오후 11 시 사이에 수신 되는 경우 true로 확인 됩니다.                                                                    |

위의 표를 참조 하 여 위의 표를 사용 하 여 다음 테이블을 사용 하 여 contoso.com 도메인의 모든 레코드 유형과 SRV 레코드에 대 한 쿼리를 일치 시키는 데 사용 되는 조건을 정의할 수 있습니다.  

|이름|값|  
|--------|---------|  
|클라이언트 서브넷|EQ, 10.0.0.0/24|  
|전송 프로토콜|EQ, TCP|  
|서버 인터페이스 IP 주소|EQ, 10.0.0.3|  
|FQDN|EQ, *. contoso .com|  
|쿼리 유형|NE, SRV|  
|하루 중 시간|EQ, 20:00-22:00|  

처리 순서에 다른 값이 있는 한 동일한 수준의 쿼리 확인 정책을 여러 개 만들 수 있습니다. 여러 정책을 사용할 수 있는 경우 DNS 서버는 다음과 같은 방식으로 들어오는 쿼리를 처리 합니다.  

![DNS 정책 처리](../../media/DNS-Policies-Overview/DNSQueryResolutionPolicyFlowchart.png)  

### <a name="recursion-policies"></a>재귀 정책  
재귀 정책은 서버 수준 정책의 특수 한 **유형** 입니다. 재귀 정책은 DNS 서버가 쿼리에 대해 재귀를 수행 하는 방법을 제어 합니다. 재귀 정책은 쿼리 처리가 재귀 경로에 도달할 때만 적용 됩니다. 쿼리 집합에 대 한 재귀의 경우 DENY 또는 IGNORE 값을 선택할 수 있습니다. 또는 쿼리 집합에 대 한 전달자 집합을 선택할 수 있습니다.  

재귀 정책을 사용 하 여 분할 두뇌 DNS 구성을 구현할 수 있습니다. 이 구성에서 DNS 서버는 쿼리에 대 한 클라이언트 집합에 대해 재귀를 수행 하 고, DNS 서버는 해당 쿼리에 대해 다른 클라이언트에 대해 재귀를 수행 하지 않습니다.  

재귀 정책에는 일반 DNS 쿼리 확인 정책에 포함 된 것과 동일한 요소가 아래 표의 요소와 함께 포함 됩니다.  

|이름|설명|  
|--------|---------------|  
|**재귀에 적용**|재귀에만이 정책을 사용 하도록 지정 합니다.|  
|**재귀 범위**|재귀 범위의 이름입니다.|  

> [!NOTE]  
> 재귀 정책은 서버 수준 에서만 만들 수 있습니다.  

### <a name="zone-transfer-policies"></a>영역 전송 정책  
영역 전송 정책은 DNS 서버에서 영역 전송이 허용 되는지 여부를 제어 합니다. 서버 수준이 나 영역 수준에서 영역 전송에 대 한 정책을 만들 수 있습니다. 서버 수준 정책은 DNS 서버에서 발생 하는 모든 영역 전송 쿼리에 적용 됩니다. 영역 수준 정책은 DNS 서버에서 호스트 되는 영역의 쿼리에만 적용 됩니다. 영역 수준 정책의 가장 일반적인 용도는 차단 또는 안전 목록을 구현 하는 것입니다.  

> [!NOTE]  
> 영역 전송 정책은 거부 또는 무시 작업만 사용할 수 있습니다.  

아래 서버 수준 영역 전송 정책을 사용 하 여 지정 된 서브넷에서 contoso.com 도메인에 대 한 영역 전송을 거부할 수 있습니다.  

```  
Add-DnsServerZoneTransferPolicy -Name DenyTransferOfContosoToFabrikam -Zone contoso.com -Action DENY -ClientSubnet "EQ,192.168.1.0/24"  
```  

처리 순서에 다른 값이 있는 한 동일한 수준의 여러 영역 전송 정책을 만들 수 있습니다. 여러 정책을 사용할 수 있는 경우 DNS 서버는 다음과 같은 방식으로 들어오는 쿼리를 처리 합니다.  

![여러 영역 전송 정책에 대 한 DNS 프로세스](../../media/DNS-Policies-Overview/DNSPolicyZone.png)  

## <a name="managing-dns-policies"></a>DNS 정책 관리  
PowerShell을 사용 하 여 DNS 정책을 만들고 관리할 수 있습니다. 아래 예제에서는 DNS 정책을 통해 구성할 수 있는 다양 한 샘플 시나리오를 살펴봅니다.  

### <a name="traffic-management"></a>트래픽 관리  
DNS 클라이언트의 위치에 따라 FQDN을 기반으로 하는 트래픽을 다른 서버에 보낼 수 있습니다. 아래 예제에서는 고객을 특정 서브넷에서 북아메리카 datacenter로, 다른 서브넷에서 유럽 데이터 센터로 보내는 트래픽 관리 정책을 만드는 방법을 보여 줍니다.  

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

스크립트의 처음 두 줄은 북아메리카 및 유럽의 클라이언트 서브넷 개체를 만듭니다. 그 뒤의 두 줄은 각 지역에 대해 하나씩 contoso.com 도메인 내에서 영역 범위를 만듭니다. 그 뒤의 두 줄은 ww.contoso.com를 서로 다른 IP 주소에 연결 하는 각 영역에 레코드를 만듭니다. 하나는 유럽에 대해, 다른 하나는 북아메리카에 대 한 레코드입니다. 마지막으로 스크립트의 마지막 줄에서는 두 개의 DNS 쿼리 확인 정책, 즉 하나는 북아메리카 서브넷에 적용 되는 정책 하나를 유럽 서브넷에 만듭니다.  

### <a name="block-queries-for-a-domain"></a>도메인에 대 한 쿼리 차단  
DNS 쿼리 확인 정책을 사용 하 여 도메인에 대 한 쿼리를 차단할 수 있습니다. 아래 예제에서는 treyresearch.net에 대 한 모든 쿼리를 차단 합니다.  

```  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicy" -Action IGNORE -FQDN "EQ,*.treyresearch.com"  
```  

### <a name="block-queries-from-a-subnet"></a>서브넷에서 쿼리를 차단  
특정 서브넷에서 들어오는 쿼리를 차단할 수도 있습니다. 아래 스크립트는 172.0.33.0/24에 대 한 서브넷을 만든 다음 해당 서브넷에서 들어오는 모든 쿼리를 무시 하는 정책을 만듭니다.  

```  
Add-DnsServerClientSubnet -Name "MaliciousSubnet06" -IPv4Subnet 172.0.33.0/24  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06"  
```  

### <a name="allow-recursion-for-internal-clients"></a>내부 클라이언트에 대 한 재귀 허용  
DNS 쿼리 확인 정책을 사용 하 여 재귀를 제어할 수 있습니다. 아래 샘플을 사용 하 여 내부 클라이언트에 대 한 재귀를 사용 하도록 설정 하 고 분할 된 두뇌 시나리오에서 외부 클라이언트에 대해 재귀를 사용 하지 않도록 설정할 수 있습니다.  

```  
Set-DnsServerRecursionScope -Name . -EnableRecursion $False   
Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True  
Add-DnsServerQueryResolutionPolicy -Name "SplitBrainPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP  "EQ,10.0.0.34"  
```  

스크립트의 첫 번째 줄은 "."로 명명 된 기본 재귀 범위를 변경 합니다. (점) 재귀를 사용 하지 않도록 설정 합니다. 두 번째 줄은 재귀가 설정 된 *Internalclients* 라는 재귀 범위를 만듭니다. 그리고 세 번째 줄은 10.0.0.34를 IP 주소로 포함 하는 서버 인터페이스를 통해에서 들어오는 모든 쿼리에 새로 생성 된 재귀 범위를 적용 하는 정책을 만듭니다.  

### <a name="create-a-server-level-zone-transfer-policy"></a>서버 수준 영역 전송 정책 만들기  
DNS 영역 전송 정책을 사용 하면 보다 세부적인 형식으로 영역 전송을 제어할 수 있습니다. 아래 샘플 스크립트를 사용 하 여 지정 된 서브넷의 모든 서버에 대해 영역 전송을 허용할 수 있습니다.  

```  
Add-DnsServerClientSubnet -Name "AllowedSubnet" -IPv4Subnet 172.21.33.0/24  
Add-DnsServerZoneTransferPolicy -Name "NorthAmericaPolicy" -Action IGNORE -ClientSubnet "ne,AllowedSubnet"  
```  

스크립트의 첫 번째 줄에서는 IP 블록 172.21.33.0/24를 사용 하 여 *allowedsubnet* 이라는 서브넷 개체를 만듭니다. 두 번째 줄은 이전에 만든 서브넷의 DNS 서버로 영역 전송을 허용 하는 영역 전송 정책을 만듭니다.  

### <a name="create-a-zone-level-zone-transfer-policy"></a>영역 수준 영역 전송 정책 만들기  
영역 수준 영역 전송 정책을 만들 수도 있습니다. 아래 예제에서는 IP 주소가 예제의 10.0.0.33 인 서버 인터페이스에서 들어오는 contoso.com의 영역 전송에 대 한 모든 요청을 무시 합니다.  

```  
Add-DnsServerZoneTransferPolicy -Name "InternalTransfers" -Action IGNORE -ServerInterfaceIP "eq,10.0.0.33" -PassThru -ZoneName "contoso.com"  
```  

## <a name="dns-policy-scenarios"></a>DNS 정책 시나리오

특정 시나리오에 대 한 DNS 정책을 사용 하는 방법에 대 한 자세한 내용은이 가이드의 다음 항목을 참조 하십시오.

- [주 서버와 지리적 위치 기반 트래픽 관리에 DNS 정책 사용](primary-geo-location.md)  
- [주-보조 배포를 사용 하 여 지리적 위치 기반 트래픽 관리에 DNS 정책 사용](primary-secondary-geo-location.md)  
- [하루 중 시간을 기준으로 지능형 DNS 응답에 DNS 정책 사용](dns-tod-intelligent.md)
- [Azure Cloud App Server를 사용 하는 시간을 기준으로 하는 DNS 응답](dns-tod-azure-cloud-app-server.md)
- [분할을 위한 dns 배포에 DNS 정책 사용](split-brain-DNS-deployment.md)
- [Active Directory에서 분할 하는 DNS에 대 한 DNS 정책 사용](dns-sb-with-ad.md)
- [Dns 쿼리에서 필터를 적용 하는 데 DNS 정책 사용](apply-filters-on-dns-queries.md)
- [응용 프로그램 부하 분산에 DNS 정책 사용](app-lb.md)
- [지리적 위치 인식을 사용 하 여 응용 프로그램 부하 분산에 DNS 정책 사용](app-lb-geo.md)

## <a name="using-dns-policy-on-read-only-domain-controllers"></a>읽기 전용 도메인 컨트롤러에서 DNS 정책 사용

DNS 정책이 읽기 전용 도메인 컨트롤러와 호환 됩니다. 새 DNS 정책을 읽기 전용 도메인 컨트롤러에 로드 하려면 DNS 서버 서비스를 다시 시작 해야 합니다. 쓰기 가능한 도메인 컨트롤러에는이 작업이 필요 하지 않습니다.
