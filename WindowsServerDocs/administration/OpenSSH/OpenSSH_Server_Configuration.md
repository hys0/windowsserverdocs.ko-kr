---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH, SSH, SSHD, 설치, 설치
contributor: maertendMSFT
ms.product: w10
author: maertendMSFT
title: Windows 용 OpenSSH 서버 구성
ms.openlocfilehash: ed424c33c4cd2c19a9b5e985ab6083bcbcb9fbdc
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546266"
---
# <a name="openssh-server-configuration-for-windows-10-1809-and-server-2019"></a>Windows 10 1809 및 서버 2019 용 OpenSSH 서버 구성

이 항목에서는 OpenSSH Server (sshd)에 대 한 Windows 관련 구성에 대해 설명 합니다. 

OpenSSH는이 설명서 집합에서 중복 되지 않은 [OpenSSH.com](https://www.openssh.com/manual.html)에서 온라인 구성 옵션에 대 한 자세한 설명서를 유지 관리 합니다. 

## <a name="configuring-the-default-shell-for-openssh-in-windows"></a>Windows에서 OpenSSH에 대 한 기본 셸 구성

기본 명령 셸은 SSH를 사용 하 여 서버에 연결할 때 사용자에 게 표시 되는 환경을 제공 합니다. 초기 기본 창은 Windows 명령 셸 (cmd.exe)입니다. 또한 windows에는 PowerShell 및 Bash가 포함 되어 있으며, 타사 명령 셸도 Windows에서 사용할 수 있으며 서버에 대 한 기본 셸로 구성 될 수 있습니다.

기본 명령 셸을 설정 하려면 먼저 OpenSSH 설치 폴더가 시스템 경로에 있는지 확인 합니다. Windows의 기본 설치 폴더는 WindowsDirectory\System32\openssh.: 다음 명령은 현재 경로 설정을 보여주고 여기에 기본 OpenSSH 설치 폴더를 추가 합니다. 

명령 셸 | 사용할 명령
------------- | -------------- 
명령 | path
PowerShell | $env:p a

기본 ssh 셸을 구성 하려면 셸 실행 파일의 전체 경로를 문자열 값 DefaultShell의 Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH에 추가 하 여 Windows 레지스트리에서 수행 합니다. 

예를 들어 다음 Powershell 명령은 기본 셸을 PowerShell .exe로 설정 합니다.

```powershell
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
```

## <a name="windows-configurations-in-sshd_config"></a>Sshd_config의 Windows 구성 

Windows에서 sshd는 기본적으로%programdata%\ssh\sshd_config에서 구성 데이터를 읽거나-f 매개 변수를 사용 하 여 sshd를 실행 하 여 다른 구성 파일을 지정할 수 있습니다.
파일이 없는 경우 sshd는 서비스가 시작 될 때 기본 구성으로 하나를 생성 합니다.

아래에 나열 된 요소는 sshd_config의 항목을 통해 가능한 Windows 관련 구성을 제공 합니다. 에서 사용할 수 있는 다른 구성 설정은 온라인 [Win32 OpenSSH 설명서](https://github.com/powershell/win32-openssh/wiki)에 자세히 설명 되어 있으므로 여기에 나열 되지 않습니다. 


### <a name="allowgroups-allowusers-denygroups-denyusers"></a>AllowGroups, Allowgroups, DenyGroups, DenyUsers 

서버에 연결할 수 있는 사용자 및 그룹을 제어 하는 작업은 AllowGroups, Allowgroups, DenyGroups 및 DenyUsers 지시어를 사용 하 여 수행 됩니다. 허용/거부 지시문은 다음 순서로 처리 됩니다. DenyUsers, AllowUsers, DenyGroups 및 finally Allowusers. 모든 계정 이름은 소문자로 지정 해야 합니다. 와일드 카드 패턴에 대 한 자세한 내용은 ssh_config의 패턴을 참조 하세요.

도메인 사용자 또는 그룹을 사용 하 여 사용자/그룹 기반 규칙을 구성 하는 경우 다음 ``` user?domain* ```형식을 사용 합니다.
Windows에서는 도메인 보안 주체를 지정 하기 위해 여러 형식을 사용할 수 있지만 대부분 표준 Linux 패턴과 충돌 합니다. 이러한 이유로, Fqdn을 포함 하는 *가 추가 됩니다. 또한이 방법은 username@host 형식 충돌을 피하기 위해 @ 대신 "?"를 사용 합니다. 

작업 그룹 사용자/그룹 및 인터넷에 연결 된 계정은 항상 로컬 계정 이름 (도메인 부분은 표준 Unix 이름과 유사)으로 확인 됩니다. 도메인 사용자 및 그룹은 [NameSamCompatible](https://docs.microsoft.com/windows/desktop/api/secext/ne-secext-extended_name_format) 형식-domain_short_name\user_name.로 엄격 하 게 확인 됩니다. 모든 사용자/그룹 기반 구성 규칙은이 형식을 준수 해야 합니다.

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

Windows OpenSSH의 경우 유일 하 게 사용할 수 있는 인증 방법은 "password" 및 "publickey"입니다.

### <a name="authorizedkeysfile"></a>AuthorizedKeysFile 

기본값은 ". ssh/authorized_keys/authorized_keys2"입니다. 절대 경로가 아니면 사용자의 홈 디렉터리 (또는 프로필 이미지 경로)를 기준으로 수행 됩니다. 고급. c:\users\user.

### <a name="chrootdirectory-support-added-in-v7700"></a>ChrootDirectory (v 7.7.0.0에 추가 된 지원)

이 지시어는 sftp 세션 에서만 지원 됩니다. Cmd.exe로의 원격 세션은이를 인식 하지 못합니다. Sftp 전용 chroot 서버를 설정 하려면 ForceCommand를 내부 sftp로 설정 합니다. Scp 및 sftp만 허용 하는 사용자 지정 셸을 구현 하 여 chroot를 사용 하 여 scp를 설정할 수도 있습니다.

### <a name="hostkey"></a>HostKey

기본값은% programdata%/ssh/ssh_host_ecdsa_key,% programdata%/ssh/ssh_host_ed25519_key 및% programdata%/ssh/ssh_host_rsa_key.입니다. 기본값이 없으면 sshd가 서비스 시작 시 자동으로이를 생성 합니다.

### <a name="match"></a>일치

이 섹션의 패턴 규칙에 유의 하십시오. 사용자 및 그룹 이름은 소문자 여야 합니다.

### <a name="permitrootlogin"></a>PermitRootLogin

Windows에는 적용 되지 않습니다. 관리자 로그인을 방지 하려면 DenyGroups 지시어를 사용 하 여 관리자를 사용 합니다.

### <a name="syslogfacility"></a>SyslogFacility

파일 기반 로깅이 필요한 경우 LOCAL0를 사용 합니다. %Programdata%\ssh\logs. 아래에 로그가 생성 됩니다.
기본값 인증을 포함 하 여 다른 모든 값은 로깅을 ETW로 보냅니다. 자세한 내용은 Windows의 로깅 기능을 참조 하세요.

### <a name="not-supported"></a>지원되지 않음 

다음 구성 옵션은 Windows Server 2019 및 Windows 10 1809에서 제공 되는 OpenSSH 버전에서 사용할 수 없습니다.

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
* StreamLocalBindUnlink 해제
* StrictModes
* X11DisplayOffset
* X11Forwarding
* X11UseLocalhost
* XAuthLocation

