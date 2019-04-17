---
title: DNS 응답은 Azure와 시간에 따라 클라우드 앱 서버
description: 이 항목은 Windows Server 2016 용 DNS 정책 시나리오 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 4846b548-8fbc-4a7f-af13-09e834acdec0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3255d3fe29f6a7dda821183fa4352964cc230a5f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="dns-responses-based-on-time-of-day-with-an-azure-cloud-app-server"></a>DNS 응답은 Azure와 시간에 따라 클라우드 앱 서버

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 DNS 정책을 사용 하 여 하루 중 시간에 따라 다른 지리적 분산된 인스턴스 응용 프로그램의 응용 프로그램 교통 분산 하는 방법을 알아보려면 사용할 수 있습니다. 

이 시나리오는 교통 같은 다른 시간대에 있는 Microsoft Azure 호스트 하는 웹 서버 대체 응용 프로그램의 서버로 한 표준 시간대에서 직접 하려는 경우 유용 합니다. 최대 사용 하는 동안 응용 프로그램 인스턴스 간에 교통 잔액을 로드할 수 있습니다 기간 교통와 기본 서버는 오버 때입니다. 

>[!NOTE]
>Azure 사용 하지 않고 지능형 DNS 응답 DNS 정책을 사용 하는 방법을 알아보려면 [지능형 DNS 응답을 기반 하루 중 시간에 대 한 DNS 정책을 사용 하 여](Scenario--Use-DNS-Policy-for-Intelligent-DNS-Responses-Based-on-the-Time-of-Day.md)합니다. 

## <a name="bkmk_azureexample"></a>Azure 클라우드 앱 서버 하루 중 시간에 따라 지능형 DNS 응답 예로

다음은 예 하루 중 시간에 따라 잔액 응용 프로그램 교통 DNS 정책을 사용 하는 방법입니다.

이 이때 가상 회사, contosogiftservices.com 해당 웹 사이트를 통해 전 세계에서 온라인 선물 솔루션을 제공 하는 Contoso 선물 서비스를 사용 합니다. 

contosogiftservices.com 웹 사이트 (와 공개 IP 192.68.30.2) 시애틀의 단일 온-프레미스 데이터 센터에만 호스트 됩니다. 

DNS 서버가 온-프레미스 데이터 센터에도 있습니다. 

비즈니스에서 최근 서 지 contosogiftservices.com에 방문자 수가 높은 매일 및 일부 고객 서비스 사용 가능성 문제를 보고 했습니다. 

Contoso 기프트 서비스 사이트 분석을 수행 하 고 모든 밤 오후 6 시 고 오후 9 시 현지 시간 사이 존재 않음을 서 지 시애틀 웹 서버에 교통에 합니다. 웹 서버 수 없는 하 게 크기가 조정 이러한 최대 사용 시간에 강화 트래픽을 처리할 고객에 게 서비스 거부가 발생 합니다. 

수 있도록는 contosogiftservices.com 고객 응답 경험 웹 사이트에서 Contoso 선물 서비스는 가상 대여할는이 시간 동안 Microsoft Azure에 \(VM\)로 기계는 웹 서버의 복사본 호스트 결정 합니다.  

Contoso 선물 서비스 VM (192.68.31.44 공용 IP 주소를 Azure에서 가져옵니다)을 배포 하는 웹 서버 매일에 Azure 사이의 5-10 오후, 긴급 1 시간 동안 수 있도록 자동화 조사 하 고 있습니다.

>[!NOTE]
>Azure Vm에 대 한 자세한 내용은 참조 [가상 컴퓨터 설명서](https://azure.microsoft.com/documentation/services/virtual-machines/) 

DNS 서버가 5-9 오후 매일 사이 30% 쿼리의 웹 서버 Azure에서 실행 중인 인스턴스를 보내도록 영역 범위가 및 DNS 정책으로 구성 됩니다.

다음 그림에서는이 시나리오를 보여 줍니다.

![응답 하루 중 시간에 대 한 DNS 정책](../../media/DNS-Policy-Tod2/dns_policy_tod2.jpg)  

## <a name="bkmk_azurehow"></a>앱 서버 작동 Azure와 시간에 따라 지능형 DNS 응답 하는 방법
 
이 문서는 방법을 보여 주는 두 가지 다른 응용 프로그램이 서버 IP 주소가-DNS 쿼리에 응답을 DNS 서버를 구성 시애틀의 하나 웹 서버를 다른 하나는 Azure 데이터 센터에 있습니다.

오후 6 시에 오후 9 시 시애틀에서 최대 사용 시간을 기반으로 하는 새 DNS 정책, 구성 후 DNS 서버가 보냅니다/72 %DNS 응답 시애틀 웹 서버의 IP 주소를 포함 하는 클라이언트와 Azure 웹 서버의 IP 주소를 포함 하는 클라이언트 DNS 응답 30% 되므로 클라이언트 교통 새 Azure 웹 서버에 전송 하 고 시애틀 웹 서버 과도 하는 것을 방지 합니다. 

그 외에, 하루 중 일반 쿼리 처리 수행 하 고 응답 온-프레미스 데이터 센터의 웹 서버에 대 한 기록을 포함 하는 기본 영역 범위에서 전송 됩니다. 

Azure 기록에 10 분 TTL VM는 Azure에서 제거 하기 전에 기록 LDNS 캐시의 만료 된 설치할 수 있도록 보장 합니다. 이러한 크기 조정의 혜택 중 하나는 사용자 DNS 데이터 온-프레미스를 유지할 수 하 고 필요에 따라 azure 확장 유지 합니다.

## <a name="bkmk_azureconfigure"></a>DNS 정책 Azure 앱 서버 하루 중 시간에 따라 지능형 DNS 응답에 대 한 구성 하는 방법
DNS 정책을 쿼리 응답 기반 하루 응용 프로그램 부하 분산 시간에 대 한 구성 하려면 다음 단계를 수행 해야 합니다.


- [영역 범위가 만들기](#bkmk_zscopes)
- [레코드 영역 범위에 추가](#bkmk_records)
- [DNS 정책 만들기](#bkmk_policies)


>[!NOTE]
>DNS 서버를 구성할 영역에 대 한 권한이 있는에서 다음이 단계를 수행 해야 합니다. 오른쪽 단추를 클릭 하거나 DnsAdmins의 회원은 다음 절차를 수행 해야 합니다. 

다음 섹션 자세한 구성 지침을 제공 합니다.

>[!IMPORTANT]
>다음 섹션에 대 한 많은 매개 예 값 포함 된 예제 Windows PowerShell 명령 포함 됩니다. 다음이 명령을 실행 하기 전에 배포에 대 한 적절 한 값으로 들어 값이 명령에서를 교체 해야 합니다. 


### <a name="bkmk_zscopes"></a>영역 범위가 만들기
영역 범위 영역의 고유한 인스턴스입니다. DNS 영역 고유한 DNS 레코드에 포함 된 각 영역 범위와의 여러 영역 범위에 있을 수 있습니다. 동일한 기록 IP 주소가 서로 다른 여러 범위 또는 동일한 IP 주소에서 사용할 수 있습니다. 

>[!NOTE]
>기본적으로 영역 범위 DNS 영역에 있습니다. 해당 영역 같은 이름이이 영역 범위 및이 범위 레거시 DNS 작업 작업 합니다. 

Azure 레코드를 호스트 하는 영역 범위 만드는 명령은 사용할 수 있습니다.

```
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AzureZoneScope"
```

자세한 내용은 참조 [DnsServerZoneScope 추가](https://technet.microsoft.com/library/mt126267.aspx)

### <a name="bkmk_records"></a>레코드 영역 범위에 추가
다음 단계 영역 범위에는 웹 서버 호스트 나타내는 레코드를 추가 하는 것입니다. 

AzureZoneScope, 기록 www.contosogiftservices.com IP 주소, 192.68.31.44 공개 Azure 클라우드에 있는으로 추가 됩니다. 

마찬가지로, 기본 영역 범위 \(contosogiftservices.com\) 기록 \(www.contosogiftservices.com\) IP 주소 192.68.30.2 시애틀 온-프레미스 데이터 센터에 실행 하는 웹 서버도 추가 됩니다.

다음 두 번째 cmdlet-ZoneScope 매개 포함 되지 않습니다. 이 인해 레코드 ZoneScope 기본에 추가 됩니다. 

또한는 LDNS 수행 캐시 하는 것 부하 분산 방해가 되 긴 시간-되도록 하는 Azure Vm 기록 TTL 600s (10 분)에 유지 됩니다. 또한 Azure Vm는으로 대체 캐시 된 레코드 클라이언트도 확인할 수 있도록 하기 위해 추가 1 시간 동안 사용할 수 있습니다.

```
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.31.44" -ZoneScope "AzureZoneScope" –TimeToLive 600

Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.30.2"
```

자세한 내용은 참조 [추가 DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx)합니다.  

### <a name="bkmk_policies"></a>DNS 정책 만들기 
영역 범위가 만든 후 다음 발생 수 있도록 이러한 범위 들어오는 쿼리 분산 DNS 정책 만들 수 있습니다.

1. 매일 오후 9을 오후 6에서에서 클라이언트 30% 70% 클라이언트의 온-프레미스 웹 서버 시애틀의 IP 주소를 수신 하는 동안 DNS에 대 한 응답, Azure 데이터 센터의 웹 서버의 IP 주소를 받습니다.
2. 그 외에 모든 클라이언트 시애틀 온-프레미스 웹 서버의 IP 주소를 받습니다.

로컬 시간 DNS 서버 표시 하는 하루 중 시간에 있습니다.

DNS 정책을 만들려면 명령은 사용할 수 있습니다.

```
Add-DnsServerQueryResolutionPolicy -Name "Contoso6To9Policy" -Action ALLOW –-ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00” -ZoneName "contosogiftservices.com" –ProcessingOrder 1
```

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx)합니다.  
  
이제 DNS 서버 하루 중 시간에 따라 Azure 웹 서버를 교통 리디렉션합니다 필요한 DNS 정책으로 구성 됩니다. 

식 참고:

`
 -ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00” 
`

이 식 DNS 서버/72% 비율로, Azure 웹 서버의 IP 주소를 30% 비율로 보내는 시애틀 웹 서버의 IP 주소를 보낼 수 있는 ZoneScope 및 무게 조합을 사용 하 여 DNS 서버를 구성 합니다.

관리 요구 사항에 교통에 따라 DNS 정책 수천을 만들 수 있습니다 고-들어오는 쿼리에서 DNS 서버를 다시 시작 하지 않고 모든 새로운 정책 동적-적용 됩니다.
