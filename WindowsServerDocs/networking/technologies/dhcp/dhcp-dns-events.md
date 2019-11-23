---
title: DNS 레코드 등록에 대 한 DHCP 로깅 이벤트
description: 이 항목에서는 Windows Server 2016의 DHCP 서버 로깅 이벤트에 대 한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: beb8c188-6fcf-4520-8825-d17f8ee9fb04
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ccd8024af30f1103afa8eac52926a6b42d32940a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355430"
---
# <a name="dhcp-logging-events-for-dns-registrations"></a>DNS 등록을 위한 DHCP 로깅 이벤트

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이제 DHCP 서버 이벤트 로그에서 DNS 등록 오류에 대 한 자세한 정보를 제공 합니다.

>[!NOTE]
>대부분의 경우 DHCP 서버에서 DNS 레코드 등록에 실패 하는 이유는 DNS 역방향\-조회 영역이 잘못 구성 되었거나 전혀 구성 되지 않은 것입니다.

다음 새 DHCP 이벤트는 DNS 역방향\-조회 영역을 잘못 구성 하거나 누락 하 여 DNS 등록에 실패 하는 경우 쉽게 식별할 수 있도록 지원 합니다.

|id|이벤트|값|
|-----|--------------------|--------------------------------------------------------|
|20317|DHCPv4. ForwardRecordDNSFailure|IPv4 주소 %1 및 FQDN %2에 대 한 전달 레코드 등록이 %3 오류로 인해 실패 했습니다. 이는이 레코드에 대 한 전방 조회 영역이 DNS 서버에 존재 하지 않기 때문에 발생할 수 있습니다.|
|20318|ForwardRecordDNSTimeout|IPv4 주소 %1 및 FQDN %2에 대 한 전달 레코드 등록이 %3 오류로 인해 실패 했습니다.|
|20319|PTRRecordDNSFailure|%3 오류로 인해 IPv4 주소 %1 및 FQDN %2에 대 한 PTR 레코드를 등록 하지 못했습니다. 이 레코드의 역방향 조회 영역이 DNS 서버에 존재 하지 않기 때문일 수 있습니다.|
|20320|PTRRecordDNSTimeout|%3 오류로 인해 IPv4 주소 %1 및 FQDN %2에 대 한 PTR 레코드를 등록 하지 못했습니다.|
|20321|DHCPv6. ForwardRecordDNSFailure|IPv6 주소 %1 및 FQDN %2에 대 한 전방 레코드 등록이 %3 오류로 인해 실패 했습니다. 이는이 레코드에 대 한 전방 조회 영역이 DNS 서버에 존재 하지 않기 때문에 발생할 수 있습니다.|
|20322|ForwardRecordDNSTimeout|IPv6 주소 %1 및 FQDN %2에 대 한 전방 레코드 등록이 %3 오류로 인해 실패 했습니다.|
|20323|PTRRecordDNSFailure|%3 오류로 인해 IPv6 주소 %1 및 FQDN %2에 대 한 PTR 레코드를 등록 하지 못했습니다. 이 레코드의 역방향 조회 영역이 DNS 서버에 존재 하지 않기 때문일 수 있습니다.|
|20324|PTRRecordDNSTimeout|%3 오류로 인해 IPv6 주소 %1 및 FQDN %2에 대 한 PTR 레코드를 등록 하지 못했습니다.|
|20325|ForwardRecordDNSError|%3 \(%4\)오류가 발생 하 여 IPv4 주소 %1 및 FQDN %2에 대 한 PTR 레코드를 등록 하지 못했습니다.|
|20326|ForwardRecordDNSError|오류 %3 \(%4 (으)로 인해 IPv6 주소 %1 및 FQDN %2에 대 한 전달 레코드를 등록 하지 못했습니다\)|
|20327|PTRRecordDNSError|%3 \(%4\)오류가 발생 하 여 IPv6 주소 %1 및 FQDN %2에 대 한 PTR 레코드를 등록 하지 못했습니다.|

