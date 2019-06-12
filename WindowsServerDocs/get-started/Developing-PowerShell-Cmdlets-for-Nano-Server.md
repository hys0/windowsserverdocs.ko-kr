---
title: Nano Server용 PowerShell Cmdlet 개발
description: 'CIM, .NET cmdlet, C++ 이식 '
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b4267f0-1c91-4a40-9262-5daf4659f686
author: jaimeo
ms.author: jaimeo
ms.date: 09/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3376d03a2e9f02b20aba608de0228efd7dfddea
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443622"
---
# <a name="developing-powershell-cmdlets-for-nano-server"></a>Nano Server용 PowerShell Cmdlet 개발

>적용 대상: Windows Server 2016

> [!IMPORTANT]
> Windows Server, 버전 1709부터 [컨테이너 기본 OS 이미지](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)로만 Nano 서버를 사용할 수 있습니다. [Nano 서버 변경 사항](nano-in-semi-annual-channel.md)을 확인하여 그 의미를 알아보세요. 
  
## <a name="overview"></a>개요  
Nano 서버의 경우 모든 Nano 서버 설치에 기본적으로 PowerShell Core를 포함합니다. PowerShell Core는 Nano 서버 및 Windows IoT Core처럼 .NET Core를 기반으로 하고 축소된 Windows 버전에서 실행되는 PowerShell의 축소된 버전입니다. PowerShell Core는 Windows Server 2016에서 실행되는 Windows PowerShell 등의 다른 PowerShell 버전과 같은 방식으로 작동합니다. 그러나 축소된 Nano 서버이기 때문에 Windows Server 2016의 PowerShell 기능 중 Nano 서버의 PowerShell Core에서 사용할 수 없는 기능도 있습니다.  
  
Nano 서버에서 실행하고 싶은 기존 PowerShell cmdlet을 보유하고 있거나 그러한 목적으로 새 cmdlet을 개발 중이라면 이 토픽의 팁과 권장 사항이 도움이 될 것입니다.  

## <a name="powershell-editions"></a>PowerShell 버전  
  
  
버전 5.1부터 PowerShell은 다양한 기능 집합 및 플랫폼 호환성을 나타내는 다양한 버전으로 사용 가능합니다.  
  
- **데스크톱 버전:** .NET Framework를 기반으로 하며 스크립트 및 모듈의 전체 설치 공간 버전의 Server Core와 같은 Windows 및 Windows 데스크톱에서 실행 중인 PowerShell 버전을 대상으로 호환성을 제공 합니다.  
- **Core Edition:** .NET Core를 기반으로 하며 스크립트 및 Nano Server와 같은 Windows 및 Windows IoT의 축소 버전에서 실행 되는 powershell 버전을 대상으로 하는 모듈을 사용 하 여 호환성을 제공 합니다.  
  
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
  
  
## <a name="installing-nano-server"></a>Nano 서버 설치  
가상 컴퓨터 또는 물리적 컴퓨터에 Nano 서버를 설치하기 위한 빠른 시작 및 세부 단계는 이 토픽의 상위 토픽인 [Nano 서버 설치](Getting-Started-with-Nano-Server.md)에 나와 있습니다.  
  
> [!NOTE]  
> Nano 서버에 대한 개발 작업의 경우 New-NanoServerImage의 -Development 매개 변수를 사용하여 Nano 서버를 설치하는 것이 유용합니다. 그러면 서명되지 않은 드라이버를 설치하고, 디버거 이진 파일을 복사하고, 디버깅을 위한 포트를 열고, 테스트 서명을 사용하고, 개발자 라이선스 없이 AppX 패키지를 설치할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
>  
>`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -Development`  
  
## <a name="determining-the-type-of-cmdlet-implementation"></a>cmdlet 구현 형식 결정  
PowerShell은 다양한 cmdlet 구현 형식을 지원하며, 사용자가 사용한 구현 형식에 따라 Nano 서버에서 작동하는 cmdlet을 만들거나 이식하는 데 필요한 프로세스 및 도구가 결정됩니다. 지원되는 구현 형식은 다음과 같습니다.  
* CIM - CIM(WMIv2) 공급자를 통해 계층화된 CDXML 파일로 구성   
* .NET - 관리형 cmdlet 인터페이스를 구현하는 .NET 어셈블리로 구성되며 일반적으로 C#으로 작성   
* PowerShell 스크립트 - PowerShell 언어로 작성된 스크립트 모듈(.psm1) 또는 스크립트(.ps1)으로 구성   
  
이식하려는 기존 cmdlet에 어떤 구현을 사용했는지 확실하지 않은 경우 사용자가 보유한 제품 또는 기능을 설치한 후 다음 위치 중 하나에서 PowerShell 모듈 폴더를 찾아 보세요.   
  
* %windir%\system32\WindowsPowerShell\v1.0\Modules   
* %ProgramFiles%\WindowsPowerShell\Modules   
* %UserProfile%\Documents\WindowsPowerShell\Modules   
* \<제품 설치 위치 >   
    
  다음 위치에서 세부 정보를 확인합니다.  
  * CIM cmdlet은 .cdxml 파일 확장명을 갖습니다.  
  * .NET cmdlet은 .dll 파일 확장명을 갖거나 RootModule, ModuleToProcess 또는 NestedModules 필드의 .psd1 파일에 나열된 GAC에 어셈블리를 설치합니다.  
* PowerShell 스크립트 cmdlet은 .psm1 또는 .ps1 파일 확장명을 갖습니다.   
  
## <a name="porting-cim-cmdlets"></a>CIM cmdlet 이식  
일반적으로 이러한 cmdlet은 아무 변환 작업 없이도 Nano 서버에서 작동합니다. 그러나 아직 기본 WMI v2 공급자를 Nano 서버에서 실행되도록 이식하지 않았다면 이식해야 합니다.  
  
### <a name="building-c-for-nano-server"></a>Nano 서버용 C++ 작성  
C++ DLL이 Nano 서버에서 작동하게 하려면 특정 버전이 아닌 Nano 서버에 대해 컴파일해야 합니다.  
  
Nano 서버에서 C++를 개발하기 위한 필수 조건 및 연습은 [Nano 서버에서 네이티브 앱 개발](http://blogs.technet.com/b/nanoserver/archive/2016/04/27/developing-native-apps-on-nano-server.aspx)을 참조하세요.  
  
  
## <a name="porting-net-cmdlets"></a>.NET cmdlet 이식  
대부분의 C# 코드는 Nano 서버에서 지원됩니다. [ApiPort](https://github.com/Microsoft/dotnet-apiport)를 사용하여 호환되지 않는 API를 검색할 수 있습니다.  
  
### <a name="powershell-core-sdk"></a>Powershell Core SDK  
"Microsoft.PowerShell.NanoServer.SDK" 모듈은 [PowerShell 갤러리](https://www.powershellgallery.com/packages/Microsoft.PowerShell.NanoServer.SDK/)에 제공되며 Visual Studio 2015 업데이트 2를 사용하여 Nano 서버에서 사용할 수 있는 CoreCLR 및 PowerShell Core 버전을 대상으로 하는 .NET cmdlet 개발을 도와줍니다. 다음 명령으로 PowerShellGet을 사용하여 모듈을 설치할 수 있습니다.  
  
`Find-Module Microsoft.PowerShell.NanoServer.SDK -Repository PSGallery | Install-Module -Scope <scope>`  
  
PowerShell Core SDK 모듈은 올바른 CoreCLR 및 PowerShell Core 참조 어셈블리를 설치하고, Visual Studio 2015에서 이러한 참조 어셈블리를 대상으로 하는 C# 프로젝트를 만들고, 개발자가 Nano 서버에서 실행되는 .NET cmdlet을 Visual Studio 2015에서 원격으로 디버깅할 수 있도록 Nano 서버 컴퓨터에 원격 디버거를 설치하는 cmdlet을 표시합니다.  
  
PowerShell Core SDK 모듈에는 Visual Studio 2015 업데이트 2가 필요합니다. 아직 Visual Studio 2015를 설치하지 않았으면 [Visual Studio Community 2015](https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx)를 설치할 수 있습니다.  
  
또한 SDK 모듈은 다음 기능을 사용하여 Visual Studio 2015에 설치됩니다.  
  
- Windows 및 웹 개발 -> 유니버설 Windows 앱 개발 도구 -> 도구(1.3.1) 및 Windows 10 SDK  
  
SDK 모듈을 사용하기 전에 Visual Studio 설치를 검토하여 이러한 필수 조건을 충족하는지 확인하세요. Visual Studio를 설치하는 동안 위의 기능을 설치하도록 선택하거나 기존에 설치된 Visual Studio 2015를 수정하여 위의 기능을 설치합니다.  
  
PowerShell Core SDK 모듈에는 다음 cmdlet이 포함되어 있습니다.  
- New-NanoCSharpProject: 새 Visual Studio를 만듭니다 C# CoreCLR 및 Nano Server의 Windows Server 2016 릴리스에 포함 된 PowerShell Core를 대상으로 하는 프로젝트입니다.  
- Show-SdkSetupReadMe: 파일 탐색기에서 SDK 루트 폴더를 열고 수동 설치를 위한 README.txt 파일을 엽니다.  
- Install-remotedebugger: 설치 하 고 Nano 서버 컴퓨터에 Visual Studio 원격 디버거를 구성 합니다.  
- Start-RemoteDebugger: Nano Server를 실행 하는 원격 컴퓨터에서 원격 디버거를 시작 합니다.  
- Stop-remotedebugger: Nano Server를 실행 하는 원격 컴퓨터에서 원격 디버거를 중지 합니다.  
  
이러한 cmdlet을 사용하는 방법에 대한 자세한 내용을 보려면 다음과 같이 모듈을 설치하고 가져온 후 각 cmdlet에서 Get-help를 실행합니다.  
  
`Get-Command -Module Microsoft.PowerShell.NanoServer.SDK | Get-Help -Full`   
  
  
### <a name="searching-for-compatible-apis"></a>호환되는 API 검색  
  
API 카탈로그에서 .NET Core를 검색하거나 Core CLR 참조 어셈블리를 디스어셈블할 수 있습니다. .NET API의 플랫폼 이식성에 대한 자세한 내용은 [플랫폼 이식성](https://github.com/Microsoft/dotnet-apiport/blob/master/docs/HowTo/PlatformPortability.md)을 참조하세요.  
  
### <a name="pinvoke"></a>PInvoke  
Nano 서버가 사용하는 Core CLR에서, kernel32.dll 및 advapi32.dll 같은 일부 기본 DLL이 다양한 API 집합으로 분할되었기 때문에 PInvoke가 올바른 API를 참조하도록 유의해야 합니다. 비호환성이 있으면 런타임 오류가 발생합니다.  
  
Nano 서버에서 지원되는 네이티브 API 목록은 [Nano 서버 API](https://msdn.microsoft.com/library/mt588480(v=vs.85).aspx)를 참조하세요.  
  
### <a name="building-c-for-nano-server"></a>Nano 서버용 C# 작성  
  
`New-NanoCSharpProject`를 사용하여 Visual Studio 2015에서 C# 프로젝트를 만들었으면 **빌드** 메뉴를 클릭하고 **프로젝트 빌드** 또는 **솔루션 빌드**를 선택하여 간단하게 Visual Studio에서 해당 프로젝트를 빌드할 수 있습니다. 생성된 어셈블리는 Nano 서버에 제공된 올바른 CoreCLR 및 PowerShell Core를 대상으로 하며, 개발자는 Nano 서버를 실행하는 컴퓨터로 해당 어셈블리를 간단하게 복사하여 사용할 수 있습니다.  
  
### <a name="building-managed-c-cppcli-for-nano-server"></a>Nano 서버용 관리형 C++(CPP/CLI) 작성  
관리형 C++는 CoreCLR에 지원되지 않습니다. CoreCLR에 이식하는 경우 C++ 코드를 C#으로 다시 작성하고 모든 네이티브 호출은 PInvoke 통해 수행해야 합니다.  
  
## <a name="porting-powershell-script-cmdlets"></a>PowerShell 스크립트 cmdlet 이식  
  
PowerShell Core는 Windows Server 2016 및 Windows 10에서 실행되는 버전을 포함하여 다른 PowerShell 버전과 완전한 PowerShell 언어 패리티를 갖고 있습니다. 그러나 PowerShell 스크립트 cmdlet를 Nano 서버로 이식할 때에는 다음 사항에 유의해야 합니다.  
* 다른 cmdlet에 종속되어 있나요? 만약 그렇다면 해당 cmdlet을 Nano 서버에서 사용할 수 있나요? 사용할 수 없는 cmdlet에 대한 정보는 [Nano 서버의 PowerShell](PowerShell-on-Nano-Server.md)을 참조하세요.  
* 런타임에 로드되는 어셈블리에 종속되어 있다면, 해당 어셈블리가 여전히 작동할까요?   
* 스크립트를 어떻게 원격으로 디버깅할 수 있나요?   
* 어떻게 WMI .Net에서 MI .Net으로 마이그레이션할 수 있나요?  
  
### <a name="dependency-on-built-in-cmdlets"></a>기본 제공 cmdlet에 대한 종속성  
Windows Server 2016의 모든 cmdlet을 Nano 서버에서 사용할 수 있는 것은 아닙니다([Nano 서버의 PowerShell](PowerShell-on-Nano-Server.md) 참조). Nano 서버 가상 컴퓨터를 설치하고 필요한 cmdlet을 사용할 수 있는지 검색하는 것이 가장 좋은 방법입니다. 이렇게 하려면 `Enter-PSSession`을 실행하여 대상 Nano 서버에 연결한 다음 `Get-Command -CommandType Cmdlet, Function`을 실행하여 사용 가능한 cmdlet 목록을 가져옵니다.  
  
### <a name="consider-using-powershell-classes"></a>PowerShell 클래스 사용을 고려  
인라인 C# 코드 컴파일을 위해 Nano 서버에서 Add-Type이 지원됩니다. 새 코드를 작성하거나 기존 코드를 이식하는 경우 PowerShell 클래스를 사용하여 사용자 지정 형식을 정의하는 방법도 고려해 볼 수 있습니다. 열거형뿐 아니라 속성 모음 시나리오에도 PowerShell 클래스를 사용할 수 있습니다. PInvoke를 수행해야 하는 경우 Add-Type을 사용하여 C#을 통해 또는 사전 컴파일된 어셈블리에서 수행합니다.  
다음은 Add-Type 사용을 보여 주는 샘플입니다.  
  
```  
Add-Type -ReferencedAssemblies ([Microsoft.Management.Infrastructure.Ciminstance].Assembly.Location) -TypeDefinition @'  
public class TestNetConnectionResult  
{  
   // The compute name  
   public string ComputerName = null;  
   // The Remote IP address used for connectivity  
   public System.Net.IPAddress RemoteAddress = null;  
}  
'@  
# Create object and set properties  
$result = New-Object TestNetConnectionResult  
$result.ComputerName = "Foo"  
$result.RemoteAddress = 1.1.1.1  
  
```  
 이 샘플에서는 Nano 서버에서 PowerShell 클래스를 사용합니다.  
   
```  
class TestNetConnectionResult    
{    
   # The compute name  
  [string] $ComputerName    
  
  #The Remote IP address used for connectivity    
  [System.Net.IPAddress] $RemoteAddress  
}  
# Create object and set properties  
$result = [TestNetConnectionResult]::new()  
$result.ComputerName = "Foo"  
$result.RemoteAddress = 1.1.1.1  
  
```  
  
### <a name="remotely-debugging-scripts"></a>원격으로 스크립트 디버깅  
  
원격으로 스크립트를 디버깅하려면 PowerShell ISE에서 `Enter-PSsession`을 사용하여 원격 컴퓨터에 연결합니다. 세션 내부에 연결된 후 `psedit <file_path>`를 실행하면 파일 복사본이 로컬 PowerShell ISE에서 열립니다. 그런 다음 중단점을 설정하여 마치 로컬로 실행하는 것처럼 스크립트를 디버깅할 수 있습니다. 또한 이 파일의 모든 변경 내용은 원격 버전에 저장됩니다.   
  
### <a name="migrating-from-wmi-net-to-mi-net"></a>WMI .NET에서 MI .NET으로 마이그레이션  
  
[WMI.NET](https://msdn.microsoft.com/library/mt481551(v=vs.110).aspx) 는 지원 되지 않으므로 이전 API를 사용 하 여 모든 cmdlet이 지원 되는 WMI API를 마이그레이션해야 합니다. [MI. NET](https://msdn.microsoft.com/library/dn387184(v=vs.85).aspx)으로 마이그레이션해야 합니다. C#을 통해 또는 CimCmdlets 모듈의 cmdlet을 통해 MI.NET에 직접 액세스할 수 있습니다.   
  
### <a name="cimcmdlets-module"></a>CimCmdlets 모듈  
  
WMI v1 cmdlet(예: Get-WmiObject)은 Nano 서버에서 지원되지 않습니다. 그러나 CimCmdlets 모듈의 CIM cmdlet(예: Get-CimInstance)은 지원됩니다. CIM cmdlet은 WMI v1 cmdlet과 매우 밀접하게 매핑됩니다. 예를 들어 Get-WmiObject 개체는 Get-CimInstance와 매우 비슷한 매개 변수를 사용한다는 연관 관계가 있습니다. 메서드 호출 구문은 약간 다르지만 Invoke-CimMethod를 통해 잘 설명되어 있습니다. 매개 변수 입력에 주의해야 합니다. MI.NET은 메서드 매개 변수 형식에 대한 요구 사항이 엄격합니다.  
  
### <a name="c-api"></a>C# API  
  
WMI .NET은 WMIv1 인터페이스를 래핑하고, MI .NET은 WMIv2(CIM) 인터페이스를 래핑합니다. 노출하는 클래스는 다를 수 있지만 기본 작업은 매우 유사합니다. 개체 인스턴스를 열거하거나 가져온 후 그 인스턴스에서 작업을 호출하여 작업을 수행합니다.   
  
  


