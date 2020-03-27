---
title: Windows Server 및 Windows 10에 대한 Always On VPN 배포
description: 이 배포를 사용 하 여 Windows Server 2016 이상에서 원격 액세스를 사용 하 여 원격 직원의 VPN (가상 사설망) 연결 Always On 배포 하 고 Windows 10 클라이언트 컴퓨터에 대 한 Always On VPN 프로필을 배포할 수 있습니다.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 5ae1a40b-4f10-4ace-8aaf-13f7ab581f4f
ms.localizationpriority: medium
ms.date: 12/20/2018
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ca064f887a524c5f41b29837e8f8fec586a8d928
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313262"
---
# <a name="always-on-vpn-deployment-for-windows-server-and-windows-10"></a>Windows Server 및 Windows 10에 대 한 Always On VPN 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**이전:** 원격 액세스](../../../Remote-Access.md)<br>
- [**다음:** Always On VPN 기능 및 기능에 대 한 자세한 정보](../../vpn-map-da.md)

Always On VPN은 원격 액세스를 위한 단일의 통합 된 솔루션을 제공 하 고 도메인에 가입 된 (작업 그룹) 또는 Azure AD-조인 된 장치 (개인적으로 소유 하는 장치 포함)를 지원 합니다. Always On VPN을 사용하는 경우 연결 형식이 사용자 또는 디바이스만으로 지정될 필요가 없지만 둘 모두를 조합할 수는 있습니다. 예를 들어 원격 디바이스 관리를 위해 디바이스 인증을 사용하도록 설정한 다음, 내부 회사 사이트 및 서비스에 연결하는 데 사용자 인증을 사용하도록 설정할 수 있습니다.

## <a name="prerequisites"></a>필수 조건

Always On VPN을 배포 하는 데 사용할 수 있는 기술이 배포 되어 있을 가능성이 높습니다. Always On VPN 배포에는 DC/DNS 서버 외에 NPS (RADIUS) 서버, CA (인증 기관) 서버 및 원격 액세스 (라우팅/v m) 서버가 필요 합니다. 인프라를 설정한 후에는 클라이언트를 등록 한 다음 여러 네트워크 변경을 통해 클라이언트를 온-프레미스에 안전 하 게 연결 해야 합니다.

- 하나 이상의 DNS (Domain Name System) 서버를 포함 하는 도메인 인프라를 Active Directory 합니다. 내부 및 외부 DNS (Domain Name System) 영역이 모두 필요 합니다 .이는 내부 영역이 외부 영역 (예: corp.contoso.com 및 contoso.com)의 위임 된 하위 도메인 이라고 가정 합니다.
- Active Directory 기반 PKI (공개 키 인프라) 및 Active Directory 인증서 서비스 (AD CS).
- NPS (네트워크 정책 서버)를 설치할 서버 (가상 또는 물리적, 기존 또는 새 서버)입니다. 네트워크에 NPS 서버가 이미 있는 경우 새 서버를 추가 하지 않고 기존 NPS 서버 구성을 수정할 수 있습니다.
- IKEv2 VPN 연결 및 LAN 라우팅을 지 원하는 작은 기능 하위 집합을 사용 하는 RAS 게이트웨이 VPN 서버로 원격 액세스
- 두 개의 방화벽을 포함 하는 경계 네트워크입니다.  방화벽에서 VPN 및 RADIUS 통신이 모두 제대로 작동 하는 데 필요한 트래픽을 허용 하는지 확인 합니다. 자세한 내용은 [ALWAYS ON VPN 기술 개요](../always-on-vpn-technology-overview.md)를 참조 하세요.
- 원격 액세스를 RAS Gateway VPN 서버로 설치 하기 위한 두 개의 실제 이더넷 네트워크 어댑터를 사용 하는 경계 네트워크의 물리적 서버 또는 VM (가상 머신). Vm에는 호스트의 VLAN (가상 LAN)이 필요 합니다. 
- 관리자 또는 이와 동등한 멤버 자격이 최소한 필요 합니다.
- 배포를 수행 하기 전에이 배포에 대 한 준비가 되었는지 확인 하려면이 가이드의 계획 섹션을 참조 하세요.
- 사용 되는 각 기술에 대 한 디자인 및 배포 가이드를 검토 합니다. 이러한 가이드는 배포 시나리오에서 조직의 네트워크에 필요한 서비스 및 구성을 제공 하는지 여부를 확인 하는 데 도움이 될 수 있습니다. 자세한 내용은 [ALWAYS ON VPN 기술 개요](../always-on-vpn-technology-overview.md)를 참조 하세요.
- CSP가 공급 업체에 한정 되지 않으므로 Always On VPN 구성을 배포 하기 위해 선택한 관리 플랫폼입니다.

>[!IMPORTANT]
>이 배포의 경우 Active Directory Domain Services를 실행 하는 컴퓨터, Active Directory 인증서 서비스 및 네트워크 정책 서버와 같은 인프라 서버에서 Windows Server 2016를 실행 해야 합니다. Windows Server 2012 R2와 같은 이전 버전의 Windows Server를 인프라 서버 및 원격 액세스를 실행 하는 서버에 사용할 수 있습니다.
>
>Microsoft Azure에서 VM (가상 컴퓨터)에 대 한 원격 액세스를 배포 하지 마십시오. 원격 액세스 VPN 및 DirectAccess를 포함 하 여 Microsoft Azure에서 원격 액세스를 사용할 수 없습니다. 자세한 내용은 [Microsoft Azure 가상 컴퓨터에 대 한 Microsoft 서버 소프트웨어 지원](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)을 참조 하세요.

## <a name="about-this-deployment"></a>이 배포 정보

제공 된 지침은 Windows 10을 실행 하는 원격 클라이언트 컴퓨터에 대해 아래에 설명 된 시나리오를 사용 하 여 지점 및 사이트 간 VPN 연결에 대 한 단일 테 넌 트 VPN RAS 게이트웨이로 원격 액세스를 배포 하는 과정을 안내 합니다. 또한 배포에 대 한 기존 인프라의 일부를 수정 하는 방법에 대 한 지침을 찾을 수 있습니다. 또한이 배포 전체에서 VPN 연결 프로세스, 구성할 서버, 프로 파일링 VPNv2 CSP 노드 및 Always On VPN을 배포 하는 기타 기술에 대 한 자세한 정보를 확인할 수 있는 링크를 찾을 수 있습니다.

**Always On VPN 배포 시나리오:**

1. Always On VPN만 배포 합니다.
2. Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 사용 하 Always On VPN을 배포 합니다.

제공 되는 시나리오에 대 한 자세한 내용 및 워크플로는 [ALWAYS ON VPN 배포](always-on-vpn-deploy-deployment.md)를 참조 하세요.

## <a name="what-isnt-provided-in-this-deployment"></a>이 배포에서 제공 되지 않는 기능

이 배포는 다음에 대 한 지침을 제공 하지 않습니다.

- Active Directory Domain Services (AD DS).
- 인증서 서비스 (AD CS)와 PKI (공개 키 인프라)를 Active Directory 합니다.
- DHCP (Dynamic Host Configuration Protocol)
- 이더넷 케이블 연결, 방화벽, 스위치 및 허브와 같은 네트워크 하드웨어
- 원격 사용자가 Always On VPN 연결을 통해 액세스할 수 있는 응용 프로그램 및 파일 서버와 같은 추가 네트워크 리소스입니다.
- Azure AD를 사용 하는 인터넷 연결에 대 한 인터넷 연결 또는 조건부 액세스. 자세한 내용은 [Azure Active Directory의 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)를 참조 하세요.

## <a name="next-steps"></a>다음 단계

- [Always On VPN 기능 및 기능에 대 한 자세한 정보](../../vpn-map-da.md)

- [Always On VPN 개선 사항에 대 한 자세한 정보](../always-on-vpn-enhancements.md)

- [몇 가지 고급 Always On VPN 기능에 대해 알아봅니다.](always-on-vpn-adv-options.md)

- [Always On VPN 기술에 대 한 자세한 정보](../always-on-vpn-technology-overview.md)

- [Always On VPN 배포 계획 시작](always-on-vpn-deploy-deployment.md)