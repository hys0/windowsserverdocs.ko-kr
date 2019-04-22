---
title: DHCP DNS 레코드 등록에 대 한 이벤트 로깅
description: 이 항목에서는 Windows Server 2016에서 로깅 이벤트 DHCP 서버에 대 한 정보를 제공합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: beb8c188-6fcf-4520-8825-d17f8ee9fb04
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7f4ce217b19cfd8a63bff1ae504362d4fc24fcd0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816904"
---
# <a name="dhcp-logging-events-for-dns-registrations"></a>DHCP DNS 등록에 대 한 이벤트 로깅

>적용 대상: Windows Server (반기 채널), Windows Server 2016

DHCP 서버 이벤트 로그는 이제 DNS 등록 오류에 대 한 자세한 정보를 제공합니다.

>[!NOTE]
>대부분의 경우에서 DHCP 서버에서 DNS 레코드 등록 오류 원인은 DNS 역방향는\-조회 영역 잘못 구성 되거나 전혀 구성 되지 않았습니다.

다음 새 DHCP 이벤트를 사용 하는 잘못 구성으로 인해 실패 하거나 없습니다. DNS 역방향 DNS 등록 하는 시점을 쉽게 파악 하는 데 도움이\-조회 영역입니다.

|ID|이벤트|값|
|-----|--------------------|--------------------------------------------------------|
|20317|DHCPv4.ForwardRecordDNSFailure|오류: %3을 사용 하 여 %1 IPv4 주소 및 FQDN %2 정방향 레코드 등록 하지 못했습니다. 이 레코드에 대 한 정방향 조회 영역을 DNS 서버에 없기 때문에 할 것 같습니다.|
|20318|DHCPv4.ForwardRecordDNSTimeout|오류: %3을 사용 하 여 %1 IPv4 주소 및 FQDN %2 정방향 레코드 등록 하지 못했습니다.|
|20319|DHCPv4.PTRRecordDNSFailure|오류: %3을 사용 하 여 %1 IPv4 주소와 FQDN %2 PTR 레코드 등록 하지 못했습니다. 이 레코드에 대 한 역방향 조회 영역을 DNS 서버에 없기 때문에 할 것 같습니다.|
|20320|DHCPv4.PTRRecordDNSTimeout|오류: %3을 사용 하 여 %1 IPv4 주소와 FQDN %2 PTR 레코드 등록 하지 못했습니다.|
|20321|DHCPv6.ForwardRecordDNSFailure|오류: %3을 사용 하 여 %1 IPv6 주소 및 FQDN %2 정방향 레코드 등록 하지 못했습니다. 이 레코드에 대 한 정방향 조회 영역을 DNS 서버에 없기 때문에 할 것 같습니다.|
|20322|DHCPv6.ForwardRecordDNSTimeout|오류: %3을 사용 하 여 %1 IPv6 주소 및 FQDN %2 정방향 레코드 등록 하지 못했습니다.|
|20323|DHCPv6.PTRRecordDNSFailure|오류: %3을 사용 하 여 IPv6 주소 %1 및 %2 FQDN에 대 한 PTR 레코드 등록 하지 못했습니다. 이 레코드에 대 한 역방향 조회 영역을 DNS 서버에 없기 때문에 할 것 같습니다.|
|20324|DHCPv6.PTRRecordDNSTimeout|오류: %3을 사용 하 여 IPv6 주소 %1 및 %2 FQDN에 대 한 PTR 레코드 등록 하지 못했습니다.|
|20325|DHCPv4.ForwardRecordDNSError|%3 오류로 %1 IPv4 주소와 FQDN %2 PTR 레코드 등록 하지 못했습니다 \(%4\)합니다.|
|20326|DHCPv6.ForwardRecordDNSError|%3 오류로 %1 IPv6 주소 및 FQDN %2 정방향 레코드 등록 하지 못했습니다. \(%4\)|
|20327|DHCPv6.PTRRecordDNSError|%3 오류로 %1 IPv6 주소 및 FQDN %2 PTR 레코드 등록 하지 못했습니다 \(%4\)합니다.|

