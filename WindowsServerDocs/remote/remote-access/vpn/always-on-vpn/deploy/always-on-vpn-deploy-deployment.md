---
title: Always On VPN 배포
description: 이 항목에서는 Always On VPN Windows Server 2016에 배포 하기 위한 자세한 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ad748de2-d175-47bf-b05f-707dc48692cf
ms.localizationpriority: medium
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 15c60f2986d3837c5c6e03f9e0a25c7e0a4e0cc0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867144"
---
# <a name="deploy-always-on-vpn"></a>Always On VPN 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

&#0171;[ **이전:** Always On VPN 고급 기능에 알아봅니다](always-on-vpn-adv-options.md)<br>
&#0187;[ **다음:** 1단계. Always On VPN 배포 계획 시작](always-on-vpn-deploy-planning.md)

이 섹션에서는 원격 도메인에 가입 된 Windows 10 클라이언트 컴퓨터에 대 한 Always On VPN 연결을 배포 하는 것에 대 한 워크플로에 대 한 알아봅니다. 않으려면 **조건부 액세스를 구성** VPN 사용자 리소스에 액세스 하는 방법을 미세 조정, 참조 [Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스](../../ad-ca-vpn-connectivity-windows10.md)합니다. Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스에 대 한 자세한 내용은 참조 하세요 [Azure Active Directory의 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)합니다. 


다음 다이어그램에서는 Always On VPN을 배포 하는 경우 다양 한 시나리오에 대 한 워크플로 프로세스를 보여 줍니다. 

_이미지를 보려면 클릭_합니다.

<a href="../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow.png" alt="Full-sized view of the Always On VPN deployment workflow" target="_blank">![thumbnail](../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow-sm.png)
</a> 

>[!IMPORTANT]
>이 배포에 대 한 것에 인프라 서버, Active Directory Domain Services, Active Directory 인증서 서비스 및 네트워크 정책 서버를 실행 하는 컴퓨터 등의 Windows Server 2016 실행 하는 요구 사항입니다. 인프라 서버 및 원격 액세스를 실행 하는 서버에 대 한 이전 버전의 Windows Server 2012 R2와 같은 Windows Server를 사용할 수 있습니다.

## <a name="step-1-plan-the-always-on-vpn-deploymentalways-on-vpn-deploy-planningmd"></a>[1 단계입니다. Always On VPN 배포 계획](always-on-vpn-deploy-planning.md)

이 단계를 계획 하 고 Always On VPN 배포 준비를 시작 합니다. 컴퓨터의 원격 액세스 서버 역할을 설치 하기 전에 VPN 서버로 사용 하 여 계획 중입니다. 적절 한 계획 한 후에 Always On VPN을 배포할 수 있으며 필요에 따라 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성할 수 있습니다.

## <a name="step-2-configure-the-always-on-vpn-server-infrastructurevpn-deploy-server-infrastructuremd"></a>[2 단계입니다. Always On VPN 서버 인프라 구성](vpn-deploy-server-infrastructure.md)

이 단계에서는 설치 및 VPN을 지 원하는 데 필요한 서버 측 구성 요소를 구성 합니다. 서버 쪽 구성 요소 사용자, VPN 서버와 NPS 서버에서 사용 된 인증서를 배포 하는 PKI를 구성 하는 포함 됩니다.  RRAS의 IKEv2 연결 및 VPN 연결에 대 한 권한 부여를 수행 하려면 NPS 서버를 지원 하도록 구성할 수도 있습니다.

서버 인프라를 구성 하려면 다음 작업을 수행 해야 합니다.
- **Active Directory Domain Services를 사용 하 여 구성 서버:** 컴퓨터와 사용자 모두에 대 한 그룹 정책에서 인증서 자동 등록을 사용 하도록 설정 하 고 VPN 사용자 그룹, VPN 서버 그룹을 NPS 서버 그룹을 만들고 각 그룹에 구성원을 추가 합니다.
- **서버의 Active Directory 인증서 CA:** 사용자 인증, VPN 서버 인증 및 NPS 서버 인증 인증서 템플릿을 만듭니다.
- **도메인에 가입 된 Windows 10 클라이언트:** 등록 하 고 사용자 인증서의 유효성을 검사 합니다.

## <a name="step-3-configure-the-remote-access-server-for-always-on-vpnvpn-deploy-rasmd"></a>[3 단계: VPN에 대 한 원격 액세스 서버를 항상 구성](vpn-deploy-ras.md)

이 단계에서는 원격 액세스 VPN IKEv2 VPN 연결을 허용, 다른 VPN 프로토콜에서 연결을 거부 및 발급 한 IP 주소에 대 한 정적 IP 주소 풀을 연결 하는 권한이 부여 된 VPN 클라이언트에 할당할을 구성할 수 있습니다.

RAS를 구성 하려면 다음 작업을 수행 해야 합니다.
- 등록 하 고 VPN 서버 인증서 유효성 검사
- 설치 및 원격 액세스 VPN 구성

## <a name="step-4-install-and-configure-the-nps-servervpn-deploy-npsmd"></a>[4 단계입니다. NPS 서버 설치 및 구성](vpn-deploy-nps.md)

이 단계에서는 Windows PowerShell 또는 서버 관리자 추가 역할 및 기능 마법사 중 하나를 사용 하 여 네트워크 정책 (NPS 서버)를 설치 합니다. 모든 인증, 권한 부여 및 VPN 서버에서 수신 하는 연결 요청에 대 한 회계 업무를 처리 하는 NPS를 구성할 수도 있습니다.

NPS를 구성 하려면 다음 작업을 수행 해야 합니다.
- Active Directory에서 NPS 서버 등록
- RADIUS NPS 서버에 대 한 계정 구성
- VPN 서버를 NPS에서 RADIUS 클라이언트로 추가
- NPS에서 네트워크 정책 구성
- NPS 서버 인증서 자동 등록

## <a name="step-5-configure-dns-and-firewall-settings-for-always-on-vpnvpn-deploy-dns-firewallmd"></a>[5 단계입니다. DNS 및 방화벽 설정에 대 한 Always On 구성 VPN](vpn-deploy-dns-firewall.md)

이 단계에서는 DNS 및 방화벽 구성 설정입니다. 원격 VPN 클라이언트 연결, 사용 내부 클라이언트를 사용 하는 동일한 DNS 서버 이름을 내부 워크스테이션의 나머지와 동일한 방식으로 확인할 수 있도록 합니다. 

## <a name="step-6-configure-windows-10-client-always-on-vpn-connectionsvpn-deploy-client-vpn-connectionsmd"></a>[6 단계입니다. Windows 10 클라이언트를 VPN 연결에 always On 구성](vpn-deploy-client-vpn-connections.md)

이 단계에서는 VPN 연결을 사용 하 여 해당 인프라와 통신 하는 Windows 10 클라이언트 컴퓨터를 구성 합니다. Windows PowerShell, System Center Configuration Manager 및 Intune 등의 Windows 10 VPN 클라이언트를 구성 하려면 여러 가지 기술을 사용할 수 있습니다. 세 가지 모두 적절 한 VPN 설정을 구성 하는 XML VPN 프로필을 필요 합니다. 

## <a name="step-7-optional-configure-conditional-access-for-vpn-connectivityad-ca-vpn-connectivity-windows10md"></a>[7 단계입니다. (선택 사항) VPN 연결에 대 한 조건부 액세스를 구성 합니다.](../../ad-ca-vpn-connectivity-windows10.md) 
이 선택적 단계에서는 미세 조정할 수 있습니다 어떻게 권한이 부여 된 VPN 사용자 리소스에 액세스 합니다. VPN 연결에 대 한 Azure AD 조건부 액세스를 사용 하 여 VPN 연결을 보호할 수 있습니다. 조건부 액세스는 Azure AD에 대 한 액세스 규칙을 만들 수 있는 정책에 따라 평가 엔진을 응용 프로그램을 연결 합니다. 자세한 내용은 [Azure Active Directory (Azure AD) 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)합니다.


## <a name="next-step"></a>다음 단계
[1 단계입니다. Always On VPN 배포 계획](always-on-vpn-deploy-planning.md): 컴퓨터의 원격 액세스 서버 역할을 설치 하기 전에 VPN 서버로 사용 하 여 계획 중입니다. 적절 한 계획 한 후에 Always On VPN을 배포할 수 있으며 필요에 따라 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성할 수 있습니다.  



---