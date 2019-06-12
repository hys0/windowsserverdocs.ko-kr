---
title: Always On VPN 배포 계획 수립
description: 이 항목에서는 Always On VPN Windows Server 2016에 배포 하기 위한 계획 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 3c9de3ec-4bbd-4db0-b47a-03507a315383
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 11/05/2018
ms.openlocfilehash: db309f451eb9187463f71dfd85a82d214c464e2b
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749462"
---
# <a name="step-1-plan-the-always-on-vpn-deployment"></a>1단계. Always On VPN 배포 계획

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**이전:** Always On VPN을 배포 하기 위한 워크플로 알아보기](always-on-vpn-deploy-deployment.md)
- [**다음:** 2단계. Server 인프라 구성](vpn-deploy-server-infrastructure.md)

이 단계를 계획 하 고 Always On VPN 배포 준비를 시작 합니다. VPN 서버를 사용 하 여 계획 하는 컴퓨터에 원격 액세스 서버 역할을 설치 하기 전에 다음 작업을 수행 합니다. 적절 한 계획 한 후에 Always On VPN을 배포할 수 있으며 필요에 따라 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성할 수 있습니다.

[!INCLUDE [always-on-vpn-standard-config-considerations-include](../../../includes/always-on-vpn-standard-config-considerations-include.md)]

## <a name="prepare-the-remote-access-server"></a>원격 액세스 서버를 준비 합니다.

VPN 서버로 사용 되는 컴퓨터에서 다음을 수행 해야 합니다.

- **VPN 서버 소프트웨어 및 하드웨어 구성이 올바른지 확인**합니다. 원격 액세스 VPN 서버로 사용 하려는 컴퓨터의 Windows Server 2016을 설치 합니다. 이 서버에 설치 하는 두 개의 실제 네트워크 어댑터, 외부 경계 네트워크에 연결할 하나 및 하나 내부 경계 네트워크에 연결할 있어야 합니다.

- **네트워크 어댑터를 인터넷에 연결 하 고 개인 네트워크에 연결 된 네트워크 어댑터를 식별**합니다. 로컬 네트워크에서 IP 주소를 사용 하 여 인트라넷 연결 어댑터 있지만 공용 IP 주소를 사용 하 여 인터넷 연결 네트워크 어댑터를 구성 합니다.

    >[!TIP]
    >경계 네트워크에서 공용 IP 주소를 사용 하지 않으려는 경우에 공용 IP 주소를 사용 하 여 경계 면 방화벽을 구성 하 고 VPN 서버에 VPN 연결 요청을 전달 하도록 방화벽을 구성할 수 있습니다.

- **VPN 서버를 네트워크에 연결할**합니다. 경계 네트워크에 지 방화벽 경계 방화벽 사이 VPN 서버를 설치 합니다.

## <a name="plan-authentication-methods"></a>인증 방법 계획

IKEv2는 터널링 프로토콜에 설명 된 VPN [Internet Engineering Task Force에 대 한 요청 주석을 7296](https://datatracker.ietf.org/doc/rfc7296/)합니다. IKEv2의 주요 이점은 기본 네트워크 연결에서 중단을 허용 하는 경우 예를 들어, 아니면에서 클라이언트 컴퓨터를 이동할 경우 연결이 일시적으로 손실 하나의 네트워크 간에 네트워크 연결 IKEv2를 다시 설정 하는 경우 VPN 연결이 자동으로 복원 — 사용자 개입 없이 합니다.

>[!TIP]
>서버의 보안 공간을 줄일도 사용 되지 않는 프로토콜을 사용 하지 않도록 설정 하는 동안 IKEv2 연결을 지원 하도록 원격 액세스 VPN 서버를 구성할 수 있습니다. 

## <a name="plan-ip-addresses-for-remote-clients"></a>원격 클라이언트에 대 한 IP 주소 계획

VPN 클라이언트를 구성 하는 고정 주소 풀에서 주소 또는 DHCP 서버에서 IP 주소를 할당 하도록 VPN 서버를 구성할 수 있습니다. 

## <a name="prepare-the-environment"></a>환경 준비

- **외부 방화벽을 구성 하는 권한이 있고 유효한 공용 IP 주소를 있는지**합니다. IKEv2 VPN 연결을 지원 하려면 방화벽에서 포트를 엽니다. 외부 클라이언트에서 연결을 허용 하도록 공용 IP 주소를 해야 합니다.

- **VPN 클라이언트에 대 한 고정 IP 주소 범위를 선택**합니다. 지원 하려는 동시 VPN 클라이언트의 최대 수를 결정 합니다. 또한 namely 요구 사항을 충족 하기 위해 내부 경계 네트워크의 고정 IP 주소 범위를 계획 합니다 *고정 주소 풀*합니다. DHCP를 사용 하 여 내부 DMZ에서 IP 주소를 제공 하는 경우 DHCP에 이러한 고정 IP 주소에 대 한 제외를 만들려고 할 수도 있습니다.

- **공용 DNS 영역을 편집할 수 있는지 확인**합니다. VPN 인프라를 지 원하는 공용 DNS 도메인에 DNS 레코드를 추가 합니다. 

- **모든 VPN 사용자가 Active Directory 사용자 (AD DS)에 대 한 사용자 계정이 있는지**합니다. 사용자는 VPN 연결을 사용 하 여 네트워크에 연결할 수 있습니다, 전에 AD DS에서 사용자 계정이 있어야 합니다.

## <a name="prepare-routing-and-firewall"></a>라우팅 준비 및 방화벽 

내부 및 외부 경계 네트워크에 경계 네트워크를 분할 하는 경계 네트워크 내 VPN 서버를 설치 합니다. 네트워크 환경에 따라 여러 라우팅 수정 해야 합니다.

- **(선택 사항) 포트 전달을 구성 합니다.** 에 지 방화벽의 포트 및 프로토콜 IKEv2 VPN과 사용 하 여 연결 된 Id 열고 VPN 서버에 전달 합니다. 대부분의 환경에서 이렇게 하려면 해야 포트 전달을 구성할 수 있습니다. 유니버설 데이터 그램 프로토콜 (UDP) 포트를 500과 4500 VPN 서버로 리디렉션하십시오.

- **DNS 서버 및 VPN 서버에서 인터넷에 액세스할 수 있도록 라우팅 구성**합니다. 이 배포는 IKEv2 및 네트워크 주소 변환 (NAT)를 사용합니다. VPN 서버 모두에 필요한 내부 네트워크 및 네트워크 리소스를 연결할 수 있는지 확인 합니다. 모든 네트워크 또는 VPN 서버에서 연결할 수 없는 리소스 연결 되지 않습니다도 원격 위치에서 VPN 연결을 통해.

대부분의 환경에서 새 내부 경계 네트워크를 연결할 VPN 서버가 경계 면 방화벽에 고정 경로 조정 합니다. 그러나 더 복잡 한 환경에서 내부 라우터를 정적 경로 추가 하거나 VPN 서버 및 VPN 클라이언트를 사용 하 여 연결 된 IP 주소 블록에 대 한 내부 방화벽 규칙을 조정 해야 할 수 있습니다.

## <a name="next-steps"></a>다음 단계

[2단계. Server 인프라 구성](vpn-deploy-server-infrastructure.md): 이 단계에서는 설치 및 VPN을 지 원하는 데 필요한 서버 측 구성 요소를 구성 합니다. 서버 쪽 구성 요소 사용자, VPN 서버와 NPS 서버에서 사용 된 인증서를 배포 하는 PKI를 구성 하는 포함 됩니다.