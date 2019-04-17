---
title: DHCP를 사용 하 여 Windows PowerShell 배포
description: 이 항목에 하나 이상의 서브넷 네트워크에 연결 된 IPv4 DHCP 클라이언트로 자동 IP 주소와 DHCP 옵션을 제공 하는 Windows Server 2016 IP (인터넷 프로토콜) 버전 4 DHCP 서버 배포 하는 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 7110ad21-a33e-48d5-bb3c-129982913bc8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2be3c02f32229c9b9ee411f5e97305776f9825d8
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-dhcp-using-windows-powershell"></a>DHCP를 사용 하 여 Windows PowerShell 배포

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 가이드를 사용 하 여 Windows PowerShell 자동으로 IP 주소와 DHCP 옵션 클라이언트를 할당 IPv4 DHCP에 하나 이상의 서브넷 네트워크에 연결 되어 있는 한 IP (인터넷 프로토콜) 버전 4 DHCP(Dynamic Host Configuration Protocol) \(DHCP\) 서버를 배포 하는 방법에 대해 설명 합니다.

>[!NOTE]
>이 문서 Word 형식에서 TechNet 갤러리에서를 다운로드 하려면 참조 [Windows Server 2016에 배포 DHCP를 사용 하 여 Windows PowerShell](https://gallery.technet.microsoft.com/Deploy-DHCP-Using-Windows-246dd293)합니다.

서버 DHCP를 사용 하 여 IP 할당 주소 절약 관리 오버에서 네트워크의 모든 컴퓨터에서 모든 네트워크 어댑터에 대 한 TCP/IP v4 설정을 수동으로 구성 필요가 없습니다. Dhcp를 컴퓨터 때 TCP/IP v4 구성 자동으로 수행 됩니다 또는 기타 DHCP 클라이언트 네트워크에 연결 되어 있습니다.

독립 실행형 서버 또는 Active Directory 도메인의 일부로 DHCP 서버 작업 그룹에 배포할 수 있습니다.

이 가이드 다음 섹션에 포함 되어 있습니다.

- [DHCP 배포 개요](#bkmk_overview)
- [기술 개요](#bkmk_technologies)
- [DHCP 배포를 계획](#bkmk_plan)
- [이 가이드를 사용 하 여 테스트 랩에](#bkmk_lab)
- [DHCP를 배포 합니다.](#bkmk_deploy)
- [서버 기능을 확인](#bkmk_verify)
- [Windows PowerShell DHCP에 대 한 명령](#bkmk_dhcpwps)
- [이 가이드 Windows PowerShell 명령 목록](#bkmk_list)

## <a name="bkmk_overview"></a>DHCP 배포 개요

다음 그림에서는이 가이드를 사용 하 여 배포할 수 있는 시나리오가 보여 줍니다. 시나리오 Active Directory 도메인 DHCP 서버를 포함합니다. DHCP 클라이언트 서로 다른 두 가지 서브넷에 IP 주소를 제공 하는 서버 구성 됩니다. 서브넷은 라우터에서 DHCP 사용 전달 된으로 구분 됩니다.

![DHCP 네트워크 토폴로지 개요](../../media/Core-Network-Guide/cng16_overview.jpg)

## <a name="bkmk_technologies"></a>기술 개요

다음 섹션의 DHCP 및 TCP/IP 간단한 개요를 제공합니다.

### <a name="dhcp-overview"></a>DHCP 개요

DHCP IP 표준 호스트 IP 구성 관리를 간소화에 대 한입니다. DHCP를 사용 하도록 클라이언트 네트워크에 대 한 동적 할당의 IP 주소 및 기타 관련된 구성 세부 정보를 관리 하는 방법으로 DHCP 서버의 사용할 표준 DHCP 제공 합니다.

DHCP 동적으로 컴퓨터나 수동으로 고정 IP 주소를 사용 하 여 모든 디바이스를 구성 하는 것이 아니라 로컬 네트워크의 프린터 등 기타 장치에는 IP 주소를 지정 하려면 DHCP를 사용할 수 있습니다.

TCP/IP 네트워크에 있는 모든 컴퓨터의 IP 주소와 관련된 서브넷 마스크 호스트 컴퓨터와 연결 되어 있는 컴퓨터 서브넷을 식별 하기 때문에 고유한 IP 주소를 있어야 합니다. DHCP를 사용 하 여 DHCP 클라이언트로 구성 되어 있는 모든 컴퓨터의 네트워크 위치와 서브넷 적합 IP 주소를 받을 수 있도록 하며 등 기본 게이트웨이 DNS 서버, DHCP 옵션을 사용 하 여 제공할 수 있습니다 자동으로 DHCP 클라이언트 네트워크에서 제대로 작동 하는 데 필요한 정보를 사용 합니다.

네트워크 TCP 기반 DHCP 복잡 하 고 컴퓨터 구성에 포함 된 관리 작업의 양을 줄입니다.

### <a name="tcpip-overview"></a>TCP/IP 개요

기본적으로 모든 버전의 Windows는 클라이언트와 Windows Server 운영 체제는 TCP/IP 설정을 IP 버전 4 네트워크 연결이 구성 자동으로 IP 주소와 DHCP 옵션 DHCP 서버에서 라고 하는 기타 정보를 얻을 수 있습니다. 이 때문 컴퓨터가 서버 컴퓨터 또는 기타 장치에 필요한 수동으로 구성 된에서 고정 IP 주소를 아니면 TCP/IP 설정을 수동으로 구성 필요가 없습니다. 

예를 들어, 것이 좋습니다 수동으로 구성 하는 DHCP 서버의 IP 주소와 DNS 서버와 Active Directory Domain Services을 실행 하는 도메인 컨트롤러의 IP 주소 \ (AD DS \).

Windows Server 2016에 TCP/IP 다음과 같습니다.

-   네트워킹 소프트웨어 산업 표준을 네트워킹 프로토콜에 따라 합니다.

-   Windows 기반 컴퓨터 (lan) 및 다양 한 영역 (네트워크) 환경을 연결을 지 원하는 경로 조정 가능 enterprise 네트워킹 프로토콜 합니다.

-   핵심 기술 및 Windows 기반 컴퓨터 정보를 공유 하기 위해 다른 시스템을 사용 하 여 연결에 대 한 유틸리티입니다.

-   파일 전송 FTP (프로토콜)와 웹 서버 등 글로벌 인터넷 서비스에 대 한 액세스 하기 위한 기초 합니다.

-   강력한, 확장, 플랫폼 간 클라이언트/서버 프레임 워크 합니다.

TCP/IP은 Windows 기반 컴퓨터에 연결 하 고 다른 Microsoft 및 Microsoft가 아닌 타사 시스템과 포함 하 여 정보를 공유할 수 있도록 하는 기본 TCP/IP 유틸리티를 제공 합니다.

- Windows Server 2016

- Windows 10

- Windows Server 2012 r 2

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

- VM 시스템 열기

- 네트워크에서 사용할 프린터

- 태블릿 및 휴대폰 전화기 이더넷 유선된 또는 무선 802.11 기술을 사용

## <a name="bkmk_plan"></a>DHCP 배포를 계획

다음 주요 계획 단계 DHCP 서버 역할을 설치 하기 전에 합니다.

### <a name="planning-dhcp-servers-and-dhcp-forwarding"></a>DHCP 서버와 DHCP 전달을 계획

DHCP 메시지는 되므로 알림된 메시지를 라우터에서 서브넷 전달 되지 않습니다. 여러 개의 서브넷 있고 각 서브넷 DHCP 서비스를 제공 하려는 경우 다음 중 하나를 수행 해야 합니다.

-   DHCP를 서브넷 각에 설치

-   라우터 서브넷 전체 DHCP 알림된 메시지를 전달 하 고 여러 범위 DHCP 서버의 서브넷 마다 하나의 범위 구성를 구성 합니다.

대부분의 경우 라우터에서 DHCP 알림된 메시지를 전달 하도록 구성는 네트워크의 각 영역에 DHCP를 배포 보다 더 많은 비용 효과적인 합니다.

### <a name="planning-ip-address-ranges"></a>IP 주소 범위 계획

각 서브넷 자체 고유한 IP 주소 범위가 있어야 합니다. 이 범위 범위가 DHCP 서버에 표시 됩니다.

범위 서브넷 DHCP 서비스를 사용 하는 컴퓨터에 IP 주소를의 관리 그룹입니다. 관리자 먼저 각 물리적 서브넷 범위를 만들고 범위를 사용 하는 클라이언트에서 사용 되는 매개 정의 합니다.

범위에는 다음과 같습니다.

-   IP 주소를 포함 하거나 서비스 임대 DHCP 사용 하는 주소를 제외 하 합니다.

-   서브넷 마스크 서브넷 접두사 IP 주소를 지정된를 결정 합니다.

-   만들 때 할당 범위 이름입니다.

-   임대 기간 값 동적 할당된 IP 주소를 수신 하는 클라이언트 DHCP에 지정 합니다.

-   DHCP 클라이언트 라우터/기본 게이트웨이 IP 주소, DNS 서버 IP 주소 등에 할당에 대 한 구성 된 DHCP 범위 옵션입니다.

-   예약은 원하는 경우 DHCP는 클라이언트 항상 동일한 IP 주소를 받을 사용 됩니다.

서버를 배포 하기 전에 서브넷 및 각 서브넷 사용할 IP 주소 범위 나열 합니다.

### <a name="planning-subnet-masks"></a>서브넷 마스크 계획

네트워크 Id 및 IP 주소 호스트 Id 서브넷 마스크를 사용 하 여 구분 됩니다. 각 서브넷 마스크 32 비트 숫자 그룹의 모든 기능을 사용 하는 네트워크를 식별 (1)의 IP 주소 호스트 ID 일부를 식별 하기 위해 ID와 모두 0 (0).

예를 들어, 131.107.16.200 IP 주소를 정상적으로 사용 되는 서브넷 마스크 다음 32 비트 이진 번호는 다음과 같습니다.

```
11111111 11111111 00000000 00000000
```

이 서브넷 마스크 번호는 16 1 비트 16 0 비트 이어서이 IP 주소 네트워크 ID와 호스트 ID 섹션의 길이 모두 16 비트가 합니다. 일반적으로이 서브넷 마스크 255.255.0.0 소수점 표기에 표시 됩니다.

다음 표에서 서브넷 마스크 인터넷 주소 클래스를 표시합니다.

|주소 클래스|서브넷 마스크 비트|서브넷 마스크|
|-----------------|------------------------|---------------|
|클래스 A|11111111 00000000 00000000 00000000|255.0.0.0|
|클래스 B|11111111 11111111 00000000 00000000|255.255.0.0|
|클래스 C|11111111 11111111 11111111 00000000|255.255.255.0|

DHCP에서 범위를 만들고 IP 주소 범위 범위를 입력 하는 경우 DHCP는 이러한 기본값 서브넷 마스크 제공 합니다. 일반적으로 서브넷 마스크 기본값은 없이 특별 요구 사항이 있는 대부분의 네트워크 하 고 각 IP 네트워크 세그먼트 실제 네트워크에 해당 하는 어디에 적합 합니다.

경우에 따라 정의 서브넷 마스크 IP 서브넷 구현 사용할 수 있습니다. IP 서브넷 IP 주소를 지정 서브넷 세부 원래 네트워크 클래스 기반 id가 기본 호스트 ID 부분을 나눌 수 있습니다.

서브넷 마스크 길이 사용자 지정 하 여 실제 호스트 id 사용 되는 비트의 수를 줄일 수 있습니다.

주소 및 라우팅 문제를 방지 하려면 모든 TCP/IP 컴퓨터에는 네트워크 세그먼트 같은 서브넷 마스크 사용 하 여 각 컴퓨터 또는 디바이스의 고유한 IP 주소가 있는지 확인 해야 합니다.

### <a name="planning-exclusion-ranges"></a>계획 제외 범위

DHCP 범위를 만들 때 IP 주소 같은 컴퓨터 및 기타 장치 DHCP 클라이언트로 임대 DHCP 서버 허용 되는 모두 포함 된 IP 주소 범위를 지정 합니다. 다음으로 이동 하 고 일부 서버 수동으로 구성 및 DHCP 서버를 사용 하는 동일한 IP 주소 범위에서 고정 된 다른 디바이스 IP 주소, IP 주소 충돌 실수로 만들 수 있습니다와 DHCP 서버 있는 모두 할당 동일한 IP 주소 서로 다른 장치를.

이 문제를 해결 하기 위해 DHCP 범위에 대 한 제외 범위를 만들 수 있습니다. 제외 범위 DHCP 서버를 사용할 수 없는 범위의 IP 주소 범위 내 연속 IP 주소입니다. 제외 범위를 만든 경우 DHCP 서버 수동으로 IP 주소가 충돌 만들지 않고도이 주소를 지정 하도록 허용 하는 범위 내에 주소를 지정 하지 않습니다.

각 영역에 대 한 제외 범위 만들어 DHCP 서버에 IP 주소 배포에서 제외할 수 있습니다. 고정 IP 주소를으로 구성 된 모든 디바이스에 대 한 제외를 사용 해야 합니다. 제외 주소 다른 서버, DHCP 비 클라이언트, 워크스테이션, 디스크 또는 라우팅 및 원격 액세스 PPP 클라이언트를 수동으로 할당 모든 IP 주소를 포함 해야 합니다.

향후 네트워크 증가 맞게 추가 주소로 제외 범위 구성 하는 것이 좋습니다. 다음 표에서과 10.0.0.1-10.0.0.254과 255.255.255.0 서브넷 마스크의 IP 주소 범위 범위에 대 한 예제 제외 범위를 제공합니다.

|구성 항목|예 값|
|-----------------------|------------------|
|IP 주소 시작 제외 범위|10.0.0.1|
|제외 범위 종료 IP 주소|10.0.0.25|

### <a name="planning-tcpip-static-configuration"></a>TCP/IP 고정 구성 계획

특정 디바이스 DNS 서버, DHCP 서버 라우터 등에서 고정 IP 주소를 구성 합니다. 또한 추가 장치를 항상 되도록 하려면 되는 프린터 등 동일한 IP 주소가 할 수도 있습니다. 구성 하려면 정적 각 서브넷 장치 하 고 DHCP 서버 정적으로 구성 된 디바이스의 IP 주소 임대 하지 않는 되도록 DHCP 서버에서 사용 하려는 제외 범위 계획을 수립 합니다. 제외 범위는 제한 된 시퀀스 DHCP 서비스에서 제외 범위 내에 IP 주소입니다. 제외 범위 보증할 DHCP 클라이언트 네트워크에 이러한 범위에 있는 주소 서버에서 제공 되지 않습니다.

예를 들어, 서브넷 IP 주소 범위는 192.168.0.254 통해 192.168.0.1에서 고정 IP 주소를 구성 하 고 싶은 10 장치가 있는 경우에 192.168.0 제외 범위를 만들 수 있습니다. *x* 10 개 이상의 IP 주소를 포함 하는 범위: 192.168.0.15 통해 192.168.0.1 합니다.

여기에서 고정 IP 주소와 서버 및 다른 디바이스를 구성 하 10 제외 IP 주소를 사용 하 고 5 추가 IP 주소가 앞으로 추가 하려는 경우 하는 새 디바이스에 정적 구성에 맞게 사용할 수 있는 남아 있습니다. 이 제외 범위가 DHCP 서버 주소 풀 192.168.0.254 통해 192.168.0.16의 그대로 유지 됩니다.

다음 표에서에 AD DS 및 DNS에 대 한 자세한 예제 구성 항목 제공 됩니다.

|구성 항목|예 값|
|-----------------------|------------------|
|네트워크 연결 바인딩을|이더넷|
|DNS 서버 설정|DC1.corp.contoso.com|
|기본 설정된 DNS 서버 IP 주소|10.0.0.2|
|범위 값<br /><br />1. 범위 이름<br />2. IP 주소를 시작합니다.<br />3. 종료 IP 주소<br />4. 서브넷 마스크<br />5. 기본 게이트웨이 (선택 사항)<br />6. 임대 기간|1. 기본 서브넷<br />2.  10.0.0.1<br />3.  10.0.0.254<br />4.  255.255.255.0<br />5.  10.0.0.1<br />6. 8 일|
|IPv6 DHCP 서버 작동 모드|사용 안 함|

## <a name="bkmk_lab"></a>이 가이드를 사용 하 여 테스트 랩에

DHCP를 테스트 랩에 배포 하는 생산 환경에서 배포 하기 전에이 가이드를 사용할 수 있습니다. 

>[!NOTE]
>섹션으로 건너뜁니다 수 DHCP를 테스트 랩에 배포 하지 않을 경우 [배포 DHCP](#bkmk_deploy)합니다.

실험 요구 사항을 실제 서버 또는 \(VMs\) 가상 컴퓨터를 사용 하는 여부 및 Active Directory 도메인을 사용 하 여 또는 독립 실행형 DHCP를 배포 여부에 따라 다릅니다. 

이 가이드를 사용 하 여 DHCP 배포 테스트를 하려면 최소 리소스를 확인 하려면 다음 정보를 사용할 수 있습니다.

### <a name="test-lab-requirements-with-vms"></a>Vm 테스트 랩 요구 사항

DHCP를 Vm 테스트 랩에 배포 하려면 다음 리소스 필요 합니다.

도메인 배포 또는 독립 실행형 배포 Hyper\ V 호스트로 구성 되어 있는 한 서버가 필요 합니다.

**도메인 배포**

이 배포 하나의 물리적 서버, 가상 스위치 하나로, 두 가상 서버 및 한 가상 클라이언트 필요합니다.

실제 서버, Hyper-v 관리자 다음과 같은 항목을 만듭니다.

1. 하나 **내부** 가상 스위치를 합니다. 만드는 **외부** 가상 스위치를 Vm 테스트를 DHCP에서 IP 주소 받기 Hyper\ V 호스트 DHCP를 포함 하는 서브넷 켜져 있으면 때문 합니다. 또한 배포 하는 테스트 DHCP 서버 서브넷 Hyper\ V 호스트가 설치 되어 있는 다른 컴퓨터에 IP 주소를 할당 될 수 있습니다.
1. Windows Server 2106 실행 VM Active Directory Domain Services 가상 내부에 연결 되어 있는 도메인 컨트롤러도 구성 된 만든 전환 합니다. 이 가이드를 찾으려면이 서버 10.0.0.2의 정적으로 구성 된 IP 주소가 있어야 합니다. AD DS 배포에 대 한 내용은 섹션을 참조 **d c 배포 1** Windows Server 2016에에서 [Core 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01)합니다.
1. 하나 VM 실행 하 고 있는이 가이드를 사용 하 여 DHCP 서버로 구성는 Windows Server 2106 가상 내부에 연결 되어 만든 전환 합니다. 
1. 가상 내부에 연결 되어 있는 Windows 클라이언트 운영 체제를 실행 한 VM 전환 생성 하 고 있는지 DHCP 서버는 동적으로 IP 주소와 DHCP 옵션에 할당 DHCP 클라이언트 확인 하기 위해 사용 됩니다.

**독립 실행형 DHCP 서버 배포**

이 배포 하나의 물리적 서버, 가상 스위치 하나로, 가상 서버 및 한 가상 클라이언트 필요합니다.

실제 서버, Hyper-v 관리자 다음과 같은 항목을 만듭니다.

1. 하나 **내부** 가상 스위치를 합니다. 만드는 **외부** 가상 스위치를 Vm 테스트를 DHCP에서 IP 주소 받기 Hyper\ V 호스트 DHCP를 포함 하는 서브넷 켜져 있으면 때문 합니다. 또한 배포 하는 테스트 DHCP 서버 서브넷 Hyper\ V 호스트가 설치 되어 있는 다른 컴퓨터에 IP 주소를 할당 될 수 있습니다.
1. 하나 VM 실행 하 고 있는이 가이드를 사용 하 여 DHCP 서버로 구성는 Windows Server 2106 가상 내부에 연결 되어 만든 전환 합니다.
1. 가상 내부에 연결 되어 있는 Windows 클라이언트 운영 체제를 실행 한 VM 전환 생성 하 고 있는지 DHCP 서버는 동적으로 IP 주소와 DHCP 옵션에 할당 DHCP 클라이언트 확인 하기 위해 사용 됩니다.

### <a name="test-lab-requirements-with-physical-servers"></a>실제 서버를 테스트 랩 요구 사항

DHCP를 물리적 서버를 테스트 랩에 배포 하려면 다음 리소스 필요 합니다.

**도메인 배포**

이 배포 한 허브 또는 스위치, 두 실제 서버 실제 클라이언트 하나의 필요 다음과 같습니다.

1. 하나 이더넷 허브 또는 스위치 이더넷 케이블 물리적 컴퓨터 연결할 수 있는
1. 실제 실행 하는 컴퓨터 Windows Server 2106 된 Active Directory Domain Services 도메인 컨트롤러로 구성 되어 있습니다. 이 가이드를 찾으려면이 서버 10.0.0.2의 정적으로 구성 된 IP 주소가 있어야 합니다. AD DS 배포에 대 한 내용은 섹션을 참조 **d c 배포 1** Windows Server 2016에에서 [Core 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01)합니다.
1. 이 가이드를 사용 하 여 DHCP 서버로 구성는 Windows Server 2106 실행 한 물리적 컴퓨터 합니다. 
1. DHCP 서버 확인 하는 데 사용할 Windows 클라이언트 운영 체제를 실행 한 물리적 컴퓨터는 DHCP 클라이언트 IP 주소와 DHCP 옵션을 할당 동적으로 합니다.

>[!NOTE]
>이 배포에 대 한 테스트 컴퓨터 부족 한 경우이 구성 생산 환경 적합 하지 않지만 AD DS 및 DHCP-하나 테스트 컴퓨터를 사용할 수 있습니다.

**독립 실행형 DHCP 서버 배포**

이 배포 한 허브 또는 스위치, 하나의 물리적 서버 실제 클라이언트 하나의 필요 다음과 같습니다.

1. 하나 이더넷 허브 또는 스위치 이더넷 케이블 물리적 컴퓨터 연결할 수 있는
2. 이 가이드를 사용 하 여 DHCP 서버로 구성는 Windows Server 2106 실행 한 물리적 컴퓨터 합니다. 
3. DHCP 서버 확인 하는 데 사용할 Windows 클라이언트 운영 체제를 실행 한 물리적 컴퓨터는 DHCP 클라이언트 IP 주소와 DHCP 옵션을 할당 동적으로 합니다.


## <a name="bkmk_deploy"></a>DHCP를 배포 합니다.

이 섹션 DHCP 한 서버에 배포 하는 데 사용할 수 있는 Windows PowerShell 명령 예를 제공 합니다. 서버에서 예 명령을 실행 하기 전에 네트워크와 환경에 맞게 명령을 수정 해야 합니다. 

예를 들어 명령을 실행 하기 전에 다음과 같은 항목에 대 한 명령에 들어 값 교체 해야 합니다.

- 컴퓨터 이름
- (1 범위 서브넷 당) 구성 하려면 각 영역에 대 한 범위 IP 주소
- 서브넷 마스크 구성 하려면 각 IP 주소 범위를
- 각 영역에 대 한 범위 이름
- 각 영역에 대 한 제외 범위
- 기본 게이트웨이, 도메인 이름, WINS 또는 DNS 서버 등 DHCP 옵션 값을
- 인터페이스 이름

>[!IMPORTANT]
>귀하의 환경에 대 한 모든 명령의 명령을 실행 하기 전에 수정를 검사 합니다.

### <a name="where-to-install-dhcp---on-a-physical-computer-or-a-vm"></a>실제 컴퓨터 또는 VM 설치 DHCP-위치 있나요?

실제 컴퓨터 또는 가상 컴퓨터에 DHCP 서버 역할 설치할 수 \(VM\) Hyper\ V 호스트에 설치 되어 있는 합니다. Hyper-v 가상 스위치를에 VM 가상 네트워크 어댑터를 연결 해야 DHCP VM에서 설치 하는 경우 DHCP 서버 Hyper-v 호스트 연결 되어 실제 네트워크에서 컴퓨터에 IP 주소 할당 제공 하도록 하려면 **외부**합니다.

자세한 내용은 섹션을 참조 **Hyper-v 관리자를 사용 하 여 가상 스위치를 만들기** 항목에서 [가상 네트워크 만들](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network)합니다.

### <a name="run-windows-powershell-as-an-administrator"></a>Windows PowerShell을 관리자 권한으로 실행

다음 절차 Windows PowerShell을 관리자 권한으로 실행를 사용할 수 있습니다.

1. Windows Server 2016을 실행 하는 컴퓨터에서 클릭 **시작**, 다음 Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭 합니다. 에 메뉴가 나타납니다. 

2. 메뉴를 클릭 **더 많은**을 차례로 클릭 하 고 **관리자 권한으로 실행**합니다. 메시지가 표시 되 면 컴퓨터에서 관리자 권한이 있는 계정 자격 증명을 입력 합니다. 로그온 하는 컴퓨터에 있는 사용자 계정 수준 관리자 계정 인지 자격 증명 묻는 메시지가 나타나지 않습니다.

3. Windows PowerShell을 관리자 권한으로 엽니다.

### <a name="rename-the-dhcp-server-and-configure-a-static-ip-address"></a>고정 IP 주소를 구성 하 고 DHCP 서버 이름 바꾸기

이미 완료 하는 경우는 다음과 같은 Windows PowerShell 명령을 DHCP 서버 바꾸고 구성 서버에 대해 고정 IP 주소를 사용할 수 있습니다.

**고정 IP 주소를 구성**

올바른 DNS 서버 IP 주소와 DHCP 서버 TCP/IP 속성을 구성 하 고 DHCP 서버에 고정 IP 주소를 지정 하 뒤 다음 명령을 사용할 수 있습니다. 인터페이스 이름 및이 이때에 IP 주소를 사용 하 여 컴퓨터 구성 원하는 값으로도 교체 해야 합니다.

 `New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24`

 `Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2`

다음이 명령에 대 한 자세한 내용은 다음 항목을 참조 합니다.

- [New-NetIPAddress](https://technet.microsoft.com/itpro/powershell/windows/tcpip/new-netipaddress)
- [Set-DnsClientServerAddress](https://technet.microsoft.com/itpro/powershell/windows/dns-client/set-dnsclientserveraddress)

**컴퓨터 이름 바꾸기**

다음 명령을 바꾼 후 컴퓨터를 다시 시작을 사용할 수 있습니다.

`Rename-Computer -Name DHCP1`

 `Restart-Computer`

다음이 명령에 대 한 자세한 내용은 다음 항목을 참조 합니다.

- [Rename-Computer](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/rename-computer)
- [Restart-Computer](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/restart-computer)

### <a name="join-the-computer-to-the-domain-optional"></a>컴퓨터에서 도메인 \(Optional\)에 가입

DHCP 서버 Active Directory 도메인 환경으로 설치 하는 컴퓨터가 도메인에 속해야 합니다. 관리자 권한으로 Windows PowerShell 열고 도메인 NetBios 이름을 바꾼 후 다음 명령을 실행 **CORP** 귀하의 환경에 대 한 적절 한 값으로 합니다.

    Add-Computer CORP

메시지가 표시 되는 경우에 컴퓨터에서 도메인에 가입 수 있는 권한이 있는 사용자 계정 도메인에 대 한 자격 증명을 입력 합니다. 

    Restart-Computer

Add-Computer 명령에 대 한 자세한 내용은 다음 항목을 참조 합니다.

- [Add-Computer](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/add-computer)

### <a name="install-dhcp"></a>DHCP를 설치 합니다.

컴퓨터를 다시 시작한 후 Windows PowerShell을 관리자 권한으로 엽니다 하 고 DHCP 다음 명령을 실행 하 여 설치 합니다.

    Install-WindowsFeature DHCP -IncludeManagementTools

이 명령에 대 한 자세한 내용은 다음 항목을 참조 합니다.

- [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/server-manager/install-windowsfeature)

### <a name="create-dhcp-security-groups"></a>DHCP 보안 그룹 만들기

보안 그룹을 만들려면 Windows PowerShell에서 네트워크 셸 \(netsh\) 명령을 실행 하 고 DHCP 서비스를 다시 시작 하는 새 그룹 활성화 됩니다 되도록 해야 합니다.

DHCP 서버의 netsh 다음 명령을 실행 될 때의 **DHCP 관리자** 및 **DHCP 사용자** 보안 그룹에서 만든 **로컬 사용자 및 그룹** DHCP 서버에서 합니다.

    netsh dhcp add securitygroups

다음 명령을 로컬 컴퓨터에서 DHCP 서비스 다시 시작합니다.

    Restart-service dhcpserver

다음이 명령에 대 한 자세한 내용은 다음 항목을 참조 합니다.

- [네트워크 셸 (Netsh)](../netsh/netsh.md)
- [Restart-Service](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/restart-service)

### <a name="authorize-the-dhcp-server-in-active-directory-optional"></a>DHCP 서버 Active Directory \(Optional\)에 권한을 부여합니다

DHCP를 설치 하는 도메인 환경에서 도메인에서 작동 하도록 DHCP 서버 권한을 부여 하려면 다음 단계를 수행 해야 합니다.

>[!NOTE]
>도메인 Active Directory에 설치 되어 있는 무단된 DHCP 서버 제대로 작동 하지 않을 수 및 IP 주소 DHCP 클라이언트를 임대 하지 않습니다. 무단 DHCP 서버의 자동 비활성화 무단된 DHCP 서버 클라이언트 네트워크에 잘못 된 IP 주소를 지정 하는 방법 하지 못하게 되는 보안 기능입니다.

DHCP 서버 Active Directory에 DHCP 서버 인증 된 목록에 추가 하려면 다음 명령을 사용할 수 있습니다. 

>[!NOTE]
>도메인 환경 없는 경우이 명령을 실행 되지 않습니다.

 `Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com -IPAddress 10.0.0.3`

DHCP 서버가 Active Directory에 권한이 있는지를 확인 하려면 다음 명령을 사용할 수 있습니다.

    Get-DhcpServerInDC

다음은 Windows PowerShell에 표시 되는 결과 예입니다.

    
        IPAddress   DnsName
        ---------   -------
        10.0.0.3    DHCP1.corp.contoso.com
    

다음이 명령에 대 한 자세한 내용은 다음 항목을 참조 합니다.

- [Add-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverindc)
- [Get-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc)

### <a name="notify-server-manager-that-post-install-dhcp-configuration-is-complete-optional"></a>구성을 완료 \(Optional\)는 서버 관리자 해당 post\ 설치 DHCP 알림

보안 그룹을 만들고 Active Directory에 DHCP 서버 승인 등 post\ 설치 작업을 완료 한 후 서버 관리자에 DHCP 게시물 설치 구성 마법사를 사용 하 여 post\ 설치 단계를 완료 해야 한다는 사용자 인터페이스에서 알림을 여전히 표시 될 수 있습니다.

이 Windows PowerShell 명령을 사용 하 여 다음 레지스트리 키를 구성 하 여 서버 관리자에 표시 되지 않는이 now\ 불필요 한 부정확 한 메시지를 방지할 수 있습니다.

    Set-ItemProperty –Path registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12 –Name ConfigurationState –Value 2

이 명령에 대 한 자세한 내용은 다음 항목을 참조 합니다.

- [Set-ItemProperty](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/set-itemproperty?f=255&MSPPError=-2147217396)

### <a name="set-server-level-dns-dynamic-update-configuration-settings-optional"></a>서버 수준 DNS 동적 업데이트 구성 설정 \(Optional\) 설정

업데이트 하는 데 DNS 동적 DHCP 클라이언트 컴퓨터에 대 한 DHCP 서버 하려는 경우이 설정을 사용 하려면 다음 명령의 실행할 수 있습니다. 설정, 설정 하지 않는 한 범위 수준, 서버에서 구성 모든 범위에 영향을 하 않도록 서버 수준입니다. 도이 예 명령을 클라이언트 이상 만료 되 면 리소스 DNS 레코드 클라이언트에 대 한 삭제할 DHCP 서버를 구성 합니다.

    Set-DhcpServerv4DnsSetting -ComputerName "DHCP1.corp.contoso.com" -DynamicUpdates "Always" -DeleteDnsRRonLeaseExpiry $True

다음 명령을 DHCP 서버 하거나 등록 취소할 DNS 서버에 기록 클라이언트를 사용 하 여 자격 증명을 구성에 사용할 수 있습니다. 이 이때 자격 증명을 DHCP 서버에 저장합니다. 첫 번째 명령을 사용 하 여 **Get 자격 증명** 만들 수는 **PSCredential** 개체를의 개체를 저장 하는 **$Credential** 변수 합니다. 명령 사용자 이름 및 암호를 묻는 구분 하므로 DNS 서버에 기록 리소스를 업데이트할 수 있는 권한이 있는 계정 자격 증명을 제공 합니다.

    
    $Credential = Get-Credential
    Set-DhcpServerDnsCredential -Credential $Credential -ComputerName "DHCP1.corp.contoso.com"
    

다음이 명령에 대 한 자세한 내용은 다음 항목을 참조 합니다.

- [설정 DhcpServerv4DnsSetting](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4dnssetting)
- [Set-DhcpServerDnsCredential](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverdnscredential)

### <a name="configure-the-corpnet-scope"></a>회사 범위 구성

DHCP 설치가 완료 되 면 구성 하 고 회사 범위를 활성화, 제외 범위 범위를에 대 한 만들고 구성 하 고 DHCP 옵션 기본 게이트웨이, DNS 서버 IP 주소, DNS 도메인 이름 뒤 다음 명령을 사용할 수 있습니다.

    
    Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active`
    
    Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15`
    
    Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com`
    
    Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2
    

다음이 명령에 대 한 자세한 내용은 다음 항목을 참조 합니다.

- [추가 DhcpServerv4Scope](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4scope)
- [추가 DhcpServerv4ExclusionRange](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4exclusionrange)
- [설정 DhcpServerv4OptionValue](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4optionvalue)

### <a name="configure-the-corpnet2-scope-optional"></a>Corpnet2 구성 \(Optional\) 범위

두 번째 서브넷 라우터 첫 번째 서브넷에 연결 된 DHCP 전달이 활성화 되어 있는 경우이 예 Corpnet2 라는 두 번째 범위를 추가 하려면 뒤 다음 명령을 사용할 수 있습니다. 이 이때 제외 범위 및 IP 주소를 기본 게이트웨이 구성 \ (의 subnet\에서 라우터의 IP 주소) Corpnet2 서브넷 합니다.

 `Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active`

 `Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15`

 `Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com`

이 DHCP 서버에서 처리 하는 추가 서브넷을 사용 하는 경우 모든 명령 매개에 대 한 다양 한 값을 사용 하 여 각 서브넷 범위를 추가 하려면 이러한 명령 반복 수 있습니다.

>[!IMPORTANT]
>DHCP 클라이언트 및 서버 DHCP 간에 모든 라우터에서 DHCP 메시지를 전달 구성 되어 있는지 확인 합니다. 자세한 내용은 라우터 설명서를 참조 구성 DHCP 전달 하는 방법에 합니다.

## <a name="bkmk_verify"></a>서버 기능을 확인

DHCP 서버의 IP 주소 동적 할당 DHCP 클라이언트 제공 하는 것을 확인 하려면 다른 컴퓨터 서브넷 서비스에 연결할 수 있습니다. 이더넷 케이블이 네트워크 어댑터와 컴퓨터의 전원에 연결한 후 IP 주소 DHCP에서 요청 합니다. 성공한 구성을 사용 하 여 확인할 수 있습니다는 **ipconfig /all** 명령을 선택 하 고 결과 검토 하거나 연결 테스트를 수행 하 여와 같은 하려고 할 때 다른 응용 프로그램 또는 Windows 탐색기 브라우저나 파일 공유에 사용 하 여 웹 리소스에 액세스 합니다.

클라이언트에서 DHCP에서 IP 주소를 받지 못하면 다음 문제 해결 단계를 수행 합니다.

1. 이더넷 케이블이 모두 컴퓨터 및 이더넷 스위치, 허브, 또는 라우터에에 연결 되어 있는지 확인 합니다.
1. 라우터에서 DHCP 서버에서 분리 되어 네트워크 세그먼트로 클라이언트 컴퓨터를 연결 하는 경우는 라우터에서 DHCP 메시지를 전달 하도록 구성 되어 있는지 확인 합니다.
1. 인증 된 DHCP 서버 목록 Active Directory에서 검색 하 고 다음 명령을 실행 DHCP 서버 Active Directory에 권한이 있는지 확인 합니다. [Get DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc)합니다.
1. 여 범위 DHCP 콘솔을 열어서 활성화 되어 있는지 확인 \ (서버 관리자 **도구**, **DHCP**\), 범위 right\ 클릭 한 다음을 검토 하기 위해 서버 트리 각 범위를 확장 합니다. 결과 메뉴는 선택 항목이 포함 되어 있는 경우 **정품 인증**, 클릭 **정품 인증**합니다. \ (메뉴를 선택 하 고 읽고 범위 이미 정품 인증 된 경우 **비활성화**. \) 

## <a name="bkmk_dhcpwps"></a>Windows PowerShell DHCP에 대 한 명령

다음 참조 Windows Server 2016에 대 한 모든 DHCP 서버 Windows PowerShell 명령에 대해 설명 명령 및 구문을 제공합니다. 항목 명령을 같은 명령의 시작 부분에 고 동사 기반 알파벳 순서로 나열 **다운로드** 또는 **설정**합니다.

>[!NOTE]
>Windows Server 2016 명령 Windows Server 2012 r 2에 사용할 수 없습니다.

- [DhcpServer 모듈](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/index)

다음 참조 Windows Server 2012 r 2에 대 한 모든 DHCP 서버 Windows PowerShell 명령에 대해 설명 명령 및 구문을 제공합니다. 항목 명령을 같은 명령의 시작 부분에 고 동사 기반 알파벳 순서로 나열 **다운로드** 또는 **설정**합니다.

>[!NOTE]
>Windows Server 2012 r 2 명령 Windows Server 2016에 사용할 수 있습니다.

- [Windows PowerShell DHCP 서버 Cmdlet](https://technet.microsoft.com/library/jj590751.aspx)

## <a name="bkmk_list"></a>이 가이드 Windows PowerShell 명령 목록

다음은 다양 한 명령과 예제 값이이 설명서에서 사용 되는 간단한 목록입니다.

    
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
    


