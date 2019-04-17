---
title: DNS 정책에 대 한 사용 하 여 Split-Brain DNS 배포
description: 이 항목은 Windows Server 2016 용 DNS 정책 시나리오 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: a255a4a5-c1a0-4edc-b41a-211bae397e3c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0b25ac752ea347f4d184628eb26bc7e297443306
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-split-brain-dns-deployment"></a>DNS 정책을 Split\ 두뇌 DNS 배포를 위해 사용 하 여

>Windows Server 2016 적용 됩니다.

이 항목을 사용 하 여 Windows Server에서 DNS 정책을 구성 하는 방법을 알아보세요&reg; 2016 split-brain DNS 배포 하는 경우 단일 버전을 두 가지 경우 영역-조직 인트라넷 내부 사용자 및 외부 사용자, 사용자가 인터넷에는 일반적으로 대 한 합니다.

>[!NOTE]
>DNS 정책 Active directory split\ 두뇌 DNS 배포 통합 DNS 영역에 대 한 사용 하는 방법에 대 한 정보를 참조 하세요. [DNS 정책에 대 한 사용 Split-Brain Active Directory에 DNS](dns-sb-with-ad.md)합니다.

이전에이 시나리오 DNS 관리자 유지 서로 다른 두 DNS 서버, 서비스 각 사용자 내부 및 외부의 각 세트를 제공 하는 데 필요 합니다. 경우에 영역 내 몇 가지 기록 split\ brained 했거나 같은 부모 도메인에 위임 된 두 개 (내부 및 외부) 영역을 관리 문제 알게 되었습니다. 

다른 구성 split-brain 배포를 위해 상황은 선택적 순환 제어 DNS 이름 확인 합니다. 어떤 경우에도 정식 이름 서버 외부 사용자를 위한 역할을 하 고 해야 재귀 차단 하는 동안 내부 사용자에 대해 인터넷을 통해 반복 확인을 수행 하기 Enterprise DNS 서버 예상 됩니다. 

이 항목 다음 섹션에 포함 되어 있습니다.

- [DNS의 예 Split-Brain 배포](#bkmk_sbexample)
- [예 DNS 선택적 순환 제어](#bkmk_recursion)

##<a name="bkmk_sbexample"></a>DNS의 예 Split-Brain 배포
다음은 DNS 정책을 사용 하 여 split-brain dns 앞에서 설명한 시나리오를 수행 하는 방법을의 예입니다.

이 섹션 다음과 같은 항목이 포함 되어 있습니다.

- [어떻게 DNS Split-Brain 배포 작동](#bkmk_sbhow)
- [DNS 구성 하는 방법 Split-Brain 배포](#bkmk_sbconfigure)


이 이때 가상 회사, Contoso www.career.contoso.com에 경력 웹 사이트를 유지 하는 사용 합니다.

사이트에 게시 내부 업무를 사용할 수 있는 내부 사용자에 대 한 두 버전 합니다. 내부이 사이트는 10.0.0.39 로컬 IP 주소에서 확인할 수 있습니다. 

두 번째 버전 65.55.39.10 공개 IP 주소에서 사용할 수 있는 같은 사이트의 공개 버전이입니다.

DNS 정책 없는 경우, 관리자가이 두 영역 별도 Windows Server DNS 서버에서 개최 된을 개별적으로 관리 필요 합니다. 

DNS 정책을 사용 하 여 해당이 영역 이제에서 호스트할 수 있습니다 같은 DNS 서버 합니다.  

다음 그림에서는이 시나리오를 보여 줍니다.

![Split-Brain DNS 배포](../../media/DNS-Split-Brain/Dns-Split-Brain-01.jpg)  


##<a name="bkmk_sbhow"></a>어떻게 DNS Split-Brain 배포 작동

필요한 DNS 정책을 사용 하 여 DNS 서버 구성한 경우 각 이름 확인 요청 DNS 서버에 대 한 정책은 평가 됩니다.

서버 인터페이스 내부 및 외부 클라이언트를 구분 하기 위해이 예제 기준으로 사용 됩니다.

쿼리 시는 수신 하는 서버 인터페이스 정책 맞으면 관련된 영역 범위 쿼리에 응답 하는 데 사용 됩니다. 

따라서 내부 IP 주소, 포함 된 DNS 응답이 표시 개인 IP (10.0.0.56)에서 수신 하는 www.career.contoso.com에 대 한 DNS 쿼리에 예에서 하 고는 공개 네트워크 인터페이스 수신 DNS 쿼리에 (이것이 일반 쿼리 해상도과 동일) 기본 영역 범위에 공개 IP 주소를 포함 하는 DNS 응답을 받습니다.  

##<a name="bkmk_sbconfigure"></a>DNS 구성 하는 방법 Split-Brain 배포
DNS 구성 Split-Brain 배포 DNS 정책을 사용 하 여 다음 단계를 사용 해야 합니다.

- [영역 범위가 만들기](#bkmk_zscopes)  
- [레코드 영역 범위에 추가](#bkmk_records)  
- [DNS 정책 만들기](#bkmk_policies)

다음 섹션 자세한 구성 지침을 제공 합니다.

>[!IMPORTANT]
>다음 섹션에 대 한 많은 매개 예 값 포함 된 예제 Windows PowerShell 명령 포함 됩니다. 다음이 명령을 실행 하기 전에 배포에 대 한 적절 한 값으로 들어 값이 명령에서를 교체 해야 합니다. 

###<a name="bkmk_zscopes"></a>영역 범위가 만들기

영역 범위 영역의 고유한 인스턴스입니다. DNS 영역 고유한 DNS 레코드에 포함 된 각 영역 범위와의 여러 영역 범위에 있을 수 있습니다. 동일한 기록 IP 주소가 서로 다른 여러 범위 또는 동일한 IP 주소에서 사용할 수 있습니다. 

>[!NOTE]
>기본적으로 영역 범위 DNS 영역에 있습니다. 해당 영역 같은 이름이이 영역 범위 및이 범위 레거시 DNS 작업 작업 합니다. 이 기본 영역 범위 www.career.contoso.com의 외부 버전을 운영할 예정입니다.

영역 범위 내부 영역 범위를 만들려면 contoso.com 분할 명령은 사용할 수 있습니다. 내부 영역 범위 www.career.contoso.com의 내부 버전을 유지 하려면 사용 됩니다.

`Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "internal"`

자세한 내용은 참조 [DnsServerZoneScope 추가](https://technet.microsoft.com/library/mt126267.aspx)

###<a name="bkmk_records"></a>레코드 영역 범위에 추가

다음 단계를 나타내는 웹 서버 호스트 내부 두 영역 범위-로 및 기본 (외부 클라이언트) 레코드가 추가 하는 것입니다. 

기록 내부 영역 범위 내에 **www.career.contoso.com** 개인 IP;는 IP 주소, 10.0.0.39와 추가 기본 영역 범위 동일한 기록에서 **www.career.contoso.com**, IP 주소 65.55.39.10와 함께 추가 됩니다.

더 **– ZoneScope** 매개 변수 기록 기본 영역 범위에 추가 되 면 다음 예제 명령을에서 제공 됩니다. 기록 바닐라 영역에 추가 하는 것과 비슷합니다.

`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10"
`
`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39” -ZoneScope "internal"
`

자세한 내용은 참조 [추가 DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx)합니다.

###<a name="bkmk_policies"></a>DNS 정책 만들기

외부 네트워크 및 내부 네트워크에 대 한 서버 인터페이스 확인 한 후 영역 범위가 만든 내부 및 외부 영역 범위가 연결 DNS 정책 만들어야 합니다.

>[!NOTE]
>이 이때 내부 및 외부 클라이언트를 구분 하는 조건으로 서버 인터페이스를 사용 합니다. 다른 방법 내부 및 외부 클라이언트를 구분 하는 조건으로 서브넷 클라이언트를 사용 하 여입니다. 내부 클라이언트 속해 있는 서브넷을 식별할 수 있는 DNS 정책을 구분 클라이언트 서브넷에 따라를 구성할 수 있습니다. 클라이언트 서브넷 기준을 사용 하 여 교통 관리를 구성 하는 방법에 대 한 참고 [기본 서버와 지리적 위치를 기반 교통 관리에 대 한 사용 하 여 DNS 정책을](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/scenario--use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers)합니다.

DNS 서버 개인 인터페이스 쿼리 받으면 DNS 쿼리에 응답 내부 영역 범위에서 반환 됩니다.

>[!NOTE]
>정책이 영역 기본 범위 매핑 필요 합니다. 

다음 예제 명령에서 10.0.0.56 위의 그림 표시 된 대로 개인 네트워크 인터페이스에 IP 주소입니다.

`Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,10.0.0.56" -ZoneScope "internal,1" -ZoneName contoso.com`

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx)합니다.  


## <a name="bkmk_recursion"></a>예 DNS 선택적 순환 제어

다음은 DNS 정책을 사용 하 여 DNS 선택적 순환 제어 하는 이전에 설명 된 시나리오를 수행 하는 방법을의 예입니다.

이 섹션 다음과 같은 항목이 포함 되어 있습니다.

- [어떻게 DNS 선택적 재귀 제어 작동](#bkmk_recursionhow)
- [DNS 선택적 순환 제어 구성 하는 방법](#bkmk_recursionconfigure)

이 이때 이전 예와 Contoso www.career.contoso.com에 경력 웹 사이트를 유지 하는 동일한 가상 회사를 사용 합니다.

DNS split-brain 배포 예에서 같은 DNS 서버 응답 내부 및 외부 클라이언트 하 고 다른 답변과 제공 합니다. 

일부 DNS 배포 외부 클라이언트 역할을 정식 이름 서버 뿐만 아니라 내부 클라이언트 반복 이름을 확인을 수행 하도록 동일한 DNS 서버가 필요할 수 있습니다. 이 경우에는 DNS 선택적 순환 제어를 이라고 합니다.

이전 버전의 Windows Server에서 재귀 활성화 의미 모든 영역에 대 한 전체 DNS 서버에서 활성화 된입니다. DNS 서버 외부 쿼리를 듣는이 때문에 재귀 열려 확인자 DNS 서버를 만드는 내부 및 외부 클라이언트 활성화 됩니다. 

DNS 서버를 구성 열려 확인자 소모 리소스에 노출 될 수 있습니다 하 고 공격에 비친 풍경 만드는 악성 클라이언트가 악용 될 수 있습니다. 

이 인해 Contoso DNS 관리자 contoso.com 외부 클라이언트 반복 이름을 확인을 수행 하 여 DNS 서버를 원하지 않는 합니다. 외부 클라이언트 순환 제어 키가 차단 될 수 있는 동안에 순환 제어 내부 클라이언트에 대 한 필요성만. 

다음 그림에서는이 시나리오를 보여 줍니다.

![선택적 순환 제어](../../media/DNS-Split-Brain/Dns-Split-Brain-02.jpg) 


### <a name="bkmk_recursionhow"></a>어떻게 DNS 선택적 재귀 제어 작동

Contoso DNS 서버는 권한이 없는 쿼리 수신 하는 경우와 같이 www.microsoft.com에 대 한 다음 이름을 확인 요청은 평가 DNS 서버에 대 한 정책은 합니다. 

영역 정책을 수준 이러한 쿼리 모든 영역에서 속하지 않는 하기 때문에 \ (split-brain example\에 정의 된) 대로 평가 되지 않습니다. 

DNS 서버 재귀 정책 및 개인 인터페이스 일치 하는에 받은 쿼리 평가 하 고 **SplitBrainRecursionPolicy**합니다. 이 정책 재귀 사용 하도록 설정 재귀 범위를 가리킵니다.

그런 다음 DNS 서버는 인터넷에서 www.microsoft.com 답변 받기 반복적으로 실행 하 고 응답 로컬 캐시 합니다. 

쿼리 외부 인터페이스, DNS 정책 일치 하지 및-이 경우에 기본 재귀 설정에서 수신 하는 경우 **사용 안 함** -적용 됩니다.

이렇게 하면 내부 클라이언트 캐싱 확인자도 작동 하는 동안 역할을 외부 클라이언트 열려 확인자 서버를 않습니다. 

### <a name="bkmk_recursionconfigure"></a>DNS 선택적 순환 제어 구성 하는 방법

DNS 선택적 순환 제어를 DNS 정책을 사용 하 여 구성 하려면 다음 단계를 사용 해야 합니다.

- [DNS 재귀가 범위 만들기](#bkmk_recscopes)
- [DNS 재귀가 정책 만들기](#bkmk_recpolicy)

#### <a name="bkmk_recscopes"></a>DNS 재귀가 범위 만들기

재귀 범위는 그룹 재귀 DNS 서버를 제어 하는 설정의 고유한 인스턴스 됩니다. 재귀 범위 전달자 목록이 포함 되어 및 재귀가 사용할 수 있는지 여부를 지정 합니다. DNS 서버 많은 재귀 범위에 있을 수 있습니다. 

레거시 재귀 설정과 전달자 목록이 기본 재귀 범위 이라고 합니다. 추가 하거나 이름 점을으로 식별 기본 재귀 범위를 제거할 수 \("." \).

이 여기에서 내부 클라이언트에 대 한 새 재귀 범위를 만드는 재귀가 활성화 되어 있는 동안 기본 재귀 설정 비활성화 됩니다.

    
    Set-DnsServerRecursionScope -Name . -EnableRecursion $False
    Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True 
    

자세한 내용은 참조 [DnsServerRecursionScope 추가](https://technet.microsoft.com/library/mt126268.aspx)

#### <a name="bkmk_recpolicy"></a>DNS 재귀가 정책 만들기

특정 조건와 일치 하는 쿼리 집합에 대 한 재귀가 범위를 선택 하는 재귀가 정책을 DNS 서버를 만들 수 있습니다. 

DNS 서버를 일부 쿼리를 신뢰할 수 없는 경우 DNS 서버 재귀 정책 쿼리 해결 하는 방법을 제어할 수 있습니다. 

여기에서 사용 재귀 내부 재귀 범위 개인 네트워크 인터페이스 연관 된

DNS 재귀가 정책을 구성 하려면 명령은 사용할 수 있습니다.

    
    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainRecursionPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP  "EQ,10.0.0.39"
    

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx)합니다.

이제 DNS 서버 선택적 순환 제어 내부 클라이언트를 사용 하도록 설정 된 split-brain 이름 서버 또는 DNS 서버 필요한 DNS 정책으로 구성 됩니다.

관리 요구 사항에 교통에 따라 DNS 정책 수천을 만들 수 있습니다 고-들어오는 쿼리에서 DNS 서버를 다시 시작 하지 않고 모든 새로운 정책 동적-적용 됩니다. 

자세한 내용은 참조 [DNS 정책 시나리오 가이드](DNS-Policy-Scenario-Guide.md)합니다.
