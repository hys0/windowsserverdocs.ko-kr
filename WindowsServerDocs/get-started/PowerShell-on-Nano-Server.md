---
title: Nano Server의 PowerShell
description: Nano Server의 제한된 PowerShell 기능 집합의 차이점
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b25b939-1e2c-4bed-a8d3-2a8e8e46b53d
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 8a19082121e2d859bc4694fd3f7332e9d0d0b3b9
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082457"
---
# <a name="powershell-on-nano-server"></a>Nano Server의 PowerShell

>적용 대상: Windows Server 2016
  
> [!IMPORTANT]
> Windows Server, 버전 1709부터 [컨테이너 기본 OS 이미지](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)로만 Nano 서버를 사용할 수 있습니다. [Nano 서버 변경 사항](nano-in-semi-annual-channel.md)을 확인하여 그 의미를 알아보세요. 
  
## <a name="powershell-editions"></a>PowerShell 버전   
  
버전 5.1부터 PowerShell은 다양한 기능 집합 및 플랫폼 호환성을 나타내는 다양한 버전으로 사용 가능합니다.  
  
- **Desktop Edition:** .NET Framework를 기반으로 구축되며 Server Core 및 Windows Desktop과 같은 전체 버전의 Windows에서 실행되는 PowerShell 버전을 대상 지정하는 스크립트 및 모듈과 호환성을 제공합니다.  
- **Core Edition:** .NET Framework를 기반으로 구축되며 Nano 서버 및 Windows IoT와 같은 축소된 버전의 Windows에서 실행되는 PowerShell 버전을 대상 지정하는 스크립트 및 모듈과 호환성을 제공합니다.  
  
실행 중인 PowerShell 버전은 $PSVersionTable의 PSEdition 속성에 표시됩니다.  
```powershell  
$PSVersionTable  
  
Name                           Value  
----                           -----  
PSVersion                      5.1.14300.1000  
PSEdition                      Desktop  
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}  
CLRVersion                     4.0.30319.42000  
BuildVersion                   10.0.14300.1000  
WSManStackVersion              3.0  
PSRemotingProtocolVersion      2.3  
SerializationVersion           1.1.0.1  
```  
  
모듈 작성자는 CompatiblePSEditions 모듈 매니페스트 키를 사용하여 해당 모듈이 하나 이상의 PowerShell 버전과 호환되도록 선언할 수 있습니다. 이 키는 PowerShell 5.1 이상에서만 지원됩니다.  
```powershell  
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1  
$moduleInfo = Test-ModuleManifest -Path \TestModuleWithEdition.psd1  
$moduleInfo.CompatiblePSEditions  
Desktop  
Core  
  
$moduleInfo | Get-Member CompatiblePSEditions  
  
   TypeName: System.Management.Automation.PSModuleInfo  
  
Name                 MemberType Definition  
----                 ---------- ----------  
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}  
  
```  
사용 가능한 모듈 목록을 가져올 때 PowerShell 버전별로 목록을 필터링할 수 있습니다.  
```powershell  
Get-Module -ListAvailable | ? CompatiblePSEditions -Contains "Desktop"  
  
    Directory: C:\Program Files\WindowsPowerShell\Modules  
  
  
ModuleType Version    Name                                ExportedCommands  
---------- -------    ----                                ----------------  
Manifest   1.0        ModuleWithPSEditions  
  
Get-Module -ListAvailable | ? CompatiblePSEditions -Contains "Core" | % CompatiblePSEditions  
Desktop  
Core  
  
```  
스크립트 작성자는 #requires 문에서 PSEdition 매개 변수를 사용하여 호환 가능한 PowerShell 버전에서 스크립트가 실행되는 경우에만 스크립트가 실행되도록 할 수 있습니다.  
```powershell  
Set-Content C:\script.ps1 -Value "#requires -PSEdition Core  
Get-Process -Name PowerShell"  
Get-Content C:\script.ps1  
#requires -PSEdition Core  
Get-Process -Name PowerShell  
  
C:\script.ps1  
C:\script.ps1 : The script 'script.ps1' cannot be run because it contained a "#requires" statement for PowerShell editions 'Core'. The edition of PowerShell that is required by the script does not match the currently running PowerShell Desktop edition.  
At line:1 char:1  
+ C:\script.ps1  
+ ~~~~~~~~~~~~~  
    + CategoryInfo          : NotSpecified: (script.ps1:String) [], RuntimeException  
    + FullyQualifiedErrorId : ScriptRequiresUnmatchedPSEdition  
```  
  
## <a name="differences-in-powershell-on-nano-server"></a>Nano 서버에서 PowerShell의 차이점  
Nano 서버의 경우 모든 Nano 서버 설치에 기본적으로 PowerShell Core를 포함합니다. PowerShell Core는 Nano 서버 및 Windows IoT Core처럼 .NET Core를 기반으로 하고 축소된 Windows 버전에서 실행되는 PowerShell의 축소된 버전입니다. PowerShell Core는 Windows Server 2016에서 실행되는 Windows PowerShell 등의 다른 PowerShell 버전과 같은 방식으로 작동합니다. 그러나 축소된 Nano 서버이기 때문에 Windows Server 2016의 PowerShell 기능 중 Nano 서버의 PowerShell Core에서 사용할 수 없는 기능도 있습니다.  
  
  
**Nano 서버에서 사용할 수 없는 Windows PowerShell 기능**  
* ADSI, ADO 및 WMI 유형 어댑터   
* Enable-PSRemoting, Disable-PSRemoting(PowerShell 원격 기능은 기본적으로 사용하도록 설정되며 [Nano Server 설치](Getting-Started-with-Nano-Server.md)의 "Windows PowerShell 원격 기능 사용" 섹션 참조).  
* 예약된 작업 및 PSScheduledJob 모듈   
* 도메인 가입을 위한 컴퓨터 cmdlet { Add | Remove }(Nano Server를 도메인에 가입하는 다양한 방법은 [Nano Server 설치](Getting-Started-with-Nano-Server.md)의 "Nano Server를 도메인에 가입" 섹션 참조).  
* Reset-ComputerMachinePassword, Test-ComputerSecureChannel   
* 프로필(`Set-PSSessionConfiguration`으로 들어오는 원격 연결에 대한 시작 스크립트를 추가할 수 있음)  
* 클립보드 cmdlet   
* EventLog cmdlet { Clear | Get | Limit | New | Remove | Show | Write }(대신 New-WinEvent 및 Get-WinEvent cmdlet 사용).   
* Get-PfxCertificate cmdlet   
* TraceSource cmdlet { Get | Set }   
* 카운터 cmdlet { Get | Export | Import }   
* 일부 웹 관련 cmdlet  { New-WebServiceProxy, Send-MailMessage, ConvertTo-Html }  
* PSDiagnostics 모듈을 사용하여 로깅 및 추적    
* Get-hotfix(Nano 서버에서 업데이트를 가져오고 관리하려면 [Nano 서버 관리](Manage-Nano-Server.md) 참조).  
* 암시적 원격 cmdlet { Export-PSSession | Import-PSSession }   
* New-PSTransportOption   
* PowerShell 트랜잭션 및 트랜잭션 cmdlet { Complete | Get | Start | Undo | Use }   
* PowerShell 워크플로 인프라, 모듈 및 cmdlet   
* Out-Printer   
* Update-List   
* WMI v1 cmdlet: Get-WmiObject, Invoke-WmiMethod, Register-WmiEvent, Remove-WmiObject, Set-WmiInstance(대신 CimCmdlets 모듈 사용)   
  
## <a name="using-windows-powershell-desired-state-configuration-with-nano-server"></a>Nano 서버와 함께 Windows PowerShell 필요한 상태 구성 사용  
  
Windows PowerShell DSC(필요한 상태 구성)를 사용하여 Nano 서버를 대상 노드로 관리할 수 있습니다. 현재는 DSC 푸시 모드에서 Nano 서버를 실행하는 노드만 관리할 수 있습니다. 모든 DSC 기능이 Nano 서버와 연동하는 것은 아닙니다.  
  
자세한 내용은 [Nano 서버에서 DSC 사용](https://msdn.microsoft.com/powershell/dsc/nanoDsc)을 참조하세요.  
  
  


