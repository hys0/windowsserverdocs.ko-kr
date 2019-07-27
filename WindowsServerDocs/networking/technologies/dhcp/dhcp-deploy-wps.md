---
title: Windows PowerShell을 사용하여 DHCP 배포
description: 이 항목을 사용 하 여 네트워크에 있는 하나 이상의 서브넷에 연결 된 IPv4 DHCP 클라이언트에 자동 IP 주소 및 DHCP 옵션을 제공 하는 Windows Server 2016 인터넷 프로토콜 (IP) 버전 4 DHCP 서버를 배포할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 7110ad21-a33e-48d5-bb3c-129982913bc8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c02de23f285106ebee7fd6c78e4cf012437d616e
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544657"
---
# <a name="deploy-dhcp-using-windows-powershell"></a>Windows PowerShell을 사용하여 DHCP 배포

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 가이드에서는 Windows PowerShell을 사용 하 여 ip (인터넷 프로토콜) 버전 4 동적 호스트 구성 프로토콜 \(dhcp\) 서버를 배포 하는 방법에 대 한 지침을 제공 하 여 ip 주소 및 dhcp 옵션을 IPv4 dhcp에 자동으로 할당 합니다. 네트워크에 있는 하나 이상의 서브넷에 연결 된 클라이언트입니다.

>[!NOTE]
>TechNet 갤러리에서이 문서를 Word 형식으로 다운로드 하려면 [Windows Server 2016에서 Windows PowerShell을 사용 하 여 DHCP 배포](https://gallery.technet.microsoft.com/Deploy-DHCP-Using-Windows-246dd293)를 참조 하세요.

DHCP 서버를 사용 하 여 IP 주소를 할당 하면 네트워크에 있는 모든 컴퓨터의 모든 네트워크 어댑터에 대 한 TCP/IP v4 설정을 수동으로 구성할 필요가 없기 때문에 관리 오버 헤드가 절약 됩니다. DHCP를 사용 하면 컴퓨터 또는 다른 DHCP 클라이언트가 네트워크에 연결 되어 있을 때 TCP/IP v4 구성이 자동으로 수행 됩니다.

작업 그룹의 DHCP 서버를 독립 실행형 서버로 배포 하거나 Active Directory 도메인의 일부로 배포할 수 있습니다.

이 가이드에는 다음 섹션이 수록되어 있습니다.

- [DHCP 배포 개요](#bkmk_overview)
- [기술 개요](#bkmk_technologies)
- [DHCP 배포 계획](#bkmk_plan)
- [테스트 랩에서이 가이드 사용](#bkmk_lab)
- [DHCP 배포](#bkmk_deploy)
- [서버 기능 확인](#bkmk_verify)
- [DHCP 용 Windows PowerShell 명령](#bkmk_dhcpwps)
- [이 가이드의 Windows PowerShell 명령 목록](#bkmk_list)

## <a name="bkmk_overview"></a>DHCP 배포 개요

다음 그림에서는이 가이드를 사용 하 여 배포할 수 있는 시나리오를 보여 줍니다. 시나리오에는 Active Directory 도메인에 하나의 DHCP 서버가 포함 됩니다. 서버는 두 개의 서로 다른 서브넷에 있는 DHCP 클라이언트에 IP 주소를 제공 하도록 구성 됩니다. 서브넷은 DHCP 전달이 사용 하도록 설정 된 라우터로 구분 됩니다.

![DHCP 네트워크 토폴로지 개요](../../media/Core-Network-Guide/cng16_overview.jpg)

## <a name="bkmk_technologies"></a>기술 개요

다음 섹션에서는 DHCP 및 TCP/IP에 대 한 간략 한 개요를 제공 합니다.

### <a name="dhcp-overview"></a>DHCP 개요

DHCP는 호스트 IP 구성의 관리를 단순화하기 위한 IP 표준입니다. DHCP 표준은 네트워크에 있는 DHCP 지원 클라이언트의 IP 주소 및 기타 관련 구성 세부 사항의 동적 할당을 관리하는 방법으로서 DHCP 서버를 사용합니다.

DHCP를 사용 하면 DHCP 서버를 사용 하 여 고정 IP 주소를 사용 하는 모든 장치를 수동으로 구성 하는 대신 로컬 네트워크의 컴퓨터 또는 다른 장치 (예: 프린터)에 IP 주소를 동적으로 할당할 수 있습니다.

IP 주소 및 해당 관련 서브넷 마스크는 컴퓨터가 연결된 호스트 컴퓨터 및 서브넷을 모두 식별하므로 TCP/IP 네트워크의 모든 컴퓨터에는 고유한 IP 주소가 있어야 합니다. DHCP를 사용하여 DHCP 클라이언트로 구성된 모든 컴퓨터에 해당 네트워크 위치 및 서브넷에 적합한 IP 주소가 수신되도록 하고 기본 게이트웨이 및 DNS 서버와 같은 DHCP 옵션을 사용하여 DHCP 클라이언트가 네트워크에서 제대로 작동하는 데 필요한 정보를 이 클라이언트에 자동으로 제공할 수 있습니다.

TCP/IP 기반 네트워크의 경우 DHCP는 컴퓨터 구성과 관련 된 관리 작업의 복잡성 및 양을 줄입니다.

### <a name="tcpip-overview"></a>TCP/IP 개요

기본적으로 모든 버전의 Windows Server 및 Windows 클라이언트 운영 체제에는 DHCP 서버에서 IP 주소 및 DHCP 옵션 이라고 하는 기타 정보를 자동으로 가져오도록 구성 된 IP 버전 4 네트워크 연결에 대 한 TCP/IP 설정이 있습니다. 따라서 컴퓨터가 서버 컴퓨터 이거나 수동으로 구성 된 고정 IP 주소가 필요한 다른 장치인 경우에만 TCP/IP 설정을 수동으로 구성할 필요가 없습니다. 

예를 들어 DHCP 서버의 ip 주소와 Active Directory Domain Services \(AD DS\)를 실행 하는 DNS 서버 및 도메인 컨트롤러의 ip 주소를 수동으로 구성 하는 것이 좋습니다.

Windows Server 2016의 TCP/IP는 다음과 같습니다.

- 업계 표준 네트워킹 프로토콜을 기준으로 하는 네트워킹 소프트웨어

- Windows 기반 컴퓨터를 LAN(Local Area Network)과 WAN(Wide Area Network) 환경 모두에 연결할 수 있는, 라우트 가능한 엔터프라이즈 네트워킹 프로토콜

- 정보 공유를 목적으로 Windows 기반 컴퓨터를 상이한 시스템과 연결하기 위한 핵심 기술 및 유틸리티

- 웹 및 FTP (파일 전송 프로토콜) 서버와 같은 글로벌 인터넷 서비스에 대 한 액세스 권한을 얻기 위한 기초입니다.

- 강력하고, 확장 가능하며, 플랫폼 간 작동이 가능한 클라이언트/서버 프레임워크

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

- 네트워크로 준비 된 프린터

- 유선 이더넷 또는 무선 802.11 기술을 사용 하는 태블릿 및 휴대폰 전화

## <a name="bkmk_plan"></a>DHCP 배포 계획

다음은 DHCP 서버 역할을 설치 하기 전의 주요 계획 단계입니다.

### <a name="planning-dhcp-servers-and-dhcp-forwarding"></a>DHCP 서버 및 DHCP 전달 계획

DHCP 메시지는 브로드캐스트 메시지이기 때문에 라우터에 의해 서브넷 간에 전달되지 않습니다. 서브넷이 여러 개이고 각 서브넷에 대해 DHCP 서비스를 제공하려면 다음 중 하나를 수행해야 합니다.

- 각 서브넷에 DHCP 서버 설치

- 라우터가 서브넷을 가로질러 DHCP 브로드캐스트 메시지를 전달하도록 구성하고 각 서브넷당 하나씩 여러 범위를 DHCP 서버에 구성합니다.

대개의 경우 DHCP 브로드캐스트 메시지를 전달하도록 라우터를 구성하는 경우가 네트워크의 실제 세그먼트 각각에 DHCP 서버를 배포하는 경우보다 비용 효율적입니다.

### <a name="planning-ip-address-ranges"></a>IP 주소 범위 계획

각 서브넷에는 자체의 고유한 IP 주소 범위가 있어야 합니다. 이 주소 범위는 DHCP 서버에서 범위로 표현됩니다.

범위란 서브넷에서 DHCP 서비스를 사용하는 컴퓨터에 대한 IP 주소의 관리 그룹을 의미합니다. 관리자는 먼저 실제 서브넷마다 범위를 하나씩 만든 다음 범위를 사용하여 클라이언트에서 사용하는 매개 변수를 정의합니다.

범위에는 다음과 같은 속성이 있습니다.

- DHCP 서비스 임대에 사용되는 주소를 포함하거나 제외할 IP 주소의 범위

- 지정된 IP 주소의 서브넷을 결정하는 서브넷 마스크

- 범위를 만들 때 할당되는 범위 이름

- 동적으로 할당되는 IP 주소를 받는 DHCP 클라이언트에 할당되는 임대 기간 값

- DHCP 클라이언트에 할당하도록 구성된 모든 DHCP 범위 옵션(예: DNS 서버 IP 주소, 라우터/기본 게이트웨이 IP 주소)

- DHCP 클라이언트가 항상 같은 IP 주소를 받도록 하기 위해 선택적으로 사용되는 예약

서버를 배포하기 전에 서브넷과 각 서브넷에 대해 사용할 IP 주소 범위를 나열합니다.

### <a name="planning-subnet-masks"></a>서브넷 마스크 계획

IP 주소 내에서 네트워크 ID와 호스트 ID는 서브넷 마스크를 사용하여 구분됩니다. 각 서브넷 마스크는 네트워크 ID를 식별하는 모두 1인 연속적인 비트 그룹과 IP 주소의 호스트 ID 부분을 식별하는 모두 0인 비트 그룹을 사용하는 32비트 숫자입니다.

예를 들어 IP 주소 131.107.16.200에 일반적으로 사용되는 서브넷 마스크는 다음의 32비트 이진 번호입니다.

```
11111111 11111111 00000000 00000000
```

이 서브넷 마스크 번호는 16 1 비트, 16 비트 16 비트 (이 IP 주소의 네트워크 ID 및 호스트 ID 섹션의 길이는 모두 16 비트) 임을 나타냅니다. 일반적으로 이 서브넷 마스크는 255.255.0.0과 같은 점으로 구분된 10진수 표기법으로 표시됩니다.

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

이 문제를 해결하기 위해 DHCP 범위에 대해 제외 범위를 만들 수 있습니다. 제외 범위는 DHCP 서버에서 사용할 수 없는 범위 IP 주소 범위 내에 있는 연속 된 IP 주소 범위입니다. 제외 범위를 만든 경우 DHCP 서버가 해당 범위의 주소를 할당하지 않으므로 IP 주소 충돌 없이 이 주소를 수동으로 할당할 수 있습니다.

각 범위에 대한 제외 범위를 만들어 해당 IP 주소를 DHCP 서버의 배포에서 제외할 수 있습니다. 고정 IP 주소로 구성된 모든 장치를 제외해야 합니다. 제외 주소 범위에는 다른 서버, 비 DHCP 클라이언트, 디스크가 없는 워크스테이션 또는 라우팅 및 원격 액세스 및 PPP 클라이언트에 수동으로 할당한 모든 IP 주소가 포함되어야 합니다.

향후의 네트워크 확장을 고려하여 추가적인 주소로 제외 범위를 구성하는 것이 좋습니다. 다음 표에서는 IP 주소 범위가 10.0.0.1-10.0.0.254이 고 서브넷 마스크가 255.255.255.0 인 범위에 대 한 예제 제외 범위를 제공 합니다.

|구성 항목|예제 값|
|-----------------------|------------------|
|제외 범위 시작 IP 주소|10.0.0.1|
|제외 범위 끝 IP 주소|10.0.0.25|

### <a name="planning-tcpip-static-configuration"></a>TCP/IP 고정 구성 계획

라우터, DHCP 서버 및 DNS 서버와 같은 특정 장치는 고정 IP 주소로 구성해야 합니다. 또한 프린터와 같이 항상 같은 IP 주소를 사용하는 것이 편리한 장치도 있습니다. 각 서브넷에 대해 정적으로 구성할 장치를 나열한 다음 고정적으로 구성된 장치의 IP 주소를 DHCP 서버에서 임대하지 않도록 하기 위해 DHCP 서버에서 사용할 제외 범위를 계획합니다. 제외 범위는 DHCP 서비스 제공에서 제외되는 범위로, 범위 내의 제한된 연속 IP 주소입니다. 제외 범위에 속하는 주소는 서버가 네트워크의 DHCP 클라이언트에 제공하지 않습니다.

예를 들어 서브넷의 IP 주소 범위가 192.168.0.1 ~ 192.168.0.254이 고 고정 IP 주소를 사용 하 여 10 개의 장치를 구성 하려는 경우에는 192.168.0의 제외 범위를 만들 수 있습니다. IP 주소를 10 개 이상 포함 하는 *x* 범위: 192.168.0.1 ~ 192.168.0.15.

이 예제에서는 제외되는 IP 주소 중 10개를 고정 IP 주소를 가진 서버 및 기타 장치로 구성하고 나머지 5개의 주소는 향후에 추가할 수 있는 새 장치의 고정 구성을 위해 남겨둡니다. 이 제외 범위를 적용하면 DHCP 서버는 192.168.0.16부터 192.168.0.254까지의 주소 풀을 사용합니다.

다음 표에서는 AD DS 및 DNS에 대 한 추가 예제 구성 항목을 제공 합니다.

|구성 항목|예제 값|
|-----------------------|------------------|
|네트워크 연결 바인딩|이더넷|
|DNS 서버 설정|DC1.corp.contoso.com|
|기본 설정 DNS 서버 IP 주소|10.0.0.2|
|범위 값<br /><br />1.  범위 이름<br />2.  시작 IP 주소<br />3.  끝 IP 주소<br />4.  서브넷 마스크<br />5.  기본 게이트웨이(옵션)<br />6.  임대 기간|1.  주 서브넷<br />2.10.0.0.1<br />3.10.0.0.254<br />4.255.255.255.0<br />5.10.0.0.1<br />6.8 일|
|IPv6 DHCP 서버 작동 모드|사용 안 함|

## <a name="bkmk_lab"></a>테스트 랩에서이 가이드 사용

프로덕션 환경에를 배포 하기 전에이 가이드를 사용 하 여 테스트 랩에서 DHCP를 배포할 수 있습니다. 

>[!NOTE]
>테스트 랩에서 DHCP를 배포 하지 않으려면 [Dhcp 배포](#bkmk_deploy)섹션으로 건너뛸 수 있습니다.

랩에 대 한 요구 사항은 실제 서버 또는 가상 컴퓨터 \(vm\)을 사용 하는지 여부, Active Directory 도메인을 사용 하는지, 아니면 독립 실행형 DHCP 서버를 배포 하는지에 따라 달라 집니다.

다음 정보를 사용 하 여이 가이드를 사용 하 여 DHCP 배포를 테스트 하는 데 필요한 최소 리소스를 결정할 수 있습니다.

### <a name="test-lab-requirements-with-vms"></a>Vm을 사용 하 여 랩 요구 사항 테스트

Vm을 사용 하 여 테스트 랩에서 DHCP를 배포 하려면 다음 리소스가 필요 합니다.

도메인 배포 또는 독립 실행형 배포의 경우 hyper-v\-호스트로 구성 된 서버가 하나 필요 합니다.

**도메인 배포**

이 배포에는 물리적 서버 한 대, 가상 스위치, 가상 서버 2 개 및 가상 클라이언트 1 개가 필요 합니다.

실제 서버의 Hyper-v 관리자에서 다음 항목을 만듭니다.

1. **내부** 가상 스위치 하나 **외부** 가상 스위치를 만들지 마세요. hyper-v\-호스트가 dhcp 서버를 포함 하는 서브넷에 있는 경우 테스트 vm은 dhcp 서버에서 IP 주소를 수신 합니다. 또한 배포 하는 테스트 DHCP 서버는 hyper-v\-호스트가 설치 된 서브넷에 있는 다른 컴퓨터에 IP 주소를 할당할 수 있습니다.
1. 사용자가 만든 내부 가상 스위치에 연결 된 Active Directory Domain Services를 사용 하 여 도메인 컨트롤러로 구성 된 Windows Server 2016를 실행 하는 VM 하나가 있습니다. 이 가이드를 충족 하기 위해이 서버에는 고정적으로 구성 된 IP 주소 10.0.0.2가 있어야 합니다. AD DS 배포에 대 한 자세한 내용은 Windows Server 2016 [Core 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01)의 **DC1 배포** 섹션을 참조 하세요.
1. Windows Server 2016를 실행 하는 VM 하나는이 가이드를 사용 하 여 DHCP 서버로 구성 하 고 사용자가 만든 내부 가상 스위치에 연결 됩니다. 
1. 사용자가 만든 내부 가상 스위치에 연결 된 Windows 클라이언트 운영 체제를 실행 하는 하나의 VM은 DHCP 서버가 IP 주소 및 DHCP 옵션을 DHCP 클라이언트에 동적으로 할당 하 고 있는지 확인 하는 데 사용 합니다.

**독립 실행형 DHCP 서버 배포**

이 배포에는 물리적 서버 한 대, 가상 스위치, 가상 서버 1 대 및 가상 클라이언트 1 대가 필요 합니다.

실제 서버의 Hyper-v 관리자에서 다음 항목을 만듭니다.

1. **내부** 가상 스위치 하나 **외부** 가상 스위치를 만들지 마세요. hyper-v\-호스트가 dhcp 서버를 포함 하는 서브넷에 있는 경우 테스트 vm은 dhcp 서버에서 IP 주소를 수신 합니다. 또한 배포 하는 테스트 DHCP 서버는 hyper-v\-호스트가 설치 된 서브넷에 있는 다른 컴퓨터에 IP 주소를 할당할 수 있습니다.
2. Windows Server 2016를 실행 하는 VM 하나는이 가이드를 사용 하 여 DHCP 서버로 구성 하 고 사용자가 만든 내부 가상 스위치에 연결 됩니다.
3. 사용자가 만든 내부 가상 스위치에 연결 된 Windows 클라이언트 운영 체제를 실행 하는 하나의 VM은 DHCP 서버가 IP 주소 및 DHCP 옵션을 DHCP 클라이언트에 동적으로 할당 하 고 있는지 확인 하는 데 사용 합니다.

### <a name="test-lab-requirements-with-physical-servers"></a>물리적 서버를 사용 하 여 랩 요구 사항 테스트

물리적 서버를 사용 하 여 테스트 랩에서 DHCP를 배포 하려면 다음 리소스가 필요 합니다.

**도메인 배포**

이 배포에는 하나의 허브 또는 스위치, 두 개의 물리적 서버 및 물리적 클라이언트 1 개가 필요 합니다.

1. 이더넷 케이블을 사용 하 여 물리적 컴퓨터를 연결할 수 있는 이더넷 허브 또는 스위치 하나
2. Active Directory Domain Services를 사용 하 여 도메인 컨트롤러로 구성 된 Windows Server 2016를 실행 하는 물리적 컴퓨터 1 대 이 가이드를 충족 하기 위해이 서버에는 고정적으로 구성 된 IP 주소 10.0.0.2가 있어야 합니다. AD DS 배포에 대 한 자세한 내용은 Windows Server 2016 [Core 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01)의 **DC1 배포** 섹션을 참조 하세요.
3. 이 가이드를 사용 하 여 DHCP 서버로 구성할 Windows Server 2016를 실행 하는 물리적 컴퓨터 1 대 
4. Dhcp 서버가 dhcp 클라이언트에 IP 주소 및 DHCP 옵션을 동적으로 할당 하 고 있는지 확인 하는 데 사용할 Windows 클라이언트 운영 체제를 실행 하는 물리적 컴퓨터 1 대

>[!NOTE]
>이 배포에 대 한 테스트 컴퓨터가 충분 하지 않은 경우 AD DS 및 DHCP 둘 다에 대해 하나의 테스트 컴퓨터를 사용할 수 있지만 프로덕션 환경에서는이 구성을 사용 하지 않는 것이 좋습니다.

**독립 실행형 DHCP 서버 배포**

이 배포에는 허브 또는 스위치 한 대, 물리적 서버 한 대, 물리적 클라이언트 1 대가 필요 합니다.

1. 이더넷 케이블을 사용 하 여 물리적 컴퓨터를 연결할 수 있는 이더넷 허브 또는 스위치 하나
2. 이 가이드를 사용 하 여 DHCP 서버로 구성할 Windows Server 2016를 실행 하는 물리적 컴퓨터 1 대
3. Dhcp 서버가 dhcp 클라이언트에 IP 주소 및 DHCP 옵션을 동적으로 할당 하 고 있는지 확인 하는 데 사용할 Windows 클라이언트 운영 체제를 실행 하는 물리적 컴퓨터 1 대


## <a name="bkmk_deploy"></a>DHCP 배포

이 섹션에서는 하나의 서버에 DHCP를 배포 하는 데 사용할 수 있는 Windows PowerShell 명령 예제를 제공 합니다. 서버에서 이러한 예제 명령을 실행 하기 전에 네트워크 및 환경에 맞게 명령을 수정 해야 합니다. 

예를 들어 명령을 실행 하기 전에 다음 항목에 대 한 명령의 예제 값을 바꾸어야 합니다.

- 컴퓨터 이름
- 구성 하려는 각 범위에 대 한 IP 주소 범위 (서브넷 당 1 개 범위)
- 구성할 각 IP 주소 범위에 대 한 서브넷 마스크
- 각 범위에 대 한 범위 이름
- 각 범위에 대 한 제외 범위
- DHCP 옵션 값 (예: 기본 게이트웨이, 도메인 이름, DNS 또는 WINS 서버)
- 인터페이스 이름

>[!IMPORTANT]
>명령을 실행 하기 전에 사용자 환경의 모든 명령을 검사 하 고 수정 합니다.

### <a name="where-to-install-dhcp---on-a-physical-computer-or-a-vm"></a>물리적 컴퓨터 또는 VM에서 DHCP를 설치 하는 위치

Hyper-v\) \(호스트에설치된가상컴퓨터VM또는물리적컴퓨터에DHCP서버역할을설치할수있습니다.\- VM에 DHCP를 설치 하 고 DHCP 서버가 Hyper-v 호스트가 연결 된 실제 네트워크의 컴퓨터에 IP 주소 할당을 제공 하도록 하려면 VM 가상 네트워크 어댑터를 외부의 Hyper-v 가상 스위치에 연결 해야 합니다.  **/c0 >.**

자세한 내용은 [가상 네트워크 만들기](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network)항목에서 **hyper-v 관리자를 사용 하 여 가상 스위치 만들기** 섹션을 참조 하세요.

### <a name="run-windows-powershell-as-an-administrator"></a>관리자 권한으로 Windows PowerShell 실행

관리자 권한으로 Windows PowerShell을 실행 하려면 다음 절차를 사용할 수 있습니다.

1. Windows Server 2016를 실행 하는 컴퓨터에서 **시작**을 클릭 한 다음 windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭 합니다. 메뉴가 나타납니다.

2. 메뉴에서 **자세히**를 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다. 메시지가 표시 되 면 컴퓨터에 대 한 관리자 권한이 있는 계정에 대 한 자격 증명을 입력 합니다. 컴퓨터에 로그온 한 사용자 계정이 관리자 수준 계정인 경우 자격 증명 프롬프트가 표시 되지 않습니다.

3. 관리자 권한으로 Windows PowerShell이 열립니다.

### <a name="rename-the-dhcp-server-and-configure-a-static-ip-address"></a>DHCP 서버 이름 바꾸기 및 고정 IP 주소 구성

아직 수행 하지 않은 경우 다음 Windows PowerShell 명령을 사용 하 여 DHCP 서버의 이름을 바꾸고 서버에 대 한 고정 IP 주소를 구성할 수 있습니다.

**고정 IP 주소 구성**

다음 명령을 사용 하 여 DHCP 서버에 고정 IP 주소를 할당 하 고 올바른 DNS 서버 IP 주소를 사용 하 여 DHCP 서버 TCP/IP 속성을 구성할 수 있습니다. 이 예제의 인터페이스 이름과 IP 주소를, 컴퓨터를 구성하는 데 사용하려는 값으로 바꾸는 작업도 수행해야 합니다.

```
New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2
```

이러한 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [New-netipaddress](https://technet.microsoft.com/itpro/powershell/windows/tcpip/new-netipaddress)
- [-DnsClientServerAddress 설정](https://technet.microsoft.com/itpro/powershell/windows/dns-client/set-dnsclientserveraddress)

**컴퓨터 이름 바꾸기**

다음 명령을 사용 하 여 컴퓨터의 이름을 바꾼 후 컴퓨터를 다시 시작할 수 있습니다.

```
Rename-Computer -Name DHCP1
Restart-Computer
```

이러한 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [이름 바꾸기-컴퓨터](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/rename-computer)
- [Restart-Computer](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/restart-computer)

### <a name="join-the-computer-to-the-domain-optional"></a>도메인 \(에 컴퓨터 가입 옵션\)

Active Directory 도메인 환경에 DHCP 서버를 설치 하는 경우 컴퓨터를 도메인에 가입 시켜야 합니다. 관리자 권한으로 Windows PowerShell을 열고 도메인 NetBios 이름 **CORP** 를 사용자 환경에 적합 한 값으로 바꾼 후 다음 명령을 실행 합니다.

```
Add-Computer CORP
```

메시지가 표시 되 면 도메인에 컴퓨터를 가입 시킬 수 있는 권한을 가진 도메인 사용자 계정의 자격 증명을 입력 합니다. 

```
Restart-Computer
```

컴퓨터 추가 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [컴퓨터 추가](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/add-computer)

### <a name="install-dhcp"></a>DHCP 설치

컴퓨터를 다시 시작한 후 관리자 권한으로 Windows PowerShell을 열고 다음 명령을 실행 하 여 DHCP를 설치 합니다.

```
Install-WindowsFeature DHCP -IncludeManagementTools
```

이 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [설치-Add-windowsfeature](https://technet.microsoft.com/itpro/powershell/windows/server-manager/install-windowsfeature)

### <a name="create-dhcp-security-groups"></a>DHCP 보안 그룹 만들기

보안 그룹을 만들려면 Windows PowerShell에서 Network Shell \(netsh\) 명령을 실행 한 다음 새 그룹이 활성 상태가 되도록 DHCP 서비스를 다시 시작 해야 합니다.

Dhcp 서버에서 다음 netsh 명령을 실행 하면 dhcp **관리자** 및 dhcp **사용자** 보안 그룹이 dhcp 서버의 **로컬 사용자 및 그룹** 에 만들어집니다.

```
netsh dhcp add securitygroups
```

다음 명령은 로컬 컴퓨터에서 DHCP 서비스를 다시 시작 합니다.

```
Restart-Service dhcpserver
```

이러한 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [Netsh(네트워크 셸)](../netsh/netsh.md)
- [서비스 다시 시작](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/restart-service)

### <a name="authorize-the-dhcp-server-in-active-directory-optional"></a>Active Directory \(옵션에서 DHCP 서버 권한 부여\)

도메인 환경에서 DHCP를 설치 하는 경우 다음 단계를 수행 하 여 DHCP 서버가 도메인에서 작동할 수 있도록 권한을 부여 해야 합니다.

>[!NOTE]
>Active Directory 도메인에 설치 된 권한이 없는 DHCP 서버는 제대로 작동할 수 없으며, DHCP 클라이언트에 IP 주소를 임대 하지 않습니다. 권한이 없는 DHCP 서버를 자동으로 사용 하지 않도록 설정 하는 것은 권한이 없는 DHCP 서버에서 네트워크의 클라이언트에 잘못 된 IP 주소를 할당할 수 없도록 하는 보안 기능입니다.

다음 명령을 사용 하 여 Active Directory에 있는 권한이 부여 된 DHCP 서버 목록에 DHCP 서버를 추가할 수 있습니다. 

>[!NOTE]
>도메인 환경이 없는 경우에는이 명령을 실행 하지 마십시오.

```
Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com -IPAddress 10.0.0.3
```

Active Directory에서 DHCP 서버에 권한이 부여 되었는지 확인 하려면 다음 명령을 사용할 수 있습니다.

```
Get-DhcpServerInDC
```

Windows PowerShell에 표시 되는 예제 결과는 다음과 같습니다.

```
IPAddress   DnsName
---------   -------
10.0.0.3    DHCP1.corp.contoso.com
```

이러한 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [-DhcpServerInDC 추가](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverindc)
- [Get DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc)

### <a name="notify-server-manager-that-post-install-dhcp-configuration-is-complete-optional"></a>설치 후\-DHCP 구성이 완료 \(됨을 서버 관리자에 알림\)

Active Directory에서 보안 그룹을\-만들고 DHCP 서버에 권한을 부여 하는 등의 설치 후 작업을 완료 한 후에도 사용자 인터페이스에이 게시물\- 을 나타내는 경고를 표시할 수 서버 관리자. 설치 단계는 DHCP 사후 설치 구성 마법사를 사용 하 여 완료 해야 합니다.

이 Windows PowerShell 명령을 사용\-하 여 다음 레지스트리 키를 구성 하 여 서버 관리자에 불필요 하 고 부정확 한 메시지가 표시 되지 않도록 할 수 있습니다.

```
Set-ItemProperty –Path registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12 –Name ConfigurationState –Value 2
```

이 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [Get-itemproperty](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/set-itemproperty?f=255&MSPPError=-2147217396)

### <a name="set-server-level-dns-dynamic-update-configuration-settings-optional"></a>서버 수준 DNS 동적 업데이트 구성 설정 \(옵션 설정\)

Dhcp 서버에서 DHCP 클라이언트 컴퓨터에 대 한 DNS 동적 업데이트를 수행 하도록 하려면 다음 명령을 실행 하 여이 설정을 구성할 수 있습니다. 이 설정은 범위 수준 설정이 아니라 서버에서 구성 하는 모든 범위에 영향을 줍니다. 또한이 예제 명령은 클라이언트의 최소 만료 시간에 클라이언트에 대 한 DNS 리소스 레코드를 삭제 하도록 DHCP 서버를 구성 합니다.

```
Set-DhcpServerv4DnsSetting -ComputerName "DHCP1.corp.contoso.com" -DynamicUpdates "Always" -DeleteDnsRRonLeaseExpiry $True
```

다음 명령을 사용 하 여 DHCP 서버가 DNS 서버에서 클라이언트 레코드를 등록 하거나 등록 취소 하는 데 사용 하는 자격 증명을 구성할 수 있습니다. 이 예제에서는 DHCP 서버에 자격 증명을 저장 합니다. 첫 번째 명령은 **Get Credential** 을 사용 하 여 **PSCredential** 개체를 만든 다음 개체를 **$Credential** 변수에 저장 합니다. 명령을 사용 하면 사용자 이름과 암호를 입력 하 라는 메시지가 표시 되므로 DNS 서버에서 리소스 레코드를 업데이트할 수 있는 권한이 있는 계정의 자격 증명을 제공 해야 합니다.
 
```
$Credential = Get-Credential
Set-DhcpServerDnsCredential -Credential $Credential -ComputerName "DHCP1.corp.contoso.com"
``` 

이러한 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [DhcpServerv4DnsSetting](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4dnssetting)
- [DhcpServerDnsCredential](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverdnscredential)

### <a name="configure-the-corpnet-scope"></a>Corpnet 범위 구성

DHCP 설치가 완료 되 면 다음 명령을 사용 하 여 Corpnet 범위를 구성 및 활성화 하 고, 범위에 대 한 제외 범위를 만들고, DHCP 옵션 기본 게이트웨이, DNS 서버 IP 주소 및 DNS 도메인 이름을 구성할 수 있습니다.

```
Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active    
Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15
Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com
Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2
```

이러한 명령에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

- [DhcpServerv4Scope](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4scope)
- [DhcpServerv4ExclusionRange](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4exclusionrange)
- [DhcpServerv4OptionValue](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4optionvalue)

### <a name="configure-the-corpnet2-scope-optional"></a>Corpnet2 Scope \(구성 (선택 사항)\)

DHCP 전달이 사용 하도록 설정 된 라우터를 사용 하 여 첫 번째 서브넷에 연결 된 두 번째 서브넷이 있는 경우 다음 명령을 사용 하 여이 예제에 Corpnet2 라는 두 번째 범위를 추가할 수 있습니다. 또한이 예제에서는 기본 게이트웨이의 \(Corpnet2 서브넷에\) 있는 라우터 ip 주소에 대 한 제외 범위와 ip 주소를 구성 합니다.

```
Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active
Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15
Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com
```

이 DHCP 서버에서 서비스를 제공 하는 추가 서브넷이 있는 경우 모든 명령 매개 변수에 대해 서로 다른 값을 사용 하 여 이러한 명령을 반복 하 여 각 서브넷에 대 한 범위를 추가할 수 있습니다.

>[!IMPORTANT]
>Dhcp 클라이언트와 dhcp 서버 간의 모든 라우터가 DHCP 메시지 전달을 위해 구성 되었는지 확인 합니다. DHCP 전달을 구성 하는 방법에 대 한 자세한 내용은 라우터 설명서를 참조 하세요.

## <a name="bkmk_verify"></a>서버 기능 확인

Dhcp 서버가 DHCP 클라이언트에 IP 주소를 동적으로 할당 하 고 있는지 확인 하려면 다른 컴퓨터를 서비스 서브넷에 연결할 수 있습니다. 이더넷 케이블을 네트워크 어댑터에 연결 하 고 컴퓨터 전원을 연결한 후에는 DHCP 서버에서 IP 주소를 요청 합니다. **Ipconfig/all** 명령을 사용 하 여 성공적인 구성을 확인 하 고 결과를 검토 하거나 브라우저를 사용 하 여 웹 리소스에 액세스 하려고 시도 하는 등의 연결 테스트 또는 Windows 탐색기 나 기타 파일 공유를 수행 하 여 구성을 확인할 수 있습니다. 프로그램도.

클라이언트가 DHCP 서버에서 IP 주소를 수신 하지 않는 경우 다음 문제 해결 단계를 수행 합니다.

1. 이더넷 케이블이 컴퓨터와 이더넷 스위치, 허브 또는 라우터 모두에 연결 되어 있는지 확인 합니다.
2. 라우터를 통해 DHCP 서버와 분리 된 네트워크 세그먼트에 클라이언트 컴퓨터를 연결한 경우 라우터가 DHCP 메시지를 전달 하도록 구성 되어 있는지 확인 합니다.
3. Active Directory에서 권한이 부여 된 DHCP 서버 목록을 검색 하기 위해 다음 명령을 실행 하 여 Active Directory에서 DHCP 서버에 권한을 부여 했는지 확인 합니다. [-DhcpServerInDC를 가져옵니다](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc).
4. Dhcp \(콘솔 서버 관리자, **도구**, **dhcp**\)를 열고 서버 트리를 확장 하 여 범위를 검토 한 다음 각 범위를 마우스 오른쪽 단추로\-클릭 하 여 범위를 활성화 해야 합니다. 결과 메뉴에 선택 **활성화**가 포함 되어 있으면 **활성화**를 클릭 합니다. \(범위가 이미 활성화 되어 있으면 메뉴 선택이 **비활성화**를 읽습니다.\)

## <a name="bkmk_dhcpwps"></a>DHCP 용 Windows PowerShell 명령

다음 참조에서는 Windows Server 2016에 대 한 모든 DHCP 서버 Windows PowerShell 명령에 대 한 명령 설명 및 구문을 제공 합니다. 항목은 **Get** 또는 **Set**와 같이 명령의 시작 부분에 있는 동사에 따라 사전순으로 명령을 나열 합니다.

>[!NOTE]
>Windows server 2012 r 2에서는 Windows Server 2016 명령을 사용할 수 없습니다.

- [DhcpServer 모듈](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/index)

다음 참조에서는 Windows Server 2012 r 2 용 모든 DHCP 서버 Windows PowerShell 명령에 대 한 명령 설명 및 구문을 제공 합니다. 항목은 **Get** 또는 **Set**와 같이 명령의 시작 부분에 있는 동사에 따라 사전순으로 명령을 나열 합니다.

>[!NOTE]
>Windows server 2016에서 Windows Server 2012 R2 명령을 사용할 수 있습니다.

- [Windows PowerShell의 DHCP 서버 Cmdlet](https://technet.microsoft.com/library/jj590751.aspx)

## <a name="bkmk_list"></a>이 가이드의 Windows PowerShell 명령 목록

다음은이 가이드에서 사용 되는 간단한 명령과 예제 값의 목록입니다.

```
New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2
Rename-Computer -Name DHCP1
Restart-Computer

Add-Computer CORP
Restart-Computer

Install-WindowsFeature DHCP -IncludeManagementTools
netsh dhcp add securitygroups
Restart-Service dhcpserver

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
```
