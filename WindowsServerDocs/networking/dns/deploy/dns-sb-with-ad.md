---
title: Active Directory에서 스플릿 브레인 DNS에 DNS 정책 사용
description: 트래픽을 활용 하 여이 항목을 사용 하 여 Active Directory를 사용 하 여 스플릿 브레인 배포에 대 한 DNS 정책의 관리 기능은 Windows Server 2016에서 DNS 영역을 통합 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9533204-ad7e-4e49-81c1-559324a16aeb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 66931d2196b741e469cb726929f7b58985b8d0cd
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812143"
---
# <a name="use-dns-policy-for-split-brain-dns-in-active-directory"></a>Active Directory에서 스플릿 브레인 DNS에 DNS 정책 사용

>적용 대상: Windows Server (반기 채널), Windows Server 2016

분할에 대 한 DNS 정책 트래픽 관리 기능을 활용 하려면이 항목을 사용 하 여\-브레인 배포 Active Directory를 사용 하 여 Windows Server 2016에서 DNS 영역을 통합 합니다.

Windows Server 2016에서 DNS 정책을 지원 확장 되어 Active Directory 통합 DNS 영역입니다. Active Directory 통합에 다중 제공\-마스터 DNS 서버를 고가용성 기능. 

이전에이 시나리오는 DNS 관리자가 서로 다른 두 DNS 서버, 내부 및 외부 사용자가 각 집합에 각 제공 서비스를 유지 하는 데 필요 합니다. 영역 내에서 몇 가지 레코드가 된 분할만\-brained 또는 영역 (내부 및 외부)의 두 인스턴스 모두 위임 된 관리 수수께끼 알게 되었습니다이 동일한 부모 도메인에 있습니다.

> [!NOTE]
> - DNS 배포는 분할\-머리 단일 영역의 두 가지 버전, 조직 인트라넷에 내부 사용자에 대 한 버전 및 버전 – 사용자가 인터넷에서 일반적으로 외부 사용자에 대 한 경우.
> - 항목 [DNS Split-Brain 배포에 대 한 DNS 정책을 사용 하 여](split-brain-DNS-deployment.md) 분할 배포에 DNS 정책 및 영역 범위를 사용 하는 방법을 설명 합니다.\-단일 Windows Server 2016 DNS 서버의 DNS 시스템을 머리.



##  <a name="example-split-brain-dns-in-active-directory"></a>예제에서는 분할\-머리 Active Directory의 DNS

이 예제에서는 하나의 가상 회사 Contoso는 www.career.contoso.com에서 경력 웹 사이트에서 유지 관리를 사용 합니다.

사이트는 내부 작업 게시물을 사용할 수 있는 내부 사용자에 대 한 두 가지 버전이 있습니다. 이 내부 사이트 10.0.0.39 로컬 IP 주소에 제공 됩니다. 

두 번째 버전이 65.55.39.10 공용 IP 주소에서 제공 되는 동일한 사이트의 공개 버전을 보여 줍니다.

DNS 정책이 없는 경우 관리자는 별도 Windows Server DNS 서버에 이러한 두 가지 영역을 호스트 하 고 개별적으로 관리 하는 데 필요 합니다. 

DNS 정책을 사용 하 여 이러한 영역을 동일한 DNS 서버에서 호스팅될 이제 수 있습니다.

Contoso DNS 관리자에서 분할을 달성 하기 위해이 항목의 단계를 따르면 contoso.com에 대 한 DNS 서버 Active directory와 통합 하는 두 개의 네트워크 인터페이스에서 수신 대기 하는 경우\-머리 배포 합니다.

DNS 관리자는 다음 IP 주소를 사용 하 여 DNS 서버 인터페이스를 구성합니다.

- 인터넷 연결 네트워크 어댑터는 외부 쿼리에 대 한 208.84.0.53의 공용 IP 주소를 사용 하 여 구성 됩니다.
- 인터넷 연결 네트워크 어댑터는 내부 쿼리에 대 한 10.0.0.56의 개인 IP 주소를 사용 하 여 구성 됩니다.

다음 그림에서는이 시나리오를 보여 줍니다.

![AD 스플릿 브레인 DNS 배포와 통합](../../media/DNS-SB-AD/DNS-SB-AD.jpg)

## <a name="how-dns-policy-for-split-brain-dns-in-active-directory-works"></a>에 대 한 DNS 정책을 분할 하는 방법을\-머리 Active Directory의 DNS

DNS 서버를 구성 하 여 필요한 DNS 정책을 사용 하 여, 각 이름 확인 요청 DNS 서버에서 정책에 따라 평가 됩니다.

서버 인터페이스는 내부와 외부 클라이언트를 구분할 수 조건으로이 예제에서 사용 됩니다.

쿼리가 수신 되 고 있는 서버 인터페이스는 정책 중 하 나와 일치 하는 경우 관련된 영역 범위 쿼리에 응답 하도록 사용 됩니다. 

따라서; 내부 IP 주소를 포함 하는 DNS 응답 수신 프라이빗 IP (10.0.0.56)에 수신된 www.career.contoso.com에 대한 DNS 쿼리 예제 및 공용 네트워크 인터페이스에서 수신된 DNS 쿼리 (이것이 일반적인 쿼리 해상도와 동일) 기본 영역 범위에서 공용 IP 주소를 포함하는 DNS 응답을 수신합니다.  

동적 DNS에 대 한 지원을 \(DDNS\) 업데이트 및 청소 기본 영역 범위 에서만 지원 됩니다. 기본 영역 범위에서 내부 클라이언트는 서비스를 제공 하기 때문에 Contoso DNS 관리자는 (동적 DNS 또는 정적) contoso.com의 레코드를 업데이트 하려면 기존 메커니즘을 사용 하 여 계속 수 있습니다. 에 대 한 비\-기본 영역 범위 \(외부 범위에서이 예제와 같이\), DDNS 또는 고객 지원에 청소를 사용할 수 없습니다.

### <a name="high-availability-of-policies"></a>정책의 고가용성

DNS 정책이 Active Directory 통합 되지 않습니다. 이 인해 DNS 정책은 동일한 Active Directory 통합된 영역을 호스팅하는 다른 DNS 서버에 복제 되지 않습니다. 

DNS 정책은 로컬 DNS 서버에 저장 됩니다. 다음 예제에서는 Windows PowerShell 명령을 사용 하 여 다른 서버에서 DNS 정책을 내보낼 쉽게 있습니다.

    $policies = Get-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server01
    
    $policies |  Add-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server02

자세한 내용은 다음 Windows PowerShell 참조 항목을 참조 하세요.

- [Get-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/get-dnsserverqueryresolutionpolicy?view=win10-ps)
- [Add-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)


## <a name="how-to-configure-dns-policy-for-split-brain-dns-in-active-directory"></a>분할에 대 한 DNS 정책을 구성 하는 방법\-머리 Active Directory의 DNS

DNS 정책을 사용 하 여 DNS Split-Brain 배포를 구성 하려면 다음 섹션에서는 자세한 구성 지침을 제공 하는 사용 해야 합니다.

### <a name="add-the-active-directory-integrated-zone"></a>Active Directory 통합된 영역 추가

DNS 서버에 Active Directory 통합된 contoso.com 영역을 추가 하려면 다음 예제에서는 명령을 사용할 수 있습니다.

    Add-DnsServerPrimaryZone -Name "contoso.com" -ReplicationScope "Domain" -PassThru

자세한 내용은 [시연할](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverprimaryzone?view=win10-ps)합니다.

### <a name="create-the-scopes-of-the-zone"></a>영역의 범위를 만듭니다

이 섹션에서는 외부 영역 범위를 만들 영역 contoso.com 분할에 사용할 수 있습니다.

영역 범위는 영역의 고유 인스턴스입니다. DNS 영역은 자체 DNS 레코드 집합이 포함 된 각 영역 범위를 갖는 여러 영역 범위를 가질 수 있습니다. 동일한 레코드는 동일한 IP 주소 또는 IP 주소가 다른 여러 범위에 있을 수 있습니다. 

Active Directory 통합된 영역에서이 새 영역 범위를 추가 해야 하므로 영역 범위 및 내부 레코드는 도메인의 다른 복제본 서버에 Active Directory를 통해 복제 됩니다.

기본적으로 영역 범위를 모든 DNS 영역에 있습니다. 영역을 같은 이름의이 영역 범위 및 레거시 DNS 작업은이 범위에서 작동 합니다. 이 기본 영역 범위 www.career.contoso.com의 내부 버전을 호스트 합니다.

DNS 서버에서 영역 범위를 만들려면 다음 예제에서는 명령을 사용할 수 있습니다.

    Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "external"

자세한 내용은 참조 [추가 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)합니다.

### <a name="add-records-to-the-zone-scopes"></a>영역 범위에 레코드를 추가 합니다.

다음 단계는 두 가지를 웹 서버 호스트를 나타내는 레코드 범위 외부 영역 및 기본 추가할 \(내부 클라이언트에 대 한\)합니다. 

기본 내부 영역 범위에서 IP 주소, 10.0.0.39 개인 IP 주소인;를 사용 하 여 레코드 www.career.contoso.com 항목이 및 외부 영역 범위에 동일한 레코드 \(www.career.contoso.com\) 65.55.39.10 공용 IP 주소를 사용 하 여 추가 됩니다. 

레코드 \(모두 내부 기본 영역 범위 및 외부 영역 범위\) 해당 해당 영역 범위를 사용 하 여 도메인 간에 자동으로 복제 됩니다.

DNS 서버에서 영역 범위에 레코드를 추가 하려면 다음 예제에서는 명령을 사용할 수 있습니다.

    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10" -ZoneScope "external"
    
    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39”

> [!NOTE]
> 합니다 **– ZoneScope** 기본 영역 범위에 레코드가 추가 되 면 매개 변수가 포함 되지 않습니다. 이 동작은 일반 영역에 레코드를 추가 합니다. 동일 합니다.

자세한 내용은 참조 [추가 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)합니다.

### <a name="create-the-dns-policies"></a>DNS 정책 만들기

외부 네트워크와 내부 네트워크에 대 한 서버 인터페이스를 파악 한 후 영역 범위가 만든 내부 및 외부 영역 범위를 연결 하는 DNS 정책을 만들어야 합니다.

> [!NOTE]
> 이 예에서는 서버 인터페이스 \(아래 예에서는 명령에서-ServerInterface 매개 변수\) 내부 및 외부 클라이언트 간의 구분을 기준으로 합니다. 외부 및 내부 클라이언트 간에 구분 하기 위해 다른 방법은 클라이언트 서브넷을 기준으로 사용 하 여입니다. 내부 클라이언트 속한 서브넷을 찾아 DNS 클라이언트 서브넷에 따라 구분 하는 정책을 구성할 수 있습니다. 클라이언트 서브넷 조건을 사용 하 여 트래픽 관리를 구성 하는 방법에 대 한 자세한 내용은 참조 [주 서버와 지리적 위치 기반 트래픽 관리에 대 한 DNS 정책을 사용 하 여](primary-geo-location.md)합니다.

공용 인터페이스에서 DNS 쿼리를 수신할 때 정책을 구성한 후 답변 영역의 외부 범위에서 반환 됩니다. 

> [!NOTE]
> 정책이 없으면 기본 내부 영역 범위 매핑을 지정 해야 합니다. 

    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,208.84.0.53" -ZoneScope "external,1" -ZoneName contoso.com

> [!NOTE]
> 208.84.0.53는 공용 네트워크 인터페이스에 IP 주소입니다.

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)합니다.

Active Directory를 사용 하 여 스플릿 브레인 이름 서버 통합 DNS에 대 한 DNS 서버가 필요한 DNS 정책을 사용 하 여 구성 하는 이제 영역입니다.

관리 요구 사항을 트래픽이 따라 DNS 정책의 수천을 만들 수 있습니다 하 고 들어오는 쿼리-DNS 서버를 다시 시작 하지 않고 모든 새 정책-동적으로 적용 됩니다. 
