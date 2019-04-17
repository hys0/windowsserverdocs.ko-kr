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
ms.openlocfilehash: af766c2e0502d9fe633cae42d999db5cbffc32c8
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296998"
---
# Azure에서 Windows Admin Center를 배포 합니다.

## 스크립트를 사용 하 여 배포

Azure에서 Windows Admin Center 게이트웨이를 설정 하려면 [Azure 클라우드 셸](https://shell.azure.com) 에서 실행 [배포 WACAzVM.ps1](https://aka.ms/deploy-wacazvm) 다운로드할 수 있습니다. 이 스크립트는 리소스 그룹을 포함 하 여 전체 환경에 만들 수 있습니다.

[수동 배포 단계로 이동](#deploy-manually-on-an-existing-azure-virtual-machine)

### 필수 구성 요소

* [Azure 클라우드](https://shell.azure.com)셸의 계좌를 설정 합니다. 클라우드 셸을 사용 하 여 처음으로 이면 것인지 연결 하거나 Azure 저장소 계정 클라우드 셸을 사용 하 여 만들 수 있습니다.
* **PowerShell** 클라우드 셸의 홈 디렉터리로 이동 합니다. ```PS Azure:\> cd ~```
* 업로드 하는 ```Deploy-WACAzVM.ps1``` 파일, 끌어서 로컬 컴퓨터에서 어디에 클라우드 셸 창에 있습니다.

자체 인증서를 지정:

* [Azure 키 자격 증명 모음](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)에 인증서를 업로드 합니다. 먼저, Azure Portal에서 키 vault를 만든 다음 키 자격 증명 모음에 인증서를 업로드 합니다. 또는 사용자를 위해 인증서를 생성 하 여 Azure Portal을 사용할 수 있습니다.

### 스크립트 매개 변수

* **ResourceGroupName** -[문자열] VM 만들어지는 리소스 그룹의 이름을 지정 합니다.

* **이름** -[문자열] VM의 이름을 지정 합니다.

* **자격 증명** -[PSCredential] VM에 대 한 자격 증명을 지정 합니다.

* **MsiPath** -[문자열] 기존 VM에서 Windows Admin Center를 배포할 때 Windows Admin Center MSI의 로컬 경로 지정 합니다. 버전으로 기본 http://aka.ms/WACDownload 생략 합니다.

* **VaultName** -[문자열]는 인증서가 포함 된 자격 증명 모음 키의 이름을 지정 합니다.

* **CertName** -[문자열] MSI 설치에 사용할 인증서의 이름을 지정 합니다.

* **GenerateSslCert** -[스위치] MSI 자체 서명 된 ssl 인증서를 생성 해야 하는 경우 참입니다.

* **향하** 는-[int] Windows Admin Center 서비스에 대 한 ssl 포트 번호를 지정 합니다. 기본값은 443 생략 하는 경우입니다.

* **OpenPorts** -[int []] VM에 대 한 열린 포트를 지정 합니다.

* **위치** -[문자열] VM의 위치를 지정 합니다.

* **크기** -[문자열] VM의 크기를 지정합니다. 기본값은 "Standard_DS1_v2" 생략 하는 경우입니다.

* **이미지** -[문자열] VM의 이미지를 지정합니다. 기본값은 "Win2016Datacenter" 생략 하는 경우입니다.

* **VirtualNetworkName** -[문자열] VM에 대 한 가상 네트워크의 이름을 지정합니다.

* **SubnetName** -[문자열] VM에 대 한 서브넷의 이름을 지정합니다.

* **SecurityGroupName** -[문자열] VM에 대 한 보안 그룹의 이름을 지정 합니다.

* **PublicIpAddressName** -[문자열] VM에 대 한 공용 IP 주소의 이름을 지정합니다.

* **InstallWACOnly** -[스위치] WAC 기존 Azure VM에 설치 해야 하는 경우 true로 설정 합니다.

가지 MSI를 배포 하 고 MSI 설치에 사용 되는 인증서에 대 한 2 가지 옵션이 있습니다. MSI aka.ms/WACDownload에서 다운로드할 수 있거나 또는 기존 VM에 배포 하는 경우 VM에서 로컬로 MSI의 파일 경로 지정할 수 있습니다. 어떤 Azure 키 자격 증명 모음에 인증서를 찾을 수 또는 MSI 하 여 자체 서명 된 인증서를 생성 됩니다.

### 스크립트 예제

먼저, 스크립트의 매개 변수에 필요한 일반 변수를 정의 합니다.

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

#### 예제 1: 새 가상 네트워크 및 리소스 그룹의 새 VM에서 WAC 게이트웨이 배포 스크립트를 사용 합니다. Aka.ms/WACDownload에서 MSI 및 MSI에서 자체 서명 된 인증서를 사용 합니다.

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

#### 예제 2: 동일 #1 있지만 Azure 키 자격 증명 모음에서 발급 한 인증서를 사용 합니다.

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

#### 예제 3: 기존 VM에 로컬 MSI를 사용 하 여 WAC 배포 합니다.

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

### Windows Admin Center 게이트웨이 실행 중인 VM에 대 한 요구 사항

포트 443 (HTTPS) 열어야 합니다.
스크립트에 대해 정의 된 동일한 변수를 사용 하 여 네트워크 보안 그룹을 업데이트 하려면 Azure 클라우드 셸의 아래 코드를 사용할 수 있습니다.

```powershell
$nsg = Get-AzNetworkSecurityGroup -Name $SecurityGroupName -ResourceGroupName $ResourceGroupName
$newNSG = Add-AzNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name ssl-rule -Description "Allow SSL" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 443
Set-AzNetworkSecurityGroup -NetworkSecurityGroup $newNSG
```

### 관리 되는 Azure VM에 대 한 요구 사항

포트 5985 (HTTP 통해 WinRM) 열어야 하 고는 활성 수신기가 해야 합니다.
관리 되는 노드 업데이트 하려면 Azure 클라우드 셸의 아래 코드를 사용할 수 있습니다. ```$ResourceGroupName``` 및 ```$Name``` 배포 스크립트와 동일한 변수를 사용 하지만 사용 해야 합니다 ```$Credential``` 관리 중인 VM에 특정 합니다.

```powershell
Enable-AzVMPSRemoting -ResourceGroupName $ResourceGroupName -Name $Name
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any} -Credential $Credential
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {winrm create winrm/config/Listener?Address=*+Transport=HTTP} -Credential $Credential
```

## 기존 Azure 가상 컴퓨터에서 수동으로 배포

원하는 게이트웨이 VM에서 Windows Admin Center를 설치 하기 전에 HTTPS 통신에 사용할 SSL 인증서를 설치 하거나 Windows 관리 센터에서 생성 된 자체 서명 된 인증서를 사용 하도록 선택할 수 있습니다. 그러나, 두 번째 옵션을 선택 하면 브라우저에서 연결 하려고 할 때 경고를 받게 됩니다. **고급 gt_ 계속 [웹 페이지]를**선택 하 여 **웹 페이지로 이동 gt_ 세부 정보를** 클릭 하 여 하거나, Chrome, Edge에서이 경고를 무시할 수 있습니다. 만 테스트 환경에 대 한 자체 서명 된 인증서를 사용 하는 것이 좋습니다.

> [!NOTE]
> 이러한 지침은 하지는 Server Core 설치에서 데스크톱 환경 포함 Windows Server에 설치 하기 위한 것입니다. 

1. 로컬 컴퓨터에 [Windows Admin Center 다운로드](https://aka.ms/windowsadmincenter) 알려줍니다.

2. VM에 원격 데스크톱 연결 다음 MSI 로컬 컴퓨터에서 복사한 VM에 붙여 넣습니다.

3. MSI 설치를 시작을 두 번 클릭 하 고 마법사의 지침을 따릅니다. 다음은 고려해 야 합니다.

   - 기본적으로 설치 관리자는 권장된 포트 443 (HTTPS)를 사용합니다. 하려는 경우 다른 포트를 선택, 사용자의 방화벽에 해당 포트를 열려고 해야 합니다. 

   - VM에서 SSL 인증서를 이미 설치한 경우 해당 옵션을 선택 하 고 지문 입력을 확인 합니다.

4. Windows Admin Center 서비스 (c: / 프로그램 파일/Windows Admin Center/sme.exe 실행) 시작

[Windows Admin Center를 배포 하는 방법에 대 한 자세히 알아보세요.](../deploy/install.md)

### HTTPS 포트 액세스를 사용 하도록 VM 게이트웨이 구성 합니다. 

1. Azure portal의 VM을 찾아 **네트워킹**을 선택 합니다. 

2. **인바운드 포트 규칙 추가** 선택 하 고 **서비스**에서 **HTTPS** 선택 합니다. 

> [!NOTE]
> 기본 443 이외의 포트를 선택한 경우 서비스에서 **사용자 지정** 선택 하 고 **포트 범위**에서 3 단계에서 선택한 포트를 입력 합니다. 

### Azure VM에 설치 된 Windows Admin Center 게이트웨이에 액세스

이 시점에서 Windows Admin Center 게이트웨이 VM의 DNS 이름으로 이동 하 여 로컬 컴퓨터에 최신 브라우저 (가장자리 또는 Chrome)에서 액세스할 수 있어야 합니다. 

> [!NOTE]
> 443 이외의 포트를 선택한 경우에 VM\>:\<custom port\>의 https://\<DNS 이름으로 이동 하 여 Windows Admin Center를 액세스할 수 있습니다.

Windows Admin Center에 액세스 하려고 할 때 Windows Admin Center가 설치 된 가상 컴퓨터에 액세스 하도록 자격 증명 브라우저를 입력 합니다. 여기서는 로컬 사용자 또는 가상 컴퓨터의 로컬 관리자 그룹에 있는 자격 증명을 입력 해야 합니다. 

다른 Vm에는 VNet에 추가 하려면 WinRM 대상 VM에 PowerShell 또는 명령 프롬프트에서 다음을 실행 하 여 대상 Vm에서 실행 중인 확인 합니다. `winrm quickconfig`

하면 하지 않은 도메인 가입 Azure VM을 [사용 하 여 작업 그룹에서 Windows Admin Center에](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)대 한 계정 확인 해야 합니다 VM 작업 그룹에, 서버와 같은 동작 합니다.