---
title: Azure IaaS 가상 컴퓨터 관리
description: Windows Admin Center (Project Honolulu)를 사용 하 여 Azure IaaS Vm 관리
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 6f162294076d7e12df09f31b0bbd7d9244abe679
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297017"
---
# Windows Admin Center를 사용 하 여 Azure IaaS 가상 컴퓨터 관리

온-프레미스 컴퓨터 뿐만 아니라 Azure Vm에 관리를 Windows Admin Center를 사용할 수 있습니다. 다양 한 구성 가능한는-환경에 적합 한 구성을 선택 합니다.
- [온-프레미스 Windows Admin Center 게이트웨이를 Azure Vm 관리](#manage-with-an-on-premises-windows-admin-center-gateway)
- [Azure VM에 설치 된 Windows Admin Center 게이트웨이를 Azure Vm 관리](#use-a-windows-admin-center-gateway-deployed-in-azure)

## 온-프레미스 Windows Admin Center 게이트웨이 사용 하 여 관리

Windows 10 또는 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 r 2를 관리 하려면이 동일한 게이트웨이 온-프레미스 게이트웨이 (중 하나에서 Windows 10 또는 Windows Server 2016)에서 Windows Admin Center를 이미 설치한 경우 사용할 수 있습니다. Azure에서 Vm 합니다. 

### 공용 IP 사용 하 여 Vm에 연결

경우에 대상 Vm (Windows Admin Center로 관리할 Vm)가 공용 Ip, FQDN 또는 IP 주소에서 Windows Admin Center 게이트웨이를 추가 합니다. 가지 고려해 야 할 몇 가지 사항이 있습니다.

- 대상 VM에 PowerShell 또는 명령 프롬프트에서 다음을 실행 하 여 대상 VM에 WinRM 액세스를 활성화 해야 합니다. `winrm quickconfig`
- 하면 하지 않은 도메인 가입 Azure VM을 [사용 하 여 작업 그룹에서 Windows Admin Center에](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)대 한 계정 확인 해야 합니다 VM 작업 그룹에, 서버와 같은 동작 합니다.
- WinRM에 대 한 5985 포트에 대 한 인바운드 연결 HTTP를 통해 순서 대로 대상 VM을 관리 하는 Windows Admin Center에 대 한 사용 해야 합니다.
   1. 대상 VM 게스트 운영 체제에서 사용할 5985 포트에 대 한 인바운드 연결을 사용 하도록 설정 하려면 다음 PowerShell 스크립트를 실행 합니다.   
`Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any`

   2. 또한 Azure 네트워킹에서 포트를 열어야 합니다.

    - Azure VM을 **네트워킹**, **인바운드 포트 규칙 추가**선택 합니다. 
    - **기본** **인바운드 보안 규칙 추가** 창 맨 위에 있는 선택 되었는지 확인 합니다.
    - **포트 범위** 필드에 **5985**를 입력 합니다.
    
    Windows Admin Center 게이트웨이 고정 IP에 액세스할 수 있도록만 인바운드 WinRM Windows Admin Center 게이트웨이에서 보안 강화를 위해 선택할 수 있습니다.
    이 작업을 수행 하려면 **고급** **보안 인바운드 규칙 추가** 창 맨 위에 있는 선택 합니다.

    **원본**대 한 **IP 주소**선택한 다음 해당 Windows Admin Center 게이트웨이 하 원본 IP 주소를 입력 합니다.

    - **프로토콜** 에 대 한 **TCP**를 선택 합니다.
    - 나머지 기본값으로 유지할 수 있습니다.

> [!NOTE]
> 사용자 지정 포트 규칙을 만들어야 합니다. Azure 네트워킹에서 제공 하는 WinRM 포트 규칙 (HTTP)를 통해 5985 대신 5986 (HTTPS)를 통한 포트를 사용 합니다. 

### 공용 IP 없이 Vm에 연결

대상 Vm은 VNet에 연결 하는 데 온-프레미스 네트워크를 구성 해야 하는 Azure Vm 대상 공용 Ip 없는 온-프레미스 네트워크에 배포 된 Windows Admin Center 게이트웨이에서 이러한 Vm 관리 하려는 경우 연결 되어 있습니다. 3 가지 방법으로 수행할 수 있습니다: ExpressRoute, 사이트 간 VPN 또는 지점 사이트 간 VPN 합니다. [연결 옵션 환경에 적합에 대해 알아봅니다.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) 

>[!TIP]
>Windows Admin Center 게이트웨이 해당 VNet에 Azure Vm을 관리 하는 Azure VNet에 연결 지점 사이트 간 VPN을 사용 하고자 하는 경우 Windows 관리 센터에서 [Azure 네트워크 어댑터](https://aka.ms/WACNetworkAdapter) 기능을 사용할 수 있습니다. 이렇게 하려면 Windows Admin Center가 설치 된 서버에 연결, 네트워크 도구로 이동 하 고 "Azure 네트워크 어댑터 추가"를 선택 합니다. 필요한 정보를 제공 하 고 클릭 "설정"을 Windows Admin Center를 지정 하면 그 후에 연결 하 고 온-프레미스 Windows Admin Center 게이트웨이를 Azure Vm 관리 Azure VNet에 지점 사이트 간 VPN을 구성 합니다.

WinRM 대상 VM에 PowerShell 또는 명령 프롬프트에서 다음을 실행 하 여 대상 Vm에서 실행 중인지 확인 합니다. `winrm quickconfig`

하면 하지 않은 도메인 가입 Azure VM을 [사용 하 여 작업 그룹에서 Windows Admin Center에](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)대 한 계정 확인 해야 합니다 VM 작업 그룹에, 서버와 같은 동작 합니다.

문제가 발생할 경우 [문제 해결 Windows Admin Center](../support/troubleshooting.md) 경우 추가 단계가 필요한 구성 (예를 들어 로컬 관리자 계정을 사용 하 여 연결 하거나 경우 도메인에 가입 된)를 참조 하세요.

## Azure에 배포 된 Windows Admin Center 게이트웨이 사용 하 여

대상 Vm에 연결 되어 있는 VNet에서 Windows Admin Center를 배포 하 여 모든 온-프레미스 종속성 없이 Azure Vm을 관리할 수 있습니다. 

Windows Admin Center 게이트웨이 배포 될 VNet 외부에서 Vm을 관리 하려면 Windows Admin Center 게이트웨이 VNet와 대상 서버 VNet VNet-VNet 연결을 설정 해야 합니다. VNet 피어 링, VNet-VNet 연결 또는 사이트 간 연결을 사용 하 여이 연결을 설정할 수 있습니다. [사용자 환경에서 옵션을 선택 하면 센스 어떤 VNet-VNet 연결에 대 한 자세한 내용을 보려면 합니다.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal)

사용자 환경에서 기존 또는 새로 배포 된 VM에 Windows Admin Center는 설치할 수 있습니다. Windows Admin Center 설치에 대해 선택한 VM 공용 IP 및 DNS 이름이 있어야 합니다.

[Azure에서 Windows Admin Center 게이트웨이 배포 하는 방법에 대 한 자세한 정보](deploy-wac-in-azure.md)