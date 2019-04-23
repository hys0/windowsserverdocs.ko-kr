---
title: Windows PowerShell을 사용하여 DHCP 배포
description: 네트워크에 하나 이상의 서브넷에 연결 하는 IPv4 DHCP 클라이언트에 자동 IP 주소와 DHCP 옵션을 제공 하는 Windows Server 2016 IP (인터넷 프로토콜) 버전 4 DHCP 서버를 배포 하려면이 항목에서는 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 7110ad21-a33e-48d5-bb3c-129982913bc8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8a53f6293067fa0f7014e7794696cf75f7179545
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849094"
---
# <a name="deploy-dhcp-using-windows-powershell"></a>Windows PowerShell을 사용하여 DHCP 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 가이드는 IP (인터넷 프로토콜) 버전 4 배포 하려면 Windows PowerShell을 사용 하는 방법에 지침을 제공 Dynamic Host Configuration Protocol \(DHCP\) IPv4 DHCP로 IP 주소 및 DHCP를 자동으로 할당 하는 서버 옵션 네트워크에 하나 이상의 서브넷에 연결 된 클라이언트입니다.

>[!NOTE]
>TechNet 갤러리에서 Word 형식으로이 문서를 다운로드 하려면 [배포 DHCP를 사용 하 여 Windows PowerShell에서 Windows Server 2016](https://gallery.technet.microsoft.com/Deploy-DHCP-Using-Windows-246dd293)합니다.

DHCP 서버를 사용 하 여 IP를 할당할 주소 저장 관리 오버 헤드의 네트워크에 있는 모든 컴퓨터에서 모든 네트워크 어댑터에 대 한 TCP/IP v4 설정을 수동으로 구성 해야 하기 때문에 합니다. DHCP를 사용 하 여 TCP/IP v4 구성을 자동으로 수행 하는 컴퓨터 또는 다른 DHCP 클라이언트가 네트워크에 연결 되어 있습니다.

독립 실행형 서버 또는 Active Directory 도메인의 일부로 작업 그룹에 있는 DHCP 서버를 배포할 수 있습니다.

이 가이드에는 다음 섹션이 수록되어 있습니다.

- [DHCP 배포 개요](#bkmk_overview)
- [기술 개요](#bkmk_technologies)
- [DHCP 배포 계획](#bkmk_plan)
- [이 가이드를 사용 하 여 테스트 랩에서](#bkmk_lab)
- [DHCP 배포](#bkmk_deploy)
- [서버 기능 확인](#bkmk_verify)
- [DHCP 용 Windows PowerShell 명령](#bkmk_dhcpwps)
- [이 가이드에서 Windows PowerShell 명령 목록](#bkmk_list)

## <a name="bkmk_overview"></a>DHCP 배포 개요

다음 그림에서는이 가이드를 사용 하 여 배포할 수 있는 시나리오를 보여 줍니다. Active Directory 도메인에 하나 이상의 DHCP 서버를 포함 하는 시나리오입니다. 서버는 두 개의 서로 다른 서브넷에 DHCP 클라이언트에 IP 주소를 제공 하도록 구성 됩니다. 서브넷에 DHCP 전달을 사용 하도록 설정 하는 라우터로 구분 됩니다.

![DHCP 네트워크 토폴로지 개요](../../media/Core-Network-Guide/cng16_overview.jpg)

## <a name="bkmk_technologies"></a>기술 개요

다음 섹션에서는 DHCP 및 TCP/IP 한 간략 한 개요를 제공합니다.

### <a name="dhcp-overview"></a>DHCP 개요

DHCP는 호스트 IP 구성의 관리를 단순화하기 위한 IP 표준입니다. DHCP 표준은 네트워크에 있는 DHCP 지원 클라이언트의 IP 주소 및 기타 관련 구성 세부 사항의 동적 할당을 관리하는 방법으로서 DHCP 서버를 사용합니다.

DHCP를 사용 하면 DHCP 서버를 사용 하 여 컴퓨터 또는 수동으로 고정 IP 주소를 사용 하 여 모든 장치를 구성 하는 대신 로컬 네트워크에 프린터와 같은 다른 장치에 IP 주소를 동적으로 할당할 수 있습니다.

IP 주소 및 해당 관련 서브넷 마스크는 컴퓨터가 연결된 호스트 컴퓨터 및 서브넷을 모두 식별하므로 TCP/IP 네트워크의 모든 컴퓨터에는 고유한 IP 주소가 있어야 합니다. DHCP를 사용하여 DHCP 클라이언트로 구성된 모든 컴퓨터에 해당 네트워크 위치 및 서브넷에 적합한 IP 주소가 수신되도록 하고 기본 게이트웨이 및 DNS 서버와 같은 DHCP 옵션을 사용하여 DHCP 클라이언트가 네트워크에서 제대로 작동하는 데 필요한 정보를 이 클라이언트에 자동으로 제공할 수 있습니다.

IP 기반 네트워크에 대 한 DHCP 컴퓨터 구성에 포함 된 관리 작업의 양과 복잡성을 줄입니다.

### <a name="tcpip-overview"></a>TCP/IP 개요

기본적으로 모든 버전의 Windows Server 및 Windows 클라이언트 운영 체제를 자동으로 IP 주소 및 DHCP 서버에서 DHCP 옵션을 호출 하는 다른 정보를 가져오도록 구성 하는 IP 버전 4 네트워크 연결에 대 한 TCP/IP 설정을 적용 합니다. 이 인해 컴퓨터가 서버 컴퓨터 또는 정적 IP 주소를 수동으로 구성된 해야 하는 다른 장치 아니면 TCP/IP 설정을 수동으로 구성할 필요가 없습니다. 

예를 들어 것 수동으로 구성 하는 DHCP 서버의 IP 주소 및 DNS 서버 및 Active Directory Domain Services를 실행 하는 도메인 컨트롤러의 IP 주소 \(AD DS\)합니다.

Windows Server 2016의 TCP/IP는 다음과 같습니다.

-   업계 표준 네트워킹 프로토콜을 기준으로 하는 네트워킹 소프트웨어

-   Windows 기반 컴퓨터를 LAN(Local Area Network)과 WAN(Wide Area Network) 환경 모두에 연결할 수 있는, 라우트 가능한 엔터프라이즈 네트워킹 프로토콜

-   정보 공유를 목적으로 Windows 기반 컴퓨터를 상이한 시스템과 연결하기 위한 핵심 기술 및 유틸리티

-   웹 및 파일 전송 프로토콜 (FTP) 서버와 같은 글로벌 인터넷 서비스에 액세스 하기 위한 기초입니다.

-   강력하고, 확장 가능하며, 플랫폼 간 작동이 가능한 클라이언트/서버 프레임워크

TCP/IP는 Windows 기반 컴퓨터를 다음과 같은 Microsoft 시스템 및 타사 시스템에 연결하고 해당 시스템과 정보를 공유할 수 있는 기본 TCP/IP 유틸리티를 제공합니다.

- Windows Server 2016

- Windows 10

- Windows Server 2012 R2

- Windows 8.1

- Windows Server 2012

- Windows 8

- Windows Server 2008 R2

- Windows 7

- Windows Server 2008

- Windows Vista

- 인터넷 호스트

- Apple Macintosh 시스템

- IBM 메인프레임

- UNIX 및 Linux 시스템

- Open VMS 시스템

- 네트워크 프린터

- 태블릿 및 휴대폰 전화 유선된 네트워크 또는 무선 802.11 기술을 사용 하도록 설정

## <a name="bkmk_plan"></a>DHCP 배포 계획

다음은 DHCP 서버 역할을 설치 하기 전에 주요 계획 단계입니다.

### <a name="planning-dhcp-servers-and-dhcp-forwarding"></a>DHCP 서버 및 DHCP 전달 계획

DHCP 메시지는 브로드캐스트 메시지이기 때문에 라우터에 의해 서브넷 간에 전달되지 않습니다. 서브넷이 여러 개이고 각 서브넷에 대해 DHCP 서비스를 제공하려면 다음 중 하나를 수행해야 합니다.

-   각 서브넷에 DHCP 서버 설치

-   라우터가 서브넷을 가로질러 DHCP 브로드캐스트 메시지를 전달하도록 구성하고 각 서브넷당 하나씩 여러 범위를 DHCP 서버에 구성합니다.

대개의 경우 DHCP 브로드캐스트 메시지를 전달하도록 라우터를 구성하는 경우가 네트워크의 실제 세그먼트 각각에 DHCP 서버를 배포하는 경우보다 비용 효율적입니다.

### <a name="planning-ip-address-ranges"></a>IP 주소 범위 계획

각 서브넷에는 자체의 고유한 IP 주소 범위가 있어야 합니다. 이 주소 범위는 DHCP 서버에서 범위로 표현됩니다.

범위란 서브넷에서 DHCP 서비스를 사용하는 컴퓨터에 대한 IP 주소의 관리 그룹을 의미합니다. 관리자는 먼저 실제 서브넷마다 범위를 하나씩 만든 다음 범위를 사용하여 클라이언트에서 사용하는 매개 변수를 정의합니다.

범위에는 다음과 같은 속성이 있습니다.

-   DHCP 서비스 임대에 사용되는 주소를 포함하거나 제외할 IP 주소의 범위

-   지정된 IP 주소의 서브넷을 결정하는 서브넷 마스크

-   범위를 만들 때 할당되는 범위 이름

-   동적으로 할당되는 IP 주소를 받는 DHCP 클라이언트에 할당되는 임대 기간 값

-   DHCP 클라이언트에 할당하도록 구성된 모든 DHCP 범위 옵션(예: DNS 서버 IP 주소, 라우터/기본 게이트웨이 IP 주소)

-   DHCP 클라이언트가 항상 같은 IP 주소를 받도록 하기 위해 선택적으로 사용되는 예약

서버를 배포하기 전에 서브넷과 각 서브넷에 대해 사용할 IP 주소 범위를 나열합니다.

### <a name="planning-subnet-masks"></a>서브넷 마스크 계획

IP 주소 내에서 네트워크 ID와 호스트 ID는 서브넷 마스크를 사용하여 구분됩니다. 각 서브넷 마스크는 네트워크 ID를 식별하는 모두 1인 연속적인 비트 그룹과 IP 주소의 호스트 ID 부분을 식별하는 모두 0인 비트 그룹을 사용하는 32비트 숫자입니다.

예를 들어 IP 주소 131.107.16.200에 일반적으로 사용되는 서브넷 마스크는 다음의 32비트 이진 번호입니다.

```
11111111 11111111 00000000 00000000
```

이 서브넷 마스크 번호는이 IP 주소의 네트워크 ID와 호스트 ID 부분이 모두 16 비트 길이임 상태임을 나타내는 16 0 비트 뒤에 16 하나-비트입니다. 일반적으로 이 서브넷 마스크는 255.255.0.0과 같은 점으로 구분된 10진수 표기법으로 표시됩니다.

다음 표에서 인터넷 주소 클래스에 대한 서브넷 마스크를 볼 수 있습니다.

|주소 클래스|서브넷 마스크의 비트|서브넷 마스크|
|-----------------|------------------------|---------------|
|클래스 A|11111111 00000000 00000000 00000000|255.0.0.0|
|클래스 B|11111111 11111111 00000000 00000000|255.255.0.0|
|클래스 C|11111111 11111111 11111111 00000000|255.255.255.0|

DHCP에서 범위를 만들고 범위에 대한 IP 주소 범위를 입력하면 DHCP에서는 이 기본 서브넷 마스크 값을 제공합니다. 일반적으로 특별한 요구 사항이 없으며 각 IP 네트워크 세그먼트가 하나의 실제 네트워크에 해당하는 대부분의 네트워크에는 기본 서브넷 마스크 값이 적합합니다.

대개의 경우 사용자 지정된 서브넷 마스크를 사용하여 IP 서브넷 지정을 구현할 수 있습니다. IP 서브넷 지정을 사용하면 IP 주소의 기본 호스트 ID 부분을 다시 분할하여 원래 클래스 기반 네트워크 ID의 하위 분할인 서브넷을 지정할 수 있습니다.

서브넷 마스크 길이를 사용자 지정하면 실제 호스트 ID에 사용되는 비트 수를 줄일 수 있습니다.

주소 지정 및 라우팅 문제를 해결하려면 네트워크 세그먼트의 모든 TCP/IP 컴퓨터가 같은 서브넷 마스크를 사용하고 각 컴퓨터 또는 장치에 고유한 IP 주소가 있어야 합니다.

### <a name="planning-exclusion-ranges"></a>제외 범위 계획

DHCP 서버에 대해 범위를 만들면 DHCP 서버가 컴퓨터 및 기타 장치와 같은 DHCP 클라이언트에 임대되도록 허용된 모든 IP 주소를 포함하는 IP 주소 범위를 지정할 수 있습니다. 이때 DHCP 서버가 사용하는 IP 주소 범위와 동일한 범위에서 고정 IP 주소로 일부 서버 및 기타 장치를 수동으로 구성한 경우 사용자 및 DHCP 서버 둘 다가 다른 장치에 동일한 IP 주소를 할당하는, IP 주소 충돌이 발생할 수 있습니다.

이 문제를 해결하기 위해 DHCP 범위에 대해 제외 범위를 만들 수 있습니다. 제외 범위는 DHCP 서버를 사용 하 여 허용 되지 않는 범위의 IP 주소 범위 내 연속 IP 주소를 합니다. 제외 범위를 만든 경우 DHCP 서버가 해당 범위의 주소를 할당하지 않으므로 IP 주소 충돌 없이 이 주소를 수동으로 할당할 수 있습니다.

각 범위에 대한 제외 범위를 만들어 해당 IP 주소를 DHCP 서버의 배포에서 제외할 수 있습니다. 고정 IP 주소로 구성된 모든 장치를 제외해야 합니다. 제외 주소 범위에는 다른 서버, 비 DHCP 클라이언트, 디스크가 없는 워크스테이션 또는 라우팅 및 원격 액세스 및 PPP 클라이언트에 수동으로 할당한 모든 IP 주소가 포함되어야 합니다.

향후의 네트워크 확장을 고려하여 추가적인 주소로 제외 범위를 구성하는 것이 좋습니다. 다음 표에서 IP 주소 범위가 10.0.0.1-를 사용 하 여 범위에 대 한 예제 제외 범위는 10.0.0.254이 고 서브넷 마스크는 255.255.255.0입니다.

|구성 항목|예제 값|
|-----------------------|------------------|
|제외 범위 시작 IP 주소|10.0.0.1|
|제외 범위 끝 IP 주소|10.0.0.25|

### <a name="planning-tcpip-static-configuration"></a>TCP/IP 고정 구성 계획

라우터, DHCP 서버 및 DNS 서버와 같은 특정 장치는 고정 IP 주소로 구성해야 합니다. 또한 프린터와 같이 항상 같은 IP 주소를 사용하는 것이 편리한 장치도 있습니다. 각 서브넷에 대해 정적으로 구성할 장치를 나열한 다음 고정적으로 구성된 장치의 IP 주소를 DHCP 서버에서 임대하지 않도록 하기 위해 DHCP 서버에서 사용할 제외 범위를 계획합니다. 제외 범위는 DHCP 서비스 제공에서 제외되는 범위로, 범위 내의 제한된 연속 IP 주소입니다. 제외 범위에 속하는 주소는 서버가 네트워크의 DHCP 클라이언트에 제공하지 않습니다.

예를 들어 서브넷의 IP 주소 범위는 192.168.0.1부터 192.168.0.254 고정 IP 주소를 사용 하 여 구성 하려는 장치를 10 개를 192.168.0에 대 한 제외 범위를 만들면 됩니다. *x* 10 개 이상의 IP 주소를 포함 하는 범위: 192.168.0.1-192.168.0.15 합니다.

이 예제에서는 제외되는 IP 주소 중 10개를 고정 IP 주소를 가진 서버 및 기타 장치로 구성하고 나머지 5개의 주소는 향후에 추가할 수 있는 새 장치의 고정 구성을 위해 남겨둡니다. 이 제외 범위를 적용하면 DHCP 서버는 192.168.0.16부터 192.168.0.254까지의 주소 풀을 사용합니다.

다음 표에 AD DS 및 DNS에 대 한 추가 예제 구성 항목이 제공 됩니다.

|구성 항목|예제 값|
|-----------------------|------------------|
|네트워크 연결 바인딩|이더넷|
|DNS 서버 설정|DC1.corp.contoso.com|
|기본 설정 DNS 서버 IP 주소|10.0.0.2|
|범위 값<br /><br />1.  범위 이름<br />2.  시작 IP 주소<br />3.  끝 IP 주소<br />4.  서브넷 마스크<br />5.  기본 게이트웨이(옵션)<br />6.  임대 기간|1.  주 서브넷<br />2.  10.0.0.1<br />3.  10.0.0.254<br />4.  255.255.255.0<br />5.  10.0.0.1<br />6. 8 일|
|IPv6 DHCP 서버 작동 모드|사용 안 함|

## <a name="bkmk_lab"></a>이 가이드를 사용 하 여 테스트 랩에서

프로덕션 환경에 배포 하기 전에 테스트 환경에서 DHCP를 배포 하려면이 가이드를 사용할 수 있습니다. 

>[!NOTE]
>테스트 랩에서 DHCP를 배포 하지 않을 경우 섹션으로 건너뛸 수 있습니다 [DHCP 배포](#bkmk_deploy)합니다.

랩에 대 한 요구 사항을 물리적 서버나 가상 머신을 사용 하는지에 따라 달라 집니다 \(Vm\), Active Directory 도메인을 사용 하거나 독립 실행형 DHCP 서버를 배포 하는지 여부 및 합니다. 

이 가이드를 사용 하 여 DHCP 배포를 테스트 하는 데 필요한 최소 리소스를 확인 하려면 다음 정보를 사용할 수 있습니다.

### <a name="test-lab-requirements-with-vms"></a>Vm 사용 하 여 테스트 랩 요구 사항

Vm 사용 하 여 테스트 랩에서 DHCP를 배포 하려면 다음 리소스가 필요 합니다.

Hyper로 구성 된 하나의 서버가 도메인 배포 또는 독립 실행형 배포에 대 한 필요\-호스트 합니다.

**도메인 배포**

이 배포에는 하나의 물리적 서버, 하나의 가상 스위치, 두 명의 가상 서버 및 가상 클라이언트 하나 필요합니다.

물리적 서버에서 Hyper-v 관리자에서 다음 항목을 만듭니다.

1. 하나의 **내부** 가상 스위치입니다. 만들지를 **외부** 가상 스위치 때문에 경우 Hyper\-V 호스트에는 DHCP 서버를 포함 하는 서브넷, Vm 테스트 DHCP 서버에서 IP 주소를 받게 됩니다. 또한 배포 하는 테스트 DHCP 서버 IP 주소 서브넷에 있는 다른 컴퓨터에 할당할 수 있는 Hyper\-V 호스트에 설치 됩니다.
1. 내부 가상 스위치에 연결 된 Active Directory Domain Services를 사용 하 여 도메인 컨트롤러로 구성 하는 Windows Server 2016을 실행 하는 하나의 VM을 만들었습니다. 이 가이드를 일치 시키려면이 서버에 정적으로 구성 된 IP 주소를 10.0.0.2 있어야 합니다. AD DS 배포에 대 한 자세한 내용은 섹션을 참조 하세요 **DC1 배포** Windows Server 2016에서 [핵심 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01)합니다.
1. 이 가이드를 사용 하 여 DHCP 서버로 구성 하는 Windows Server 2016을 실행 하는 VM이 가상 내부로 연결 되어 하나 만든 전환 합니다. 
1. 가상 내부에 연결 된 Windows 클라이언트 운영 체제를 실행 하는 하나의 VM 생성 하는 DHCP 서버에 동적으로 할당 하는 IP 주소와 DHCP 옵션 DHCP 클라이언트에 확인을 사용할지를 전환 합니다.

**독립 실행형 DHCP 서버 배포**

이 배포에는 하나의 물리적 서버, 하나의 가상 스위치, 하나의 가상 서버 및 가상 클라이언트 하나 필요합니다.

물리적 서버에서 Hyper-v 관리자에서 다음 항목을 만듭니다.

1. 하나의 **내부** 가상 스위치입니다. 만들지를 **외부** 가상 스위치 때문에 경우 Hyper\-V 호스트에는 DHCP 서버를 포함 하는 서브넷, Vm 테스트 DHCP 서버에서 IP 주소를 받게 됩니다. 또한 배포 하는 테스트 DHCP 서버 IP 주소 서브넷에 있는 다른 컴퓨터에 할당할 수 있는 Hyper\-V 호스트에 설치 됩니다.
1. 이 가이드를 사용 하 여 DHCP 서버로 구성 하는 Windows Server 2016을 실행 하는 VM이 가상 내부로 연결 되어 하나 만든 전환 합니다.
1. 가상 내부에 연결 된 Windows 클라이언트 운영 체제를 실행 하는 하나의 VM 생성 하는 DHCP 서버에 동적으로 할당 하는 IP 주소와 DHCP 옵션 DHCP 클라이언트에 확인을 사용할지를 전환 합니다.

### <a name="test-lab-requirements-with-physical-servers"></a>물리적 서버를 사용 하 여 테스트 랩 요구 사항

물리적 서버를 사용 하 여 테스트 랩에서 DHCP를 배포 하려면 다음 리소스가 필요 합니다.

**도메인 배포**

이 배포에 하나의 허브 또는 스위치, 실제 서버 2 및 하나의 물리적 클라이언트에 필요합니다.

1. 하나의 이더넷 허브나 스위치는 이더넷 케이블을 사용 하 여 물리적 컴퓨터를 연결할 수 있습니다
1. 하나의 물리적 컴퓨터를 Active Directory Domain Services를 사용 하 여 도메인 컨트롤러로 구성 하는 Windows Server 2016을 실행 합니다. 이 가이드를 일치 시키려면이 서버에 정적으로 구성 된 IP 주소를 10.0.0.2 있어야 합니다. AD DS 배포에 대 한 자세한 내용은 섹션을 참조 하세요 **DC1 배포** Windows Server 2016에서 [핵심 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01)합니다.
1. 하나의 물리적 컴퓨터가이 가이드를 사용 하 여 DHCP 서버로 구성 하는 Windows Server 2016을 실행 합니다. 
1. DHCP 서버에 있는지 확인 하는 데 사용할 Windows 클라이언트 운영 체제를 실행 하는 하나의 물리적 컴퓨터는 동적으로 DHCP 클라이언트에 IP 주소와 DHCP 옵션 할당 됩니다.

>[!NOTE]
>하지만이 배포에 대 한 충분 한 테스트 컴퓨터가 없는 경우에이 구성은 프로덕션 환경에 대 한 권장 되지 않습니다 AD DS와 DHCP 기능에 대 한 하나의 테스트 컴퓨터를 사용할 수 있습니다.

**독립 실행형 DHCP 서버 배포**

이 배포에 하나의 허브 또는 스위치, 하나의 물리적 서버 및 하나의 물리적 클라이언트에 필요합니다.

1. 하나의 이더넷 허브나 스위치는 이더넷 케이블을 사용 하 여 물리적 컴퓨터를 연결할 수 있습니다
2. 하나의 물리적 컴퓨터가이 가이드를 사용 하 여 DHCP 서버로 구성 하는 Windows Server 2016을 실행 합니다. 
3. DHCP 서버에 있는지 확인 하는 데 사용할 Windows 클라이언트 운영 체제를 실행 하는 하나의 물리적 컴퓨터는 동적으로 DHCP 클라이언트에 IP 주소와 DHCP 옵션 할당 됩니다.


## <a name="bkmk_deploy"></a>DHCP 배포

이 섹션에서는 하나 이상의 서버에서 DHCP를 배포 하는 데 사용할 수 있는 Windows PowerShell 명령 예제를 제공 합니다. 서버에서 다음 예제에서는 명령을 실행 하기 전에 네트워크와 환경에 맞게 명령을 수정 해야 합니다. 

예를 들어, 명령은 실행 하기 전에 다음 항목에 대 한 명령에 대 한 예제 값 바꿔야 합니다.

- 컴퓨터 이름
- (서브넷당 1 범위)를 구성 하려는 각 범위에 대 한 IP 주소 범위
- 구성 하려는 각 IP 주소 범위에 대 한 서브넷 마스크
- 각 범위에 대 한 범위 이름
- 각 범위에 대 한 제외 범위
- 기본 게이트웨이, 도메인 이름 및 DNS 또는 WINS 서버와 같은 DHCP 옵션 값
- 인터페이스 이름

>[!IMPORTANT]
>검사 하 고 명령을 실행 하기 전에 사용자 환경에 대 한 모든 명령을 수정 합니다.

### <a name="where-to-install-dhcp---on-a-physical-computer-or-a-vm"></a>물리적 컴퓨터 또는 VM에서 DHCP 설치-위치?

물리적 컴퓨터 또는 가상 머신에서 DHCP 서버 역할을 설치할 수 있습니다 \(VM\) Hyper에 설치 된\-V 호스트 합니다. VM 가상 네트워크 어댑터 는Hyper-v가상스위치에연결해야VM에서DHCP를설치하는경우Hyper-v호스트가연결되는실제네트워크에서제공하는컴퓨터에IP주소할당하도록DHCP서버**외부**합니다.

자세한 내용은 섹션을 참조 하세요 **Hyper-v 관리자를 사용 하 여 가상 스위치를 만듭니다** 항목의 [가상 네트워크 만들기](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network)합니다.

### <a name="run-windows-powershell-as-an-administrator"></a>관리자 권한으로 Windows PowerShell을 실행 합니다.

관리자 권한으로 Windows PowerShell을 실행 하려면 다음 절차를 사용할 수 있습니다.

1. Windows Server 2016을 실행 하는 컴퓨터를 클릭 **시작**, Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭 합니다. 메뉴가 나타납니다. 

2. 메뉴에서 클릭 **자세한**를 클릭 하 고 **관리자 권한으로 실행**합니다. 메시지가 표시 되 면 컴퓨터에 대 한 관리자 권한이 있는 계정의 자격 증명을 입력 합니다. 로그온 하는 컴퓨터에 있는 사용자 계정 관리자 수준 계정을 인 경우 자격 증명 프롬프트를 받지 못합니다.

3. Windows PowerShell 관리자 권한으로 엽니다.

### <a name="rename-the-dhcp-server-and-configure-a-static-ip-address"></a>DHCP 서버 이름 바꾸기 및 고정 IP 주소를 구성 합니다.

아직 수행 하는 경우에 DHCP 서버 이름을 바꾸고 서버에 대 한 고정 IP 주소를 구성 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.

**고정 IP 주소를 구성 합니다.**

DHCP 서버에 고정 IP 주소를 할당 하 고 올바른 DNS 서버 IP 주소와 DHCP 서버 TCP/IP 속성을 구성 하려면 다음 명령을 사용할 수 있습니다. 이 예제의 인터페이스 이름과 IP 주소를, 컴퓨터를 구성하는 데 사용하려는 값으로 바꾸는 작업도 수행해야 합니다.

 `New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24`

 `Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2`

이러한 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [New-NetIPAddress](https://technet.microsoft.com/itpro/powershell/windows/tcpip/new-netipaddress)
- [Set-DnsClientServerAddress](https://technet.microsoft.com/itpro/powershell/windows/dns-client/set-dnsclientserveraddress)

**컴퓨터 이름 바꾸기**

솔루션 빌드 구성의 이름을 바꾸고 컴퓨터를 다시 시작 하려면 다음 명령을 사용할 수 있습니다.

`Rename-Computer -Name DHCP1`

 `Restart-Computer`

이러한 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [Rename-Computer](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/rename-computer)
- [Restart-Computer](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/restart-computer)

### <a name="join-the-computer-to-the-domain-optional"></a>컴퓨터를 도메인에 가입 \(옵션\)

Active Directory 도메인 환경에서 DHCP 서버를 설치 하는 경우에 도메인에 컴퓨터를 조인 해야 합니다. 관리자 권한으로 Windows PowerShell을 열고 도메인 NetBios 이름을 바꾼 후 다음 명령을 실행 **CORP** 환경에 적합 한 값을 사용 하 여 합니다.

    Add-Computer CORP

메시지가 표시 되 면 도메인에 컴퓨터를 가입 시킬 권한이 있는 도메인 사용자 계정의 자격 증명을 입력 합니다. 

    Restart-Computer

Add-computer 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [Add-Computer](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/add-computer)

### <a name="install-dhcp"></a>DHCP 설치

컴퓨터 다시 시작 되 면 관리자 권한으로 Windows PowerShell을 열고 후 다음 명령을 실행 하 여 DHCP를 설치 합니다.

    Install-WindowsFeature DHCP -IncludeManagementTools

이 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/server-manager/install-windowsfeature)

### <a name="create-dhcp-security-groups"></a>DHCP 보안 그룹 만들기

보안 그룹을 만들려면 네트워크 셸 실행 해야 합니다 \(netsh\) Windows PowerShell에서 명령 및 DHCP 서비스를 다시 시작 하는 새 그룹 활성화 되도록 합니다.

DHCP 서버에서 netsh 명령을 실행할 때를 **DHCP Administrators** 하 고 **DHCP Users** 보안 그룹에 만들어집니다 **로컬 사용자 및 그룹** DHCP에서 서버입니다.

    netsh dhcp add securitygroups

다음 명령은 로컬 컴퓨터의 DHCP 서비스를 다시 시작합니다.

    Restart-service dhcpserver

이러한 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [네트워크 셸 (Netsh)](../netsh/netsh.md)
- [Restart-Service](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/restart-service)

### <a name="authorize-the-dhcp-server-in-active-directory-optional"></a>Active Directory에서 DHCP 서버 권한 부여 \(옵션\)

도메인 환경에서 DHCP를 설치 하는 경우 도메인에서 작동 하는 DHCP 서버를 인증 하려면 다음 단계를 수행 해야 합니다.

>[!NOTE]
>Active Directory 도메인에 설치 되는 권한이 없는 DHCP 서버는 제대로 작동할 수 없습니다 및 IP 주소를 DHCP 클라이언트 임대 되지 않습니다. 권한이 없는 DHCP 서버 자동 비활성화를 권한이 없는 DHCP 서버 네트워크상에서 클라이언트에 잘못 된 IP 주소를 할당 하지 못하도록 하는 보안 기능입니다.

Active Directory에 권한이 부여 된 DHCP 서버 목록에 DHCP 서버를 추가 하려면 다음 명령을 사용할 수 있습니다. 

>[!NOTE]
>도메인 환경이 없는 경우이 명령을 실행 하지 마십시오.

 `Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com -IPAddress 10.0.0.3`

DHCP 서버가 Active Directory에서 권한이 있는지를 확인 하려면 다음 명령을 사용할 수 있습니다.

    Get-DhcpServerInDC

다음은 Windows PowerShell에 표시 되는 결과 예입니다.

    
        IPAddress   DnsName
        ---------   -------
        10.0.0.3    DHCP1.corp.contoso.com
    

이러한 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [Add-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverindc)
- [Get-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc)

### <a name="notify-server-manager-that-post-install-dhcp-configuration-is-complete-optional"></a>게시 하는 서버 관리자에 게 알립니다\-설치 DHCP 구성이 완료 \(옵션\)

게시를 완료 한 후\-보안 그룹을 만들고 서버 관리자 Active Directory에서 DHCP 서버 권한 부여 등의 설치 작업을 해당 게시물을 알리는 사용자 인터페이스에서 경고를 계속 표시 될 수 있습니다\- DHCP 설치 후 구성을 마법사를 사용 하 여 설치 단계를 완료 해야 합니다.

이제이 방지할 수\-불필요 한 예측과 정확 하지 않은 메시지를이 Windows PowerShell 명령을 사용 하 여 다음 레지스트리 키를 구성 하 여 서버 관리자에서 표시 합니다.

    Set-ItemProperty –Path registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12 –Name ConfigurationState –Value 2

이 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [Set-ItemProperty](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/set-itemproperty?f=255&MSPPError=-2147217396)

### <a name="set-server-level-dns-dynamic-update-configuration-settings-optional"></a>서버 수준 DNS 동적 업데이트 구성 설정을 \(옵션\)

DHCP 클라이언트 컴퓨터에 대 한 DNS 동적 업데이트를 수행 하도록 DHCP 서버를 하려는 경우이 설정을 구성 하려면 다음 명령을 실행할 수 있습니다. 이 설정을 설정 하지 않는 한 범위 수준, 서버에서 구성 되는 모든 범위는 영향 을지 것입니다 있도록 서버 수준입니다. 또한이 예제 명령은 클라이언트 이상 만료 되 면 클라이언트에 대 한 DNS 리소스 레코드를 삭제 하도록 DHCP 서버를 구성 합니다.

    Set-DhcpServerv4DnsSetting -ComputerName "DHCP1.corp.contoso.com" -DynamicUpdates "Always" -DeleteDnsRRonLeaseExpiry $True

DHCP 서버 등록 또는 DNS 서버에서 클라이언트 레코드를 등록 취소 하는 자격 증명을 구성 하려면 다음 명령을 사용할 수 있습니다. 이 예제에서는 DHCP 서버에서 자격 증명을 저장합니다. 첫 번째 명령은 **Get-credential** 만들려는 **PSCredential** 개체를 개체에 저장 합니다 **$Credential** 변수. 명령은 사용자 이름 및 암호를 묻는 메시지를 표시 합니다, 있도록 다음 DNS 서버에서 리소스 레코드를 업데이트할 수 있는 권한이 있는 계정의 자격 증명을 제공 합니다.

    
    $Credential = Get-Credential
    Set-DhcpServerDnsCredential -Credential $Credential -ComputerName "DHCP1.corp.contoso.com"
    

이러한 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [Set-DhcpServerv4DnsSetting](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4dnssetting)
- [Set-DhcpServerDnsCredential](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverdnscredential)

### <a name="configure-the-corpnet-scope"></a>Corpnet 범위 구성

DHCP 설치 완료 된 후 구성 및 Corpnet 범위 활성화 범위에 대 한 제외 범위를 만들고 DHCP 옵션 기본 게이트웨이, DNS 서버 IP 주소 및 DNS 도메인 이름 구성에 다음 명령을 사용할 수 있습니다.

    
    Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active`
    
    Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15`
    
    Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com`
    
    Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2
    

이러한 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [Add-DhcpServerv4Scope](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4scope)
- [Add-DhcpServerv4ExclusionRange](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4exclusionrange)
- [Set-DhcpServerv4OptionValue](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4optionvalue)

### <a name="configure-the-corpnet2-scope-optional"></a>Corpnet2 범위 구성 \(옵션\)

DHCP 전달이 사용 되는 라우터를 사용 하 여 첫 번째 서브넷에 연결 된 두 번째 서브넷에 있는 경우이 예제에 대 한 Corpnet2 라는 두 번째 범위를 추가 하려면 다음 명령을 사용할 수 있습니다. 이 예제에서는 또한 제외 범위 및 기본 게이트웨이 IP 주소를 구성 \(서브넷에 라우터 IP 주소\) Corpnet2 서브넷입니다.

 `Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active`

 `Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15`

 `Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com`

추가 서브넷이 DHCP 서버에서 처리 하는 경우 모든 매개 변수를 명령에 대 한 다른 값을 사용 하 여 각 서브넷에 대 한 범위를 추가 하려면이 명령을 반복할 수 있습니다.

>[!IMPORTANT]
>DHCP 메시지 전달에 대 한 DHCP 클라이언트 및 DHCP 서버 간의 모든 라우터 구성 되어 있는지 확인 합니다. DHCP 전달을 구성 하는 방법에 대 한 내용은 라우터 설명서를 참조 하세요.

## <a name="bkmk_verify"></a>서버 기능 확인

DHCP 서버 ip의 동적 할당을 DHCP 클라이언트에 제공 하는 있는지를 확인 하려면 서비스 서브넷에 다른 컴퓨터를 연결할 수 있습니다. 네트워크 어댑터를 컴퓨터의 전원 이더넷 케이블을 연결한 후 DHCP 서버에서 IP 주소를 요청 합니다. 구성을 성공적으로 사용 하 여 확인할 수 있습니다 합니다 **ipconfig /all** 명령 및 결과 검토 또는 연결 테스트를 수행 하 여 Windows 사용 하 여 브라우저 또는 파일 공유 위치를 사용 하 여 웹 리소스에 액세스 하려는 같은 탐색기 또는 다른 응용 프로그램입니다.

클라이언트는 DHCP 서버에서 IP 주소를 수신 하지 않습니다, 경우에 다음 문제 해결 단계를 수행 합니다.

1. 이더넷 케이블을 모두 컴퓨터와 이더넷 스위치, 허브 또는 라우터에 꽂혀 있는지 확인 합니다.
1. 라우터에서 DHCP 서버에서 분리 된 네트워크 세그먼트에 클라이언트 컴퓨터를 연결한 경우 라우터를 DHCP 메시지로 전달 하도록 구성 되어 있는지 확인 합니다.
1. Active Directory에서 권한이 부여 된 DHCP 서버 목록을 검색 하려면 다음 명령을 실행 하 여 DHCP 서버가 Active Directory에서 권한이 있는지 확인 합니다. [Get-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc).
1. 범위는 DHCP 콘솔을 열고 활성화 되는지를 확인 \(서버 관리자 **도구**를 **DHCP**\)합니다후오른쪽범위를검토하여서버트리를확장\-각 범위를 클릭 합니다. 나타나는 메뉴 선택 항목을 포함 하는 경우 **Activate**, 클릭 **활성화**합니다. \(메뉴 선택을 읽습니다 범위가 이미 활성화 되어 있으면 **비활성화**합니다.\) 

## <a name="bkmk_dhcpwps"></a>DHCP 용 Windows PowerShell 명령

다음 참조를 Windows Server 2016에 대 한 모든 DHCP 서버의 Windows PowerShell 명령에 대 한 명령 설명 및 구문을 제공합니다. 항목 명령와 같은 명령 시작 부분에 동사에 따라 알파벳 순서로 나열 **가져옵니다** 하거나 **설정**합니다.

>[!NOTE]
>Windows Server 2012 R2에서 Windows Server 2016 명령을 사용할 수 없습니다.

- [DhcpServer 모듈](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/index)

다음 참조를 Windows Server 2012 R2에 대 한 모든 DHCP 서버의 Windows PowerShell 명령에 대 한 명령 설명 및 구문을 제공합니다. 항목 명령와 같은 명령 시작 부분에 동사에 따라 알파벳 순서로 나열 **가져옵니다** 하거나 **설정**합니다.

>[!NOTE]
>Windows Server 2016에서 Windows Server 2012 R2 명령을 사용할 수 있습니다.

- [Windows PowerShell의 DHCP 서버 Cmdlet](https://technet.microsoft.com/library/jj590751.aspx)

## <a name="bkmk_list"></a>이 가이드에서 Windows PowerShell 명령 목록

다음은 간단한 명령 목록과이 가이드에 사용 되는 예제 값입니다.

    
    New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24
    Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2
    Rename-Computer -Name DHCP1
    Restart-Computer
    
    Add-Computer CORP
    Restart-Computer
    
    Install-WindowsFeature DHCP -IncludeManagementTools
    netsh dhcp add securitygroups
    Restart-service dhcpserver
    
    Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com -IPAddress 10.0.0.3
    Get-DhcpServerInDC
    
    Set-ItemProperty –Path registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12 –Name ConfigurationState –Value 2
    
    Set-DhcpServerv4DnsSetting -ComputerName "DHCP1.corp.contoso.com" -DynamicUpdates "Always" -DeleteDnsRRonLeaseExpiry $True
    
    $Credential = Get-Credential
    Set-DhcpServerDnsCredential -Credential $Credential -ComputerName "DHCP1.corp.contoso.com"
    
    rem At prompt, supply credential in form DOMAIN\user, password
    
    
    rem Configure scope Corpnet
    
    Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active
    
    Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15
    
    Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com
    
    Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2
    
    rem Configure scope Corpnet2
    
    Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active
    
    Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15
    
    Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com
    


