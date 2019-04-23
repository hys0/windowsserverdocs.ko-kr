---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH SSH, SSHD, 설치, 설정
contributor: maertendMSFT
ms.product: w10
author: maertendMSFT
title: Windows 용 OpenSSH 서버 구성
ms.openlocfilehash: 8e6476e4005bd5bbc2d40c8a59d39510ca1beb70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827284"
---
# <a name="openssh-server-configuration-for-windows-10-1809-and-server-2019"></a>Windows 10 1809 및 Server 2019 # OpenSSH 서버 구성

이 항목에서는 OpenSSH 서버 (sshd)에 대 한 Windows 특정 구성을 설명 합니다. 

OpenSSH 구성 옵션 온라인에 대 한 자세한 설명서를 유지 관리 [OpenSSH.com](https://www.openssh.com/manual.html),이 설명서 집합에서 중복 될는 없습니다. 

## <a name="configuring-the-default-shell-for-openssh-in-windows"></a>Windows에서 OpenSSH에 대 한 기본 셸 구성

기본 명령 셸을 SSH를 사용 하 여 서버에 연결할 때 사용자에 게 표시 환경을 제공 합니다. 초기 기본 Windows는 Windows 명령 셸 (cmd.exe). Windows PowerShell 및 Bash를 포함 하 고 제 3 자 명령 셸의 Windows에 대 한 사용 가능 하며 서버에 대 한 기본 셸로 구성할 수 있습니다.

기본 명령 셸을 설정 하려면 먼저 시스템 경로에 OpenSSH 설치 폴더 인지 확인 합니다. Windows에 기본 설치 폴더는 SystemDrive:WindowsDirectory\System32\openssh 합니다. 다음 명령을 현재 경로 설정이 표시 및 기본 OpenSSH 설치 폴더를 추가 합니다. 

명령 셸 | 명령 사용
------------- | -------------- 
Command | path
PowerShell | $env:\path

기본 ssh shell은 구성할 Windows 레지스트리에서 셸에 문자열 값 DefaultShell Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH 실행 파일의 전체 경로 추가 하 여. 

예를 들어, 다음 Powershell 명령을 PowerShell.exe를 되도록 기본 셸이 설정 합니다.

```powershell
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
```

## <a name="windows-configurations-in-sshdconfig"></a>Sshd_config의 Windows 구성 

Windows에서 sshd %programdata%\ssh\sshd_config에서 기본적으로 구성 데이터를 읽고 또는 sshd.exe-f 매개 변수를 사용 하 여 시작 하 여 다른 구성 파일을 지정할 수 있습니다.
파일이 없으면 sshd 생성 기본 구성을 사용 하 여 서비스를 시작 하는 경우.

요소 아래에 나열 된 Windows 관련 구성 가능한 sshd_config의 항목을 제공 합니다. 온라인에서 자세히 설명 되어 해당 하는 대로 여기에 나열 되지 않은 기타 구성 설정의 가능한 가지 [Win32 OpenSSH 설명서](https://github.com/powershell/win32-openssh/wiki)합니다. 


### <a name="allowgroups-allowusers-denygroups-denyusers"></a>AllowGroups, AllowUsers, DenyGroups, DenyUsers 

완료 되는 서버에 연결할 수 있는 사용자 및 그룹 제어 AllowGroups, AllowUsers, DenyGroups 및 DenyUsers using 지시문을 사용 합니다. 허용/거부 지시문은 다음 순서 대로 처리 됩니다. DenyUsers AllowUsers, DenyGroups, 하며 마지막 AllowGroups 합니다. 모든 계정 이름은 소문자에서 여야 합니다. 와일드 카드 패턴에 대 한 자세한 내용은 ssh_config에서 패턴을 참조 하세요.

도메인 사용자 또는 그룹을 사용 하 여 규칙을 기반 사용자/그룹을 구성 하는 경우 다음 형식을 사용 합니다. ``` user?domain* ```합니다.
Windows 형식의 여러 도메인 보안 주체를 지정 허용 되지만 여러 표준 Linux 패턴을 사용 하 여 충돌 합니다. 이런 이유로 * Fqdn을 처리 하기 위해 추가 됩니다. 또한이 방법을 사용 하 여 "?", 대신 @를 사용 하 여 충돌을 방지 하는 username@host 형식입니다. 

작업 그룹 사용자/그룹 및 계정을 인터넷에 연결 된 해당 로컬 계정 이름 (없는 도메인 부분을 표준 Unix 이름을 비슷합니다)를 항상 확인 됩니다. 도메인 사용자 및 그룹은 엄격 하 게 확인 [NameSamCompatible](https://docs.microsoft.com/en-us/windows/desktop/api/secext/ne-secext-extended_name_format) domain_short_name\user_name 형식입니다. 모든 사용자/그룹 기준 구성 규칙에서이 형식을 준수 해야 합니다.

도메인 사용자 및 그룹에 대 한 예제 

```
DenyUsers contoso\admin@192.168.2.23 : blocks contoso\admin from 192.168.2.23
DenyUsers contoso\* : blocks all users from contoso domain
AllowGroups contoso\sshusers : only allow users from contoso\sshusers group
```

로컬 사용자 및 그룹에 대 한 예제 

```
AllowUsers localuser@192.168.2.23
AllowGroups sshusers
```

### <a name="authenticationmethods"></a>AuthenticationMethods 

Windows OpenSSH만 사용할 수 있는 인증 메서드는 "password" 및 "publickey"입니다.

### <a name="authorizedkeysfile"></a>AuthorizedKeysFile 

기본값은 "authorized_keys.ssh/.ssh/authorized_keys2". 경로 절대 없는 경우 사용자의 홈 디렉터리 (또는 프로필 이미지 경로)를 기준으로 수행 됩니다. 예: c:\users\user.

### <a name="chrootdirectory-support-added-in-v7700"></a>ChrootDirectory (v7.7.0.0의 추가 지원)

Sftp 세션을 사용 하 여이 지시문만 지원 됩니다. Cmd.exe에 원격 세션을이 인식 하지 않습니다. Sftp 전용 chroot 서버에 설정 하려면 ForceCommand 내부 sftp로 설정 합니다. 수 또한 설정한 scp chroot를 사용 하 여 scp 및 sftp만 허용 하는 사용자 지정 셸을 구현 하 여 합니다.

### <a name="hostkey"></a>HostKey

기본값은 %programdata%/ssh/ssh_host_ecdsa_key, %programdata%/ssh/ssh_host_ed25519_key 및 %programdata%/ssh/ssh_host_rsa_key. 기본값이 없으면 sshd 자동으로 생성 서비스 시작 시 이러한 합니다.

### <a name="match"></a>일치

이 섹션의 규칙 패턴을 참고 합니다. 사용자 및 그룹 이름은 소문자에서 이어야 합니다.

### <a name="permitrootlogin"></a>PermitRootLogin

Windows에는 적용 되지 않습니다. 관리자 로그인을 방지 하려면 DenyGroups 지시문을 사용 하 여 관리자를 사용 합니다.

### <a name="syslogfacility"></a>SyslogFacility

파일 기반 로깅에 필요한 경우 LOCAL0를 사용 합니다. 로그는 %programdata%\ssh\logs 생성 됩니다.
다른 값을 기본값 인증을 비롯 한 ETW 로깅이 전달 합니다. 자세한 내용은 Windows의 로깅 기능을 참조 하세요.

### <a name="not-supported"></a>지원되지 않음 

다음 구성 옵션은 Windows Server 2019 및 Windows 10 1809에서 제공 되는 OpenSSH 버전에서 사용할 수 있습니다.

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

