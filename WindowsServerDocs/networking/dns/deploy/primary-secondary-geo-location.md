---
title: 지리적 위치를 사용 하 여 DNS 정책 기반 주 보조 배포 교통 관리
description: 이 항목은 Windows Server 2016 용 DNS 정책 시나리오 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: a9ee7a56-f062-474f-a61c-9387ff260929
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4c78a0198e29fb59f30fd8ad776c7f200312d014
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-secondary-deployments"></a>지리적 위치를 사용 하 여 DNS 정책 기반 주 보조 배포 교통 관리

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 DNS 배포 기본 및 보조 DNS 서버를 포함 하는 경우 지리적 위치를 기반으로 교통 관리에 대 한 정책을 DNS 만드는 방법을 알아보려면 사용할 수 있습니다.  

이전 시나리오 [기본 서버와 지리적 위치를 기반 교통 관리에 대 한 사용 하 여 DNS 정책을](primary-geo-location.md), 주 DNS 서버에서 DNS 정책 지리적 위치를 기반으로 교통 관리에 대 한 구성에 대 한 지침을 제공 합니다. 하지만 인터넷 인프라에, DNS 서버는 널리 사용 되는 주 보조 모델 어디 영역의 쓸 수 복사본 선택 하 고 보안 기본 서버에 저장 되 고 영역 읽기 전용 복사본이 여러 보조 서버에 저장 됩니다.   
  
보조 서버 요청 하 고 새로운 기본 DNS 서버에 영역은 변경 사항을 포함 하는 영역 업데이트를 수신 영역 전송 프로토콜 신뢰할 수 있는 전송 (횟수) 및 증분 영역 Transfer (횟수)를 사용 합니다.   
  
>[!NOTE]
>횟수에 대 한 자세한 내용은 참조 인터넷 엔지니어링 작업 포스 (IETF) [메모 5936에 대 한 요청](https://tools.ietf.org/rfc/rfc5936.txt)합니다. 횟수에 대 한 자세한 내용은 참조 인터넷 엔지니어링 작업 포스 (IETF) [메모 1995에 대 한 요청](https://tools.ietf.org/html/rfc1995)합니다.  
  
## <a name="bkmk_example"></a>주 보조 지리적 위치 기반 교통 관리 예  
다음은 DNS 쿼리를 수행 하는 클라이언트의 실제 위치를 기반으로 교통 리디렉션을 달성 하기 위해 주 보조 배포에서 DNS 정책을 사용 하는 방법을의 예입니다.  
  
사용 하 여 웹 및 솔루션; 호스팅 도메인을 제공 하는 클라우드 서비스를 Contoso 두 가상 회사-이 예제 하 고 Woodgrove 음식 서비스 세계 여러 도시에서 다양 한 음식 배달 서비스를 제공 하는 웹 사이트 woodgrove.com 라는 되어 있는.  
  
woodgrove.com 고객이 해당 웹 사이트에서 응답 경험을 가져올 되도록 Woodgrove 유럽 유럽 데이터 센터에 게 연락 하는 클라이언트와 미국 클라이언트 미국 데이터 센터에 게 연락 하려고 합니다. 다른 곳에서 전 세계에 있는 고객 데이터 센터 중 하나를 보낼 수 있습니다.  
  
Contoso 클라우드 서비스는 미국에서 크기 조정 설정과 Contoso 되는 식료품 woodgrove.com 포털 주문 섬에는 유럽의 두 개의 데이터 센터를 있습니다.  
  
Contoso DNS 배포 두 보조 서버에 포함 되어: **SecondaryServer1**, IP 주소 10.0.0.2; 및 **SecondaryServer2**, 10.0.0.3 IP 주소를 사용 합니다. 이러한 보조 서버 역할을 하는 두 가지 다양 한 지역에서 이름 서버 SecondaryServer1 유럽 및 SecondaryServer2 미국에서 위치에 있습니다
  
주 쓸 수 있는 영역 복사에는 **PrimaryServer** (IP 주소 10.0.0.1) 영역 변경 내용이 적용 됩니다. 일반 영역 보조 서버에 전송 보조 서버는 항상 최신 영역에서 PrimaryServer에 새 변경 사항으로입니다.
  
다음 그림에서는이 시나리오를 보여 줍니다.
  
![주 보조 지리적 위치 기반 교통 관리 예](../../media/Dns-Policy_PS1/dns_policy_primarysecondary1.jpg)  
   
## <a name="bkmk_works"></a>DNS 주 보조 시스템의 작동 방식

주 보조 DNS 배포 지리적 위치를 기반으로 교통 관리를 배포 하는 경우에 어떻게 보통 주 보조 영역 전송은 영역 범위 수준 전송에 대해 알아보고 하기 전에 알아야 합니다. 다음 섹션 및 정보를 제공 영역 영역 범위 수준 전송 합니다.  
  
- [DNS 주 보조 배포에서 영역 전송](#bkmk_zone)  
- [DNS 주 보조 배포에서 영역 범위 수준 전송](#bkmk_scope)  
  
### <a name="bkmk_zone"></a>DNS 주 보조 배포에서 영역 전송

DNS 주 보조 배포 만들고 영역 다음 단계를 동기화 할 수 있습니다.  
1. DNS 설치할 때 주 영역 주 DNS 서버에 만들어집니다.  
2. 보조 서버의 영역 만들고 주 서버를 지정 합니다.   
3. 기본 서버의 보조 서버 주요 영역에서 신뢰할 수 있는 보조도 추가할 수 있습니다.   
4. 보조 영역 전체 영역 transfer (횟수)를 요청 영역의 복사본을 수신 합니다.   
5. 필요에 따라 기본 서버 알림 영역 업데이트에 대 한 보조 서버에 보냅니다.  
6. 보조 서버 증분 영역 전송 요청 (횟수)를 확인합니다. 이 인해 보조 서버 남아 주 서버와 동기화 합니다.   
  
### <a name="bkmk_scope"></a>DNS 주 보조 배포에서 영역 범위 수준 전송

교통 관리 시나리오 영역 서로 다른 영역 범위가으로 분할 하려면 추가 단계 필요 합니다. 이 인해 추가 단계는 영역 범위 내 데이터 보조 서버에 전송 하 고 정책 및 DNS 클라이언트 서브넷 보조 서버에 전송 합니다.   
  
서버 기본 및 보조 DNS 인프라를 구성 하 고 나면 영역 범위 수준 전송 DNS, 다음과 같은 프로세스를 사용 하 여 자동으로 수행 됩니다.  
  
영역 범위 수준 전송 있도록 DNS 서버 OPT RR DNS (EDNS0)에 대 한 확장 메커니즘을 사용 합니다. 모든 영역 (횟수 또는 횟수) 전송 요청 범위가 영역에서는 EDNS0 OPT RR, 옵션 ID "65433"에 기본적으로 설정 되어 있는 시작 됩니다. EDNSO에 대 한 자세한 내용은 참조 IETF [메모 6891에 대 한 요청](https://tools.ietf.org/html/rfc6891)합니다.  
  
옵트아웃 (opt) RR 값 요청을 보내기 영역 범위 이름입니다. 주 DNS 서버 신뢰할 수 있는 보조 서버에서이 패킷 받으면 해당 영역 범위에 대 한 앞으로 해석 합니다.   
  
주 서버 해당 영역 범위에 있으면 응답 데이터 전송 (XFR)와 범위. 응답에 "65433" 같은 옵션 ID 가진 RR 옵트아웃 (opt)와 동일한 영역 범위로 설정 값 포함 되어 있습니다. 보조 서버가이 응답, 응답을에서 범위 정보 검색 검색 하 고 업데이트 해당 영역의 범위.  
  
이 과정 주 서버 이러한 영역 범위 요청에 알림에 대해 전송 신뢰할 수 있는 보조 목록을 유지 관리 합니다.   
  
추가 업데이트용 영역 범위에 있는 횟수 알림이와 같은 OPT RR 보조 서버에 전송 됩니다. 해당 알림이 수신 영역 범위 하면 해당 OPT RR 있는 횟수 요청 하 고 동일한 프로세스 위에서 설명한 대로입니다.  
  
## <a name="bkmk_config"></a>DNS 정책 주 보조 지리적 위치를 기반 교통 관리에 대 한 구성 하는 방법

시작 하기 전에 모든 항목의 단계를 완료 했습니다 있는지 확인 [기본 서버와 지리적 위치를 기반 교통 관리에 대 한 사용 하 여 DNS 정책을](../../dns/deploy/Scenario--Use-DNS-Policy-for-Geo-Location-Based-Traffic-Management-with-Primary-Servers.md), 주 DNS 서버, 영역 범위가, DNS 클라이언트 서브넷 영역과 DNS 정책으로 구성 하 고 있습니다.  
  
>[!NOTE]
> DNS 클라이언트 서브넷, 복사 영역 범위가 DNS 정책 기본 DNS 서버 로부터 보조 DNS 서버를 지침이이 항목에는 초기 DNS 설치 및 유효성 검사 합니다. 나중에 다음 DNS 클라이언트 서브넷, 영역 범위가 주 서버에서 정책 설정을 변경 하는 것이 좋습니다. 이 경우 기본 서버와 동기화 보조 서버 유지 하려면 자동화 스크립트 만들 수 있습니다.  
  
DNS 정책을 주 보조 지리적 위치를 기반 쿼리 응답에 대 한 구성 하려면 다음 단계를 수행 해야 합니다.  
  
- [보조 영역 만들기](#bkmk_secondary)  
- [주 영역에서 영역 전송 설정 구성](#bkmk_zonexfer)  
- [DNS 클라이언트 서브넷 복사](#bkmk_client)  
- [보조 서버의 영역 범위가 만들기](#bkmk_zonescopes)  
- [DNS 정책을 구성합니다](#bkmk_dnspolicy)  
  
다음 섹션 자세한 구성 지침을 제공 합니다.  
  
>[!IMPORTANT]
>다음 섹션에 대 한 많은 매개 예 값 포함 된 예제 Windows PowerShell 명령 포함 됩니다. 다음이 명령을 실행 하기 전에 배포에 대 한 적절 한 값으로 들어 값이 명령에서를 교체 해야 합니다.  
><br>회원 **DnsAdmins**, 다음 절차를 수행 하는 데 필요한는 오른쪽 단추를 클릭 합니다.  
  
### <a name="bkmk_secondary"></a>보조 영역 만들기

SecondaryServer1 SecondaryServer2을 복제할 영역의 보조 복사본을 만들 수 있습니다 (cmdlet 것으로 간주 되 고에서 실행 되는 원격으로 단일 관리 하는 클라이언트).   
  
예를 들어 SecondaryServer1 및 SecondarySesrver2 www.woodgrove.com의 보조 복사본을 만들 수 있습니다.  
  
보조 영역을 만들 수는 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.  
  
    
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer1  
      
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer2  
      

자세한 내용은 참조 [추가 DnsServerSecondaryZone](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserversecondaryzone?view=win10-ps)합니다.  
  
### <a name="bkmk_zonexfer"></a>주 영역에서 영역 전송 설정 구성

주 영역 설정을 구성 해야 되도록 합니다.

1. 영역을 지정된 보조 서버 주 서버에서 전송할 수 있습니다.  
2. 영역 업데이트 알림이 주 서버 보조 서버에 전송 됩니다.  
  
주 영역에 영역 전송 설정을 구성 하는 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.
  
>[!NOTE]
>다음 예제 명령 매개 **-알림** 지정 주 서버 업데이트에 대 한 알림을 선택 하 고 보조 목록에는 보냅니다.  
  
    
    Set-DnsServerPrimaryZone -Name "woodgrove.com" -Notify Notify -SecondaryServers "10.0.0.2,10.0.0.3" -SecureSecondaries TransferToSecureServers -ComputerName PrimaryServer  
     
  
자세한 내용은 참조 [설정 DnsServerPrimaryZone](https://https://docs.microsoft.com/powershell/module/dnsserver/set-dnsserverprimaryzone?view=win10-ps)합니다.  
  
  
### <a name="bkmk_client"></a>DNS 클라이언트 서브넷 복사

DNS 클라이언트 서브넷 보조 서버에 주 서버에서 복사 해야 합니다.
  
서브넷 보조 서버에 복사 하려면 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.
  
    
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer1  
      
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer2  
      

자세한 내용은 참조 [추가 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)합니다.  
  
### <a name="bkmk_zonescopes"></a>보조 서버의 영역 범위가 만들기

보조 서버 영역 범위가 만들어야 합니다. DNS에 영역 범위가 XFRs 주 서버에서에 요청를 시작할 수도 있습니다. 주 서버의 영역 범위가에서 어떤 변경 영역 범위 정보가 포함 된 알림이 보조 서버로 전송 됩니다. 보조 서버 해당 영역 범위가 증가 변경으로 업데이트할 수 있습니다.  
  
보조 서버 영역 범위를 만들 수는 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.  
  
    
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer1 -ErrorAction Ignore  
      
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer2 -ErrorAction Ignore  
  

>[!NOTE]
>이러한 예 명령을 **-ErrorAction 무시** 매개 기본 영역 범위 각 영역에 존재 하기 때문에 포함 되어 있습니다. 기본 영역 범위 생성 하거나 삭제할 수 없습니다. 이 범위를 만들려면 시도 하면 파이프라인 및 되지 것입니다. 또는 기본 영역 범위가 보조 두 가지 영역에 만들 수 있습니다.  
  
자세한 내용은 참조 [추가 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)합니다.  
  
### <a name="bkmk_dnspolicy"></a>DNS 정책을 구성합니다

기록 파티션 (영역 범위가) 및 사용자를 추가 서브넷 만든 후 쿼리에 응답 올바른 영역 범위에서 반환 되는 쿼리 DNS 클라이언트 서브넷 중 하나에 소스에서 상태가 되 면 되도록 서브넷 및 파티션, 연결 하는 정책을 만들어야 합니다. 정책이 영역 기본 범위 매핑 필요 합니다.  
  
DNS 클라이언트 서브넷 연결 되 고 영역 범위가 DNS 정책을 만들려면 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.   
    
    $policy = Get-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName PrimaryServer  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer1  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer2  
      

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다.  
  
이제 보조 DNS 서버를 리디렉션하여 교통 지리적 위치에 따라 필요한 DNS 정책으로 구성 됩니다.  
  
DNS 서버 이름 확인 쿼리 받으면 DNS 서버 평가 필드에서 구성 된 DNS 정책에 대 한 DNS 요청 합니다. 이름 해상도 요청에서 원본 IP 주소와 일치 하는 정책, 관련된 영역 범위 쿼리에 응답 하는 데 사용 되 고에서 리소스에 지리적 가까운 사용자가 이동 합니다.   
  
관리 요구 사항에 교통에 따라 DNS 정책 수천을 만들 수 있습니다 고-들어오는 쿼리에서 DNS 서버를 다시 시작 하지 않고 모든 새로운 정책 동적-적용 됩니다.
