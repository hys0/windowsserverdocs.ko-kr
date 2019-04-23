---
ms.date: 01/07/2019
ms.topic: conceptual
keywords: OpenSSH SSH, SSHD, 설치, 설정
contributor: maertendMSFT
author: maertendMSFT
title: OpenSSH의 Windows 설치
ms.openlocfilehash: f617b01ee7dabd4897f99e374420f673e209e145
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859564"
---
# <a name="installation-of-openssh-for-windows-server-2019-and-windows-10"></a>OpenSSH 2019 Windows Server 및 Windows 10 용 설치 #

OpenSSH 클라이언트와 OpenSSH 서버는 Windows Server 2019 및 Windows 10 1809 별도로 설치할 수 있는 구성 요소입니다.
이러한 Windows 버전을 사용 하 여 사용자가 설치 하 고 OpenSSH 구성 뒤에 나오는 지침을 사용 해야 합니다. 

> [!NOTE] 
> PowerShell Github 리포지토리에서 OpenSSH를 획득 하는 사용자 (https://github.com/PowerShell/OpenSSH-Portable) 여기에서 지침을 사용 해야 하 고 __안__ 다음이 지침을 따르세요. 


## <a name="installing-openssh-from-the-settings-ui-on-windows-server-2019-or-windows-10-1809"></a>Windows Server 2019 또는 Windows 10 1809 UI 설정에서 OpenSSH를 설치합니다.

OpenSSH 서버와 클라이언트의 Windows 10 1809 설치할 수 있는 기능입니다. 

OpenSSH를 설치 하려면 설정 시작한 앱으로 이동 > 앱 및 기능 > 선택적 기능 관리 합니다. 

이 목록을 OpenSSH 클라이언트가 이미 설치 되어 있는지 검사 합니다. 그렇지 않은 경우 페이지의 맨 위에 있는 선택한 "기능"을 추가 합니다. 

* OpenSSH 클라이언트를 설치 하려면 "OpenSSH 클라이언트"를 찾은 다음 "설치"를 클릭 합니다. 
* OpenSSH 서버를 설치 하려면 "OpenSSH 서버"를 찾은 다음 "설치"를 클릭 합니다. 

설치가 완료 되 면 앱에 반환 > 앱 및 기능 > 선택적 기능 관리 하는 나열 된 OpenSSH 구성 요소를 참조 해야 합니다.

> [!NOTE]
> OpenSSH 서버 설치를 만들고 "OpenSSH 서버-에-TCP" 이라는 방화벽 규칙을 사용 하도록 설정 합니다. 이 포트 22에서 SSH 트래픽을 허용 합니다. 

## <a name="installing-openssh-with-powershell"></a>PowerShell을 사용 하 여 OpenSSH 설치 

PowerShell을 사용 하 여 OpenSSH를 설치 하려면 먼저 관리자 권한으로 PowerShell을 시작 합니다.
OpenSSH 기능은 설치에 사용할 수 있는지 확인 하십시오.

```powershell
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'

# This should return the following output:

Name  : OpenSSH.Client~~~~0.0.1.0
State : NotPresent
Name  : OpenSSH.Server~~~~0.0.1.0
State : NotPresent
```

그런 다음 서버 및/또는 클라이언트 기능을 설치 합니다.

```powershell
# Install the OpenSSH Client
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Install the OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

# Both of these should return the following output:

Path          :
Online        : True
RestartNeeded : False
```

## <a name="uninstalling-openssh"></a>OpenSSH를 제거합니다.

Windows 설정을 사용 하 여 OpenSSH를 제거 하려면 설정을 시작한 앱으로 이동 > 앱 및 기능 > 선택적 기능 관리 합니다. 설치 된 기능 목록에서 OpenSSH 클라이언트 또는 OpenSSH 서버 구성 요소를 선택한 다음 제거를 선택 합니다.

PowerShell을 사용 하 여 OpenSSH를 제거 하려면 다음 명령 중 하나를 사용 합니다.

```powershell
# Uninstall the OpenSSH Client
Remove-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Uninstall the OpenSSH Server
Remove-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

제거 된 경우 서비스 사용 시 해당 OpenSSH를 제거 후 Windows 다시 시작 해야 합니다.


## <a name="initial-configuration-of-ssh-server"></a>SSH 서버의 초기 구성

초기 사용을 위해 OpenSSH 서버에서 Windows를 구성 하려면 관리자 권한으로 PowerShell을 시작 다음 SSHD 서비스를 시작 하려면 다음 명령을 실행 합니다.

```powershell
Start-Service sshd
# OPTIONAL but recommended:
Set-Service -Name sshd -StartupType 'Automatic'
# Confirm the Firewall rule is configured. It should be created automatically by setup. 
Get-NetFirewallRule -Name *ssh*
# There should be a firewall rule named "OpenSSH-Server-In-TCP", which should be enabled 
```

## <a name="initial-use-of-ssh"></a>초기 SSH 사용

Windows에서 OpenSSH 서버를 설치한 후 SSH 클라이언트가 설치 된 모든 Windows 장치에서 PowerShell을 사용 하 여 신속 하 게 테스트할 수 있습니다. PowerShell에서 다음 명령을 입력 합니다. 

```powershell
Ssh username@servername
```

다음과 유사한 메시지가 서버에 첫 번째 연결이 됩니다.

```
The authenticity of host 'servername (10.00.00.001)' can't be established.
ECDSA key fingerprint is SHA256:(<a large string>).
Are you sure you want to continue connecting (yes/no)?
```

대답 해야 "yes" 또는 "no"입니다. 로컬 시스템에 해당 서버를 추가 합니다을 "예"의 목록을 알려진 ssh 호스트 합니다.

이 시점에서 암호에 대 한 메시지가 됩니다. 보안 예방 조치로 암호 표시 되지 않습니다 입력 합니다. 

연결 되 면 다음과 유사한 명령 셸 프롬프트를 표시 됩니다.

```
domain\username@SERVERNAME C:\Users\username>
```

Windows OpenSSH 서버에서 사용 하는 기본 셸을 Windows 명령 셸입니다. 

