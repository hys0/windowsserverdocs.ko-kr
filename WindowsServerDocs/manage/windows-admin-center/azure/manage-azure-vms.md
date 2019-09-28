---
title: Azure IaaS 가상 머신 관리
description: Windows 관리 센터를 사용 하 여 Azure IaaS Vm 관리 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 7b85f64d108283d4865b718b565ad3ba40f14f02
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357344"
---
# <a name="manage-azure-iaas-virtual-machines-with-windows-admin-center"></a>Windows 관리 센터를 사용 하 여 Azure IaaS 가상 머신 관리

Windows Admin Center를 사용하여 온-프레미스 머신뿐만 아니라 Azure VM도 관리할 수 있습니다. 여러 가지 구성을 사용할 수 있습니다. 사용자 환경에 적합 한 구성을 선택 합니다.
- [온-프레미스 Windows 관리 센터 게이트웨이에서 Azure Vm 관리](#manage-with-an-on-premises-windows-admin-center-gateway)
- [Azure VM에 설치 된 Windows 관리 센터 게이트웨이에서 Azure Vm 관리](#use-a-windows-admin-center-gateway-deployed-in-azure)

## <a name="manage-with-an-on-premises-windows-admin-center-gateway"></a>온-프레미스 Windows 관리 센터 게이트웨이를 사용 하 여 관리

온-프레미스 게이트웨이 (Windows 10 또는 Windows Server 2016)에 Windows 관리 센터를 이미 설치한 경우이 동일한 게이트웨이를 사용 하 여 Windows 10 또는 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 r 2를 관리할 수 있습니다. Azure의 Vm. 

### <a name="connecting-to-vms-with-a-public-ip"></a>공용 IP를 사용 하 여 Vm에 연결

대상 Vm (Windows 관리 센터를 사용 하 여 관리 하려는 Vm)에 공용 ip가 있는 경우 IP 주소 또는 FQDN을 사용 하 여 Windows 관리 센터 게이트웨이에 추가 합니다. 고려해 야 할 몇 가지 사항이 있습니다.

- 대상 vm에서 PowerShell 또는 명령 프롬프트에서 다음을 실행 하 여 대상 VM에 대 한 WinRM 액세스를 사용 하도록 설정 해야 합니다. `winrm quickconfig`
- Azure VM에 도메인에 가입 하지 않은 경우 VM은 작업 그룹의 서버 처럼 동작 하므로 [작업 그룹에서 Windows 관리 센터를 사용 하](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)는 것을 고려해 야 합니다.
- 또한 Windows 관리 센터에서 대상 VM을 관리 하기 위해 HTTP를 통해 WinRM에 대해 포트 5985에 대 한 인바운드 연결을 사용 하도록 설정 해야 합니다.
  1. 대상 VM에서 다음 PowerShell 스크립트를 실행 하 여 게스트 OS에서 포트 5985에 대 한 인바운드 연결을 사용 하도록 설정 합니다.   
     `Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any`

  2. 또한 Azure 네트워킹에서 포트를 열어야 합니다.

     - Azure VM을 선택 하 고 **네트워킹**을 선택한 다음 **인바운드 포트 규칙 추가**를 선택 합니다. 
     - **인바운드 보안 규칙 추가** 창의 맨 위에서 **기본** 이 선택 되어 있는지 확인 합니다.
     - **포트 범위** 필드에 **5985**을 입력 합니다.
    
     Windows 관리 센터 게이트웨이에서 고정 IP를 사용 하는 경우 보안을 강화 하기 위해 Windows 관리 센터 게이트웨이에서 인바운드 WinRM 액세스만 허용 하도록 선택할 수 있습니다.
     이렇게 하려면 **인바운드 보안 규칙 추가** 창의 맨 위에 있는 **고급** 을 선택 합니다.

     **원본**에서 **IP 주소**를 선택 하 고 Windows 관리 센터 게이트웨이에 해당 하는 원본 ip 주소를 입력 합니다.

     - **프로토콜** 에서 **TCP**를 선택 합니다.
     - 나머지는 기본값으로 남겨둘 수 있습니다.

> [!NOTE]
> 사용자 지정 포트 규칙을 만들어야 합니다. Azure 네트워킹에서 제공 하는 WinRM 포트 규칙은 5985 (HTTP 사용) 대신 포트 5986 (HTTPS over)를 사용 합니다. 

### <a name="connecting-to-vms-without-a-public-ip"></a>공용 IP 없이 Vm에 연결

대상 Azure Vm에 공용 Ip가 없고 온-프레미스 네트워크에 배포 된 Windows 관리 센터 게이트웨이에서 이러한 Vm을 관리 하려면 대상 Vm이 있는 VNet에 연결 하도록 온-프레미스 네트워크를 구성 해야 합니다. 연결. 이 작업을 수행 하는 방법에는 세 가지가 있습니다. Express 경로, 사이트 간 VPN 또는 지점 및 사이트 간 VPN. [사용자 환경에서 어떤 연결 옵션이 적합 한지 알아보세요.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) 

>[!TIP]
>지점 및 사이트 간 VPN을 사용 하 여 해당 VNet에서 azure Vm을 관리 하기 위해 Windows 관리 센터 게이트웨이를 Azure VNet에 연결 하려는 경우 Windows 관리 센터의 [Azure 네트워크 어댑터](https://aka.ms/WACNetworkAdapter) 기능을 사용할 수 있습니다. 이렇게 하려면 Windows 관리 센터가 설치 된 서버에 연결 하 고 네트워크 도구로 이동 하 여 "Azure 네트워크 어댑터 추가"를 선택 합니다. 필요한 세부 정보를 제공 하 고 "설정"을 클릭 하면 Windows 관리 센터에서 지정 하는 Azure VNet에 지점 및 사이트 간 VPN을 구성 합니다. 그 후에는 온-프레미스 Windows 관리 센터 게이트웨이에서 Azure Vm에 연결 하 고 관리할 수 있습니다.

대상 VM에서 PowerShell 또는 명령 프롬프트에서 다음을 실행 하 여 WinRM이 대상 Vm에서 실행 되 고 있는지 확인 합니다. `winrm quickconfig`

Azure VM에 도메인에 가입 하지 않은 경우 VM은 작업 그룹의 서버 처럼 동작 하므로 [작업 그룹에서 Windows 관리 센터를 사용 하](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)는 것을 고려해 야 합니다.

문제가 발생 하는 경우 [Windows 관리 센터의 문제 해결](../support/troubleshooting.md) 을 참조 하 여 구성에 추가 단계가 필요한 지 확인 합니다 (예: 로컬 관리자 계정을 사용 하 여 연결 하거나 도메인에 가입 하지 않은 경우).

## <a name="use-a-windows-admin-center-gateway-deployed-in-azure"></a>Azure에 배포 된 Windows 관리 센터 게이트웨이 사용

대상 Vm이 연결 된 VNet에 Windows 관리 센터를 배포 하 여 온-프레미스 종속성 없이 Azure Vm을 관리할 수 있습니다. 

Windows 관리 센터 게이트웨이를 배포 하는 VNet 외부의 Vm을 관리 하려면 Windows 관리 센터 게이트웨이의 VNet과 대상 서버의 VNet 간에 VNet 간 연결을 설정 해야 합니다. VNet 피어 링, VNet 간 연결 또는 사이트 간 연결을 사용 하 여이 연결을 설정할 수 있습니다. [사용자 환경에서 어떤 VNet 간 연결 옵션이 적합 한지 자세히 알아보세요.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal)

Windows 관리 센터는 사용자 환경에서 기존 또는 새로 배포 된 VM에 설치할 수 있습니다. Windows 관리 센터 설치용으로 선택한 VM에는 공용 IP 및 DNS 이름이 있어야 합니다.

[Azure에서 Windows 관리 센터 게이트웨이 배포에 대 한 자세한 정보](deploy-wac-in-azure.md)