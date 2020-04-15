---
ms.date: 09/27/2018
ms.topic: conceptual
contributor: maertendMSFT
ms.product: windows-server
author: maertendmsft
title: Windows용 OpenSSH 서버 구성
ms.openlocfilehash: 61f176f7f73495a6b9dbbcb1a25f2337a44ab99b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852026"
---
# <a name="openssh-server-configuration-for-windows-10-1809-and-server-2019"></a>Windows 10 1809 및 Server 2019용 OpenSSH 서버 구성

이 항목에서는 OpenSSH 서버(sshd)에 대한 Windows 특정 구성에 대해 설명합니다. 

OpenSSH는 이 설명서 집합에 중복되지 않은 [OpenSSH.com](https://www.openssh.com/manual.html)에서 구성 옵션에 대한 자세한 설명서를 온라인으로 유지 관리합니다. 

## <a name="configuring-the-default-shell-for-openssh-in-windows"></a>Windows에서 OpenSSH에 대한 기본 셸 구성

기본 명령 셸은 SSH를 사용하여 서버에 연결할 때 사용자에게 표시되는 환경을 제공합니다. 초기 기본 창은 Windows 명령 셸(cmd.exe)입니다. 창에는 또한 PowerShell 및 Bash가 포함되며, 타사 명령 셸도 창으로 이용할 수 있으며, 서버의 기본 셸로 구성될 수 있습니다.

기본 명령 셸을 설정하려면 먼저 OpenSSH 설치 폴더가 시스템 경로에 있는지 확인합니다. Windows에서 기본 설치 폴더는 SystemDrive:WindowsDirectory\System32\openssh입니다. 다음 명령은 현재 경로 설정을 보여주고 여기에 기본 OpenSSH 설치 폴더를 추가합니다. 

명령 셸 | 사용할 명령
------------- | -------------- 
명령 | 경로
PowerShell | $env:path

기본 ssh 셸 구성은 Windows 레지스트리에서 문자열 값 DefaultShell의 Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH에 셸 실행 파일의 전체 경로를 추가하여 수행됩니다. 

예를 들어 다음 Powershell 명령은 기본 셸을 PowerShell.exe로 설정합니다.

```powershell
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
```

## <a name="windows-configurations-in-sshd_config"></a>sshd_config의 Windows 구성 

Windows에서 sshd는 기본적으로 %programdata%\ssh\sshd_config에서 구성 데이터를 읽습니다. 또는 -f 매개 변수와 함께 sshd.exe를 실행하여 다른 구성 파일을 지정할 수 있습니다.
파일이 없으면 서비스가 시작될 때 sshd가 기본 구성을 사용해서 파일을 생성합니다.

아래 나열된 요소는 sshd_config의 항목을 통해 사용 가능한 Windows 특정 구성을 제공합니다. 온라인 [Win32 OpenSSH 문서](https://github.com/powershell/win32-openssh/wiki)에 자세히 설명된 것처럼 여기에 나열되지 않은 다른 구성 설정도 사용될 수 있습니다. 


### <a name="allowgroups-allowusers-denygroups-denyusers"></a>AllowGroups, AllowUsers, DenyGroups, DenyUsers 

서버에 연결할 수 있는 사용자 및 그룹 제어는 AllowGroups, AllowUsers, DenyGroups 및 DenyUsers 지시문을 사용하여 수행됩니다. 허용/거부 지시문은 DenyUsers, AllowUsers, DenyGroups 및 AllowGroups의 순서로 처리됩니다. 모든 계정 이름은 소문자로 지정해야 합니다. 와일드카드 패턴에 대한 자세한 내용은 ssh_config의 PATTERNS를 참조하세요.

도메인 사용자 또는 그룹으로 사용자/그룹 기반 규칙을 구성할 때는 ``` user?domain* ``` 형식을 사용합니다.
Windows는 도메인 보안 주체 지정을 위해 여러 형식을 허용하지만, 많은 형식들이 표준 Linux 패턴과 충돌합니다. 따라서 FQDN 지원을 위해 *가 추가되었습니다. 또한 이 접근 방식에서는 username@host 형식과의 충돌을 방지하기 위해 @ 대신 "?"가 사용됩니다. 

작업 그룹 사용자/그룹 및 인터넷 연결 계정은 항상 해당 로컬 계정 이름으로 확인됩니다(표준 Unix 이름과 비슷하게 도메인 부분을 포함하지 않음). 도메인 사용자 및 그룹은 엄격하게 [NameSamCompatible](https://docs.microsoft.com/windows/desktop/api/secext/ne-secext-extended_name_format) 형식(domain_short_name\user_name)으로 확인됩니다. 모든 사용자/그룹 기반 구성 규칙은 이 형식을 따라야 합니다.

도메인 사용자 및 그룹 예 

```
DenyUsers contoso\admin@192.168.2.23 : blocks contoso\admin from 192.168.2.23
DenyUsers contoso\* : blocks all users from contoso domain
AllowGroups contoso\sshusers : only allow users from contoso\sshusers group
```

로컬 사용자 및 그룹 예 

```
AllowUsers localuser@192.168.2.23
AllowGroups sshusers
```

### <a name="authenticationmethods"></a>AuthenticationMethods 

Windows OpenSSH의 경우 사용 가능한 유일한 인증 방법은 "password"와 "publickey"입니다.

### <a name="authorizedkeysfile"></a>AuthorizedKeysFile 

기본값은 ".ssh/authorized_keys .ssh/authorized_keys2"입니다. 경로가 절대 경로가 아니면 사용자의 홈 디렉터리(또는 프로필 이미지 경로)를 기준으로 합니다. 예: c:\users\user. 사용자가 관리자 그룹에 속한 경우 %programdata%/ssh/administrators_authorized_keys가 대신 사용됩니다.

### <a name="chrootdirectory-support-added-in-v7700"></a>ChrootDirectory(v7.7.0.0에 지원 추가됨)

이 지시문은 sftp 세션에서만 지원됩니다. cmd.exe로의 원격 세션에서는 이 규칙을 따르지 않습니다. sftp 전용 chroot 서버를 설정하려면 ForceCommand를 internal-sftp로 설정합니다. scp 및 sftp만 허용하는 사용자 지정 셸을 구현하여 chroot로 scp를 설정할 수도 있습니다.

### <a name="hostkey"></a>HostKey

기본값은 %programdata%/ssh/ssh_host_ecdsa_key, %programdata%/ssh/ssh_host_ed25519_key, %programdata%/ssh/ssh_host_dsa_key 및 %programdata%/ssh/ssh_host_rsa_key입니다. 기본값이 제공되지 않았으면 sshd가 서비스 시작 시에 값을 자동으로 생성합니다.

### <a name="match"></a>일치

이 섹션의 패턴 규칙을 참조하세요. 사용자 및 그룹 이름은 소문자여야 합니다.

### <a name="permitrootlogin"></a>PermitRootLogin

Windows에 적용되지 않습니다. 관리자 로그인을 방지하려면 DenyGroups 지시문이 포함된 관리자를 사용합니다.

### <a name="syslogfacility"></a>SyslogFacility

파일 기반 로깅이 필요하면 LOCAL0을 사용합니다. 로그는 %programdata%\ssh\logs 아래에 생성됩니다.
기본값 AUTH를 포함하여 다른 모든 값은 로깅을 ETW로 지정합니다. 자세한 내용은 Windows의 로깅 기능을 참조하세요.

### <a name="not-supported"></a>지원되지 않음 

다음 구성 옵션은 Windows Server 2019 및 Windows 10 1809로 제공되는 OpenSSH 버전에서 사용할 수 없습니다.

* AcceptEnv
* AllowStreamLocalForwarding
* AuthorizedKeysCommand
* AuthorizedKeysCommandUser
* AuthorizedPrincipalsCommand
* AuthorizedPrincipalsCommandUser
* 압축
* ExposeAuthInfo
* GSSAPIAuthentication
* GSSAPICleanupCredentials
* GSSAPIStrictAcceptorCheck
* HostbasedAcceptedKeyTypes
* HostbasedAuthentication
* HostbasedUsesNameFromPacketOnly
* IgnoreRhosts
* IgnoreUserKnownHosts
* KbdInteractiveAuthentication
* KerberosAuthentication
* KerberosGetAFSToken
* KerberosOrLocalPasswd
* KerberosTicketCleanup
* PermitTunnel
* PermitUserEnvironment
* PermitUserRC
* PidFile
* PrintLastLog
* RDomain
* StreamLocalBindMask
* StreamLocalBindUnlink
* StrictModes
* X11DisplayOffset
* X11Forwarding
* X11UseLocalhost
* XAuthLocation

