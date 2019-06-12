---
title: Windows Server 및 Windows 10에 대한 Always On VPN 배포
description: Windows 10 클라이언트 컴퓨터에 대 한 이상 Windows Server 2016에서 원격 액세스 및 Always On VPN 프로필을 사용 하 여 원격 직원에 대 한 Always On 가상 개인 네트워크 (VPN) 연결을 배포 하려면이 배포를 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 5ae1a40b-4f10-4ace-8aaf-13f7ab581f4f
ms.localizationpriority: medium
ms.date: 12/20/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 533f0273f6802be209ae5ad79b57f46dd6775149
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749466"
---
# <a name="always-on-vpn-deployment-for-windows-server-and-windows-10"></a>Windows Server 및 Windows 10에 대 한 always On VPN 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**이전:** 원격 액세스](../../../Remote-Access.md)<br>
- [**다음:** Always On VPN 기능 알아보기](../../vpn-map-da.md)

Always On VPN 원격 액세스를 지 원하는 도메인에 가입 된 응집력 있는 단일 솔루션, 비도메인 가입 (작업 그룹) 또는 개인적으로 소유한 장치 Azure AD-조인 된 장치를 제공 합니다. Always On VPN을 사용하는 경우 연결 형식이 사용자 또는 디바이스만으로 지정될 필요가 없지만 둘 모두를 조합할 수는 있습니다. 예를 들어 원격 디바이스 관리를 위해 디바이스 인증을 사용하도록 설정한 다음, 내부 회사 사이트 및 서비스에 연결하는 데 사용자 인증을 사용하도록 설정할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

가장 가능성이 높은 기술 있는 Always On VPN을 배포 하는 데 사용할 수 있는 배포 합니다. DC/DNS 서버 이외의 Always On VPN 배포에는 NPS (RADIUS) 서버, CA (인증 기관) 서버 및 원격 액세스 (라우팅 및 VPN) 서버에 필요합니다. 인프라 설정 되 면에 클라이언트를 등록 하 고 온-프레미스 네트워크의 여러 변경 내용을 통해 안전 하 게에 클라이언트를 연결 해야 합니다.

- Active Directory 도메인 인프라, 하나 이상의 도메인 이름 시스템 (DNS) 서버를 포함 합니다. 내부 및 외부 도메인 이름 시스템 (DNS) 영역은 필요한 경우 내부 영역 외부 영역 (예: corp.contoso.com 및 contoso.com)의 하위 도메인 위임된 이라고 가정입니다.
- Active Directory 기반 PKI (공개 키 인프라) 및 Active Directory 인증서 서비스 (AD CS).
- 서버에서 가상 또는 물리적, 기존 또는 새 서버 NPS (네트워크 정책)를 설치 합니다. 네트워크의 NPS 서버가 이미 있는 경우 새 서버를 추가 하는 대신 기존 NPS 서버 구성을 수정할 수 있습니다.
- IKEv2 VPN 연결 및 라우팅 LAN을 지 원하는 기능의 작은 하위 집합을 사용 하 여 RAS 게이트웨이 VPN 서버로 원격 액세스 합니다.
- 두 개의 방화벽을 포함 하는 경계 네트워크  방화벽이 제대로 작동 하려면 VPN 및 RADIUS 통신 하기 위해 필요한 트래픽을 허용 하는지 확인 합니다. 자세한 내용은 [항상의 VPN 기술 개요](../always-on-vpn-technology-overview.md)합니다.
- 물리적 서버 또는 가상 머신 (VM) RAS 게이트웨이 VPN 서버로 원격 액세스를 설치 하려면 두 개의 실제 이더넷 네트워크 어댑터를 사용 하 여 경계 네트워크. Vm은 호스트에 대 한 가상 LAN (VLAN)에 필요 합니다. 
- 관리자 또는 이와 동등한 자격이 필요한 최소입니다.
- 배포를 수행 하기 전에이 배포에 대 한 준비가 되도록이 가이드의 계획 섹션을 읽어보세요.
- 각 기술에 대 한 디자인 및 배포 가이드를 검토 합니다. 이러한 가이드는 배포 시나리오는 서비스 및 조직의 네트워크에 필요한 구성을 제공 하는지 여부를 확인할 수 있습니다. 자세한 내용은 [항상의 VPN 기술 개요](../always-on-vpn-technology-overview.md)합니다.
- 사용자가 선택한 CSP 공급 업체별 없기 때문에 Always On VPN 구성을 배포 하기 위한 관리 플랫폼입니다.

>[!IMPORTANT]
>이 배포에 대 한 것에 인프라 서버, Active Directory Domain Services, Active Directory 인증서 서비스 및 네트워크 정책 서버를 실행 하는 컴퓨터 등의 Windows Server 2016 실행 하는 요구 사항입니다. 인프라 서버 및 원격 액세스를 실행 하는 서버에 대 한 이전 버전의 Windows Server 2012 R2와 같은 Windows Server를 사용할 수 있습니다.
>
>Microsoft Azure에서 가상 컴퓨터 (VM)에서 원격 액세스를 배포 하지 마십시오. 원격 액세스를 사용 하 여 Microsoft Azure에서 지원 되지 않습니다, 원격 액세스 VPN 및 DirectAccess 등. 자세한 내용은 [Microsoft Azure virtual machines에 대 한 Microsoft 서버 소프트웨어 지원](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)합니다.

## <a name="about-this-deployment"></a>이 배포에 대 한

제공 된 지침에는 단일 테 넌 트 RAS 게이트웨이 VPN 지점-사이트 간 VPN 연결에 대 한 Windows 10을 실행 하는 원격 클라이언트 컴퓨터에 대 한 아래에 언급 된 시나리오 중 하나를 사용 하 여 원격 액세스를 배포 하는 방법을 안내 합니다. 배포에 대 한 기존 인프라의 일부를 수정 하기 위한 지침을 찾을 수도 있습니다. 또한이 배포 전체에서 VPN 연결 프로세스, 구성 하는 서버, ProfileXML VPNv2 CSP 노드 및 Always On VPN을 배포 하는 다른 기술에 대 한 자세한 도움이 링크를 찾을 있습니다.

**Always On VPN 배포 시나리오:**

1. 항상 VPN에만 배포 합니다.
2. Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 사용 하 여 Always On VPN을 배포 합니다.

자세한 내용 및 제시 된 시나리오의 워크플로 참조 하세요 [배포 Always On VPN](always-on-vpn-deploy-deployment.md)합니다.

## <a name="what-isnt-provided-in-this-deployment"></a>이 배포에 제공 되지 것

이 배포에 대 한 지침을 제공 하지 않습니다.

- Active Directory Domain Services (AD DS).
- Active Directory 인증서 서비스 (AD CS) 및 공개 키 인프라 (PKI).
- 동적 호스트 구성 프로토콜 (DHCP)입니다.
- 이더넷 케이블 연결, 방화벽, 스위치 및 허브 등의 하드웨어와 네트워크입니다.
- Always On VPN 연결을 통해 원격 사용자가 액세스할 수 있는 응용 프로그램 및 파일 서버 등의 추가 네트워크 리소스.
- 인터넷 연결 또는 Azure AD를 사용 하 여 인터넷 연결에 대 한 조건부 액세스를 제공 합니다. 자세한 내용은 참조 하세요 [Azure Active Directory의 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)합니다.

## <a name="next-steps"></a>다음 단계

- [Always On VPN 특징과 기능에 자세히 알아보기](../../vpn-map-da.md)

- [Always On VPN 향상 된 기능에 자세히 알아보기](../always-on-vpn-enhancements.md)

- [고급 Always On VPN 기능 중 일부에 대해 알아봅니다](always-on-vpn-adv-options.md)

- [Always On VPN 기술에 자세히 알아보기](../always-on-vpn-technology-overview.md)

- [Always On VPN 배포 계획 시작](always-on-vpn-deploy-deployment.md)