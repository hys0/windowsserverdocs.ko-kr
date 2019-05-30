---
title: 주-보조 배포를 사용한 지리적 위치 기반 트래픽 관리에 DNS 정책 사용
description: 이 항목은 DNS 정책 시나리오 가이드에 대 한 Windows Server 2016의 일부
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: a9ee7a56-f062-474f-a61c-9387ff260929
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6869ee5f39f1719a3c71025207ef9ffe740492ff
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266785"
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-secondary-deployments"></a>주-보조 배포를 사용한 지리적 위치 기반 트래픽 관리에 DNS 정책 사용

>적용 대상: Windows Server (반기 채널), Windows Server 2016

기본 및 보조 DNS 서버를 포함 하는 DNS 배포 하는 경우 지역 위치 기반 트래픽 관리에 대 한 DNS 정책을 만드는 방법에 알아보려면이 항목을 사용할 수 있습니다.  

이전 시나리오 [주 서버와 지리적 위치 기반 트래픽 관리에 대 한 DNS 정책을 사용 하 여](primary-geo-location.md), 주 DNS 서버의 지리적 위치 기반 트래픽 관리에 대 한 DNS 정책을 구성 하기 위한 지침을 제공 합니다. 그러나 인터넷 인프라에서 DNS 서버는 널리 사용 되는 주-보조 모델에서는 여기서 영역의 쓰기 가능한 복사본은 선택 하 고 안전한 주 서버에 저장 하 고 읽기 전용 복사본이 영역의 여러 보조 서버에 저장 됩니다.   
  
보조 서버는 요청 하 고 주 DNS 서버에서 영역에 새 변경 내용을 포함 하는 영역 업데이트를 받을 신뢰할 수 있는 전송 (AXFR) 및 증분 영역 전송 (IXFR) 영역 전송 프로토콜을 사용 합니다.   
  
>[!NOTE]
>AXFR에 대 한 자세한 내용은 참조는 Task Force IETF (Internet Engineering) [메모 5936에 대 한 요청](https://tools.ietf.org/rfc/rfc5936.txt)합니다. IXFR에 대 한 자세한 내용은 참조는 Task Force IETF (Internet Engineering) [메모 1995에 대 한 요청](https://tools.ietf.org/html/rfc1995)합니다.  
  
## <a name="primary-secondary-geo-location-based-traffic-management-example"></a>기본-보조 지리적 위치 기반 트래픽 관리 예제  
다음은 기본 보조 배포에서 DNS 정책을 사용 트래픽 리디렉션은 DNS 쿼리를 수행 하는 클라이언트의 실제 위치를 기반으로 하는 방법의 예입니다.  
  
이 예제에서는 두 가상의 회사-웹 및 도메인 호스팅 솔루션을 제공 하는 Contoso 클라우드 서비스 사용 및 Woodgrove 식품 서비스, 전 세계에 걸쳐 여러 도시에서 음식 배달 서비스를 제공 하 고 웹 사이트 (가) 라는 woodgrove.com 합니다.  
  
Woodgrove.com 고객 웹 사이트에서 응답성이 뛰어난 환경을 얻을 수 있도록, 하려면 Woodgrove 유럽 데이터 센터로 전송 된 유럽 클라이언트와 미국 데이터 센터에 전달 하는 미국 클라이언트 하려고 합니다. 다른 곳에 위치한 전 세계의 고객 데이터 센터 중 하나을 보낼 수 있습니다.  
  
Contoso 클라우드 서비스에서 미국 및 유럽, Contoso는 해당 식료품 woodgrove.com에 대 한 포털 주문를 호스트에서 다른 두 데이터 센터를 있습니다.  
  
두 명의 보조 서버를 포함 하는 Contoso DNS 배포: **SecondaryServer1**, IP 주소가 10.0.0.2; 및 **SecondaryServer2**, IP 주소 10.0.0.3 합니다. 이러한 보조 서버 역할을 하는 이름 서버는 두 개의 서로 다른 지역에서 유럽과 미국에 있는 SecondaryServer2에 SecondaryServer1와
  
쓰기 가능한 영역의 주 복사본에 없는 **PrimaryServer** (IP 주소 10.0.0.1) 여기서 영역 변경 합니다. 보조 서버에 일반 영역 전송 보조 서버는 항상 최신는 PrimaryServer에 영역에 새 변경 사항입니다.
  
다음 그림에서는이 시나리오를 보여 줍니다.
  
![기본-보조 지리적 위치 기반 트래픽 관리 예제](../../media/Dns-Policy_PS1/dns_policy_primarysecondary1.jpg)  
   
## <a name="how-the-dns-primary-secondary-system-works"></a>DNS 기본 보조 시스템 작동 방식

기본-보조 DNS 배포의 지리적 위치 기반 트래픽 관리를 배포할 때에 전송이 영역 범위 수준 전송 알아보기 전에 먼저 발생 하는 방법을 정상 기본 보조 영역을 이해 하는 것이 중요 합니다. 다음 섹션에서는 영역 및 영역 범위 수준 전송 정보를 제공 합니다.  
  
- [DNS 기본 보조 배포에서 영역 전송](#zone-transfers-in-a-dns-primary-secondary-deployment)  
- [DNS 기본 보조 배포에서 영역 범위 수준 전송](#zone-scope-level-transfers-in-a-dns-primary-secondary-deployment)  
  
### <a name="zone-transfers-in-a-dns-primary-secondary-deployment"></a>DNS 기본 보조 배포에서 영역 전송

DNS 기본 보조 배포를 만들고 다음 단계와 영역을 동기화 할 수 있습니다.  
1. DNS를 설치 하는 경우에 주 DNS 서버에서 주 영역이 만들어집니다.  
2. 보조 서버에서 영역을 만들 고 주 서버를 지정 합니다.   
3. 주 서버에서 주 영역에 신뢰할 수 있는 보조 복제본으로 보조 서버를 추가할 수 있습니다.   
4. 보조 영역 (AXFR) 전체 영역 전송 요청을 만들고 영역의 복사본을 수신 합니다.   
5. 필요한 경우 주 서버 영역 업데이트에 대 한 보조 서버에 알림을 보냅니다.  
6. 보조 서버 (IXFR) 증분 영역 전송 요청을 수행 합니다. 이 때문에 보조 서버를 주 서버와 동기화 해야 합니다.   
  
### <a name="zone-scope-level-transfers-in-a-dns-primary-secondary-deployment"></a>DNS 기본 보조 배포에서 전송 하는 영역 범위 수준

트래픽 관리 시나리오에는 다른 영역 범위도 영역을 분할 하는 추가 단계가 필요 합니다. 이 인해 가지 추가 단계가 보조 서버에 영역 범위 내의 데이터를 전송 하 고 보조 서버에 정책 및 DNS 클라이언트 서브넷을 전송할 필요 합니다.   
  
기본 및 보조 서버와 DNS 인프라를 구성 하 고 나면 다음 프로세스를 사용 하 여 dns 영역 범위 수준 전송은 자동으로 수행 됩니다.  
  
영역 범위 수준 전송을 위해, DNS 서버 OPT RR EDNS0 (DNS)에 대 한 확장 메커니즘을 사용 합니다. 범위의 영역에서 모든 영역 전송 (AXFR 또는 IXFR) 요청 공격이 시작 되는 EDNS0 OPT RR, 옵션 ID는 기본적으로 "65433"로 설정 됩니다. EDNSO에 대 한 자세한 내용은 IETF 참조 [메모 6891에 대 한 요청](https://tools.ietf.org/html/rfc6891)합니다.  
  
OPT RR의 값에는 요청은 전송 영역 범위 이름입니다. 주 DNS 서버를 신뢰할 수 있는 보조 서버에서이 패킷을 받으면 요청 해당 영역 범위에 대해 오는 것으로 해석 합니다.   
  
주 서버에 있는 경우 해당 영역 범위 사용 하 여 응답 데이터 전송 (XFR) 해당 범위에서. 응답에 옵션 id가 같은 "65433" OPT RR와 동일한 영역 범위를 설정 하는 값을 포함 합니다. 보조 서버가이 응답을 받게, 응답에서 범위 정보를 검색 및 영역의 해당 범위를 업데이트 합니다.  
  
이 프로세스가 완료 된 후 주 서버에 이러한 영역 범위 요청 알림에 대 한 전송 신뢰할 수 있는 보조 복제본의 목록을 유지 관리 합니다.   
  
더 이상 업데이트용 영역 범위에는 IXFR 알림이 동일한 OPT RR와 보조 서버에 전송 됩니다. 해당 알림을 수신 하는 영역 범위 선택 RR 해당 포함 된 IXFR 요청 하 고 동일한 과정은 위에서 설명한 대로 다음과 같은 합니다.  
  
## <a name="how-to-configure-dns-policy-for-primary-secondary-geo-location-based-traffic-management"></a>기본-보조 지리적 위치 기반 트래픽 관리에 대 한 DNS 정책을 구성 하는 방법

시작 하기 전에 확인 항목의 단계를 모두 완료 한 [주 서버와 지리적 위치 기반 트래픽 관리에 대 한 DNS 정책을 사용 하 여](../../dns/deploy/Scenario--Use-DNS-Policy-for-Geo-Location-Based-Traffic-Management-with-Primary-Servers.md), 주 DNS 서버 영역, 영역 범위, DNS 클라이언트 서브넷 및 DNS 정책으로 구성 되어 있습니다.  
  
>[!NOTE]
> 보조 DNS 서버를 주 DNS 서버에서 DNS 클라이언트 서브넷, 영역 범위 및 DNS 정책을 복사 하려면이 항목의 지침 초기 DNS 설정 및 유효성 검사 됩니다. 나중에 다음 DNS 클라이언트 서브넷, 영역 범위 및 주 서버에서 정책 설정을 변경 하는 것이 좋습니다. 이 경우에는 주 서버와 동기화 된 보조 서버를 유지 하는 자동화 스크립트를 만들 수 있습니다.  
  
기본-보조 지역을 기반으로 쿼리 응답에 대 한 DNS 정책을 구성 하려면 다음 단계를 수행 해야 합니다.  
  
- [보조 영역 만들기](#create-the-secondary-zones)  
- [주 영역에서 영역 전송 설정 구성](#configure-the-zone-transfer-settings-on-the-primary-zone)  
- [DNS 클라이언트 서브넷 복사](#copy-the-dns-client-subnets)  
- [보조 서버에서 영역 범위 만들기](#create-the-zone-scopes-on-the-secondary-server)  
- [DNS 정책을 구성합니다](#configure-dns-policy)  
  
다음 섹션에서는 자세한 구성 지침을 제공 합니다.  
  
>[!IMPORTANT]
>다음 섹션에서는 예제 많은 매개 변수 값이 포함 된 예제 Windows PowerShell 명령을 포함 합니다. 이러한 명령에 대 한 예제 값은 다음이 명령을 실행 하기 전에 배포에 적합 한 값으로 바꾸는 것을 확인 합니다.  
><br>멤버 자격이 **DnsAdmins**, 또는 이와 동등한 다음 절차를 수행 해야 합니다.  
  
### <a name="create-the-secondary-zones"></a>보조 영역 만들기

SecondaryServer1 및 SecondaryServer2를 복제 하는 데 사용할 영역의 보조 복사본을 만들 수 있습니다 (cmdlet 가정 하 고 실행 되는 동안 원격으로 단일 관리 클라이언트에서).   
  
예를 들어 SecondaryServer1 및 SecondarySesrver2 www.woodgrove.com의 보조 복사본을 만들 수 있습니다.  
  
다음 Windows PowerShell 명령을 사용 하 여 보조 영역을 만들 수 있습니다.  
  
    
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer1  
      
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer2  
      

자세한 내용은 참조 [추가 DnsServerSecondaryZone](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserversecondaryzone?view=win10-ps)합니다.  
  
### <a name="configure-the-zone-transfer-settings-on-the-primary-zone"></a>주 영역에서 영역 전송 설정 구성

주 영역 설정을 구성 해야 되도록 합니다.

1. 지정된 된 보조 서버를 주 서버에서 영역 전송이 허용 됩니다.  
2. 영역 업데이트 알림은 보조 서버를 주 서버로 전송 됩니다.  
  
주 영역에 영역 전송 설정을 구성 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.
  
>[!NOTE]
>다음 예제에서는 명령 매개 변수에서에서 **-알림** 주 서버에서 보조 복제본의 select 목록에 업데이트에 대 한 알림을 보내도록를 지정 합니다.  
  
    
    Set-DnsServerPrimaryZone -Name "woodgrove.com" -Notify Notify -SecondaryServers "10.0.0.2,10.0.0.3" -SecureSecondaries TransferToSecureServers -ComputerName PrimaryServer  
     
  
자세한 내용은 참조 [집합 시연할](https://docs.microsoft.com/powershell/module/dnsserver/set-dnsserverprimaryzone?view=win10-ps)합니다.  
  
  
### <a name="copy-the-dns-client-subnets"></a>DNS 클라이언트 서브넷 복사

주 서버에서 DNS 클라이언트 서브넷 보조 서버에 복사 해야 합니다.
  
보조 서버에 서브넷을 복사 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.
  
    
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer1  
      
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer2  
      

자세한 내용은 참조 [추가 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)합니다.  
  
### <a name="create-the-zone-scopes-on-the-secondary-server"></a>보조 서버에서 영역 범위를 만듭니다

보조 서버에서 영역 범위를 만들어야 합니다. DNS에서 영역 범위 XFRs 주 서버에서 요청를 시작할 수도 있습니다. 주 서버에서 영역 범위에서 변경 되 면 영역 범위 정보를 포함 하는 알림을 보조 서버로 보냅니다. 보조 서버 증분 변경 사항으로 해당 영역 범위를 업데이트할 수 있습니다.  
  
보조 서버에서 영역 범위를 만들 수는 다음 Windows PowerShell 명령을 사용할 수 있습니다.  
  
    
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer1 -ErrorAction Ignore  
      
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer2 -ErrorAction Ignore  
  

>[!NOTE]
>이러한 예제에서는 명령에는 **-ErrorAction 무시** 기본 영역 범위는 각 영역에 존재 하기 때문에 매개 변수는 포함 되어 있습니다. 기본 영역 범위를 생성 또는 삭제할 수 없습니다. 해당 범위를 만들려고 하면 파이프라인 하며 실패 합니다. 또는 두 개의 보조 영역에는 기본값이 아닌 영역 범위를 만들 수 있습니다.  
  
자세한 내용은 참조 [추가 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)합니다.  
  
### <a name="configure-dns-policy"></a>DNS 정책 구성

서브넷을 만든 후 (영역 범위), 파티션 및 사용자 레코드를 추가 했습니다, 그리고 영역의 올바른 범위 내에서 쿼리 응답의 DNS 클라이언트 서브넷 중 하나의 소스에서 쿼리 되 면 반환 되도록 서브넷과 파티션, 연결 하는 정책을 만들어야 합니다. 정책이 기본 영역 범위 매핑을 지정 해야 합니다.  
  
DNS 클라이언트 서브넷에 연결 되 고 영역 범위가 DNS 정책을 만들려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.   
    
    $policy = Get-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName PrimaryServer  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer1  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer2  
      

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다.  
  
이제 보조 DNS 서버는 지리적 위치에 따라 트래픽을 리디렉션할 수 필요한 DNS 정책을 사용 하 여 구성 됩니다.  
  
DNS 서버 이름 확인 쿼리를 받으면 DNS 서버는 구성 된 DNS 정책에 대 한 DNS 요청에 있는 필드를 평가 합니다. 이름 확인 요청에서 원본 IP 주소를 일치 하는 정책 면 관련된 영역 범위 하는 데는 쿼리에 응답 하 고 사용자 지리적으로 가장 가까운 하는 리소스에 전달 됩니다.   
  
관리 요구 사항을 트래픽이 따라 DNS 정책의 수천을 만들 수 있습니다 하 고 들어오는 쿼리-DNS 서버를 다시 시작 하지 않고 모든 새 정책-동적으로 적용 됩니다.
