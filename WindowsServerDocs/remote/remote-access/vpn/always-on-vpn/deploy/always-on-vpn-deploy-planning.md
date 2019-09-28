---
title: Always On VPN 배포 계획 수립
description: 이 항목에서는 Windows Server 2016에 Always On VPN을 배포 하는 방법에 대 한 계획 지침을 제공 합니다.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 3c9de3ec-4bbd-4db0-b47a-03507a315383
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 11/05/2018
ms.openlocfilehash: f92cfdbe13633dd4c59012f566c6888fdc7fc7a1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388162"
---
# <a name="step-1-plan-the-always-on-vpn-deployment"></a>1단계. Always On VPN 배포 계획

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**선행** Always On VPN을 배포 하기 위한 워크플로에 대해 알아보기](always-on-vpn-deploy-deployment.md)
- [**그런** 2단계. 서버 인프라 구성](vpn-deploy-server-infrastructure.md)

이 단계에서는 Always On VPN 배포 계획 및 준비를 시작 합니다. 를 VPN 서버로 사용 하려는 컴퓨터에 원격 액세스 서버 역할을 설치 하기 전에 다음 작업을 수행 합니다. 적절 한 계획 후에 Always On VPN을 배포 하 고, 선택적으로 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성할 수 있습니다.

[!INCLUDE [always-on-vpn-standard-config-considerations-include](../../../includes/always-on-vpn-standard-config-considerations-include.md)]

## <a name="prepare-the-remote-access-server"></a>원격 액세스 서버 준비

VPN 서버로 사용 되는 컴퓨터에서 다음을 수행 해야 합니다.

- **VPN 서버 소프트웨어 및 하드웨어 구성이 올바른지 확인**하십시오. 원격 액세스 VPN 서버로 사용할 컴퓨터에 Windows Server 2016을 설치 합니다. 이 서버에는 두 개의 실제 네트워크 어댑터가 설치 되어 있어야 합니다. 하나는 외부 경계 네트워크에 연결 하 고 다른 하나는 내부 경계 네트워크에 연결 합니다.

- **인터넷에 연결 되는 네트워크 어댑터와 개인 네트워크에 연결**하는 네트워크 어댑터를 식별 합니다. 공용 IP 주소를 사용 하 여 인터넷에 연결 되는 네트워크 어댑터를 구성 하 고, 인트라넷을 향하는 어댑터는 로컬 네트워크의 IP 주소를 사용할 수 있습니다.

    >[!TIP]
    >경계 네트워크에서 공용 IP 주소를 사용 하지 않으려는 경우 공용 IP 주소를 사용 하 여에 지 방화벽을 구성 하 고 vpn 연결 요청을 VPN 서버로 전달 하도록 방화벽을 구성할 수 있습니다.

- **VPN 서버를 네트워크에 연결**합니다. 경계 네트워크에 경계 네트워크, 경계 방화벽 사이에 VPN 서버를 설치 합니다.

## <a name="plan-authentication-methods"></a>인증 방법 계획

IKEv2는 [인터넷 엔지니어링 작업 Force Request For Comments 7296](https://datatracker.ietf.org/doc/rfc7296/)에 설명 된 VPN 터널링 프로토콜입니다. IKEv2의 주요 이점은 기본 네트워크 연결의 중단을 허용는 것입니다. 예를 들어 일시적으로 연결이 끊어지거나 사용자가 클라이언트 컴퓨터를 한 네트워크에서 다른 네트워크로 이동 하는 경우 네트워크 연결 IKEv2를 다시 조정 하면 사용자의 개입 없이 VPN 연결을 자동으로 복원 합니다.

>[!TIP]
>IKEv2 연결을 지원 하도록 원격 액세스 VPN 서버를 구성 하 고 사용 하지 않는 프로토콜을 사용 하지 않도록 설정 하 여 서버의 보안 공간을 줄일 수 있습니다. 

## <a name="plan-ip-addresses-for-remote-clients"></a>원격 클라이언트에 대 한 IP 주소 계획

구성 하는 고정 주소 풀 또는 DHCP 서버에서 IP 주소에서 VPN 클라이언트에 주소를 할당 하도록 VPN 서버를 구성할 수 있습니다. 

## <a name="prepare-the-environment"></a>환경 준비

- **외부 방화벽을 구성할 수 있는 권한이 있고 유효한 공용 IP 주소가 있는지 확인**합니다. 방화벽에서 포트를 열어 IKEv2 VPN 연결을 지원 합니다. 외부 클라이언트의 연결을 허용 하는 공용 IP 주소도 필요 합니다.

- **VPN 클라이언트의 고정 IP 주소 범위를 선택**합니다. 지원 하려는 동시 VPN 클라이언트의 최대 수를 결정 합니다. 또한 내부 경계 네트워크에서 해당 요구 사항을 충족 하는 고정 IP 주소 (즉, *고정 주소 풀*)의 범위를 계획 합니다. DHCP를 사용 하 여 내부 DMZ에 IP 주소를 제공 하는 경우 DHCP에서 이러한 고정 IP 주소에 대 한 제외를 만들어야 할 수도 있습니다.

- **공용 DNS 영역을 편집할 수 있는지 확인**합니다. 공용 DNS 도메인에 DNS 레코드를 추가 하 여 VPN 인프라를 지원 합니다. 

- **모든 VPN 사용자에 게 Active Directory 사용자 (AD DS)의 사용자 계정이 있는지 확인**합니다. 사용자가 VPN 연결을 사용 하 여 네트워크에 연결할 수 있으려면 먼저 AD DS 사용자 계정이 있어야 합니다.

## <a name="prepare-routing-and-firewall"></a>라우팅 및 방화벽 준비 

경계 네트워크를 내부 및 외부 경계 네트워크로 분할 하는 경계 네트워크 내에 VPN 서버를 설치 합니다. 네트워크 환경에 따라 몇 가지 라우팅 수정 작업을 수행 해야 할 수도 있습니다.

- **필드 포트 전달을 구성 합니다.** 에 지 방화벽은 IKEv2 VPN과 연결 된 포트 및 프로토콜 Id를 열고 VPN 서버로 전달 해야 합니다. 대부분의 환경에서 이렇게 하려면 포트 전달을 구성 해야 합니다. UDP (Universal 데이터 그램 프로토콜) 포트 500 및 4500을 VPN 서버로 리디렉션합니다.

- **DNS 서버 및 VPN 서버가 인터넷에 연결할 수 있도록 라우팅을 구성**합니다. 이 배포에서는 IKEv2 및 NAT (Network Address Translation)를 사용 합니다. VPN 서버가 필요한 모든 내부 네트워크 및 네트워크 리소스에 연결할 수 있는지 확인 합니다. 또한 VPN 서버에서 연결할 수 없는 네트워크 또는 리소스는 원격 위치에서 VPN 연결을 통해 연결할 수 없습니다.

대부분의 환경에서 새로운 내부 경계 네트워크에 연결 하려면에 지 방화벽 및 VPN 서버에서 고정 경로를 조정 합니다. 그러나 더 복잡 한 환경에서는 내부 라우터에 고정 경로를 추가 하거나 vpn 서버 및 VPN 클라이언트와 연결 된 IP 주소 블록에 대 한 내부 방화벽 규칙을 조정 해야 할 수 있습니다.

## <a name="next-steps"></a>다음 단계

[2단계. 서버 인프라](vpn-deploy-server-infrastructure.md)구성: 이 단계에서는 VPN을 지 원하는 데 필요한 서버 쪽 구성 요소를 설치 하 고 구성 합니다. 서버 쪽 구성 요소에는 사용자, VPN 서버 및 NPS 서버에서 사용 하는 인증서를 배포 하도록 PKI를 구성 하는 작업이 포함 됩니다.