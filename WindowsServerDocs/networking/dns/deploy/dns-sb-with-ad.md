---
title: DNS 정책에 대 한 사용 하 여 Split-Brain DNS Active Directory에
description: 교통 활용할 수 있도록이 항목을 사용할 수의 Active directory split-brain 배포용 DNS 정책 관리 기능을 통합 Windows Server 2016에 DNS 영역 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9533204-ad7e-4e49-81c1-559324a16aeb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d294fcad3b48c8698dffd93e94f6ef7ffc681ea2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-split-brain-dns-in-active-directory"></a>DNS 정책에 대 한 사용 하 여 Split-Brain DNS Active Directory에

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목을 사용 하 여 Active directory split\ 두뇌 배포 DNS 통합 된 DNS 정책 교통 관리 기능을 활용 영역 Windows Server 2016에 있습니다.

Windows Server 2016 DNS 정책 지원 Active Directory 하기 위해 확장 DNS 시간대에 통합 되어 있습니다. Active Directory 통합 DNS 서버를 multi\ 마스터 높은 가용성 기능을 제공 합니다. 

이전에이 시나리오 DNS 관리자 유지 서로 다른 두 DNS 서버, 서비스 각 사용자 내부 및 외부의 각 세트를 제공 하는 데 필요 합니다. 경우에 영역 내 몇 가지 기록 split\ brained 했거나 같은 부모 도메인에 위임 된 두 개 (내부 및 외부) 영역을 관리 문제 알게 되었습니다.

>[!NOTE]
> - DNS 배치 단일 영역의 두 버전, 회사 인트라넷과에서 사용자의 내부 버전 및 한 버전 외부 장애인 –, 일반적으로 사용자가 인터넷에 있을 때 split\ 뇌는 합니다.
> - 항목 [DNS 정책에 대 한 사용 Split-Brain DNS 배포](split-brain-DNS-deployment.md) 배포 하는 Windows Server 2016 DNS 서버에 split\ 두뇌 DNS 시스템 DNS 정책 및 영역 범위를 사용 하는 방법을 설명 합니다.



##  <a name="example-split-brain-dns-in-active-directory"></a>예제 Split\ 두뇌 DNS Active Directory에

이 이때 가상 회사, Contoso www.career.contoso.com에 경력 웹 사이트를 유지 하는 사용 합니다.

사이트에 게시 내부 업무를 사용할 수 있는 내부 사용자에 대 한 두 버전 합니다. 내부이 사이트는 10.0.0.39 로컬 IP 주소에서 확인할 수 있습니다. 

두 번째 버전 65.55.39.10 공개 IP 주소에서 사용할 수 있는 같은 사이트의 공개 버전이입니다.

DNS 정책 없는 경우, 관리자가이 두 영역 별도 Windows Server DNS 서버에서 개최 된을 개별적으로 관리 필요 합니다. 

DNS 정책을 사용 하 여 해당이 영역 이제에서 호스트할 수 있습니다 같은 DNS 서버 합니다.

DNS 서버를 contoso.com 통합, Active Directory가 두 한 네트워크 인터페이스에서 수신 하는 경우 Contoso DNS 관리자 split\ 두뇌 배포 달성 하기 위해이 항목의 단계에 따라 수 있습니다.

DNS 관리자 다음 IP 주소를 가진 DNS 서버 인터페이스를 구성합니다.

- 인터넷 향하는 네트워크 어댑터의 외부 쿼리 208.84.0.53 공용 IP 주소를으로 구성 됩니다.
- 인터넷 향하는 네트워크 어댑터의 내부 쿼리 10.0.0.56 개인 IP 주소도 구성 됩니다.

다음 그림에서는이 시나리오를 보여 줍니다.

![Split-Brain 광고는 DNS 배포 통합](../../media/DNS-SB-AD/DNS-SB-AD.jpg)

## <a name="how-dns-policy-for-split-brain-dns-in-active-directory-works"></a>DNS 정책에 대 한 Active Directory에 Split\ 두뇌 DNS의 작동 방식

필요한 DNS 정책을 사용 하 여 DNS 서버 구성한 경우 각 이름 확인 요청 DNS 서버에 대 한 정책은 평가 됩니다.

서버 인터페이스 내부 및 외부 클라이언트를 구분 하기 위해이 예제 기준으로 사용 됩니다.

쿼리 시는 수신 하는 서버 인터페이스 정책 맞으면 관련된 영역 범위 쿼리에 응답 하는 데 사용 됩니다. 

따라서 내부 IP 주소, 포함 된 DNS 응답이 표시 개인 IP (10.0.0.56)에서 수신 하는 www.career.contoso.com에 대 한 DNS 쿼리에 예에서 하 고는 공개 네트워크 인터페이스 수신 DNS 쿼리에 (이것이 일반 쿼리 해상도과 동일) 기본 영역 범위에 공개 IP 주소를 포함 하는 DNS 응답을 받습니다.  

동적 DNS \(DDNS\) 업데이트 및 청소에 대 한 지원이 영역 기본 범위만 지원 됩니다. 내부 클라이언트 기본 영역 범위에서 서비스를 때문에 Contoso DNS 관리자 (동적 DNS 또는 고정)에서 contoso.com 레코드를 업데이트 하는 기존 메커니즘을 사용 하 여 계속 수 있습니다. 영역 non\ 기본 범위가 대 한 \ (등의 외부 범위에이 example\), DDNS 또는 청소 지원을 사용할 수 없습니다.

### <a name="high-availability-of-policies"></a>정책 높은 공급 일

DNS 정책 통합 Active Directory 되지 않습니다. 이 인해 DNS 정책 같은 Active Directory 통합된 영역 호스트 하는 다른 DNS 서버를 복제 되지 않습니다. 

DNS 정책이 로컬 DNS 서버에 저장 됩니다. 다음 예제 Windows PowerShell 명령을 사용 하 여 다른 한 서버에서 DNS 정책을 내보낼 쉽게 있습니다.

    $policies = Get-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server01
    
    $policies |  Add-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server02

자세한 내용은 다음과 같은 Windows PowerShell 참조 항목을 참조 합니다.

- [Get-DnsServerQueryResolutionPolicy](https://technet.microsoft.com/itpro/powershell/windows/dns-server/get-dnsserverqueryresolutionpolicy)
- [Add-DnsServerQueryResolutionPolicy](https://technet.microsoft.com/itpro/powershell/windows/dns-server/add-dnsserverqueryresolutionpolicy)


## <a name="how-to-configure-dns-policy-for-split-brain-dns-in-active-directory"></a>DNS 정책에 대 한 Active Directory에 Split\ 두뇌 DNS 구성 하는 방법

DNS 구성 Split-Brain DNS 정책을 사용 하 여 배포를 자세한 구성 지침을 제공 하는 다음 섹션 사용 해야 합니다.

### <a name="add-the-active-directory-integrated-zone"></a>추가 된 Active Directory 통합된 영역

DNS 서버를 Active Directory 통합된 contoso.com 영역을 추가 하려면 다음 예 명령을 사용할 수 있습니다.

    Add-DnsServerPrimaryZone -Name "contoso.com" -ReplicationScope "Domain" -PassThru

자세한 내용은 참조 [추가 DnsServerPrimaryZone](https://technet.microsoft.com/library/jj649876.aspx)합니다.

### <a name="create-the-scopes-of-the-zone"></a>영역 범위 만들기

이 섹션 분할 contoso.com 외부 영역 범위를 만들려면 해당 영역에 사용할 수 있습니다.

영역 범위 영역의 고유한 인스턴스입니다. DNS 영역 고유한 DNS 레코드에 포함 된 각 영역 범위와의 여러 영역 범위에 있을 수 있습니다. 동일한 기록 IP 주소가 서로 다른 여러 범위 또는 동일한 IP 주소에서 사용할 수 있습니다. 

이 새 영역 범위 Active Directory 통합된 영역을 추가 하는 때문에 영역 범위 및 내부의 기록 도메인에 있는 다른 복제 서버 Active Directory를 통해 복제 됩니다.

기본적으로 영역 범위 모든 DNS 영역에 있습니다. 해당 영역 같은 이름이이 영역 범위 및이 범위 레거시 DNS 작업 작업 합니다. 이 기본 영역 범위 www.career.contoso.com의 내부 버전을 운영할 예정입니다.

DNS 서버에 영역 범위를 만들 수 명령은 사용할 수 있습니다.

    Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "external"

자세한 내용은 참조 [추가 DnsServerZoneScope](https://technet.microsoft.com/library/mt126267.aspx)합니다.

### <a name="add-records-to-the-zone-scopes"></a>레코드 영역 범위에 추가

다음 단계 두에는 웹 서버 호스트 나타내는 기록 범위 외부 영역 및 기본 추가 하는 \(for internal clients\) 합니다. 

기본 내부 영역 범위에 www.career.contoso.com 레코드를 10.0.0.39는 개인 IP 주소, IP 주소와 추가 고 외부 영역 범위 동일한 녹화 \(www.career.contoso.com\) 65.55.39.10 공용 IP 주소와 추가 됩니다. 

레코드 \ (기본 내부 영역 범위 및 외부 영역 scope\ 둘 다)을 자동으로 복제 자녀가 해당 영역 범위가 된 도메인.

DNS 서버에서 영역 범위에 레코드를 추가 하려면 다음 예 명령을 사용할 수 있습니다.

    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10" -ZoneScope "external"
    
    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39”

>[!NOTE]
>**– ZoneScope** 기록 기본 영역 범위에 추가 되 면 매개가 포함 되지 않습니다. 이 작업은 레코드 표준 시간대를 추가 하는 것과 동일한 합니다.

자세한 내용은 참조 [추가 DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx)합니다.

### <a name="create-the-dns-policies"></a>DNS 정책 만들기

외부 네트워크 및 내부 네트워크에 대 한 서버 인터페이스 확인 한 후 영역 범위가 만든 내부 및 외부 영역 범위가 연결 DNS 정책 만들어야 합니다.

>[!NOTE]
>사용 하 여 서버 인터페이스가이 예제 \ (예 명령 below\-ServerInterface 매개) 내부 및 외부 클라이언트를 구분을 기준으로 합니다. 다른 방법 내부 및 외부 클라이언트를 구분 하는 조건으로 서브넷 클라이언트를 사용 하 여입니다. 내부 클라이언트 속해 있는 서브넷을 식별할 수 있는 DNS 정책을 구분 클라이언트 서브넷에 따라를 구성할 수 있습니다. 클라이언트 서브넷 기준을 사용 하 여 교통 관리를 구성 하는 방법에 대 한 참고 [기본 서버와 지리적 위치를 기반 교통 관리에 대 한 사용 하 여 DNS 정책을](primary-geo-location.md)합니다.

DNS 쿼리에 공용 인터페이스에서 수신 하는 정책, 구성 하면 대답 영역 외부 범위에서 반환 됩니다. 

>[!NOTE]
>정책이 기본 내부 영역 범위 매핑 필요 합니다. 

    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,208.84.0.53" -ZoneScope "external,1" -ZoneName contoso.com

>[!NOTE]
>208.84.0.53 공용 네트워크 인터페이스에 IP 주소입니다.

자세한 내용은 참조 [추가 DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx)합니다.

이제 통합 DNS Active directory split-brain 이름 서버에 대 한 필요한 DNS 정책을 사용 하 여 DNS 서버 구성 되어 영역 합니다.

관리 요구 사항에 교통에 따라 DNS 정책 수천을 만들 수 있습니다 고-들어오는 쿼리에서 DNS 서버를 다시 시작 하지 않고 모든 새로운 정책 동적-적용 됩니다. 
