---
title: Azure 클라우드 응용 프로그램 서버로 시간 기반 DNS 응답
description: 이 항목은 Windows Server 2016에 대 한 DNS 정책 시나리오 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: 4846b548-8fbc-4a7f-af13-09e834acdec0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4307ce1512980277af819e0710e0447d8dbac8c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406198"
---
# <a name="dns-responses-based-on-time-of-day-with-an-azure-cloud-app-server"></a>Azure 클라우드 응용 프로그램 서버로 시간 기반 DNS 응답

>적용 대상: Windows Server(반기 채널), Windows Server 2016

하루 중 시간을 기반으로 하는 DNS 정책을 사용 하 여 응용 프로그램의 서로 다른 지리적으로 분산 된 인스턴스 응용 프로그램 트래픽을 분산 하는 방법에 알아보려면이 항목을 사용할 수 있습니다. 

이 시나리오는 다른 표준 시간대에 있는 Microsoft Azure에서 호스팅되는 웹 서버와 같은 다른 응용 프로그램 서버를 한 표준 시간대에 트래픽을 전달 하려는 경우에 유용 합니다. 사용량이 많은 기간 중 응용 프로그램 인스턴스 간에 트래픽의 부하를 분산 하면 트래픽이 주 서버는 오버 로드 하는 경우 기간입니다. 

> [!NOTE]
> Azure를 사용 하지 않고 지능형 DNS 응답에 대 한 DNS 정책을 사용 하는 방법을 알아보려면 다음을 참조 [기반에 대 한 지능형 DNS 응답 시간을 사용 하 여 DNS 정책](Scenario--Use-DNS-Policy-for-Intelligent-DNS-Responses-Based-on-the-Time-of-Day.md)합니다. 

## <a name="example-of-intelligent-dns-responses-based-on-the-time-of-day-with-azure-cloud-app-server"></a>Azure 클라우드 응용 프로그램 서버와 시간에 따라 지능형 DNS 응답의 예

다음은 하루 중 시간에 따라 응용 프로그램 트래픽 분산을 DNS 정책 사용 방법의 예입니다.

이 예제에서는 가상의 회사를 해당 웹 사이트를 통해 전 세계에 걸쳐 온라인 gifting 솔루션에서 제공 하는 Contoso 선물 서비스를 사용 하 여 contosogiftservices.com 합니다. 

Contosogiftservices.com 웹 사이트는 시애틀의 단일 온-프레미스 데이터 센터 (공용 IP 192.68.30.2 사용) 에서만 호스팅됩니다. 

DNS 서버는 온-프레미스 데이터 센터에도 있습니다. 

비즈니스에서에 최근 서 지 contosogiftservices.com 방문자 수가 높을수록 매일 있으며 일부 고객의 서비스 가용성 문제는 보고 합니다. 

Contoso 선물 서비스는 사이트 분석을 수행 하 고 현지 시간으로 오후 6 시와 오후 9 시 사이의 매일 저녁 급증 함에에서는 시애틀 웹 서버에 대 한 트래픽을 검색 합니다. 웹 서버 고객에 게 서비스 거부가 발생 하는 이러한 피크 시간에 늘어난된 트래픽을 처리 하도록 확장할 수 없습니다. 

Contosogiftservices.com 고객 웹 사이트에서 응답성이 뛰어난 환경을 얻을 수 있도록, Contoso 선물 서비스 하기로 결정이 시간 동안이 가상 컴퓨터를 임대 합니다 \(VM\) 해당 웹 서버의 복사본을 호스팅할 Microsoft Azure에서.  

Contoso 선물 서비스 (192.68.31.44) VM에 대 한 Azure에서 공용 IP 주소를 가져옵니다와 azure 간의 오후 5-10 시 대체 1 시간 동안 허용 되기는 했지만 웹 서버를 배포 하는 자동화를 개발 합니다.

> [!NOTE]
> Azure Vm에 대 한 자세한 내용은 참조 [가상 컴퓨터 설명서](https://azure.microsoft.com/documentation/services/virtual-machines/) 

DNS 서버는 5-9 오후 매일 사이의 30%의 쿼리는 Azure에서 실행 되는 웹 서버 인스턴스에 전송 되도록 영역 범위 및 DNS 정책을 사용 하 여 구성 됩니다.

다음 그림에서는이 시나리오를 보여 줍니다.

![하루 응답 시간에 대 한 DNS 정책](../../media/DNS-Policy-Tod2/dns_policy_tod2.jpg)  

## <a name="how-intelligent-dns-responses-based-on-time-of-day-with-azure-app-server-works"></a>응용 프로그램 서버를 작동 하는 Azure와 시간을 기준으로 지능형 DNS 응답 하는 방법
 
이 문서에는 두 개의 서로 다른 응용 프로그램 서버 IP 주소로-DNS 쿼리에 응답 하도록 DNS 서버를 구성 하려면 웹 서버 1 개 시애틀에는 및 다른 하나는 Azure 데이터 센터는 방법을 보여줍니다.

오후 6 시에 오후 9 시 시애틀의 사용량이 적은 시간을 기반으로 하는 새 DNS 정책의 구성한 후 DNS 서버에서 보내는 시애틀 웹 서버의 IP 주소를 포함 하는 클라이언트에 대 한 DNS 응답의 / 72% 및 Azure 웹 서버의 IP 주소를 포함 하는 클라이언트에 대 한 DNS 응답의 30% 있으므로 클라이언트 트래픽을 새 Azure 웹 서버로 보내는 및 시애틀 웹 서버 오버 로드를 방지 합니다. 

그 외 시간에는 일반적인 쿼리 처리가 수행 되며, 온-프레미스 데이터 센터의 웹 서버에 대 한 레코드를 포함 하는 기본 영역 범위에서 응답이 전송 됩니다. 

Azure 레코드에서 10 분의 TTL Azure VM을 제거 하기 전에 레코드가 LDNS 캐시에서 만료 된 것을 확인 합니다. 이러한 크기 조정의 이점 중 하나는 DNS 데이터를 온-프레미스에 유지 하 고 요구 사항에 따라 Azure에 확장을 유지할 수 있다는 것입니다.

## <a name="how-to-configure-dns-policy-for-intelligent-dns-responses-based-on-time-of-day-with-azure-app-server"></a>Azure 응용 프로그램 서버와 시간에 따라 지능형 DNS 응답에 대 한 DNS 정책을 구성 하는 방법

시간 기반 일 응용 프로그램 부하 분산의 쿼리 응답에 대 한 DNS 정책을 구성 하려면 다음 단계를 수행 해야 합니다.

- [영역 범위 만들기](#create-the-zone-scopes)
- [영역 범위에 레코드 추가](#add-records-to-the-zone-scopes)
- [DNS 정책 만들기](#create-the-dns-policies)

> [!NOTE]
> 구성할 영역에 대 한 권한이 있는 DNS 서버에서 이러한 단계를 수행 해야 합니다. 다음 절차를 수행 하려면 DnsAdmins, 또는 이와 동등한의 멤버 자격이 필요 합니다. 

다음 섹션에서는 자세한 구성 지침을 제공 합니다.

> [!IMPORTANT]
> 다음 섹션에서는 예제 많은 매개 변수 값이 포함 된 예제 Windows PowerShell 명령을 포함 합니다. 이러한 명령에 대 한 예제 값은 다음이 명령을 실행 하기 전에 배포에 적합 한 값으로 바꾸는 것을 확인 합니다. 


### <a name="create-the-zone-scopes"></a>영역 범위를 만듭니다

영역 범위는 영역의 고유 인스턴스입니다. DNS 영역은 자체 DNS 레코드 집합이 포함 된 각 영역 범위를 갖는 여러 영역 범위를 가질 수 있습니다. 동일한 레코드는 동일한 IP 주소 또는 IP 주소가 다른 여러 범위에 있을 수 있습니다. 

> [!NOTE]
> 기본적으로 영역 범위 DNS 영역에 있습니다. 영역을 같은 이름의이 영역 범위 및 레거시 DNS 작업은이 범위에서 작동 합니다. 

Azure 레코드를 호스트 하도록 영역 범위를 만들려면 다음 예제에서는 명령을 사용할 수 있습니다.

```
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AzureZoneScope"
```

자세한 내용은 참조 [DnsServerZoneScope 추가](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

### <a name="add-records-to-the-zone-scopes"></a>영역 범위에 레코드를 추가 합니다.
다음 단계 영역 범위에는 웹 서버 호스트를 나타내는 레코드를 추가 하는 것입니다. 

AzureZoneScope, 레코드 www.contosogiftservices.com Azure 퍼블릭 클라우드에 있는 IP 주소, 192.68.31.44와 함께 추가 됩니다. 

마찬가지로 -0contosogiftservices @ no__t-1 @no__t 기본 영역 범위에서 contosogiftservices @ no__t-3 @no__t 레코드는 시애틀 온-프레미스 데이터 센터에서 실행 되는 웹 서버의 IP 주소 192.68.30.2를 사용 하 여 추가 됩니다.

아래 두 번째 cmdlet – ZoneScope 매개 변수가 포함 되지 않습니다. 이 때문에 기본 ZoneScope 레코드가 추가 됩니다. 

또한 Azure Vm에 대 한 레코드의 TTL은 LDNS 캐시 하지 않는 오래-로드 균형 조정을 방해 하 게 되도록 600s (10 분)에 보관 됩니다. 또한 Azure Vm은 캐시 된 레코드와 함께 클라이언트도는 해결할 수 있도록 대체 방법으로 추가 1 시간 동안 사용할 수입니다.

```
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.31.44" -ZoneScope "AzureZoneScope" –TimeToLive 600

Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.30.2"
```

자세한 내용은 참조 [추가 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)합니다.  

### <a name="create-the-dns-policies"></a>DNS 정책 만들기 
영역 범위를 만든 후에 다음 작업이 수행 되도록 이러한 범위 간에 들어오는 쿼리를 분산 하는 DNS 정책을 만들 수 있습니다.

1. 매일 오후 6 시부터 오후 9 시까지 클라이언트의 30%는 DNS 응답의 Azure 데이터 센터에서 웹 서버의 IP 주소를 수신 하는 반면, 70%의 클라이언트는 시애틀 온-프레미스 웹 서버의 IP 주소를 받습니다.
2. 모든 클라이언트는 다른 시간에 시애틀 온-프레미스 웹 서버의 IP 주소를 수신 합니다.

하루 중 시간에는 DNS 서버의 현지 시간으로 표현 될 수 있습니다.

다음 예제 명령은 DNS 정책을 만드는 데 사용할 수 있습니다.

```
Add-DnsServerQueryResolutionPolicy -Name "Contoso6To9Policy" -Action ALLOW -ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00” -ZoneName "contosogiftservices.com" –ProcessingOrder 1
```

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다.  
  
이제 하루 중 시간에 따라 Azure 웹 서버에 트래픽을 리디렉션할 수 필요한 DNS 정책을 사용 하 여 DNS 서버가 구성 됩니다. 

참고 식:

`
 -ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00” 
`

이 식은 시애틀 웹 서버의 IP 주소/72 %의 경우 Azure 웹 서버의 IP 주소 30 %의 시간을 보내는 동안 전송 하도록 DNS 서버에 알려 주는 ZoneScope 및 가중치 조합을 사용 하 여 DNS 서버를 구성 합니다.

관리 요구 사항을 트래픽이 따라 DNS 정책의 수천을 만들 수 있습니다 하 고 들어오는 쿼리-DNS 서버를 다시 시작 하지 않고 모든 새 정책-동적으로 적용 됩니다.
