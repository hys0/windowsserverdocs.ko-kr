---
title: Azure에서 Windows Admin Center 게이트웨이 배포
description: Azure에서 Windows Admin Center 게이트웨이 배포 하는 방법
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: a3fa1838096d910505faf9a2c5bd819b3a256fe2
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280415"
---
# <a name="deploy-windows-admin-center-in-azure"></a>Azure에서 Windows Admin Center 배포

## <a name="deploy-using-script"></a>스크립트를 사용 하 여 배포

다운로드할 수 있습니다 [배포 WACAzVM.ps1](https://aka.ms/deploy-wacazvm) 에서 실행 하는 [Azure Cloud Shell](https://shell.azure.com) 를 Azure에서 Windows Admin Center 게이트웨이 설정 합니다. 이 스크립트는 리소스 그룹을 포함 하 여 전체 환경에 만들면 됩니다.

[수동 배포 단계를 이동 합니다.](#deploy-manually-on-an-existing-azure-virtual-machine)

### <a name="prerequisites"></a>사전 요구 사항

* 계정 설정 [Azure Cloud Shell](https://shell.azure.com)합니다. Cloud Shell을 사용 하 여 처음으로 이기 Cloud Shell을 사용 하 여 Azure storage 계정을 만들거나 연결 하 라는 메시지가 표시 됩니다.
* 에 **PowerShell** Cloud Shell을 홈 디렉터리로 이동 합니다. ```PS Azure:\> cd ~```
* 업로드할는 ```Deploy-WACAzVM.ps1``` 파일을 끌어서 로컬 컴퓨터에서 원하는 위치에 Cloud Shell 창에 있습니다.

경우 사용자 고유의 인증서를 지정 합니다.

* 인증서를 업로드 [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis)합니다. 먼저 Azure 포털에서 key vault를 만든 다음 key vault에 인증서를 업로드 합니다. 또는 인증서를 생성 하려면 Azure Portal을 사용할 수 있습니다.

### <a name="script-parameters"></a>스크립트 매개 변수

* **ResourceGroupName** -[String] VM이 만들어지는 리소스 그룹의 이름을 지정 합니다.

* **이름** -[String] VM의 이름을 지정 합니다.

* **자격 증명** -[PSCredential] VM에 대 한 자격 증명을 지정 합니다.

* **MsiPath** -[String] 기존 VM에서 Windows Admin Center 배포할 때 Windows Admin Center MSI의 로컬 경로 지정 합니다. 버전을 기본값으로 http://aka.ms/WACDownload 생략 합니다.

* **VaultName** -[String] 인증서가 포함 된 key vault의 이름을 지정 합니다.

* **CertName** -[String] MSI 설치에 사용할 인증서의 이름을 지정 합니다.

* **GenerateSslCert** -[스위치] MSI는 자체 서명 된 ssl 인증서를 생성 해야 하면 True입니다.

* **PortNumber** -[int] Windows Admin Center 서비스에 대 한 ssl 포트 번호를 지정 합니다. 기본값은 생략 하는 경우 443입니다.

* **OpenPorts** -[int []] VM에 대 한 열려 있는 포트를 지정 합니다.

* **위치** -[String] VM의 위치를 지정 합니다.

* **크기** -[String] VM의 크기를 지정 합니다. 기본값은 생략 "Standard_DS1_v2"입니다.

* **이미지** -[String] VM의 이미지를 지정 합니다. 기본값은 생략 "Win2016Datacenter"입니다.

* **VirtualNetworkName** -[String] VM에 대 한 가상 네트워크의 이름을 지정 합니다.

* **SubnetName** -[String] VM에 대 한 서브넷의 이름을 지정 합니다.

* **SecurityGroupName** -[String] VM에 대 한 보안 그룹의 이름을 지정 합니다.

* **PublicIpAddressName** -[String] VM에 대 한 공용 IP 주소의 이름을 지정 합니다.

* **InstallWACOnly** -WAC 기존 Azure VM에 설치 해야 하는 경우 [스위치] True로 설정 합니다.

MSI를 배포 하 고 MSI 설치에 사용 된 인증서에 대 한 다른 옵션을 2 가지가 있습니다. Aka.ms/WACDownload에서 MSI를 다운로드 하거나 또는 기존 VM에 배포 하는 경우 VM에서 로컬 MSI의 파일 경로 지정할 수 있습니다. 두 Azure Key Vault에서 인증서를 찾을 수 있습니다 또는 자체 서명 된 인증서는 MSI에서 생성 됩니다.

### <a name="script-examples"></a>스크립트 예제

먼저 스크립트의 매개 변수에 필요한 일반적인 변수를 정의 합니다.

```PowerShell
$ResourceGroupName = "wac-rg1" 
$VirtualNetworkName = "wac-vnet"
$SecurityGroupName = "wac-nsg"
$SubnetName = "wac-subnet"
$VaultName = "wac-key-vault"
$CertName = "wac-cert"
$Location = "westus"
$PublicIpAddressName = "wac-public-ip"
$Size = "Standard_D4s_v3"
$Image = "Win2016Datacenter"
$Credential = Get-Credential
```

#### <a name="example-1-use-the-script-to-deploy-wac-gateway-on-a-new-vm-in-a-new-virtual-network-and-resource-group-use-the-msi-from-akamswacdownload-and-a-self-signed-cert-from-the-msi"></a>예 1: 새 가상 네트워크 및 리소스 그룹에 새 VM에 WAC 게이트웨이 배포 하는 스크립트를 사용 합니다. MSI에서 자체 서명 된 인증서 및 aka.ms/WACDownload에서 MSI를 사용 합니다.

```PowerShell
$scriptParams = @{
    ResourceGroupName = $ResourceGroupName
    Name = "wac-vm1"
    Credential = $Credential
    VirtualNetworkName = $VirtualNetworkName
    SubnetName = $SubnetName
    GenerateSslCert = $true
}
./Deploy-WACAzVM.ps1 @scriptParams
```

#### <a name="example-2-same-as-1-but-using-a-certificate-from-azure-key-vault"></a>예 2: Azure Key Vault에서 인증서를 사용 하 여 있지만 # 1과 동일 합니다.

```PowerShell
$scriptParams = @{
    ResourceGroupName = $ResourceGroupName
    Name = "wac-vm2"
    Credential = $Credential
    VirtualNetworkName = $VirtualNetworkName
    SubnetName = $SubnetName
    VaultName = $VaultName
    CertName = $CertName
}
./Deploy-WACAzVM.ps1 @scriptParams
```

#### <a name="example-3-using-a-local-msi-on-an-existing-vm-to-deploy-wac"></a>예제 3: 기존 VM에서 로컬 MSI를 사용 하 여 WAC 배포 합니다.

```PowerShell
$MsiPath = "C:\Users\<username>\Downloads\WindowsAdminCenter<version>.msi"
$scriptParams = @{
    ResourceGroupName = $ResourceGroupName
    Name = "wac-vm3"
    Credential = $Credential
    MsiPath = $MsiPath
    InstallWACOnly = $true
    GenerateSslCert = $true
}
./Deploy-WACAzVM.ps1 @scriptParams
```

### <a name="requirements-for-vm-running-the-windows-admin-center-gateway"></a>Windows Admin Center 게이트웨이 실행 하는 VM에 대 한 요구 사항

포트 443(https) 열려 있어야 합니다.
스크립트에 대해 정의 된 동일한 변수를 사용 하 여 네트워크 보안 그룹을 업데이트 하려면 Azure Cloud Shell에서 아래 코드를 사용할 수 있습니다.

```powershell
$nsg = Get-AzNetworkSecurityGroup -Name $SecurityGroupName -ResourceGroupName $ResourceGroupName
$newNSG = Add-AzNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name ssl-rule -Description "Allow SSL" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 443
Set-AzNetworkSecurityGroup -NetworkSecurityGroup $newNSG
```

### <a name="requirements-for-managed-azure-vms"></a>관리 되는 Azure VM에 대 한 요구 사항

: 포트 5985 (HTTP 통한 WinRM)가 열려 있어야 하 고 활성 수신기가 있는 해야 합니다.
관리 되는 노드를 업데이트 하려면 Azure Cloud Shell에서 다음 코드를 사용할 수 있습니다. ```$ResourceGroupName``` 및 ```$Name``` 배포 스크립트와 같은 변수를 사용 하지만 사용 해야 합니다는 ```$Credential``` 관리 중인 VM에 특정 합니다.

```powershell
Enable-AzVMPSRemoting -ResourceGroupName $ResourceGroupName -Name $Name
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any} -Credential $Credential
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {winrm create winrm/config/Listener?Address=*+Transport=HTTP} -Credential $Credential
```

## <a name="deploy-manually-on-an-existing-azure-virtual-machine"></a>기존 Azure 가상 머신에서 수동으로 배포

원하는 게이트웨이 VM에서 Windows Admin Center 설치 하기 전에 HTTPS 통신에 사용할 SSL 인증서를 설치 하거나 Windows Admin Center 생성 한 자체 서명 된 인증서를 사용 하도록 선택할 수 있습니다. 그러나 하면 경고 후자 옵션을 선택 하면 브라우저에서 연결 하려고 할 때입니다. 클릭 하 여에 지에서이 경고를 무시할 수 있습니다 **세부 정보 > 웹 페이지로 이동** 또는 선택 하 여 Chrome **고급 > [웹] 페이지로 계속**합니다. 테스트 환경에 대 한 자체 서명 된 인증서만 사용 하는 것이 좋습니다.

> [!NOTE]
> 이러한 지침은 하지 Server Core 설치에서 데스크톱 환경 포함 Windows Server에 설치 됩니다. 

1. [다운로드 Windows Admin Center](https://aka.ms/windowsadmincenter) 로컬 컴퓨터에 있습니다.

2. VM에 원격 데스크톱 연결을 설정 하 고 MSI를 로컬 컴퓨터에서 복사를 VM에 붙여 넣습니다.

3. 설치를 시작 하는 MSI를 두 번 클릭 하 고 마법사의 지침을 따릅니다. 다음 고려해 야 합니다.

   - 기본적으로 설치 관리자는 권장 되는 포트 443 (HTTPS)을 사용합니다. 하려는 경우 다른 포트도 방화벽에서 해당 포트를 열어야 할 경우 유의 하세요. 

   - VM에서 SSL 인증서를 이미 설치한 경우 해당 옵션을 선택 하 고 지문을 입력을 확인 합니다.

4. (C: / Program 파일/Windows 관리자 Center/sme.exe 실행) Windows Admin Center 서비스를 시작 합니다.

[Windows Admin Center 배포에 대해 알아봅니다.](../deploy/install.md)

### <a name="configure-the-gateway-vm-to-enable-https-port-access"></a>HTTPS 포트 액세스할 수 있도록 VM 게이트웨이 구성 합니다. 

1. Azure portal 선택에서 VM을 이동할 **네트워킹**합니다. 

2. 선택 **인바운드 포트 규칙 추가** 선택한 **HTTPS** 아래의 **서비스**합니다. 

> [!NOTE]
> 기본값 443 이외의 포트를 선택한 경우 선택 **사용자 지정** 티 드 서비스 아래 3 단계에서 선택한 포트를 입력 하 고 **범위 포트**합니다. 

### <a name="accessing-a-windows-admin-center-gateway-installed-on-an-azure-vm"></a>Azure VM에 설치할 Windows Admin Center 게이트웨이 액세스

이 시점에서 게이트웨이 VM의 DNS 이름으로 이동 하 여 로컬 컴퓨터에 Windows Admin Center (Edge 또는 Chrome) 최신 브라우저에서 액세스할 수 있어야 합니다. 

> [!NOTE]
> 443 이외의 포트를 선택한 경우에 https://로 이동 하 여 Windows Admin Center 액세스할 수 있습니다\<VM의 DNS 이름\>:\<사용자 지정 포트\>

Windows Admin Center 액세스 하려고 할 때 브라우저 Windows Admin Center 설치 된 가상 컴퓨터에 액세스 하는 자격 증명 됩니다. 다음은 로컬 사용자 또는 가상 컴퓨터의 로컬 관리자 그룹에 있는 자격 증명을 입력 해야 합니다. 

VNet의 다른 Vm에 추가 하려면 대상 VM에서 PowerShell 또는 명령 프롬프트에서 다음을 실행 하 여 WinRM 대상 Vm에서 실행 중인지 확인 합니다. `winrm quickconfig`

있습니다 하지 않은 도메인에 가입 된 Azure VM을 하는 경우 VM 처럼 작업 그룹에서 서버에 대 한 계정 수 있는지 확인 해야 하므로 [Windows Admin Center 사용 하 여 작업 그룹에서](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)합니다.