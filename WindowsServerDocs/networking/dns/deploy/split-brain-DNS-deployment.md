---
title: 스플릿 브레인 DNS 배포에 DNS 정책 사용
description: 이 항목은 DNS 정책 시나리오 가이드에 대 한 Windows Server 2016의 일부
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: a255a4a5-c1a0-4edc-b41a-211bae397e3c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4ec4bc8e77e8411101b9a2b83a85ad5e1a0765b2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873504"
---
# <a name="use-dns-policy-for-split-brain-dns-deployment"></a>분할에 대 한 DNS 정책을 사용 하 여\-머리 DNS 배포

>적용 대상: Windows Server 2016

이 항목을 사용 하 여 Windows Server에서 DNS 정책을 구성 하는 방법을 알아봅니다&reg; 스플릿 브레인 DNS 배포의 경우 2016 있으면 다음 두 가지 버전의 단일 영역-인터넷에 있는 사용자는 일반적으로 외부 사용자에 대 한 조직 인트라넷에 내부 사용자에 대 한 합니다.

>[!NOTE]
>분할에 대 한 DNS 정책을 사용 하는 방법에 대 한 내용은\-브레인 DNS 배포와 Active Directory 통합 DNS 영역을 참조 하십시오 [Split-Brain DNS Active Directory에 대 한 DNS 정책을 사용 하 여](dns-sb-with-ad.md)입니다.

이전에이 시나리오는 DNS 관리자가 서로 다른 두 DNS 서버, 내부 및 외부 사용자가 각 집합에 각 제공 서비스를 유지 하는 데 필요 합니다. 영역 내에서 몇 가지 레코드가 된 분할만\-brained 또는 영역 (내부 및 외부)의 두 인스턴스 모두 위임 된 관리 수수께끼 알게 되었습니다이 동일한 부모 도메인에 있습니다. 

스플릿 브레인 배포 다른 구성 시나리오에는 DNS 이름 확인에 대 한 선택적 재귀 컨트롤입니다. 일부 환경에서는 엔터프라이즈 DNS 서버는 또한 해야, 외부 사용자에 대 한 신뢰할 수 있는 이름 서버 역할을 하 고 해당 재귀를 차단 하는 동안 내부 사용자에 대 한 인터넷을 통해 재귀 확인을 수행 해야 합니다. 

이 항목에는 다음 섹션이 수록되어 있습니다.

- [스플릿 브레인 DNS 배포의 예](#bkmk_sbexample)
- [DNS 선택적 재귀 컨트롤의 예](#bkmk_recursion)

##<a name="bkmk_sbexample"></a>스플릿 브레인 DNS 배포의 예
다음은 정책 DNS를 사용 하 여 스플릿 브레인 DNS의 앞에서 설명한 시나리오를 수행 하는 방법의 예입니다.

이 섹션에서는 다음 항목을 다룹니다.

- [스플릿 브레인 DNS 배포의 작동 원리](#bkmk_sbhow)
- [스플릿 브레인 DNS 배포를 구성 하는 방법](#bkmk_sbconfigure)


이 예제에서는 하나의 가상 회사 Contoso는 www.career.contoso.com에서 경력 웹 사이트에서 유지 관리를 사용 합니다.

사이트는 내부 작업 게시물을 사용할 수 있는 내부 사용자에 대 한 두 가지 버전이 있습니다. 이 내부 사이트 10.0.0.39 로컬 IP 주소에 제공 됩니다. 

두 번째 버전이 65.55.39.10 공용 IP 주소에서 제공 되는 동일한 사이트의 공개 버전을 보여 줍니다.

DNS 정책이 없는 경우 관리자는 별도 Windows Server DNS 서버에 이러한 두 가지 영역을 호스트 하 고 개별적으로 관리 하는 데 필요 합니다. 

DNS 정책을 사용 하 여 이러한 영역을 동일한 DNS 서버에서 호스팅될 이제 수 있습니다.  

다음 그림에서는이 시나리오를 보여 줍니다.

![스플릿 브레인 DNS 배포](../../media/DNS-Split-Brain/Dns-Split-Brain-01.jpg)  


##<a name="bkmk_sbhow"></a>스플릿 브레인 DNS 배포의 작동 원리

DNS 서버를 구성 하 여 필요한 DNS 정책을 사용 하 여, 각 이름 확인 요청 DNS 서버에서 정책에 따라 평가 됩니다.

서버 인터페이스는 내부와 외부 클라이언트를 구분할 수 조건으로이 예제에서 사용 됩니다.

쿼리가 수신 되 고 있는 서버 인터페이스는 정책 중 하 나와 일치 하는 경우 관련된 영역 범위 쿼리에 응답 하도록 사용 됩니다. 

따라서; 내부 IP 주소를 포함 하는 DNS 응답 수신 개인 IP (10.0.0.56)에 수신 된 www.career.contoso.com에 대 한 DNS 쿼리 예제 및 공용 네트워크 인터페이스에서 수신 된 DNS 쿼리 (이것이 일반적인 쿼리 해상도와 동일) 기본 영역 범위에서 공용 IP 주소를 포함 하는 DNS 응답을 수신 합니다.  

##<a name="bkmk_sbconfigure"></a>스플릿 브레인 DNS 배포를 구성 하는 방법
DNS 정책을 사용 하 여 DNS Split-Brain 배포를 구성 하려면 다음 단계를 사용 해야 합니다.

- [영역 범위 만들기](#bkmk_zscopes)  
- [영역 범위에 레코드 추가](#bkmk_records)  
- [DNS 정책 만들기](#bkmk_policies)

다음 섹션에서는 자세한 구성 지침을 제공 합니다.

>[!IMPORTANT]
>다음 섹션에서는 예제 많은 매개 변수 값이 포함 된 예제 Windows PowerShell 명령을 포함 합니다. 이러한 명령에 대 한 예제 값은 다음이 명령을 실행 하기 전에 배포에 적합 한 값으로 바꾸는 것을 확인 합니다. 

###<a name="bkmk_zscopes"></a>영역 범위 만들기

영역 범위는 영역의 고유 인스턴스입니다. DNS 영역은 자체 DNS 레코드 집합이 포함 된 각 영역 범위를 갖는 여러 영역 범위를 가질 수 있습니다. 동일한 레코드는 동일한 IP 주소 또는 IP 주소가 다른 여러 범위에 있을 수 있습니다. 

>[!NOTE]
>기본적으로 영역 범위 DNS 영역에 있습니다. 영역을 같은 이름의이 영역 범위 및 레거시 DNS 작업은이 범위에서 작동 합니다. 이 기본 영역 범위 www.career.contoso.com의 외부 버전을 호스팅합니다.

다음 예제 명령은 내부 영역 범위를 만들 영역 범위 contoso.com 분할에 사용할 수 있습니다. 내부 영역 범위 www.career.contoso.com의 내부 버전을 유지 하려면 사용 됩니다.

`Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "internal"`

자세한 내용은 참조 [DnsServerZoneScope 추가](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

###<a name="bkmk_records"></a>영역 범위에 레코드 추가

다음 단계 (외부 클라이언트)에 대 한 두 개의 영역 범위-내부로 웹 서버 호스트와 기본값을 나타내는 레코드를 추가 하는 것입니다. 

레코드는 내부 영역 범위에서 **www.career.contoso.com** 추가 됩니다 10.0.0.39 개인 IP; 인 IP 주소와 기본 영역 범위에서 동일한 레코드를 **www.career.contoso.com**, 65.55.39.10 IP 주소와 함께 추가 됩니다.

더 **– ZoneScope** 기본 영역 범위에 레코드가 추가 되는 경우 다음 예제에서는 명령에서 매개 변수를 제공 합니다. 바닐라 영역에 레코드를 추가 하는 것과 비슷합니다.

`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10"
`
`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39” -ZoneScope "internal"
`

자세한 내용은 참조 [추가 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)합니다.

###<a name="bkmk_policies"></a>DNS 정책 만들기

외부 네트워크와 내부 네트워크에 대 한 서버 인터페이스를 파악 한 후 영역 범위가 만든 내부 및 외부 영역 범위를 연결 하는 DNS 정책을 만들어야 합니다.

>[!NOTE]
>이 예제에서는 조건으로 서버 인터페이스를 사용 하 여 내부와 외부 클라이언트를 구분할 수 있습니다. 외부 및 내부 클라이언트 간에 구분 하기 위해 다른 방법은 클라이언트 서브넷을 기준으로 사용 하 여입니다. 내부 클라이언트 속한 서브넷을 찾아 DNS 클라이언트 서브넷에 따라 구분 하는 정책을 구성할 수 있습니다. 클라이언트 서브넷 조건을 사용 하 여 트래픽 관리를 구성 하는 방법에 대 한 자세한 내용은 참조 [주 서버와 지리적 위치 기반 트래픽 관리에 대 한 DNS 정책을 사용 하 여](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/scenario--use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers)합니다.

DNS 서버는 개인 인터페이스에 대 한 쿼리를 받으면 DNS 쿼리 응답은 내부 영역 범위에서 반환 됩니다.

>[!NOTE]
>정책이 기본 영역 범위 매핑을 지정 해야 합니다. 

다음 예제에서는 명령을 10.0.0.56 앞의 그림에 표시 된 것과 같이 개인 네트워크 인터페이스의 IP 주소입니다.

`Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,10.0.0.56" -ZoneScope "internal,1" -ZoneName contoso.com`

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다.  


## <a name="bkmk_recursion"></a>DNS 선택적 재귀 컨트롤의 예

다음은 정책 DNS를 사용 하 여 DNS 선택적 재귀 컨트롤의 앞에서 설명한 시나리오를 수행 하는 방법의 예입니다.

이 섹션에서는 다음 항목을 다룹니다.

- [어떻게 DNS 선택적 재귀 제어는](#bkmk_recursionhow)
- [DNS 선택적 재귀 제어를 구성 하는 방법](#bkmk_recursionconfigure)

이 예제에서는 Contoso www.career.contoso.com에서 경력 웹 사이트를 유지 관리 하는 이전 예와 같은 가상의 회사를 사용 합니다.

DNS 스플릿 브레인 배포 예제 동일한 DNS 서버는 외부 및 내부 클라이언트에 응답 하 고 다른 클라이언트에 제공 합니다. 

일부 DNS 배포 외부 클라이언트에 대 한 신뢰할 수 있는 이름 서버로 작동 하는 것 외에도 내부 클라이언트에 대 한 재귀적 이름 확인을 수행 하는 동일한 DNS 서버가 필요할 수 있습니다. 이 경우에는 DNS 선택적 재귀 제어를 라고 합니다.

Windows Server의 이전 버전에서는 재귀를 사용 하도록 설정 의미 모든 영역에 대 한 전체 DNS 서버에 설정 된 것입니다. DNS 서버를 외부 쿼리도 수신 하므로 재귀 DNS 서버 열기 해결 프로그램을 만드는 내부 및 외부 클라이언트에 대해 활성화 됩니다. 

DNS 서버 열려 해결 프로그램 리소스 소모에 취약할 수 및 악의적인 클라이언트 반사 공격에 악용할 수로 구성 된입니다. 

이 때문에 Contoso DNS 관리자는 외부 클라이언트에 대 한 재귀적 이름 확인을 수행 하는 contoso.com에 대 한 DNS 서버를 원하지 않습니다. 외부 클라이언트에 대 한 순환 제어 차단 될 수 있지만 내부 클라이언트에 대 한 재귀 컨트롤에 대 한 요구에만 있습니다. 

다음 그림에서는이 시나리오를 보여 줍니다.

![선택적 순환 제어](../../media/DNS-Split-Brain/Dns-Split-Brain-02.jpg) 


### <a name="bkmk_recursionhow"></a>어떻게 DNS 선택적 재귀 제어는

Contoso DNS 서버는 신뢰할 수 없는 쿼리를 받은 경우와 같은 www.microsoft.com에 대 한 다음 이름 확인 요청은 평가 DNS 서버에서 정책에 따라 합니다. 

영역 수준 정책 하므로 이러한 쿼리는 모든 영역에서 속하지 않는, \(스플릿 브레인이 예제에 정의 된 대로\) 평가 되지 않습니다. 

DNS 서버는 재귀 정책과 일치 하는 개인 인터페이스에 수신 되는 쿼리를 평가 **SplitBrainRecursionPolicy**합니다. 이 정책은 재귀를 사용할 수는 재귀 범위를 가리킵니다.

그런 다음 DNS 서버는 인터넷을 통해 www.microsoft.com에 대 한 답변을 받을를 반복적으로 실행 하 고 로컬에서 응답을 캐시할. 

외부 인터페이스, DNS 정책 일치 및 재귀 기본값-이 경우에 쿼리를 받은 경우 **비활성화** -적용 됩니다.

이 서버에서 내부 클라이언트에 대 한 캐싱 확인자로 작동 하는 동안 역할 외부의 클라이언트에 대 한 열린 해결 프로그램을 방지 합니다. 

### <a name="bkmk_recursionconfigure"></a>DNS 선택적 재귀 제어를 구성 하는 방법

DNS 정책을 사용 하 여 DNS 선택적 순환 제어를 구성 하려면 다음 단계를 사용 해야 합니다.

- [DNS 재귀 범위 만들기](#bkmk_recscopes)
- [DNS 재귀 정책 만들기](#bkmk_recpolicy)

#### <a name="bkmk_recscopes"></a>DNS 재귀 범위 만들기

재귀 범위는 DNS 서버에서 재귀를 제어 하는 설정 그룹의 고유 인스턴스입니다. 재귀 범위 전달자의 목록을 포함 하 고 재귀 사용 되는지 여부를 지정 합니다. DNS 서버는 여러 재귀 범위를 가질 수 있습니다. 

레거시 재귀 설정과 전달자 목록 기본 재귀 범위 라고 합니다. 추가 하거나 이름에 점이 식별 된 기본 재귀 범위를 제거할 수 \("."\)합니다.

이 예제에서는 재귀 설정 되는 내부 클라이언트에 대 한 새 재귀 범위를 만드는 동안 기본 재귀 설정을 비활성화 됩니다.

    
    Set-DnsServerRecursionScope -Name . -EnableRecursion $False
    Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True 
    

자세한 내용은 참조 [DnsServerRecursionScope 추가](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverrecursionscope?view=win10-ps)

#### <a name="bkmk_recpolicy"></a>DNS 재귀 정책 만들기

특정 조건에 일치 하는 쿼리 집합에 대 한 재귀 범위를 선택 하는 재귀 정책을 DNS 서버를 만들 수 있습니다. 

DNS 서버에 일부 쿼리에 대 한 권한이 없는 경우 DNS 서버 재귀 정책 쿼리를 해결 하는 방법을 제어할 수 있도록 메시지를 표시 합니다. 

이 예제에서 사용 하도록 설정 하는 재귀 내부 재귀 범위는 개인 네트워크 인터페이스를 사용 하 여 연결 됩니다.

DNS 재귀 정책을 구성 하려면 다음 예제에서는 명령을 사용할 수 있습니다.

    
    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainRecursionPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP "EQ,10.0.0.39"
    

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다.

이제 내부 클라이언트에 대해 사용 하도록 설정 하는 선택적 재귀 컨트롤과 스플릿 브레인 이름 서버 또는 DNS 서버에 대 한 필요한 DNS 정책을 사용 하 여 DNS 서버가 구성 됩니다.

관리 요구 사항을 트래픽이 따라 DNS 정책의 수천을 만들 수 있습니다 하 고 들어오는 쿼리-DNS 서버를 다시 시작 하지 않고 모든 새 정책-동적으로 적용 됩니다. 

자세한 내용은 [DNS 정책 시나리오 가이드](DNS-Policy-Scenario-Guide.md)합니다.
