---
title: Active Directory에서 스플릿 브레인 DNS에 DNS 정책 사용
description: 이 항목을 사용 하 여 Windows Server 2016에서 Active Directory 통합 DNS 영역을 사용 하 여 분할 두뇌 배포에 대 한 DNS 정책의 트래픽 관리 기능을 활용할 수 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9533204-ad7e-4e49-81c1-559324a16aeb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1a05bdcbf6205b8be7044c92e3dcf71a6e62bed6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356032"
---
# <a name="use-dns-policy-for-split-brain-dns-in-active-directory"></a>Active Directory에서 스플릿 브레인 DNS에 DNS 정책 사용

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 Windows Server 2016에 Active Directory 통합 DNS 영역을 사용 하 여 분할\-두뇌 배포에 대 한 DNS 정책의 트래픽 관리 기능을 활용할 수 있습니다.

Windows Server 2016에서는 Active Directory 통합 DNS 영역에 대 한 DNS 정책 지원이 확장 되었습니다. Active Directory 통합은 DNS 서버에 다중\-마스터 고가용성 기능을 제공 합니다. 

이전에이 시나리오는 DNS 관리자가 서로 다른 두 DNS 서버, 내부 및 외부 사용자가 각 집합에 각 제공 서비스를 유지 하는 데 필요 합니다. 영역 내에 있는 소수의 레코드만 분할\-brained 또는 영역 인스턴스 (내부 및 외부)가 모두 동일한 부모 도메인에 위임 된 경우이는 관리 난제.

> [!NOTE]
> - DNS 배포는 두 가지 버전의 단일 영역, 조직 인트라넷의 내부 사용자에 대 한 버전, 외부 사용자 (일반적으로 인터넷 사용자)에 대 한 한 가지 버전이 있는 경우를\-합니다.
> - [분할-두뇌 Dns 배포에 대 한 Dns 정책 사용](split-brain-DNS-deployment.md) 항목에서는 dns 정책 및 영역 범위를 사용 하 여 단일 Windows SERVER 2016 dns 서버에 분할\-두뇌 dns 시스템을 배포 하는 방법을 설명 합니다.



##  <a name="example-split-brain-dns-in-active-directory"></a>예제 분할\-Active Directory에 있는 DNS

이 예제에서는 하나의 가상 회사 Contoso는 www.career.contoso.com에서 경력 웹 사이트에서 유지 관리를 사용 합니다.

사이트는 내부 작업 게시물을 사용할 수 있는 내부 사용자에 대 한 두 가지 버전이 있습니다. 이 내부 사이트 10.0.0.39 로컬 IP 주소에 제공 됩니다. 

두 번째 버전이 65.55.39.10 공용 IP 주소에서 제공 되는 동일한 사이트의 공개 버전을 보여 줍니다.

DNS 정책이 없는 경우 관리자는 별도 Windows Server DNS 서버에 이러한 두 가지 영역을 호스트 하 고 개별적으로 관리 하는 데 필요 합니다. 

DNS 정책을 사용 하 여 이러한 영역을 동일한 DNS 서버에서 호스팅될 이제 수 있습니다.

Contoso.com에 대 한 DNS 서버가 Active Directory 통합 되어 있고 두 네트워크 인터페이스에서 수신 대기 하는 경우 Contoso DNS 관리자는이 항목의 단계를 따라 분할\-두뇌 배포를 수행할 수 있습니다.

DNS 관리자는 다음 IP 주소를 사용 하 여 DNS 서버 인터페이스를 구성 합니다.

- 인터넷 연결 네트워크 어댑터는 외부 쿼리에 대해 208.84.0.53의 공용 IP 주소를 사용 하 여 구성 됩니다.
- 인트라넷 연결 네트워크 어댑터는 내부 쿼리에 대해 10.0.0.56의 개인 IP 주소를 사용 하 여 구성 됩니다.

다음 그림에서는이 시나리오를 보여 줍니다.

![분할-두뇌 AD 통합 DNS 배포](../../media/DNS-SB-AD/DNS-SB-AD.jpg)

## <a name="how-dns-policy-for-split-brain-dns-in-active-directory-works"></a>분할\-Active Directory의 dns 정책에 대 한 DNS 정책 작동 방법

DNS 서버를 구성 하 여 필요한 DNS 정책을 사용 하 여, 각 이름 확인 요청 DNS 서버에서 정책에 따라 평가 됩니다.

서버 인터페이스는 내부와 외부 클라이언트를 구분할 수 조건으로이 예제에서 사용 됩니다.

쿼리가 수신 되 고 있는 서버 인터페이스는 정책 중 하 나와 일치 하는 경우 관련된 영역 범위 쿼리에 응답 하도록 사용 됩니다. 

따라서; 내부 IP 주소를 포함 하는 DNS 응답 수신 프라이빗 IP (10.0.0.56)에 수신된 www.career.contoso.com에 대한 DNS 쿼리 예제 및 공용 네트워크 인터페이스에서 수신된 DNS 쿼리 (이것이 일반적인 쿼리 해상도와 동일) 기본 영역 범위에서 공용 IP 주소를 포함하는 DNS 응답을 수신합니다.  

동적 DNS \(DDNS\) 업데이트 및 청소는 기본 영역 범위 에서만 지원 됩니다. 내부 클라이언트는 기본 영역 범위에서 서비스 되므로 Contoso DNS 관리자는 기존 메커니즘 (동적 DNS 또는 정적)을 계속 사용 하 여 contoso.com의 레코드를 업데이트할 수 있습니다. \-기본 영역 범위 (예:이\)예제에서는 외부 범위) \(DDNS 또는 청소 지원을 사용할 수 없습니다.

### <a name="high-availability-of-policies"></a>정책의 고가용성

DNS 정책은 Active Directory 통합 되지 않습니다. 이로 인해 DNS 정책이 동일한 Active Directory 통합 영역을 호스트 하는 다른 DNS 서버에 복제 되지 않습니다. 

DNS 정책은 로컬 DNS 서버에 저장 됩니다. 다음 예제 Windows PowerShell 명령을 사용 하 여 한 서버에서 다른 서버에 DNS 정책을 쉽게 내보낼 수 있습니다.

    $policies = Get-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server01
    
    $policies |  Add-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server02

자세한 내용은 다음 Windows PowerShell 참조 항목을 참조 하세요.

- [Get-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/get-dnsserverqueryresolutionpolicy?view=win10-ps)
- [Add-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)


## <a name="how-to-configure-dns-policy-for-split-brain-dns-in-active-directory"></a>Active Directory에서\-을 분할 하는 데 필요한 DNS 정책을 구성 하는 방법

Dns 정책을 사용 하 여 DNS 분할 두뇌 배포를 구성 하려면 자세한 구성 지침을 제공 하는 다음 섹션을 사용 해야 합니다.

### <a name="add-the-active-directory-integrated-zone"></a>Active Directory 통합 영역 추가

다음 예제 명령을 사용 하 여 Active Directory 통합 contoso.com 영역을 DNS 서버에 추가할 수 있습니다.

    Add-DnsServerPrimaryZone -Name "contoso.com" -ReplicationScope "Domain" -PassThru

자세한 내용은 [시연할](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverprimaryzone?view=win10-ps)를 참조 하세요.

### <a name="create-the-scopes-of-the-zone"></a>영역의 범위를 만듭니다

이 섹션을 사용 하 여 영역 contoso.com를 분할 하 여 외부 영역 범위를 만들 수 있습니다.

영역 범위는 영역의 고유 인스턴스입니다. DNS 영역은 자체 DNS 레코드 집합이 포함 된 각 영역 범위를 갖는 여러 영역 범위를 가질 수 있습니다. 동일한 레코드는 동일한 IP 주소 또는 IP 주소가 다른 여러 범위에 있을 수 있습니다. 

Active Directory 통합 영역에이 새 영역 범위를 추가 하기 때문에 영역 범위와 그 안의 레코드는 Active Directory를 통해 도메인의 다른 복제본 서버에 복제 됩니다.

기본적으로 영역 범위는 모든 DNS 영역에 있습니다. 영역을 같은 이름의이 영역 범위 및 레거시 DNS 작업은이 범위에서 작동 합니다. 이 기본 영역 범위는 www.career.contoso.com의 내부 버전을 호스팅합니다.

다음 예제 명령을 사용 하 여 DNS 서버에 영역 범위를 만들 수 있습니다.

    Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "external"

자세한 내용은 참조 [추가 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)합니다.

### <a name="add-records-to-the-zone-scopes"></a>영역 범위에 레코드를 추가 합니다.

다음 단계는 웹 서버 호스트를 나타내는 레코드를 내부 클라이언트\)에 대 한 외부 및 기본 \(의 두 영역 범위에 추가 하는 것입니다. 

기본 내부 영역 범위에서 www.career.contoso.com 레코드는 개인 IP 주소인 IP 주소 10.0.0.39를 사용 하 여 추가 됩니다. 외부 영역 범위에서 동일한 레코드 \(www.career.contoso.com\)는 공용 IP 주소 65.55.39.10를 사용 하 여 추가 됩니다. 

\(레코드는 기본 내부 영역 범위와 외부 영역 범위\) 모두 해당 영역 범위를 사용 하 여 도메인에서 자동으로 복제 됩니다.

다음 예제 명령을 사용 하 여 DNS 서버의 영역 범위에 레코드를 추가할 수 있습니다.

    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10" -ZoneScope "external"
    
    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39”

> [!NOTE]
> **– ZoneScope** 매개 변수는 레코드가 기본 영역 범위에 추가 될 때 포함 되지 않습니다. 이 작업은 일반 영역에 레코드를 추가 하는 것과 같습니다.

자세한 내용은 참조 [추가 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)합니다.

### <a name="create-the-dns-policies"></a>DNS 정책 만들기

외부 네트워크와 내부 네트워크에 대 한 서버 인터페이스를 파악 한 후 영역 범위가 만든 내부 및 외부 영역 범위를 연결 하는 DNS 정책을 만들어야 합니다.

> [!NOTE]
> 이 예에서는 서버 \(인터페이스를 사용 하 여 아래 예제 명령의-ServerInterface 매개 변수를 사용 하 여 내부 및 외부 클라이언트를 구분 하는 조건으로\) 합니다. 외부 및 내부 클라이언트 간에 구분 하기 위해 다른 방법은 클라이언트 서브넷을 기준으로 사용 하 여입니다. 내부 클라이언트 속한 서브넷을 찾아 DNS 클라이언트 서브넷에 따라 구분 하는 정책을 구성할 수 있습니다. 클라이언트 서브넷 조건을 사용 하 여 트래픽 관리를 구성 하는 방법에 대 한 자세한 내용은 참조 [주 서버와 지리적 위치 기반 트래픽 관리에 대 한 DNS 정책을 사용 하 여](primary-geo-location.md)합니다.

정책을 구성 하 고 나면 공용 인터페이스에서 DNS 쿼리를 받을 때 영역의 외부 범위에서 응답이 반환 됩니다. 

> [!NOTE]
> 기본 내부 영역 범위 매핑을 위한 정책은 필요 하지 않습니다. 

    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,208.84.0.53" -ZoneScope "external,1" -ZoneName contoso.com

> [!NOTE]
> 208.84.0.53는 공용 네트워크 인터페이스의 IP 주소입니다.

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다.

이제 DNS 서버가 Active Directory 통합 DNS 영역을 사용 하는 분할 된 서버 이름 서버에 필요한 DNS 정책으로 구성 됩니다.

관리 요구 사항을 트래픽이 따라 DNS 정책의 수천을 만들 수 있습니다 하 고 들어오는 쿼리-DNS 서버를 다시 시작 하지 않고 모든 새 정책-동적으로 적용 됩니다. 
