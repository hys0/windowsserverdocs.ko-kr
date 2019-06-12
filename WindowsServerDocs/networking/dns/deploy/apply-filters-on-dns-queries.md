---
title: DNS 쿼리에 필터를 적용 하는 것에 대 한 DNS 정책을 사용 하 여
description: 이 항목은 DNS 정책 시나리오 가이드에 대 한 Windows Server 2016의 일부
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: b86beeac-b0bb-4373-b462-ad6fa6cbedfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e9322da3142c584c7b9d0a28396a1d1fd62ce6ee
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446405"
---
# <a name="use-dns-policy-for-applying-filters-on-dns-queries"></a>DNS 쿼리에 필터를 적용 하는 것에 대 한 DNS 정책을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목을 사용 하 여 Windows Server에서 DNS 정책을 구성 하는 방법을 알아봅니다&reg; 2016 제공 하는 조건을 기반으로 하는 쿼리 필터를 만들 수 있습니다. 

DNS 정책에서 쿼리 필터를 사용 하는 DNS 쿼리 및 DNS 쿼리를 보내는 DNS 클라이언트에 따라 사용자 지정 방식으로 응답 하도록 DNS 서버를 구성할 수 있습니다.

예를 들어, 쿼리 필터와 차단 목록 알려진된 악의적인 도메인의 DNS 쿼리를 차단 하에서 쿼리에 응답 하 고 이러한 도메인의 DNS를 방지 하는 DNS 정책을 구성할 수 있습니다. DNS 서버에서 응답이 보내지므로 악의적인 도메인 구성원의 DNS 쿼리 시간이 초과 됩니다.

또 다른 예로 특정 집합이 클라이언트가 특정 이름을 확인할 수 있도록 허용 목록 쿼리 필터를 만드는 것입니다.

## <a name="bkmk_criteria"></a> 쿼리 필터 조건
다음 조건 중 쿼리 논리를 조합 하는 필터 (및/또는/NOT)를 만들 수 있습니다.

|이름|설명|
|-----------------|---------------------|
|클라이언트 서브넷|미리 정의 된 클라이언트 서브넷의 이름입니다. 쿼리를 전송한 서브넷을 확인 하는 데 사용 합니다.|
|전송 프로토콜|쿼리에 사용 되는 프로토콜을 전송 합니다. 가능한 값은 UDP 및 TCP입니다.|
|인터넷 프로토콜|쿼리에서 사용 되는 네트워크 프로토콜입니다. 가능한 값은 IPv4 및 i p v 6입니다.|
|서버 인터페이스 IP 주소|DNS 요청을 수신 하는 DNS 서버의 네트워크 인터페이스의 IP 주소입니다.|
|FQDN|정규화 된 도메인 이름 쿼리에서 레코드의 와일드 카드를 사용 하 여 가능성입니다.|
|쿼리 유형|쿼리 중인 레코드 종류 \(A, SRV, TXT 등\)합니다.|
|하루 중 시간|쿼리가 수신 되는 날의 시간입니다.|

다음 예제에서는 블록을 만들 DNS 정책에 대 한 필터 하는 중 하나 또는 DNS 이름 확인 쿼리를 허용 하는 방법을 보여 줍니다.

>[!NOTE]
>이 항목의 예제 명령은 Windows PowerShell 명령을 사용 하 여 **추가 DnsServerQueryResolutionPolicy**합니다. 자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다. 

## <a name="bkmk_block1"></a>도메인에서 쿼리를 차단

경우에 따라 악성으로 확인 된 도메인에 대 한 또는 조직의 사용 지침을 따르지 않는 도메인에 대 한 DNS 이름 확인을 차단 하는 것이 좋습니다. DNS 정책을 사용 하 여 도메인에 대 한 차단 쿼리를 수행할 수 있습니다.

이 예제에서 구성 하는 정책을 모든 특정 영역에 만들어지지 않습니다 – 대신 DNS 서버에 구성 된 모든 영역에 적용 되는 서버 수준 정책을 만듭니다. 서버 수준 정책에 가장 먼저 평가 되며 따라서 먼저 쿼리에 일치 시킬 수신 되는 DNS 서버에서.

다음 예제 명령은 도메인을 사용 하 여 모든 쿼리를 차단 하는 서버 수준 정책을 구성 **contosomalicious.com 접미사**합니다.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicy" -Action IGNORE -FQDN "EQ,*.contosomalicious.com" -PassThru 
`

>[!NOTE]
>구성 하는 경우는 **작업** 매개 변수 값을 가진 **무시**, DNS 서버가 응답을 사용 하 여 쿼리를 전혀 삭제 하도록 구성 되어 있습니다. 이렇게 하면 시간 제한 초과로 악의적인 도메인의 DNS 클라이언트.

## <a name="bkmk_block2"></a>서브넷에서 쿼리를 차단
이 예제와 함께 일부 맬웨어에 감염 된 것으로 확인 하 고 DNS 서버를 사용 하 여 악의적인 사이트에 게 연락 하려는 경우 서브넷에서 쿼리를 차단할 수 있습니다. 

` Add-DnsServerClientSubnet -Name "MaliciousSubnet06" -IPv4Subnet 172.0.33.0/24 -PassThru

Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06" -PassThru `

다음 예제에서는 감염 된 서브넷에서 악의적인 특정 도메인에 대 한 쿼리를 차단 하는 FQDN 조건 함께에서 서브넷 기준이 사용 하는 방법을 보여 줍니다.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06" –FQDN “EQ,*.contosomalicious.com” -PassThru
`

## <a name="bkmk_block3"></a>쿼리는 형식의 블록
특정 유형의 쿼리 서버에 대 한 이름 확인을 차단 해야 합니다. 예를 들어 증폭 공격을 만들려는 악의적으로 사용 될 '임의의' 쿼리를 차단할 수 있습니다.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyQType" -Action IGNORE -QType "EQ,ANY" -PassThru
`

## <a name="bkmk_allow1"></a>도메인만 쿼리 허용
사용할 수 없습니다만 쿼리를 차단 하도록 DNS 정책, 특정 도메인 또는 서브넷에서 쿼리를 자동으로 승인 하도록 사용할 수 있습니다. 허용 목록을 구성 하면 DNS 서버가 다른 도메인의 다른 모든 쿼리를 차단 하는 동안 허용 된 도메인에서 쿼리를만 처리 합니다.

다음 예제 명령은 컴퓨터 및 DNS 서버를 쿼리하려면 contoso.com 및 자식 도메인에 연결 된 장치에 있습니다.

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicyDomain" -Action IGNORE -FQDN "NE,*.contoso.com" -PassThru 
`

## <a name="bkmk_allow2"></a>서브넷만 쿼리 허용
만들 수도 있습니다 허용 목록을 IP 서브넷에 대해 무시할 수 있는 모든 쿼리가 이러한 서브넷에서 생성 되지 않습니다.

`
Add-DnsServerClientSubnet -Name "AllowedSubnet06" -IPv4Subnet 172.0.33.0/24 -PassThru
`
`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicySubnet” -Action IGNORE -ClientSubnet  "NE, AllowedSubnet06" -PassThru
`

## <a name="bkmk_allow3"></a>특정 QTypes만 허용
허용 목록을 QTYPEs에 적용할 수 있습니다. 

예를 들어를 쿼리 하는 DNS 서버 인터페이스 164.8.1.1 외부 고객이 있는 경우 특정 QTYPEs만 SRV 또는 TXT 레코드 또는 이름 확인에 대 한 모니터링을 위해 내부 서버에서 사용 되는 같은 다른 QTYPEs 있을 때는 쿼리할 수는 있습니다.

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListQType" -Action IGNORE -QType "NE,A,AAAA,MX,NS,SOA" –ServerInterface “EQ,164.8.1.1” -PassThru
`

관리 요구 사항을 트래픽이 따라 DNS 정책의 수천을 만들 수 있습니다 하 고 들어오는 쿼리-DNS 서버를 다시 시작 하지 않고 모든 새 정책-동적으로 적용 됩니다. 
