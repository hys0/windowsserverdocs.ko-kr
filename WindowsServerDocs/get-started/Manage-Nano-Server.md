---
title: Nano 서버 관리
description: 업데이트, 서비스 패키지, 네트워킹 추적, 성능 모니터링
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 599d6438-a506-4d57-a0ea-1eb7ec19f46e
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 165b7e7aea7a7d0bb56d21f350f6ee646d5fa973
ms.sourcegitcommit: af80963a1d16c0b836da31efd9c5caaaf6708133
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/31/2019
ms.locfileid: "67280405"
---
# <a name="manage-nano-server"></a>Nano 서버 관리

>적용 대상: Windows Server 2016

> [!IMPORTANT]
> Windows Server, 버전 1709부터 [컨테이너 기본 OS 이미지](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)로만 Nano 서버를 사용할 수 있습니다. [Nano 서버 변경 사항](nano-in-semi-annual-channel.md)을 확인하여 그 의미를 알아보세요.   

Nano 서버는 원격으로 관리됩니다. 로컬 로그온 기능이 전혀 없으며 터미널 서비스를 지원하지도 않습니다. 그러나 Windows PowerShell, WMI(Windows Management Instrumentation), Windows 원격 관리, EMS(응급 관리 서비스)를 포함하여 Nano 서버를 원격으로 관리할 수 있는 다양한 옵션이 제공됩니다.  

원격 관리 도구를 사용하려면 아마도 Nano 서버의 IP 주소를 알아야 할 것입니다. IP 주소를 확인하는 몇 가지 방법이 있습니다.  
  
-   Nano 복구 콘솔을 사용합니다(자세한 내용은 이 토픽의 Nano 서버 복구 콘솔 섹션 참조).  
  
-   컴퓨터에 직렬 케이블을 연결하고 EMS를 사용합니다.  
  
-   Nano 서버를 구성할 때 할당한 컴퓨터 이름을 사용하면 ping으로 IP 주소를 가져올 수 있습니다. 정의합니다(예: `ping NanoServer-PC /4`).  
  
## <a name="using-windows-powershell-remoting"></a>Windows PowerShell 원격 기능 사용  
Windows PowerShell 원격 기능으로 Nano 서버를 관리하려면 관리 컴퓨터의 신뢰할 수 있는 호스트 목록에 Nano 서버의 IP 주소를 추가하고, 사용하는 계정을 Nano 서버의 관리자에 추가하고, 해당 기능을 사용할 생각이라면 CredSSP를 사용하도록 설정해야 합니다.  

> [!NOTE]
> 대상 Nano 서버와 관리 컴퓨터가 동일한 AD DS 포리스트(또는 트러스트 관계의 포리스트)에 있는 경우 Nano 서버를 신뢰할 수 있는 호스트 목록에 추가하면 안 됩니다. 그 대신 정규화된 도메인 이름을 사용하여 Nano 서버에 연결할 수 있습니다. 예: PS C:\> Enter-PSSession -ComputerName nanoserver.contoso.com -Credential (Get-Credential)
  
  
신뢰할 수 있는 호스트 목록에 Nano 서버를 추가하려면 관리자 권한 Windows PowerShell 명령 프롬프트에서 이 명령을 실행 합니다.  
  
`Set-Item WSMan:\localhost\Client\TrustedHosts "<IP address of Nano Server>"`  
  
원격 Windows PowerShell 세션을 시작하려면 관리자 권한 로컬 Windows PowerShell 세션을 시작한 후 다음 명령을 실행합니다.  
  
  
```  
$ip = "<IP address of Nano Server>"  
$user = "$ip\Administrator"  
Enter-PSSession -ComputerName $ip -Credential $user  
```  
  
  
이제 정상적으로 Nano 서버에서 Windows PowerShell 명령을 실행할 수 있습니다.  
  
> [!NOTE]  
> 이 Nano 서버 릴리스에서 사용할 수 없는 Windows PowerShell 명령도 있습니다. 사용할 수 있는 명령을 보려면 `Get-Command -CommandType Cmdlet` 실행  
  
`Exit-PSSession` 명령으로 원격 세션 중지  
  
## <a name="using-windows-powershell-cim-sessions-over-winrm"></a>WinRM을 통해 Windows PowerShell CIM 세션 사용  
WinRM(Windows Remote Management)을 통해 Windows PowerShell에서 CIM 세션 및 인스턴스를 사용하여 WMI 명령을 실행할 수 있습니다.  
  
Windows PowerShell 프롬프트에서 다음 명령을 실행하여 CIM 세션을 시작합니다.  
  
  
```  
$ip = "<IP address of the Nano Server\>"  
$user = $ip\Administrator  
$cim = New-CimSession -Credential $user -ComputerName $ip  
```  
  
  
세션이 설정되면 다음과 같은 다양한 WMI 명령을 실행할 수 있습니다.  
  
  
```  
Get-CimInstance -CimSession $cim -ClassName Win32_ComputerSystem | Format-List *  
Get-CimInstance -CimSession $Cim -Query "SELECT * from Win32_Process WHERE name LIKE 'p%'"  
```  
  
  
## <a name="windows-remote-management"></a>Windows 원격 관리  
WinRM(Windows Remote Management)을 사용하여 Nano 서버에서 원격으로 프로그램을 실행할 수 있습니다. WinRM을 사용하려면 먼저 관리자 권한 명령 프롬프트에서 다음 명령을 실행하여 코드 페이지를 설정합니다.  
  
```
winrm quickconfig
winrm set winrm/config/client @{TrustedHosts="<ip address of Nano Server>"}
chcp 65001
```
  
이제 Nano 서버에서 원격으로 명령을 실행할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

```
winrs -r:<IP address of Nano Server> -u:Administrator -p:<Nano Server administrator password> ipconfig
```
  
Windows Remote Management에 대한 자세한 내용은 [WinRM(Windows 원격 관리) 개요](https://technet.microsoft.com/library/dn265971.aspx)를 참조하세요.  
   
   
  
## <a name="running-a-network-trace-on-nano-server"></a>Nano 서버에서 네트워크 추적 실행  
 Netsh trace, Tracelog.exe 및 Logman.exe는 Nano 서버에서 사용할 수 없습니다. 네트워크 패킷을 캡처하려면 다음 Windows PowerShell cmdlet을 사용합니다.  
   
   
```  
New-NetEventSession [-Name]  
Add-NetEventPacketCaptureProvider -SessionName  
Start-NetEventSession [-Name]  
Stop-NetEventSession [-Name]  
```  
이러한 cmdlet은 [Windows PowerShell의 네트워크 이벤트 패킷 캡처 Cmdlet](https://technet.microsoft.com/library/dn268520(v=wps.630).aspx)에 자세히 설명되어 있습니다.  

## <a name="installing-servicing-packages"></a>서비스 패키지 설치  
서비스 패키지를 설치하려면 -ServicingPackagePath 매개 변수를 사용합니다(경로 배열을 .cab 파일에 전달할 수 있음).  
  
`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -ServicingPackagePath \\path\to\kb123456.cab`  
  
서비스 패키지 또는 핫픽스는 종종 .cab 파일이 포함된 KB 항목으로 다운로드됩니다. 다음 단계에 따라 .cab file 파일을 추출합니다. 그런 다음 -ServicingPackagePath 매개 변수를 사용하여 이 파일을 설치할 수 있습니다.  
  
1.  서비스 패키지를 다운로드합니다(관련 기술 자료 문서에서 또는 [Microsoft 업데이트 카탈로그](https://catalog.update.microsoft.com/v7/site/home.aspx)에서). 로컬 디렉터리 또는 네트워크 공유에 저장합니다(예: C:\ServicingPackages).  
2.  추출된 서비스 패키지를 저장할 폴더를 만듭니다.  예: c:\KB3157663_expanded  
3.  Windows PowerShell 콘솔을 열고 `Expand` 명령을 사용하여 `-f:*` 매개 변수 및 서비스 패키지를 추출할 경로가 포함된 서비스 패키지의 .msu 파일 경로를 지정합니다.  예: `Expand "C:\ServicingPackages\Windows10.0-KB3157663-x64.msu" -f:* "C:\KB3157663_expanded"`  
  
    확장된 파일은 다음과 비슷하게 표시됩니다.  
C:>dir C:\KB3157663_expanded   
C 드라이브의 볼륨은 OS  
볼륨 일련 번호는 B05B-CC3D  
   
      C:\KB3157663_expanded의 디렉터리  
   
      2016/04/19  오후 01:17    \<DIR>          .  
      2016/04/19  오후 01:17    \<DIR&gt;          .  
        2016/04/17  오전 12:31               517 Windows10.0-KB3157663-x64-pkgProperties.txt  
2016/04/17  오전 12:30 AM        93,886,347 Windows10.0-KB3157663-x64.cab  
2016/04/17  오전 12:31               454 Windows10.0-KB3157663-x64.xml  
2016/04/17  오전 12:36           185,818 WSUSSCAN.cab  
               4개 파일     94,073,136바이트  
               2개 디렉터리  328,559,427,584바이트 여유 공간  
4.  -ServicingPackagePath 매개 변수를 사용하여 `New-NanoServerImage` 명령을 실행하고 이 디렉터리의 .cab 파일을 지정합니다(예: `New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -ServicingPackagePath C:\KB3157663_expanded\Windows10.0-KB3157663-x64.cab`).  

## <a name="managing-updates-in-nano-server"></a>Nano Server에서 업데이트 관리

현재 WMI(Windows Management Instrumentation)용 Windows 업데이트 공급자를 사용하여 적용 가능한 업데이트 목록을 찾은 후 전체 또는 일부를 설치할 수 있습니다. WSUS(Windows Server Update Services)를 사용하는 경우 WSUS 서버에 연결하여 업데이트를 가져오도록 Nano 서버를 구성할 수도 있습니다.  

어떤 경우든 가장 먼저 할 일은 Nano 서버 컴퓨터에 원격 Windows PowerShell 세션을 설정하는 것입니다. 이 예제에서는 세션에 *$sess*를 사용합니다. 다른 요소를 사용하는 경우 필요한 대로 해당 요소를 대체하면 됩니다.  


### <a name="view-all-available-updates"></a>사용 가능한 모든 업데이트 보기  
---  
다음 명령을 사용하여 적용 가능한 전체 업데이트 목록을 가져옵니다.  
```  
$sess = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession  

$scanResults = Invoke-CimMethod -InputObject $sess -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=0";OnlineScan=$true}  
```  
**참고:**  
사용 가능한 업데이트가 없는 경우 이 명령은 다음 오류를 반환합니다.  
```  
Invoke-CimMethod : A general error occurred that is not covered by a more specific error code.  

At line:1 char:16  

+ ... anResults = Invoke-CimMethod -InputObject $sess -MethodName ScanForUp ...  

+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~  

    + CategoryInfo          : NotSpecified: (MSFT_WUOperatio...-5b842a3dd45d")  

   :CimInstance) [Invoke-CimMethod], CimException  

    + FullyQualifiedErrorId : MI RESULT 1,Microsoft.Management.Infrastructure.  

   CimCmdlets.InvokeCimMethodCommand  
```  

### <a name="install-all-available-updates"></a>사용 가능한 업데이트 모두 설치  
---  
다음 명령을 사용하여 사용 가능한 **모든** 업데이트를 한 번에 검색하여 다운로드 및 설치할 수 있습니다.  

```  
$sess = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession  

$scanResults = Invoke-CimMethod -InputObject $sess -MethodName ApplyApplicableUpdates  

Restart-Computer  
```  
**참고:**  
Windows Defender는 업데이트 설치를 차단합니다. 이 문제를 해결하려면 Windows Defender를 제거하고, 업데이트를 설치한 다음 Windows Defender를 다시 설치합니다. 또는 다른 컴퓨터에 업데이트를 다운로드하여 Nano 서버에 복사한 다음 DISM.exe를 사용하여 업데이트를 적용합니다.  


### <a name="verify-installation-of-updates"></a>업데이트 설치 확인  
---  
다음 명령을 사용하여 현재 설치된 업데이트 목록을 가져옵니다.  
```  
$sess = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession  

$scanResults = Invoke-CimMethod -InputObject $sess -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=1";OnlineScan=$true}  
```  

**참고:**  
이러한 명령은 설치된 업데이트 목록을 표시하지만 출력에 "설치됨"이라고 구체적으로 표시하지는 않습니다. 보고서처럼 출력에 이러한 내용이 포함되기를 원한다면 다음 명령을 실행합니다.  
```  
Get-WindowsPackage--Online  
```  

### <a name="using-wsus"></a>WSUS 사용  
---  
위에 나열된 명령은 인터넷에서 Windows Update 및 Microsoft 업데이트 서비스를 쿼리하여 업데이트를 찾아서 다운로드합니다. WSUS를 사용하는 경우 Nano 서버에서 레지스트리 키를 설정하면 WSUS 서버를 대신 사용할 수 있습니다.  
  
[비 Active Directory 환경에서 자동 업데이트 구성](https://technet.microsoft.com/library/cc708449(v=ws.10).aspx)의 "Windows 업데이트 에이전트 환경 옵션 레지스트리 키" 테이블을 참조하세요.  
  
적어도 **WUServer** 및 **WUStatusServer** 레지스트리 키를 설정해야 하지만, WSUS을 구현한 방법에 따라 다른 값이 필요할 수 있습니다. 언제든지 동일한 환경에서 다른 Windows Server를 검사하여 이러한 설정을 확인할 수 있습니다.  

WSUS에 대한 이러한 값이 설정되면 위 섹션의 명령은 해당 서버를 쿼리하여 업데이트를 찾아서 소스를 다운로드합니다.  

### <a name="automatic-updates"></a>자동 업데이트  
---  
현재 자동으로 업데이트를 설치하는 방법은 위의 단계를 로컬 Windows PowerShell 스크립트로 변환한 다음 예약 작업을 실행하고 일정에 따라 시스템을 다시 시작하는 예약 작업을 만드는 것입니다.


## <a name="performance-and-event-monitoring-on-nano-server"></a>Nano 서버의 성능 및 이벤트 모니터링
[comment]: # (Venkat Yalla에서.)
Nano 서버는 [ETW(Windows 용 이벤트 추적)](https://aka.ms/u2pa0i) 프레임 워크를 완벽하게 지원하지만, 추적 및 성능 카운터에 사용되는 몇 가지 친숙한 도구는 현재 Nano 서버에서 사용할 수 없습니다. 그러나 Nano 서버에는 대부분의 일반적인 성능 분석 시나리오를 수행할 수 있는 도구와 cmdlet이 있습니다.

상위 수준 워크플로는 여느 Windows Server 설치와 똑같이 유지됩니다. 오버헤드가 낮은 추적은 대상(Nano 서버) 컴퓨터에서 수행되고, 그 결과로 얻는 추적 파일 및/또는 로그는 별도의 컴퓨터에서 [Windows Performance Analyzer](https://msdn.microsoft.com/library/windows/hardware/hh448170.aspx), [Message Analyzer](https://www.microsoft.com/download/details.aspx?id=44226) 등의 도구를 사용하여 오프라인으로 후 처리됩니다.

> [!NOTE]
> PowerShell 원격을 사용하여 파일을 전송하는 방법에 대한 자세한 내용은 리프레셔에 대한 [Nano 서버와 파일을 복사하는 방법](https://aka.ms/nri9c8)을 참조하세요.

다음 섹션에는 가장 일반적인 성능 데이터 수집 활동과 함께 Nano 서버에서 이러한 활동 수행을 위해 지원하는 방법이 나열되어 있습니다.

### <a name="query-available-event-providers"></a>사용 가능한 이벤트 공급자 쿼리
[Windows Performance Recorder](https://msdn.microsoft.com/library/hh448229.aspx)는 다음과 같이 사용 가능한 이벤트 공급자를 쿼리하는 도구입니다.
```
wpr.exe -providers
```

사용자는 관심 있는 이벤트의 형식에 대한 출력을 필터링 할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.
```
PS C:\> wpr.exe -providers | select-string "Storage"

       595f33ea-d4af-4f4d-b4dd-9dacdd17fc6e                              : Microsoft-Windows-StorageManagement-WSP-Host
       595f7f52-c90a-4026-a125-8eb5e083f15e                              : Microsoft-Windows-StorageSpaces-Driver
       69c8ca7e-1adf-472b-ba4c-a0485986b9f6                              : Microsoft-Windows-StorageSpaces-SpaceManager
       7e58e69a-e361-4f06-b880-ad2f4b64c944                              : Microsoft-Windows-StorageManagement
       88c09888-118d-48fc-8863-e1c6d39ca4df                              : Microsoft-Windows-StorageManagement-WSP-Spaces
```

### <a name="record-traces-from-a-single-etw-provider"></a>단일 ETW 공급자에서 레코드 추적
새 [이벤트 추적 관리 cmdlet](https://technet.microsoft.com/library/dn919247.aspx)을 이 용도로 사용할 수 있습니다. 다음은 워크플로 예입니다.

추적을 만들고 시작한 다음, 이벤트를 저장할 파일 이름을 지정합니다.
```
PS C:\> New-EtwTraceSession -Name "ExampleTrace" -LocalFilePath c:\etrace.etl
```

추적에 공급자 GUID를 추가합니다. ```wpr.exe -providers```를 사용하여 공급자 이름을 GUID로 변환합니다. 
```
PS C:\> wpr.exe -providers | select-string "Kernel-Memory"

       d1d93ef7-e1f2-4f45-9943-03d245fe6c00                              : Microsoft-Windows-Kernel-Memory

PS C:\> Add-EtwTraceProvider -Guid "{d1d93ef7-e1f2-4f45-9943-03d245fe6c00}" -SessionName "ExampleTrace"
```

추적 제거 -- 이 작업은 추적 세션을 중지하고, 이벤트를 관련 로그 파일에 플러시합니다.
```
PS C:\> Remove-EtwTraceSession -Name "ExampleTrace"

PS C:\> dir .\etrace.etl

    Directory: C:\

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/14/2016  11:17 AM       16515072 etrace.etl
```
> [!NOTE]
> 다음 예에서는 단일 추적 공급자를 세션에 추가하는 방법을 보여 주지만, 공급자 GUID가 다른 추적 세션에서 ```Add-EtwTraceProvider``` cmdlet을 여러 차례 사용하여 여러 원본에서 추적을 사용하도록 설정하는 방법도 있습니다. 또 다른 방법은 아래에 설명된 ```wpr.exe``` 프로필을 사용하는 것입니다.

### <a name="record-traces-from-multiple-etw-providers"></a>여러 ETW 공급자에서 레코드 추적
[Windows Performance Recorder](https://msdn.microsoft.com/library/hh448229.aspx)의 ```-profiles``` 옵션은 동시에 여러 동급자에서 추적을 활성화합니다. CPU, 네트워크, DiskIO 등 여러 가지 기본 제공 프로필 중에 선택할 수 있습니다.
```
PS C:\Users\Administrator\Documents> wpr.exe -profiles 

Microsoft Windows Performance Recorder Version 10.0.14393 (CoreSystem)
Copyright (c) 2015 Microsoft Corporation. All rights reserved.

        GeneralProfile              First level triage
        CPU                         CPU usage
        DiskIO                      Disk I/O activity
        FileIO                      File I/O activity
        Registry                    Registry I/O activity
        Network                     Networking I/O activity
        Heap                        Heap usage
        Pool                        Pool usage
        VirtualAllocation           VirtualAlloc usage
        Audio                       Audio glitches
        Video                       Video glitches
        Power                       Power usage
        InternetExplorer            Internet Explorer
        EdgeBrowser                 Edge Browser
        Minifilter                  Minifilter I/O activity
        GPU                         GPU activity
        Handle                      Handle usage
        XAMLActivity                XAML activity
        HTMLActivity                HTML activity
        DesktopComposition          Desktop composition activity
        XAMLAppResponsiveness       XAML App Responsiveness analysis
        HTMLResponsiveness          HTML Responsiveness analysis
        ReferenceSet                Reference Set analysis
        ResidentSet                 Resident Set analysis
        XAMLHTMLAppMemoryAnalysis   XAML/HTML application memory analysis
        UTC                         UTC Scenarios
        DotNET                      .NET Activity
        WdfTraceLoggingProvider     WDF Driver Activity
```

사용자 지정 프로필을 만드는 방법에 대한 자세한 지침은 [WPR.exe 설명서](https://msdn.microsoft.com/library/windows/hardware/hh448223.aspx)를 참조하세요.

### <a name="record-etw-traces-during-operating-system-boot-time"></a>운영 체제가 부팅되는 동안 레코드 ETW 추적
시스템이 부팅되는 동안 ```New-AutologgerConfig``` cmdlet을 사용하여 이벤트를 수집합니다. 사용법은 ```New-EtwTraceSession``` cmdlet과 매우 유사하지만, Autologger의 구성에 추가되는 공급자가 다음 부팅 초기에만 활성화됩니다. 전체적인 워크플로는 다음과 같습니다.

먼저 새 Autologger config 파일을 만듭니다.
```
PS C:\> New-AutologgerConfig -Name "BootPnpLog" -LocalFilePath c:\bootpnp.etl 
```

이 파일에 ETW 공급자를 추가합니다. 이 예에서는 커널 PnP 공급자를 사용합니다. ```Add-EtwTraceProvider```를 다시 호출하고, 여러 원본에서 부팅 추적 컬렉션을 사용하도록 Autologger 이름은 같지만 GUID는 다르게 지정합니다.
```
Add-EtwTraceProvider -Guid "{9c205a39-1250-487d-abd7-e831c6290539}" -AutologgerName BootPnpLog
```

이렇게 하면 ETW 세션이 즉시 시작하는 것이 아니라 다음 부팅에 시작하는 세션이 하나 구성됩니다. 다시 부팅하면 Autologger 구성 이름을 가진 새 ETW 세션이 추가된 추적 공급자가 활성화된 상태로 자동 시작됩니다. Nano 서버가 부팅되면 다음 명령은 기록된 이벤트를 관련 추적 파일에 플러시한 후 추적 세션을 중지합니다.
```
PS C:\> Remove-EtwTraceSession -Name BootPnpLog
```

다음 부팅 시 다른 추적 세션이 자동으로 생성되지 않게 하려면 다음과 같이 Autologger 구성을 제거합니다.
```
PS C:\> Remove-AutologgerConfig -Name BootPnpLog
```

다양한 시스템 또는 디스크 없는 시스템에서 부팅 및 설치 추적을 수집하려면 [설치 및 부팅 이벤트 수집](../administration/get-started-with-setup-and-boot-event-collection.md)을 고려해 보세요.

### <a name="capture-performance-counter-data"></a>성능 카운터 데이터 캡처
일반적으로 Perfmon.exe GUI를 사용하여 성능 카운터 데이터를 모니터링합니다. Nano 서버에서는 그에 해당하는 ```Typeperf.exe``` 명령줄을 사용합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

사용 가능한 카운터 쿼리--출력을 필터링하여 원하는 항목을 간편하게 찾을 수 있습니다.
```
PS C:\> typeperf.exe -q | Select-String "UDPv6"

\UDPv6\Datagrams/sec
\UDPv6\Datagrams Received/sec
\UDPv6\Datagrams No Port/sec
\UDPv6\Datagrams Received Errors
\UDPv6\Datagrams Sent/sec
```

옵션을 사용하여 카운터 값을 수집하는 횟수 및 간격을 지정할 수 있습니다. 아래 예에서는 프로세서 유휴 시간을 3초마다 5회 수집합니다.
```
PS C:\> typeperf.exe "\Processor Information(0,0)\% Idle Time" -si 3 -sc 5

"(PDH-CSV 4.0)","\\ns-g2\Processor Information(0,0)\% Idle Time"
"09/15/2016 09:20:56.002","99.982990"
"09/15/2016 09:20:59.002","99.469634"
"09/15/2016 09:21:02.003","99.990081"
"09/15/2016 09:21:05.003","99.990454"
"09/15/2016 09:21:08.003","99.998577"
Exiting, please wait...
The command completed successfully.
```

다른 명령줄 옵션을 사용하여 구성 파일에서 알고 싶은 성능 카운터 이름을 지정하고, 출력을 로그 파일로 리디렉션할 수 있으며, 그 외에도 여러 가지 일을 할 수 있습니다. 자세한 내용은 [typeperf.exe 설명서](https://technet.microsoft.com/library/bb490960.aspx)를 참조하세요.

또한 Nano 서버 대상과 함께 Perfmon.exe의 그래픽 인터페이스를 원격으로 사용할 수 있습니다. 성능 카운터를 보기에 추가할 때 기본 *<Local computer>* 대신 컴퓨터 이름에서 Nano 서버 대상을 지정합니다.

### <a name="interact-with-the-windows-event-log"></a>Windows 이벤트 로그와 상호 작용

Nano 서버는 ```Get-WinEvent``` cmdlet을 지원합니다. 이 cmdlet은 Windows 이벤트 로그 필터링 및 쿼리 기능을 로컬과 원격 컴퓨터에 모두 제공합니다. 자세한 옵션과 예제는 [Get-WinEvent 설명서 페이지](https://technet.microsoft.com/library/hh849682.aspx)에서 확인할 수 있습니다. 다음은 지난 이틀 동안 *시스템* 로그에 명시된 *오류*를 검색하는 간단한 예입니다.
```
PS C:\> $StartTime = (Get-Date) - (New-TimeSpan -Day 2)
PS C:\> Get-WinEvent -FilterHashTable @{LogName='System'; Level=2; StartTime=$StartTime} | select TimeCreated, Message

TimeCreated           Message
-----------           -------
9/15/2016 11:31:19 AM Task Scheduler service failed to start Task Compatibility module. Tasks may not be able to reg...
9/15/2016 11:31:16 AM The Virtualization Based Security enablement policy check at phase 6 failed with status: {File...
9/15/2016 11:31:16 AM The Virtualization Based Security enablement policy check at phase 0 failed with status: {File...
```

Nano 서버는 이벤트 로그 및 게시자에 대한 정보를 검색할 수 있는 ```wevtutil.exe```도 지원합니다. 자세한 내용은 [wevtutil.exe 설명서](https://aka.ms/qvod7p)를 참조하세요. 

### <a name="graphical-interface-tools"></a>그래픽 인터페이스 도구
웹 브라우저를 통해 [웹 기반 서버 관리 도구](https://blogs.technet.microsoft.com/servermanagement/2016/08/17/deploy-setup-server-management-tools/)를 사용하여 Nano 서버 대상을 관리하고 Nano 서버 이벤트 로그를 제공할 수 있습니다. 마지막으로, MMC 스냅인 이벤트 뷰어(eventvwr.msc)를 사용하여 로그를 볼 수도 있습니다. 데스크톱 컴퓨터에서 뷰어를 열고 원격 Nano 서버를 가리키기만 하면 됩니다.




## <a name="using-windows-powershell-desired-state-configuration-with-nano-server"></a>Nano 서버와 함께 Windows PowerShell 필요한 상태 구성 사용  
  
Windows PowerShell DSC(필요한 상태 구성)를 사용하여 Nano 서버를 대상 노드로 관리할 수 있습니다. 현재는 DSC 푸시 모드에서 Nano 서버를 실행하는 노드만 관리할 수 있습니다. 모든 DSC 기능이 Nano 서버와 연동하는 것은 아닙니다.  
  
자세한 내용은 [Nano 서버에서 DSC 사용](https://msdn.microsoft.com/powershell/dsc/nanoDsc)을 참조하세요.  
