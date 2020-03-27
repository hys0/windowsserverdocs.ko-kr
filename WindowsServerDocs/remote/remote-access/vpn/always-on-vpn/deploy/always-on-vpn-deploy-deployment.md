---
title: Always On VPN 배포
description: 이 항목에서는 Windows Server 2016에 Always On VPN을 배포 하는 방법에 대 한 자세한 지침을 제공 합니다.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: ad748de2-d175-47bf-b05f-707dc48692cf
ms.localizationpriority: medium
ms.date: 11/05/2018
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 852d7b0ee79193a603c621cfa7b0525b31ebb3b4
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313309"
---
# <a name="deploy-always-on-vpn"></a>Always On VPN 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**이전:** Always On VPN 고급 기능에 대 한 자세한 정보](always-on-vpn-adv-options.md)
- [**다음:** 1 단계. Always On VPN 배포 계획 시작](always-on-vpn-deploy-planning.md)

이 섹션에서는 원격 도메인에 가입 된 Windows 10 클라이언트 컴퓨터에 대 한 Always On VPN 연결을 배포 하기 위한 워크플로에 대해 알아봅니다. VPN 사용자가 리소스에 액세스 하는 방법을 미세 조정 하도록 **조건부 액세스를 구성** 하려면 [Azure AD를 사용 하 여 vpn 연결에 대 한 조건부 액세스](../../ad-ca-vpn-connectivity-windows10.md)를 참조 하세요. Azure AD를 사용 하는 VPN 연결에 대 한 조건부 액세스에 대 한 자세한 내용은 [Azure Active Directory의 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)를 참조 하세요. 

다음 다이어그램은 Always On VPN을 배포할 때 다양 한 시나리오에 대 한 워크플로 프로세스를 보여 줍니다.

[Always On VPN 배포 워크플로의 ![흐름도](../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow-sm.png)](../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow.png)

> [!IMPORTANT]
> 이 배포의 경우 Active Directory Domain Services를 실행 하는 컴퓨터, Active Directory 인증서 서비스 및 네트워크 정책 서버와 같은 인프라 서버에서 Windows Server 2016를 실행 해야 합니다. Windows Server 2012 R2와 같은 이전 버전의 Windows Server를 인프라 서버 및 원격 액세스를 실행 하는 서버에 사용할 수 있습니다.

## <a name="step-1-plan-the-always-on-vpn-deployment"></a>[1 단계. Always On VPN 배포 계획](always-on-vpn-deploy-planning.md)

이 단계에서는 Always On VPN 배포 계획 및 준비를 시작 합니다. 를 VPN 서버로 사용 하려는 컴퓨터에 원격 액세스 서버 역할을 설치 하기 전에 적절 한 계획 후에 Always On VPN을 배포 하 고, 선택적으로 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성할 수 있습니다.

## <a name="step-2-configure-the-always-on-vpn-server-infrastructure"></a>[2 단계. Always On VPN 서버 인프라 구성](vpn-deploy-server-infrastructure.md)

이 단계에서는 VPN을 지 원하는 데 필요한 서버 쪽 구성 요소를 설치 하 고 구성 합니다. 서버 쪽 구성 요소에는 사용자, VPN 서버 및 NPS 서버에서 사용 하는 인증서를 배포 하도록 PKI를 구성 하는 작업이 포함 됩니다.  또한 RRAS를 구성 하 여 VPN 연결에 대 한 권한 부여를 수행 하는 IKEv2 연결 및 NPS 서버를 지원 합니다.

서버 인프라를 구성 하려면 다음 작업을 수행 해야 합니다.

- **Active Directory Domain Services으로 구성 된 서버에서 다음을 수행 합니다.** 그룹 정책에서 인증서 자동 등록을 사용 하도록 설정 하 고 컴퓨터와 사용자 모두에 대해 VPN 사용자 그룹, VPN 서버 그룹 및 NPS 서버 그룹을 만들고 각 그룹에 구성원을 추가 합니다.
- **Active Directory 인증서 서버 CA에서 다음을 수행 합니다.** 사용자 인증, VPN 서버 인증 및 NPS 서버 인증 인증서 템플릿을 만듭니다.
- **도메인에 가입 된 Windows 10 클라이언트에서:** 사용자 인증서를 등록 하 고 유효성을 검사 합니다.

## <a name="step-3-configure-the-remote-access-server-for-always-on-vpn"></a>[3 단계. Always On VPN에 대 한 원격 액세스 서버 구성](vpn-deploy-ras.md)

이 단계에서는 원격 액세스 VPN을 구성 하 여 IKEv2 VPN 연결을 허용 하 고, 다른 VPN 프로토콜의 연결을 거부 하 고, 권한 있는 VPN 클라이언트를 연결 하기 위해 IP 주소를 발급 하는 고정 IP 주소 풀을 할당 합니다.

RAS를 구성 하려면 다음 작업을 수행 해야 합니다.

- VPN 서버 인증서 등록 및 유효성 검사
- 원격 액세스 VPN 설치 및 구성

## <a name="step-4-install-and-configure-the-nps-server"></a>[4 단계. NPS 서버 설치 및 구성](vpn-deploy-nps.md)

이 단계에서는 Windows PowerShell 또는 서버 관리자 역할 및 기능 추가 마법사를 사용 하 여 NPS (네트워크 정책 서버)를 설치 합니다. 또한 VPN 서버에서 받는 연결 요청에 대 한 모든 인증, 권한 부여 및 계정 의무를 처리 하도록 NPS를 구성 합니다.

NPS를 구성 하려면 다음 작업을 수행 해야 합니다.

- Active Directory에 NPS 서버 등록
- NPS 서버에 대 한 RADIUS 계정 구성
- NPS에서 RADIUS 클라이언트로 VPN 서버 추가
- NPS에서 네트워크 정책 구성
- NPS 서버 인증서 자동 등록

## <a name="step-5-configure-dns-and-firewall-settings-for-always-on-vpn"></a>[5 단계. Always On VPN에 대 한 DNS 및 방화벽 설정 구성](vpn-deploy-dns-firewall.md)

이 단계에서는 DNS 및 방화벽 설정을 구성 합니다. 원격 VPN 클라이언트는 연결 될 때 내부 클라이언트에서 사용 하는 것과 동일한 DNS 서버를 사용 하 여 내부 워크스테이션의 나머지 부분과 동일한 방식으로 이름을 확인할 수 있도록 합니다. 

## <a name="step-6-configure-windows-10-client-always-on-vpn-connections"></a>[6 단계. Windows 10 클라이언트 Always On VPN 연결 구성](vpn-deploy-client-vpn-connections.md)

이 단계에서는 VPN 연결을 사용 하 여 해당 인프라와 통신 하도록 Windows 10 클라이언트 컴퓨터를 구성 합니다. 여러 기술을 사용 하 여 Windows PowerShell, Microsoft 끝점 Configuration Manager 및 Intune을 비롯 한 Windows 10 VPN 클라이언트를 구성할 수 있습니다. 세 가지 모두 적절 한 VPN 설정을 구성 하려면 XML VPN 프로필이 필요 합니다.

## <a name="step-7-optional-configure-conditional-access-for-vpn-connectivity"></a>[7 단계. 필드 VPN 연결에 대 한 조건부 액세스 구성](../../ad-ca-vpn-connectivity-windows10.md)

이 선택적 단계에서는 권한 있는 VPN 사용자가 리소스에 액세스 하는 방법을 미세 조정할 수 있습니다. VPN 연결에 대 한 Azure AD 조건부 액세스를 사용 하 여 VPN 연결을 보호할 수 있습니다. 조건부 액세스는 Azure AD 연결 응용 프로그램에 대 한 액세스 규칙을 만들 수 있는 정책 기반 평가 엔진입니다. 자세한 내용은 [Azure Active Directory (AZURE AD) 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)를 참조 하세요.

## <a name="next-step"></a>다음 단계

[1 단계. Always On VPN 배포 계획](always-on-vpn-deploy-planning.md):를 vpn 서버로 사용 하려는 컴퓨터에 원격 액세스 서버 역할을 설치 하기 전에 사용 합니다. 적절 한 계획 후에 Always On VPN을 배포 하 고, 선택적으로 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성할 수 있습니다.  
