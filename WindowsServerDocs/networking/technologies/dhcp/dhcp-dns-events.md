---
title: DNS 레코드 등록에 대 한 이벤트를 DHCP 기록
description: 이 항목에서는 로깅 이벤트를 Windows Server 2016 DHCP 서버에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: beb8c188-6fcf-4520-8825-d17f8ee9fb04
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 61a5099cd5e1ef1d4687baa8c20411c96ea8f519
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="dhcp-logging-events-for-dns-registrations"></a>DNS 등록에 대 한 이벤트를 DHCP 기록

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이제 서버 이벤트 로그가 DHCP DNS 등록 오류에 대 한 자세한 정보를 제공 합니다.

>[!NOTE]
>대부분의 경우 서버 DHCP에서 DNS 레코드 등록 실패 하는 이유는 DNS Reverse\ 조회 영역이 올바르게 구성 되어 또는 전혀 구성 되어 있지는 합니다.

다음과 같은 새로운 DHCP 이벤트 지원 DNS 등록을 한 잘못 구성 된 때문에 실패 하거나 DNS Reverse\ 조회 영역이 누락 된 때를 쉽게 식별할 수 있습니다.

|ID|이벤트|값|
|-----|--------------------|--------------------------------------------------------|
|20317|DHCPv4.ForwardRecordDNSFailure|IPv4 주소 %1 및 FQDN %2 앞으로 레코드 등록 %3 오류가 발생 했습니다. 이 경우이 기록에 대 한 앞으로 조회 영역이 DNS 서버에 존재 하지 않는 않기 때문일 수 있습니다.|
|20318|DHCPv4.ForwardRecordDNSTimeout|IPv4 주소 %1 및 FQDN %2 앞으로 레코드 등록 %3 오류가 발생 했습니다.|
|20319|DHCPv4.PTRRecordDNSFailure|IPv4 주소 %1 및 FQDN %2 PTR 녹화 등록 %3 오류가 발생 했습니다. 이 경우이 기록에 대 한 역방향 조회 영역이 DNS 서버에 존재 하지 않습니다 않기 때문일 수 있습니다.|
|20320|DHCPv4.PTRRecordDNSTimeout|IPv4 주소 %1 및 FQDN %2 PTR 녹화 등록 %3 오류가 발생 했습니다.|
|20321|DHCPv6.ForwardRecordDNSFailure|앞으로 레코드 등록 IPv6 주소 %1 및 FQDN %2%3 오류가 발생 했습니다. 이 경우이 기록에 대 한 앞으로 조회 영역이 DNS 서버에 존재 하지 않는 않기 때문일 수 있습니다.|
|20322|DHCPv6.ForwardRecordDNSTimeout|앞으로 레코드 등록 IPv6 주소 %1 및 FQDN %2%3 오류가 발생 했습니다.|
|20323|DHCPv6.PTRRecordDNSFailure|IPv6 주소 %1 및 FQDN %2 PTR 녹화 등록 %3 오류가 발생 했습니다. 이 경우이 기록에 대 한 역방향 조회 영역이 DNS 서버에 존재 하지 않습니다 않기 때문일 수 있습니다.|
|20324|DHCPv6.PTRRecordDNSTimeout|IPv6 주소 %1 및 FQDN %2 PTR 녹화 등록 %3 오류가 발생 했습니다.|
|20325|DHCPv4.ForwardRecordDNSError|IPv4 주소 %1 및 FQDN %2 PTR 녹화 등록 %3 오류 \(%4\) 하지 못했습니다.|
|20326|DHCPv6.ForwardRecordDNSError|오류 %3 \(%4\) IPv6 주소 %1 및 FQDN %2 레코드 등록 앞으로 실패|
|20327|DHCPv6.PTRRecordDNSError|오류 %3 \(%4\) IPv6 주소 %1 및 FQDN %2 레코드 등록 PTR 하지 못했습니다.|

