---
title: Nano 서버용 개발
description: PowerShell 원격 기능 및 CIM 세션
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 57079470-a1c1-4fdc-af15-1950d3381860
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 8d793dde9c41bc99b55eeb0da3a5ee4b025f08d6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443645"
---
# <a name="developing-for-nano-server"></a>Nano 서버용 개발

>적용 대상: Windows Server 2016

> [!IMPORTANT]
> Windows Server, 버전 1709부터 [컨테이너 기본 OS 이미지](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)로만 Nano 서버를 사용할 수 있습니다. [Nano 서버 변경 사항](nano-in-semi-annual-channel.md)을 확인하여 그 의미를 알아보세요. 

다음 토픽에서는 Nano 서버의 PowerShell이 어떻게 다른지 주요 차이점을 설명하고 Nano 서버에 사용할 고유의 PowerShell cmdlet 개발을 위한 지침을 제공합니다.

- [Nano 서버의 PowerShell](PowerShell-on-Nano-Server.md)
- [Nano 서버용 PowerShell Cmdlet 개발](Developing-PowerShell-Cmdlets-for-Nano-Server.md)

## <a name="using-windows-powershell-remoting"></a>Windows PowerShell 원격 기능 사용  
Windows PowerShell 원격 기능으로 Nano 서버를 관리하려면 관리 컴퓨터의 신뢰할 수 있는 호스트 목록에 Nano 서버의 IP 주소를 추가하고, 사용하는 계정을 Nano 서버의 관리자에 추가하고, 해당 기능을 사용할 생각이라면 CredSSP를 사용하도록 설정해야 합니다.  

> [!NOTE]
> Nano Server를 추가 해서는 안 경우 대상 Nano 서버와 관리 컴퓨터가 동일한 AD DS 포리스트 (또는 트러스트 관계가 있는 포리스트)-신뢰할 수 있는 호스트 목록에 수 연결한 Nano 서버에 정규화 된 도메인 이름을 사용 하 여 예를 들어: PS C:\> Enter-pssession-ComputerName nanoserver.contoso.com-Credential (Get-credential)
  
  
신뢰할 수 있는 호스트 목록에 Nano 서버를 추가하려면 관리자 권한 Windows PowerShell 명령 프롬프트에서 이 명령을 실행 합니다.  
  
`Set-Item WSMan:\localhost\Client\TrustedHosts "<IP address of Nano Server>"`  
  
원격 Windows PowerShell 세션을 시작하려면 관리자 권한 로컬 Windows PowerShell 세션을 시작한 후 다음 명령을 실행합니다.  
  
  
```  
$ip = "\<IP address of Nano Server>"  
$user = "$ip\Administrator"  
Enter-PSSession -ComputerName $ip -Credential $user  
```  
  
  
이제 정상적으로 Nano 서버에서 Windows PowerShell 명령을 실행할 수 있습니다.  
  
> [!NOTE]  
> 이 Nano 서버 릴리스에서 사용할 수 없는 Windows PowerShell 명령도 있습니다. 사용할 수 있는 확인 하려면 실행 `Get-Command -CommandType Cmdlet`  
  
명령 사용 하 여 원격 세션 중지 `Exit-PSSession`  
  
## <a name="using-windows-powershell-cim-sessions-over-winrm"></a>WinRM을 통해 Windows PowerShell CIM 세션 사용  
WinRM(Windows Remote Management)을 통해 Windows PowerShell에서 CIM 세션 및 인스턴스를 사용하여 WMI 명령을 실행할 수 있습니다.  
  
Windows PowerShell 프롬프트에서 다음 명령을 실행하여 CIM 세션을 시작합니다.  
  
  
```  
$ip = "<IP address of the Nano Server\>"  
$ip\Administrator  
$cim = New-CimSession -Credential $user -ComputerName $ip  
```  
  
  
세션이 설정되면 다음과 같은 다양한 WMI 명령을 실행할 수 있습니다.  
  
  
```  
Get-CimInstance -CimSession $cim -ClassName Win32_ComputerSystem | Format-List *  
Get-CimInstance -CimSession $Cim -Query "SELECT * from Win32_Process WHERE name LIKE 'p%'"  
```  
  
  