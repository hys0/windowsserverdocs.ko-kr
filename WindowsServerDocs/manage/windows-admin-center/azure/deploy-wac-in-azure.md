---
title: Azure에서 Windows 관리 센터 게이트웨이 배포
description: Azure에서 Windows 관리 센터 게이트웨이를 배포 하는 방법
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 42216375d1784a5bc853994a9de7cff72920088d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357316"
---
# <a name="deploy-windows-admin-center-in-azure"></a>Azure에서 Windows 관리 센터 배포

## <a name="deploy-using-script"></a>스크립트를 사용 하 여 배포

[Azure Cloud Shell](https://shell.azure.com) 에서 실행 하는 Deploy-WACAzVM를 다운로드 하 여 Azure에서 Windows 관리 센터 게이트웨이를 설정할 수 있습니다 [.](https://aka.ms/deploy-wacazvm) 이 스크립트는 리소스 그룹을 포함 하 여 전체 환경을 만들 수 있습니다.

[수동 배포 단계로 이동](#deploy-manually-on-an-existing-azure-virtual-machine)

### <a name="prerequisites"></a>사전 요구 사항

* [Azure Cloud Shell](https://shell.azure.com)에서 계정을 설정 합니다. Cloud Shell를 처음 사용 하는 경우 Cloud Shell를 사용 하 여 Azure storage 계정을 연결 하거나 만들지 묻는 메시지가 표시 됩니다.
* **PowerShell** Cloud Shell에서 홈 디렉터리로 이동 합니다.```PS Azure:\> cd ~```
* ```Deploy-WACAzVM.ps1``` 파일을 업로드 하려면 로컬 컴퓨터에서 Cloud Shell 창의 아무 곳에 나 끌어 놓습니다.

사용자 고유의 인증서를 지정 하는 경우:

* [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis)에 인증서를 업로드 합니다. 먼저, Azure Portal에서 주요 자격 증명 모음을 만든 다음 키 자격 증명 모음에 인증서를 업로드 합니다. 또는 Azure Portal을 사용 하 여 인증서를 생성할 수 있습니다.

### <a name="script-parameters"></a>스크립트 매개 변수

* **ResourceGroupName** -[STRING] VM이 만들어지는 리소스 그룹의 이름을 지정 합니다.

* **이름** -[STRING] VM의 이름을 지정 합니다.

* **자격 증명** -[PSCREDENTIAL] VM에 대 한 자격 증명을 지정 합니다.

* **Msipath** -[String] 기존 VM에 Windows 관리 센터를 배포할 때 Windows 관리 센터 MSI의 로컬 경로를 지정 합니다. 생략 된 경우의 http://aka.ms/WACDownload 버전으로 기본 설정 됩니다.

* **VaultName** -[String] 인증서를 포함 하는 키 자격 증명 모음의 이름을 지정 합니다.

* **CertName** -[STRING] MSI 설치에 사용할 인증서의 이름을 지정 합니다.

* **Generatesslcert** -[스위치] MSI에서 자체 서명 된 ssl 인증서를 생성 해야 하는 경우 True입니다.

* **PortNumber** -[Int] Windows 관리 센터 서비스의 ssl 포트 번호를 지정 합니다. 생략 하는 경우 기본값은 443입니다.

* **Openports** -[int []] VM에 대 한 열린 포트를 지정 합니다.

* **Location** -[STRING] VM의 위치를 지정 합니다.

* **Size** -[STRING] VM의 크기를 지정 합니다. 생략 하는 경우 기본값은 "Standard_DS1_v2"입니다.

* **Image** -[STRING] VM의 이미지를 지정 합니다. 생략 하는 경우 기본값은 "Win2016Datacenter"입니다.

* **VirtualNetworkName** -[STRING] VM에 대 한 가상 네트워크의 이름을 지정 합니다.

* **SubnetName** -[STRING] VM에 대 한 서브넷의 이름을 지정 합니다.

* **SecurityGroupName** -[STRING] VM에 대 한 보안 그룹의 이름을 지정 합니다.

* **PublicIpAddressName** -[STRING] VM에 대 한 공용 IP 주소의 이름을 지정 합니다.

* **InstallWACOnly** -[스위치] 기존 Azure VM에 WAC을 설치 해야 하는 경우 True로 설정 합니다.

MSI를 배포 하기 위한 두 가지 옵션과 MSI 설치에 사용 되는 인증서가 있습니다. Aka.ms/WACDownload에서 MSI를 다운로드 하거나 기존 VM에 배포 하는 경우 VM에서 로컬로 MSI의 filepath를 제공할 수 있습니다. 인증서는 Azure Key Vault에서 찾을 수 있으며, MSI에서 자체 서명 된 인증서를 생성 합니다.

### <a name="script-examples"></a>스크립트 예제

먼저 스크립트의 매개 변수에 필요한 공통 변수를 정의 합니다.

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

#### <a name="example-1-use-the-script-to-deploy-wac-gateway-on-a-new-vm-in-a-new-virtual-network-and-resource-group-use-the-msi-from-akamswacdownload-and-a-self-signed-cert-from-the-msi"></a>예 1: 스크립트를 사용 하 여 새 가상 네트워크 및 리소스 그룹의 새 VM에 WAC gateway를 배포 합니다. Aka.ms/WACDownload의 MSI 및 MSI에서 자체 서명 된 인증서를 사용 합니다.

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

#### <a name="example-2-same-as-1-but-using-a-certificate-from-azure-key-vault"></a>예 2: #1와 동일 하지만 Azure Key Vault 인증서를 사용 합니다.

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

#### <a name="example-3-using-a-local-msi-on-an-existing-vm-to-deploy-wac"></a>예제 3: 기존 VM에서 로컬 MSI를 사용 하 여 WAC 배포

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

### <a name="requirements-for-vm-running-the-windows-admin-center-gateway"></a>Windows 관리 센터 게이트웨이를 실행 하는 VM에 대 한 요구 사항

포트 443 (HTTPS)이 열려 있어야 합니다.
스크립트에 대해 정의 된 것과 동일한 변수를 사용 하 여 Azure Cloud Shell 아래 코드를 사용 하 여 네트워크 보안 그룹을 업데이트할 수 있습니다.

```powershell
$nsg = Get-AzNetworkSecurityGroup -Name $SecurityGroupName -ResourceGroupName $ResourceGroupName
$newNSG = Add-AzNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name ssl-rule -Description "Allow SSL" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 443
Set-AzNetworkSecurityGroup -NetworkSecurityGroup $newNSG
```

### <a name="requirements-for-managed-azure-vms"></a>관리 되는 Azure VM에 대 한 요구 사항

포트 5985 (WinRM over HTTP)가 열려 있고 활성 수신기가 있어야 합니다.
Azure Cloud Shell에서 아래 코드를 사용 하 여 관리 되는 노드를 업데이트할 수 있습니다. ```$ResourceGroupName```및 ```$Name``` 는 배포 스크립트와 동일한 변수를 사용 하지만 관리 중인 VM에 대 한 ```$Credential``` 특정를 사용 해야 합니다.

```powershell
Enable-AzVMPSRemoting -ResourceGroupName $ResourceGroupName -Name $Name
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any} -Credential $Credential
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {winrm create winrm/config/Listener?Address=*+Transport=HTTP} -Credential $Credential
```

## <a name="deploy-manually-on-an-existing-azure-virtual-machine"></a>기존 Azure 가상 컴퓨터에 수동으로 배포

원하는 게이트웨이 VM에 Windows 관리 센터를 설치 하기 전에 HTTPS 통신에 사용할 SSL 인증서를 설치 하거나 Windows 관리 센터에서 생성 한 자체 서명 된 인증서를 사용 하도록 선택할 수 있습니다. 그러나 후자 옵션을 선택 하면 브라우저에서 연결을 시도할 때 경고가 표시 됩니다. 자세히를 클릭 하 여 Edge에서이 경고를 무시할 수 있습니다 **> 웹 페이지로 이동** 하거나 Chrome에서 고급 > 선택 하 여 **[웹 페이지]를 진행**합니다. 테스트 환경에는 자체 서명 된 인증서를 사용 하는 것이 좋습니다.

> [!NOTE]
> 이러한 지침은 Server Core 설치가 아닌 데스크톱 환경을 사용 하는 Windows Server에를 설치 하는 데 사용 됩니다. 

1. 로컬 컴퓨터에 [Windows 관리 센터를 다운로드](https://aka.ms/windowsadmincenter) 합니다.

2. VM에 대 한 원격 데스크톱 연결을 설정한 다음 로컬 컴퓨터에서 MSI를 복사 하 여 VM에 붙여넣습니다.

3. MSI를 두 번 클릭 하 여 설치를 시작 하 고 마법사의 지시를 따릅니다. 다음에 유의 하세요.

   - 기본적으로 설치 관리자는 권장 포트 443 (HTTPS)를 사용 합니다. 다른 포트를 선택 하려면 방화벽 에서도 해당 포트를 열어야 합니다. 

   - VM에 SSL 인증서를 이미 설치한 경우 해당 옵션을 선택 하 고 지문을 입력 해야 합니다.

4. Windows 관리 센터 서비스를 시작 합니다 (C:/Program Files/Windows 관리 센터/sme 실행).

[Windows 관리 센터 배포에 대해 자세히 알아보세요.](../deploy/install.md)

### <a name="configure-the-gateway-vm-to-enable-https-port-access"></a>HTTPS 포트 액세스를 사용 하도록 게이트웨이 VM 구성: 

1. Azure Portal에서 VM으로 이동 하 고 **네트워킹**을 선택 합니다. 

2. **인바운드 포트 규칙 추가** 를 선택 하 고 **서비스**에서 **HTTPS** 를 선택 합니다. 

> [!NOTE]
> 기본 443 이외의 포트를 선택한 경우 서비스 아래에서 **사용자 지정** 을 선택 하 고 **포트 범위**아래에서 3 단계에서 선택한 포트를 입력 합니다. 

### <a name="accessing-a-windows-admin-center-gateway-installed-on-an-azure-vm"></a>Azure VM에 설치 된 Windows 관리 센터 게이트웨이 액세스

이 시점에서 게이트웨이 VM의 DNS 이름으로 이동 하 여 로컬 컴퓨터의 최신 브라우저 (Edge 또는 Chrome)에서 Windows 관리 센터에 액세스할 수 있어야 합니다. 

> [!NOTE]
> 443 이외의 포트를 선택한 경우 VM\<\>의 https://DNS 이름으로 이동 하 여 Windows 관리 센터에 액세스할 수 있습니다.\<사용자 지정 포트\>

Windows 관리 센터에 액세스 하려고 하면 브라우저에서 Windows 관리 센터가 설치 된 가상 컴퓨터에 액세스 하기 위한 자격 증명을 묻는 메시지를 표시 합니다. 여기에서 가상 컴퓨터의 로컬 사용자 또는 로컬 관리자 그룹에 있는 자격 증명을 입력 해야 합니다. 

VNet에서 다른 Vm을 추가 하려면 대상 VM에서 PowerShell 또는 명령 프롬프트에서 다음을 실행 하 여 WinRM이 대상 Vm에서 실행 중인지 확인 합니다.`winrm quickconfig`

Azure VM에 도메인에 가입 하지 않은 경우 VM은 작업 그룹의 서버 처럼 동작 하므로 [작업 그룹에서 Windows 관리 센터를 사용 하](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)는 것을 고려해 야 합니다.