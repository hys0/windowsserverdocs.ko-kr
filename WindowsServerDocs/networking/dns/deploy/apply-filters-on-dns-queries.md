---
title: DNS 정책을 DNS 쿼리에에서 필터를 적용 하는 데 사용 하 여
description: 이 항목은 Windows Server 2016 용 DNS 정책 시나리오 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: b86beeac-b0bb-4373-b462-ad6fa6cbedfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ff10af5f88a03f806a5e5b5fa698c7c3637816bd
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-applying-filters-on-dns-queries"></a>DNS 정책을 DNS 쿼리에에서 필터를 적용 하는 데 사용 하 여

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목을 사용 하 여 Windows Server에서 DNS 정책을 구성 하는 방법을 알아보세요&reg; 2016 제공 하는 조건에 따라 쿼리 필터를 만들 수 있습니다. 

DNS 정책에서 쿼리 필터를 사용 하 여 DNS 쿼리 및 DNS 쿼리에 보내는 DNS 클라이언트를 기반으로 사용자가 지정한 방식 응답 DNS 서버를 구성할 수 있습니다.

예를 들어, 필터 사용 하 여 쿼리 차단 목록 알려진된 악성 도메인에서 DNS 쿼리에 차단 하 DNS이 도메인 쿼리에 응답 하지 않도록 DNS 정책을 구성할 수 있습니다. DNS 서버에서 응답이 전송 하기 때문에 악성 도메인 구성원 DNS 쿼리에 시간이 초과 되었습니다.

다른 예 쿼리 필터 특정 집합이 클라이언트가 특정 이름을 확인할 수 있도록 허용 목록 만드는 것입니다.

## <a name="bkmk_criteria"></a>쿼리 필터 조건
다음 조건을 논리 조합 사용 하 여 쿼리 필터 (및/또는/없음)를 만들 수 있습니다.

|이름|설명|
|-----------------|---------------------|
|클라이언트 서브넷|미리 정의 된 클라이언트 서브넷의 이름입니다. 쿼리를 보낸 서브넷 확인할 수 있습니다.|
|전송 프로토콜|프로토콜 쿼리에 사용 되는 전송 합니다. 가능한 한 값은 UDP 및 TCP입니다.|
|인터넷 프로토콜|네트워크 프로토콜 쿼리에 사용 합니다. 가능한 한 값은 IPv4 IPv6입니다.|
|서버 인터페이스 IP 주소|DNS 서버 DNS 요청을 받은 네트워크 인터페이스의 IP 주소|
|FQDN|완벽 하 게 된 도메인의 이름이 쿼리에 기록 와일드 카드를 사용 하 여 가능성 합니다.|
|쿼리 유형|기록 쿼리 중인 유형의 \ (A, SRV, TXT. \)|
|하루 중 시간|쿼리 수신 하는 하루 중 시간입니다.|

다음은 DNS 정책에 대 한 필터를 차단 하거나 만들거나 DNS 이름 해상도 쿼리를 허용 하는 방법을 보여 줍니다.

>[!NOTE]
>이 항목의 예 명령을 사용 하 여 Windows PowerShell 명령 **추가 DnsServerQueryResolutionPolicy**합니다. 자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx)합니다. 

##<a name="bkmk_block1"></a>도메인에서 차단 쿼리

DNS 차단 하려는 경우에 따라, 악성으로 식별 하는 도메인 또는 준수 하지 않는 사용 지침 조직 도메인 이름 확인 합니다. 도메인에 대 한 쿼리가 차단 DNS 정책을 사용 하 여 수행할 수 있습니다.

특정 영역에 여기서에서 구성 정책 생성 되지 않습니다 – 서버 수준 정책을 DNS 서버에서 구성 된 모든 영역에 적용 되는 대신 만듭니다. 서버 수준 정책 먼저 평가 하 고 하므로 먼저 때 쿼리 일치 하는 받은 DNS 서버 합니다.

명령은 구성 된 도메인 쿼리와 차단 하는 서버 수준 정책을 **contosomalicious.com 접미사**합니다.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicy" -Action IGNORE -FQDN "EQ,*.contosomalicious.com" -PassThru 
`

>[!NOTE]
>구성 하는 경우는 **알림** 매개 값으로 **무시**, DNS 서버 전혀 응답이 없는 쿼리 핀을 구성 합니다. 이렇게 하면 시간 초과 악성 도메인에 있는 DNS 클라이언트 됩니다.

##<a name="bkmk_block2"></a>차단 쿼리 서브넷에서
일부 맬웨어에 감염 되는지를으로 확인 하 고 DNS 서버를 사용 하 여 악성 사이트에 게 연락 하려는 경우이 들어와 서브넷 쿼리를 차단할 수 있습니다. 

' 추가 DnsServerClientSubnet-"MaliciousSubnet06" 이름을-IPv4Subnet 172.0.33.0/24 통과

추가 DnsServerQueryResolutionPolicy-"BlockListPolicyMalicious06" 이름을-작업 무시 ClientSubnet "EQ MaliciousSubnet06"-통과 '

이때 감염된 서브넷에서 특정 악성 도메인에 대 한 쿼리가 차단 FQDN 기준 함께에서 서브넷 조건을 사용 하는 방법을 보여 줍니다.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06" –FQDN “EQ,*.contosomalicious.com” -PassThru
`

##<a name="bkmk_block3"></a>쿼리 형식을 차단합니다
특정 유형의 쿼리 서버에 대 한 이름 해상도 차단 하도록 할 수 있습니다. 예를 들어 '는' 쿼리를 증폭 공격 만드는 악의적으로 사용할 수 있는 차단할 수 있습니다.

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyQType" -Action IGNORE -QType "EQ,ANY" -PassThru
`

##<a name="bkmk_allow1"></a>도메인에서만 쿼리 허용
하지만 정책을 사용 하 여 DNS 쿼리를 차단 하도록, 특정 도메인 또는 서브넷 쿼리 승인 자동으로 사용할 수 있습니다. 허용 목록를 구성할 때 DNS 서버에서 허용된 하는 도메인 쿼리 다른 도메인의 다른 모든 쿼리를 차단 하는 동안만 처리 합니다.

컴퓨터 및 DNS 서버를 쿼리를 contoso.com 및 자녀가 도메인에 연결 된 장치 명령은 수 있게 합니다.

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicyDomain" -Action IGNORE -FQDN "NE,*.contoso.com" -PassThru 
`

##<a name="bkmk_allow2"></a>쿼리만 서브넷 허용
만들 수도 있습니다 허용 목록을 IP 서브넷 무시 모든 쿼리에서 이러한 서브넷 발생 하지 않도록 합니다.

`
Add-DnsServerClientSubnet -Name "AllowedSubnet06" -IPv4Subnet 172.0.33.0/24 -PassThru
`
`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicySubnet” -Action IGNORE -ClientSubnet  "NE, AllowedSubnet06" -PassThru
`

##<a name="bkmk_allow3"></a>특정 QTypes 허용
허용 목록 QTYPEs에 적용할 수 있습니다. 

예를 들어, 외부 고객 DNS 서버 인터페이스 164.8.1.1 쿼리를 사용 하는 경우 특정 QTYPEs 쿼리에서 사용 하는 내부 서버 또는 모니터링 목적을 위해 이름 확인을 위해 SRV 또는 TXT 기록 등 기타 QTYPEs 중일 수는 있습니다.

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListQType" -Action IGNORE -QType "NE,A,AAAA,MX,NS,SOA" –ServerInterface “EQ,164.8.1.1” -PassThru
`

관리 요구 사항에 교통에 따라 DNS 정책 수천을 만들 수 있습니다 고-들어오는 쿼리에서 DNS 서버를 다시 시작 하지 않고 모든 새로운 정책 동적-적용 됩니다. 
