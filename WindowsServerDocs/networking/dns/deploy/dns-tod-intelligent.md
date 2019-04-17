---
title: DNS 정책을 사용 하 여 지능형 DNS 응답 하루 중 시간에 따라에 대 한
description: 이 항목은 Windows Server 2016 용 DNS 정책 시나리오 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 161446ff-a072-4cc4-b339-00a04857ff3a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 46821daff4a0046bf78d7f56dc7c5deabcc437e4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-intelligent-dns-responses-based-on-the-time-of-day"></a>DNS 정책을 사용 하 여 지능형 DNS 응답 하루 중 시간에 따라에 대 한

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 DNS 정책을 사용 하 여 하루 중 시간에 따라 다른 지리적 분산된 인스턴스 응용 프로그램의 응용 프로그램 교통 분산 하는 방법을 알아보려면 사용할 수 있습니다.  
  
이 시나리오는 교통 체증 등 웹 서버를 다른 시간대에 있는 암호 확인용 응용 프로그램 서버에 한 표준 시간대에서 직접 하려는 경우 유용 합니다. 최대 사용 하는 동안 응용 프로그램 인스턴스 간에 교통 잔액을 로드할 수 있습니다 기간 교통와 기본 서버는 오버 때입니다.   
  
### <a name="bkmk_example1"></a>하루 중 시간에 따라 지능형 DNS 응답 예로  
다음은 예 하루 중 시간에 따라 잔액 응용 프로그램 교통 DNS 정책을 사용 하는 방법입니다.  
  
이 이때 가상 회사, contosogiftservices.com 해당 웹 사이트를 통해 전 세계에서 온라인 선물 솔루션을 제공 하는 Contoso 선물 서비스를 사용 합니다.   
  
두 개의 데이터 센터 (미국) 시애틀의 설정과 한 더블린 (유럽)에서 contosogiftservices.com 웹 호스트 됩니다. DNS 서버가 DNS 정책을 사용 하 여 인식 응답 지리적 위치를 보내는 데 구성 됩니다. 비즈니스에서 최근 서 지 contosogiftservices.com에 방문자 수가 높은 매일 및 일부 고객 서비스 사용 가능성 문제를 보고 했습니다.  
  
Contoso 기프트 서비스 사이트 분석을 수행 하 고 모든 밤 오후 6 시 고 오후 9 시 현지 시간 사이 존재 않음을 서 지의 웹 서버에 교통 합니다. 웹 서버 수 없는 하 게 크기가 조정 이러한 최대 사용 시간에 강화 트래픽을 처리할 고객에 게 서비스 거부가 발생 합니다. 동일한 최대 사용 시간 교통 오버 유럽 및 미국 센터에서 발생합니다. 0x80070643 하루 중에 서버 최대 기능 잘 아래에 있는 교통 볼륨 처리 합니다.  
  
수 있도록는 contosogiftservices.com 고객 응답 경험 웹 사이트에서 Contoso 선물 서비스 더블린; 오후 6 시 사이 오후 9 시 시애틀 응용 프로그램 서버에 몇 가지 더블린 교통 이동 하려는 고 오후 6 시 사이 시애틀 오후 9 시 더블린 응용 프로그램 서버에 몇 가지 시애틀 교통 리디렉션합니다 하려고 합니다.  
  
다음 그림에서는이 시나리오를 보여 줍니다.  
  
![하루 DNS 정책 예제 시간](../../media/DNS-Policy-Tod1/dns_policy_tod1.jpg)  
  
### <a name="bkmk_works1"></a>작동 하루 중 시간에 따라 어떻게 지능형 DNS 응답  
  
DNS 서버 DNS 서버 오후 6 시 사이 각 지리적 위치 오후 9 시 하루 DNS 정책의 시간으로 구성 된 경우 다음을 수행 합니다.  
  
- 로컬 데이터 센터의 웹 서버의 IP 주소와 받을 처음 4 쿼리에 응답 합니다.  
- 원격 데이터 센터의 웹 서버의 IP 주소와 받을 5 번째 쿼리를 대답이 나와 있습니다.   
  
이 정책 기반 동작 오프 원격 웹 서버에서 로컬 응용 프로그램 서버에 대 한 부담 간소화 하 고 고객이 사이트 성능을 향상 하는 로컬 웹 서버 교통 로드 20% 로드 합니다.  
  
DNS 서버 사용량이 교통 관리 기반 일반 지리적 위치를 수행합니다. DNS 클라이언트 쿼리가 북미 지역 또는 유럽, 위치에서 보내는 뿐만 아니라, DNS 서버 로드 시애틀 및 더블린 데이터 센터 교통량을 조정 합니다.  
  
여러 DNS 정책을 DNS에서 구성 된는 일련의, 규칙은 및 순위가 높은 우선 순위에서 DNS에서 처리 됩니다. DNS 사용 시간을 포함 하는 경우와 일치 하는 첫 번째 정책 합니다. 이런 이유이 때문에 대 한 구체적인 정책 높은 우선 순위 부여를 해야 합니다. 정책 하루 중 시간을 만들고 정책의 목록에 높은 우선 순위를 제공 하는 경우 DNS 처리 한 DNS 클라이언트 쿼리가 및 정책에 정의 된의 매개 변수와 일치 하는 경우 이러한 정책을 처음 사용 합니다. 일치 하지 않는 DNS 일치 하는 항목을 찾을 때까지 기본 정책을 처리 하기 위해 정책 목록 아래로 이동 합니다.  
  
정책 입력과 조건에 대 한 자세한 내용은 참조 [DNS 정책 개요](../../dns/deploy/DNS-Policies-Overview.md)합니다.  
  
### <a name="bkmk_how1"></a>DNS 정책 하루 중 시간에 따라 지능형 DNS 응답에 대 한 구성 하는 방법  
DNS 정책을 쿼리 응답 기반 하루 응용 프로그램 부하 분산 시간에 대 한 구성 하려면 다음 단계를 수행 해야 합니다.  
  
- [DNS 클라이언트 서브넷 만들기](#bkmk_subnets)  
- [영역 범위가 만들기](#bkmk_zscopes)  
- [레코드 영역 범위에 추가](#bkmk_records)  
- [DNS 정책 만들기](#bkmk_policies)  
  
>[!NOTE]
>DNS 서버를 구성할 영역에 대 한 권한이 있는에서 다음이 단계를 수행 해야 합니다. 회원 **DnsAdmins**, 다음 절차를 수행 하는 데 필요한는 오른쪽 단추를 클릭 합니다.  
  
다음 섹션 자세한 구성 지침을 제공 합니다.  
  
>[!IMPORTANT]
>다음 섹션에 대 한 많은 매개 예 값 포함 된 예제 Windows PowerShell 명령 포함 됩니다. 다음이 명령을 실행 하기 전에 배포에 대 한 적절 한 값으로 들어 값이 명령에서를 교체 해야 합니다.  
  
#### <a name="bkmk_subnets"></a>DNS 클라이언트 서브넷 만들기  
첫 번째 단계 서브넷 또는 교통량 이동 하려는 지역의 IP 주소 공간을 확인 하는 것입니다. 예를 들어, 미국과 유럽 풍경에 대 한 교통량을 이동 하려면 서브넷 또는 해당이 지역의 IP 주소 공간을 확인 해야 합니다.  
  
지리적 IP 지도에서이 정보를 얻을 수 있습니다. 이러한 지리적 IP 배포 시에 따라, 만들어야 "DNS 클라이언트 서브넷." DNS 클라이언트 서브넷 DNS 서버에 전송 되어 쿼리를 V4 또는 IPv6 서브넷 논리 그룹입니다.  
  
DNS 클라이언트 서브넷 만들 수는 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.  
  
```  
Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet "192.0.0.0/24, 182.0.0.0/24"  
  
Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24, 151.1.0.0/24"  
  
```  
자세한 내용은 참조 [추가 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)합니다.  
  
#### <a name="bkmk_zscopes"></a>영역 범위가 만들기  
구성 요소를 클라이언트 서브넷 하나의 범위 구성 된 DNS 클라이언트 서브넷 각 영역 두 가지 영역 범위로 이동 하 고 싶은 트래픽을 분할 해야 합니다.  
  
예를 들어, www.contosogiftservices.com DNS 이름에 대 한 교통량을 이동 하려면 만들어야 두 서로 다른 영역 범위가 미국 및 유럽 contosogiftservices.com 영역에서 합니다.  
  
영역 범위 영역의 고유한 인스턴스입니다. DNS 영역 고유한 DNS 레코드에 포함 된 각 영역 범위와의 여러 영역 범위에 있을 수 있습니다. 동일한 기록 IP 주소가 서로 다른 여러 범위 또는 동일한 IP 주소에서 사용할 수 있습니다.  
  
>[!NOTE]
>기본적으로 영역 범위 DNS 영역에 있습니다. 해당 영역 같은 이름이이 영역 범위 및이 범위 레거시 DNS 작업 작업 합니다.  
  
다음 Windows PowerShell 명령을 영역 범위가 만드는 사용할 수 있습니다.  
  
```  
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"  
  
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"  
  
```  
자세한 내용은 참조 [추가 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)합니다.  
  
#### <a name="bkmk_records"></a>레코드 영역 범위에 추가  
이제 두 영역 범위가에 웹 서버 호스트 나타내는 레코드를 추가 해야 합니다.  
  
예를 들어, **SeattleZoneScope**, 기록 **www.contosogiftservices.com** IP 주소, 192.0.0.1 시애틀 데이터 센터에 있는 함께 추가 됩니다. 마찬가지로,에서 **DublinZoneScope**, 기록 **www.contosogiftservices.com** 더블린 데이터 센터에 141.1.0.3 IP 주소 추가  
  
기록 영역 범위에 추가 하는 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.  
  
```  
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope  
  
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.3" -ZoneScope "DublinZoneScope"  
  
```  
기록 기본 범위 내에 추가 하면 ZoneScope 매개 포함 되지 않습니다. 표준 시간대 DNS 레코드를 추가 하는 것 같습니다.  
  
자세한 내용은 참조 [추가 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)합니다.  
  
#### <a name="bkmk_policies"></a>DNS 정책 만들기  
기록 파티션 (영역 범위가) 및 사용자를 추가 서브넷 만든 후 쿼리에 응답 올바른 영역 범위에서 반환 되는 쿼리 DNS 클라이언트 서브넷 중 하나에 소스에서 상태가 되 면 되도록 서브넷 및 파티션, 연결 하는 정책을 만들어야 합니다. 정책이 영역 기본 범위 매핑 필요 합니다.  
  
이러한 DNS 정책, 구성 하 고 나면 DNS 서버 문제는 다음과 같습니다.  
  
1. 유럽 DNS 클라이언트 DNS 쿼리에 응답에 더블린 데이터 센터의 웹 서버의 IP 주소를 받습니다.  
2. 미국 DNS 클라이언트 DNS 쿼리에 응답에 시애틀 데이터 센터의 웹 서버의 IP 주소를 받습니다.  
3. 오후 6 시 사이 더블린 오후 9 시 유럽 클라이언트에서 쿼리의 20 %DNS 쿼리에 응답에 시애틀 데이터 센터의 웹 서버의 IP 주소를 받습니다.  
4. 오후 6 시 사이 시애틀 오후 9 시 미국 클라이언트에서 쿼리의 20 %DNS 쿼리에 응답에 더블린 데이터 센터의 웹 서버의 IP 주소를 받습니다.  
5. 이곳의 나머지 부분에서 쿼리 절반 시애틀 데이터 센터의 IP 주소 얻고 나머지 절반 더블린 데이터 센터의 IP 주소 받기.  
  
  
DNS 클라이언트 서브넷 연결 되 고 영역 범위가 DNS 정책을 만들려면 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.  
  
>[!NOTE]
>여기에서 DNS 서버 GMT 표준 시간대의 이므로 최대 사용 시간에 해당 GMT 시간 기간 표시 해야 합니다.  
  
```  
Add-DnsServerQueryResolutionPolicy -Name "America6To9Policy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,4;DublinZoneScope,1" -TimeOfDay "EQ,01:00-04:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 1  
  
Add-DnsServerQueryResolutionPolicy -Name "Europe6To9Policy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "SeattleZoneScope,1;DublinZoneScope,4" -TimeOfDay "EQ,17:00-20:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 2  
  
Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3  
  
Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 4  
  
Add-DnsServerQueryResolutionPolicy -Name "RestOfWorldPolicy" -Action ALLOW --ZoneScope "DublinZoneScope,1;SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 5  
  
```  
자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다.  
  
이제 DNS 서버를 기반으로 지리적 위치와 시간에 교통 리디렉션하여 필요한 DNS 정책으로 구성 됩니다.  
  
DNS 서버 이름 확인 쿼리 받으면 DNS 서버 평가 필드에서 구성 된 DNS 정책에 대 한 DNS 요청 합니다. 이름 해상도 요청에서 원본 IP 주소와 일치 하는 정책, 관련된 영역 범위 쿼리에 응답 하는 데 사용 되 고에서 리소스에 지리적 가까운 사용자가 이동 합니다.  
  
관리 요구 사항에 교통에 따라 DNS 정책 수천을 만들 수 있습니다 고-들어오는 쿼리에서 DNS 서버를 다시 시작 하지 않고 모든 새로운 정책 동적-적용 됩니다.


