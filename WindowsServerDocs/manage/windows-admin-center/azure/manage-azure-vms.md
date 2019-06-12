---
title: Azure IaaS 가상 머신 관리
description: Windows Admin Center (프로젝트 브라 티)를 사용 하 여 Azure IaaS Vm 관리
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ac98f42c4ad5606cc8d2b142f209f9bdb2b9611c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445904"
---
# <a name="manage-azure-iaas-virtual-machines-with-windows-admin-center"></a>Windows Admin Center 사용 하 여 Azure IaaS 가상 머신 관리

온-프레미스 컴퓨터 뿐만 아니라 Azure Vm에 관리 하려면 Windows Admin Center 사용할 수 있습니다. 가능한 다른 여러 구성을 가지-사용자 환경에 적합 한 구성을 선택 합니다.
- [온-프레미스 Windows Admin Center 게이트웨이에서 Azure Vm 관리](#manage-with-an-on-premises-windows-admin-center-gateway)
- [Azure VM에 설치할 Windows Admin Center 게이트웨이에서 Azure Vm 관리](#use-a-windows-admin-center-gateway-deployed-in-azure)

## <a name="manage-with-an-on-premises-windows-admin-center-gateway"></a>온-프레미스 Windows Admin Center 게이트웨이 사용 하 여 관리

(중 하나에 Windows 10 또는 Windows Server 2016)에 온-프레미스 게이트웨이에서 Windows Admin Center 이미 설치한 경우 Windows 10 또는 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2를 관리 하려면이 동일한 게이트웨이 사용할 수 있습니다. Azure에서 Vm입니다. 

### <a name="connecting-to-vms-with-a-public-ip"></a>공용 IP 사용 하 여 Vm에 연결

대상 Vm (Windows Admin Center 사용 하 여 관리 하려는 Vm)에 추가할 Windows Admin Center 게이트웨이 IP 주소 또는 FQDN으로 공용 Ip, 있으면 합니다. 고려해 야 할 몇 가지 고려 사항이 있습니다.

- 대상 VM에서 PowerShell 또는 명령 프롬프트에서 다음을 실행 하 여 대상 VM WinRM 액세스를 활성화 해야 합니다. `winrm quickconfig`
- 있습니다 하지 않은 도메인에 가입 된 Azure VM을 하는 경우 VM 처럼 작업 그룹에서 서버에 대 한 계정 수 있는지 확인 해야 하므로 [Windows Admin Center 사용 하 여 작업 그룹에서](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)합니다.
- 대상 VM을 관리 하려면 Windows Admin Center 대 한 순서 대로 HTTP를 통한 WinRM에 대 한 인바운드 연결: 포트 5985 설정할 수도 있습니다.
  1. 대상 포트 5985 게스트 OS에 인바운드 연결을 사용 하도록 설정 하려면 VM에서 다음 PowerShell 스크립트를 실행 합니다.   
     `Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any`

  2. 또한 Azure 네트워킹에서 포트를 열어야 합니다.

     - Azure VM을 선택 **네트워킹**, 한 다음 **인바운드 포트 규칙 추가**합니다. 
     - 확인 **기본** 맨 위에 있는 선택 된 **인바운드 보안 규칙 추가** 창입니다.
     - 에 **포트 범위** 필드를 입력 합니다 **5985**합니다.
    
     Windows Admin Center 게이트웨이 고정 IP에 액세스할 수 있도록만 인바운드 WinRM Windows Admin Center 게이트웨이에서 보안 강화를 위해 선택할 수 있습니다.
     이 위해 선택 **고급** 맨 위에 있는 합니다 **인바운드 보안 규칙 추가** 창입니다.

     에 대 한 **소스**를 선택 **IP 주소**, Windows Admin Center 게이트웨이에 해당 원본 IP 주소를 입력 합니다.

     - 에 대 한 **프로토콜** 선택 **TCP**합니다.
     - 나머지 기본값으로 유지할 수 있습니다.

> [!NOTE]
> 사용자 지정 포트 규칙을 만들어야 합니다. Azure 네트워킹에서 제공 하는 WinRM 포트 규칙 (HTTP)를 통해 5985 대신 포트 5986 (https)를 사용 합니다. 

### <a name="connecting-to-vms-without-a-public-ip"></a>공용 IP 하지 않고 Vm에 연결

대상 Vm에는 VNet에 연결 하려면 온-프레미스 네트워크를 구성 해야 하는 대상 Azure Vm에 공용 Ip가 없는 경우 온-프레미스 네트워크에 배포 된 Windows Admin Center 게이트웨이에서 이러한 Vm을 관리. 연결 합니다. 3 가지 방법으로 이렇게 할 수 있습니다. ExpressRoute, 사이트 간 VPN 또는 지점-사이트 간 VPN입니다. [연결 옵션 환경에서 의미가 알아봅니다.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) 

>[!TIP]
>지점-사이트 간 VPN을 사용 하 여 Windows Admin Center 게이트웨이를 사용할 수 있습니다 VNet에 Azure Vm을 관리 하는 Azure VNet을 연결할 하려는 경우는 [Azure 네트워크 어댑터](https://aka.ms/WACNetworkAdapter) Windows Admin Center 기능입니다. 이렇게 하려면 Windows Admin Center 설치 된 서버에 연결 하 고 네트워크 tool로 이동 "추가 Azure 네트워크 어댑터"를 선택 합니다. 필요한 정보를 제공 하 고 클릭 하는 경우 "설정"을 Windows Admin Center 지정 하면 그 후에 연결할 수 있고 온-프레미스 Windows Admin Center 게이트웨이에서 Azure Vm을 관리 하는 Azure VNet에 지점-사이트 간 VPN을 구성 합니다.

대상 VM에서 PowerShell 또는 명령 프롬프트에서 다음을 실행 하 여 WinRM 대상 Vm에서 실행 중인지 확인 합니다. `winrm quickconfig`

있습니다 하지 않은 도메인에 가입 된 Azure VM을 하는 경우 VM 처럼 작업 그룹에서 서버에 대 한 계정 수 있는지 확인 해야 하므로 [Windows Admin Center 사용 하 여 작업 그룹에서](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)합니다.

문제가 실행 하는 경우를 참조 하세요 [문제 해결 Windows Admin Center](../support/troubleshooting.md) (예를 들어 사용자는 로컬 관리자 계정을 사용 하 여 연결 또는 도메인에 가입 되지) 추가 단계는 구성에 필요 합니다.

## <a name="use-a-windows-admin-center-gateway-deployed-in-azure"></a>Azure에 배포 된 Windows Admin Center 게이트웨이 사용 합니다.

온-프레미스 종속 되지 않고 Windows Admin Center 대상 Vm에 연결 되어 있는 VNet에 배포 하 여 Azure Vm을 관리할 수 있습니다. 

Windows Admin Center 게이트웨이 배포 하는 VNet 외부에서 Vm을 관리 하려면 Windows Admin Center 게이트웨이의 VNet과 대상 서버의 VNet 간에 VNet 대 VNet 연결을 설정 해야 합니다. VNet 피어 링, VNet 대 VNet 연결 또는 사이트 간 연결을 사용 하 여이 연결을 설정할 수 있습니다. [환경의 옵션은 것이 좋습니다는 VNet 대 VNet 연결에 대 한 자세한 내용을 알아보세요.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal)

사용자 환경에서 기존 또는 새로 배포 된 VM에서 Windows Admin Center 설치할 수 있습니다. Windows Admin Center 설치를 위한 선택 하는 VM에 공용 IP 및 DNS 이름이 있어야 합니다.

[Azure에서 Windows Admin Center 게이트웨이 배포 하는 방법에 대 한 자세한 정보](deploy-wac-in-azure.md)