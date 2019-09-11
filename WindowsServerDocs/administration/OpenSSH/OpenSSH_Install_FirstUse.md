---
ms.date: 01/07/2019
ms.topic: conceptual
keywords: OpenSSH, SSH, SSHD, 설치, 설치
contributor: maertendMSFT
author: maertendMSFT
title: Windows 용 OpenSSH 설치
ms.openlocfilehash: 6a5d4d47fbb3f962c2a19582eb0a72810145a28c
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866878"
---
# <a name="installation-of-openssh-for-windows-server-2019-and-windows-10"></a>Windows Server 2019 및 Windows 10 용 OpenSSH 설치 #

OpenSSH Client 및 OpenSSH 서버는 Windows Server 2019 및 Windows 10 1809에서 별도로 설치할 수 있는 구성 요소입니다.
이러한 Windows 버전을 사용 하는 사용자는 OpenSSH를 설치 하 고 구성 하기 위해 다음 지침을 따라야 합니다. 

> [!NOTE] 
> PowerShell Github 리포지토리에서 OpenSSH을 획득 한 사용자 (이 https://github.com/PowerShell/OpenSSH-Portable) 설명서의 지침을 사용 해야 함), 이러한 지침 __을 사용 하면__ 안 됩니다. 


## <a name="installing-openssh-from-the-settings-ui-on-windows-server-2019-or-windows-10-1809"></a>Windows Server 2019 또는 Windows 10 1809의 설정 UI에서 OpenSSH 설치

OpenSSH client 및 server는 Windows 10 1809의 설치 가능한 기능입니다. 

OpenSSH를 설치 하려면 설정을 시작한 후 앱 > 앱 및 기능으로 이동 하 > 선택적 기능을 관리 합니다. 

OpenSSH client가 이미 설치 되어 있는지 확인 하려면이 목록을 검색 합니다. 그렇지 않은 경우 페이지 맨 위에 있는 "기능 추가"를 선택 하 고 다음을 수행 합니다. 

* OpenSSH client를 설치 하려면 "OpenSSH Client"를 찾은 다음 "설치"를 클릭 합니다. 
* OpenSSH 서버를 설치 하려면 "OpenSSH Server"를 찾은 다음 "설치"를 클릭 합니다. 

설치가 완료 되 면 앱 및 기능 > 앱으로 돌아가 선택적 기능 > 관리 합니다. 그러면 나열 된 OpenSSH 구성 요소가 표시 됩니다.

> [!NOTE]
> OpenSSH 서버를 설치 하면 "OpenSSH" 라는 방화벽 규칙이 생성 되 고 사용 하도록 설정 됩니다. 이 경우 포트 22에서 인바운드 SSH 트래픽이 허용 됩니다. 

## <a name="installing-openssh-with-powershell"></a>PowerShell을 사용 하 여 OpenSSH 설치 

PowerShell을 사용 하 여 OpenSSH를 설치 하려면 먼저 관리자 권한으로 PowerShell을 시작 합니다.
OpenSSH 기능을 설치할 수 있는지 확인 하려면 다음을 수행 합니다.

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

## <a name="uninstalling-openssh"></a>OpenSSH 제거

Windows 설정을 사용 하 여 OpenSSH를 제거 하려면 설정을 시작 하 고 앱 > 앱 및 기능으로 이동 하 > 선택적 기능을 관리 합니다. 설치 된 기능 목록에서 OpenSSH Client 또는 OpenSSH 서버 구성 요소를 선택한 다음 제거를 선택 합니다.

PowerShell을 사용 하 여 OpenSSH를 제거 하려면 다음 명령 중 하나를 사용 합니다.

```powershell
# Uninstall the OpenSSH Client
Remove-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Uninstall the OpenSSH Server
Remove-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

OpenSSH를 제거한 후에도 Windows를 다시 시작 해야 할 수 있습니다.


## <a name="initial-configuration-of-ssh-server"></a>SSH 서버의 초기 구성

Windows에서 초기 사용을 위해 OpenSSH 서버를 구성 하려면 관리자 권한으로 PowerShell을 시작한 후 다음 명령을 실행 하 여 SSHD 서비스를 시작 합니다.

```powershell
Start-Service sshd
# OPTIONAL but recommended:
Set-Service -Name sshd -StartupType 'Automatic'
# Confirm the Firewall rule is configured. It should be created automatically by setup. 
Get-NetFirewallRule -Name *ssh*
# There should be a firewall rule named "OpenSSH-Server-In-TCP", which should be enabled 
```

## <a name="initial-use-of-ssh"></a>SSH의 초기 사용

Windows에 OpenSSH 서버를 설치 하면 SSH 클라이언트가 설치 된 Windows 장치에서 PowerShell을 사용 하 여 신속 하 게 테스트할 수 있습니다. PowerShell에서 다음 명령을 입력 합니다. 

```powershell
Ssh username@servername
```

서버에 대 한 첫 번째 연결로 인해 다음과 유사한 메시지가 나타납니다.

```
The authenticity of host 'servername (10.00.00.001)' can't be established.
ECDSA key fingerprint is SHA256:(<a large string>).
Are you sure you want to continue connecting (yes/no)?
```

대답은 "yes" 또는 "no" 여야 합니다. 예를 누르면 해당 서버가 알려진 ssh 호스트의 로컬 시스템 목록에 추가 됩니다.

이때 암호를 입력 하 라는 메시지가 표시 됩니다. 보안 예방 조치로 사용자가 입력 하면 암호가 표시 되지 않습니다. 

연결 되 면 다음과 유사한 명령 셸 프롬프트가 표시 됩니다.

```
domain\username@SERVERNAME C:\Users\username>
```

Windows OpenSSH server에서 사용 하는 기본 셸은 Windows 명령 셸입니다. 

