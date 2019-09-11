---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH, SSH, SSHD, 설치, 설치
contributor: maertendMSFT
author: maertendMSFT
title: Windows 용 OpenSSH 서버 구성
ms.product: w10
ms.openlocfilehash: ed9f3653c79f1329b1334f52fe14c1184bc99539
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866873"
---
# <a name="openssh-key-management"></a>OpenSSH 키 관리

Windows 환경의 인증은 사용자 이름-암호 쌍을 사용 하 여 수행 됩니다.
이는 공통 도메인을 공유 하는 시스템에서 효과적으로 작동 합니다. 온-프레미스 및 클라우드 호스팅 시스템 간에 도메인 간에 작업할 경우 더 어려워집니다.

일반적으로 Linux 환경에서는 공개 키/개인 키 쌍을 사용 하 여 인증을 구동 합니다.
OpenSSH에는이를 지 원하는 데 도움이 되는 도구가 포함 되어 있습니다.

* 보안 키 생성에 대 한 __ssh ssh-keygen__
* __ssh-에이전트__ 및 __ssh-__ 개인 키를 안전 하 게 저장 하기 위한 추가
* 서버를 처음 사용 하는 동안 공개 키 파일을 안전 하 게 복사 하는 __scp__ 및 __sftp__

이 문서에서는 Windows에서 이러한 도구를 사용 하 여 SSH를 통한 키 인증 사용을 시작 하는 방법에 대 한 개요를 제공 합니다. SSH 키 관리에 익숙하지 않은 경우 "Secure Shell (SSH)를 사용 하 여 대화형 및 자동화 된 액세스 관리의 보안" 이라는 [NIST 문서 IR 7966](http://nvlpubs.nist.gov/nistpubs/ir/2015/NIST.IR.7966.pdf) 을 검토 하는 것이 좋습니다.

## <a name="about-key-pairs"></a>키 쌍 정보

키 쌍은 특정 인증 프로토콜에 사용 되는 공개 및 개인 키 파일을 참조 합니다. 

SSH 공개 키 인증은 비대칭 암호화 알고리즘을 사용 하 여 두 개의 키 파일을 생성 합니다. 하나는 "개인"과 다른 하나는 "공용"입니다. 개인 키 파일은 암호와 같으며 모든 상황에서 보호 되어야 합니다. 누군가가 개인 키를 획득 하는 경우 액세스 권한이 있는 모든 SSH 서버에 로그인 할 수 있습니다. 공개 키는 SSH 서버에 배치 되 고 개인 키를 손상 시 키 지 않고 공유 될 수 있습니다.

Ssh 서버에서 키 인증을 사용 하는 경우 SSH 서버와 클라이언트는 개인 키에 대해 제공 된 사용자 이름의 공개 키를 비교 합니다. 클라이언트 쪽 개인 키에 대해 공개 키의 유효성을 검사할 수 없는 경우 인증에 실패 합니다. 

키 쌍이 생성 될 때 암호를 제공 하도록 요구 하 여 키 쌍으로 multi-factor authentication을 구현할 수 있습니다 (아래 키 생성 참조). 인증 하는 동안 사용자를 인증 하기 위해 SSH 클라이언트에 개인 키가 있는 경우에 사용 되는 암호를 입력 하 라는 메시지가 표시 됩니다. 

## <a name="host-key-generation"></a>호스트 키 생성

공개 키에는 Windows에서 관리자와 시스템에만 액세스할 수 있도록 하는 특정 ACL 요구 사항이 있습니다. 이 작업을 더 쉽게 수행 하려면 

* 키 Acl을 올바르게 설정 하기 위해 OpenSSHUtils PowerShell 모듈을 만들었으며 서버에 설치 해야 합니다.
* Sshd를 처음 사용 하는 경우 호스트에 대 한 키 쌍이 자동으로 생성 됩니다. Ssh 에이전트를 실행 하는 경우 키가 로컬 저장소에 자동으로 추가 됩니다. 

SSH 서버에서 키 인증을 쉽게 수행 하려면 관리자 권한 PowerShell 프롬프트에서 다음 명령을 실행 합니다.

```powershell

# Install the OpenSSHUtils module to the server. This will be valuable when deploying user keys.
Install-Module -Force OpenSSHUtils -Scope AllUsers

# Start the ssh-agent service to preserve the server keys
Start-Service ssh-agent

# Now start the sshd service
Start-Service sshd
```

Sshd 서비스와 연결 된 사용자가 없기 때문에 호스트 키는 \ProgramData\ssh. 아래에 저장 됩니다.


## <a name="user-key-generation"></a>사용자 키 생성

키 기반 인증을 사용 하려면 먼저 클라이언트에 대 한 몇 가지 공개/개인 키 쌍을 생성 해야 합니다. PowerShell 또는 cmd에서 ssh-ssh-keygen를 사용 하 여 일부 키 파일을 생성 합니다.

```powershell
cd ~\.ssh\
ssh-keygen
```

다음과 같은 내용이 표시 됩니다 ("username"이 사용자 이름으로 대체 됨).

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (C:\Users\username\.ssh\id_ed25519):
```

Enter 키를 눌러 기본값을 적용 하거나 키를 생성 하려는 경로를 지정할 수 있습니다. 이때 암호를 사용 하 여 개인 키 파일을 암호화 하 라는 메시지가 표시 됩니다.
암호는 키 파일과 함께 작동 하 여 2 단계 인증을 제공 합니다. 이 예제에서는 암호를 비워 둡니다. 

```
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in C:\Users\username\.ssh\id_ed25519.
Your public key has been saved in C:\Users\username\.ssh\id_ed25519.pub.
The key fingerprint is: 
SHA256:OIzc1yE7joL2Bzy8!gS0j8eGK7bYaH1FmF3sDuMeSj8 username@server@LOCAL-HOSTNAME

The key's randomart image is:
+--[ED25519 256]--+
|        .        |
|         o       |
|    . + + .      |
|   o B * = .     |
|   o= B S .      |
|   .=B O o       |
|  + =+% o        |
| *oo.O.E         |
|+.o+=o. .        |
+----[SHA256]-----+
```

이제 public/private ED25519 키 쌍이 있습니다. .pub 파일은 공개 키 이며 나머지는 개인 키입니다.

```
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/28/2018  11:09 AM           1679 id_ed25519
-a----        9/28/2018  11:09 AM            414 id_ed25519.pub
```

암호에 해당 하는 개인 키 파일은 암호를 보호 하는 것과 동일한 방식으로 보호 해야 합니다.
이를 위해 ssh 에이전트를 사용 하 여 windows 로그인과 관련 된 Windows 보안 컨텍스트 내에서 개인 키를 안전 하 게 저장 합니다. 이렇게 하려면 관리자 권한으로 ssh 에이전트 서비스를 시작 하 고 ssh-추가를 사용 하 여 개인 키를 저장 합니다. 

```powershell
# Make sure you're running as an Administrator
Start-Service ssh-agent

# This should return a status of Running
Get-Service ssh-agent

# Now load your key files into ssh-agent
ssh-add ~\.ssh\id_ed25519

```

이러한 단계를 완료 한 후에는이 클라이언트에서 인증을 위해 개인 키가 필요할 때마다 ssh 에이전트는 자동으로 로컬 개인 키를 검색 하 고 SSH 클라이언트에 전달 합니다.

> [!NOTE]
> 개인 키를 보안 위치에 백업한 다음 로컬 시스템에서 삭제 한 *후* ssh-에이전트에 추가 하는 것이 좋습니다.
> 에이전트에서 개인 키를 검색할 수 없습니다.
> 개인 키에 대 한 액세스 권한을 상실 한 경우 새 키 쌍을 만들고 상호 작용 하는 모든 시스템에서 공개 키를 업데이트 해야 합니다.

## <a name="deploying-the-public-key"></a>공개 키 배포

위에서 만든 사용자 키를 사용 하려면 users\username\ssh. 아래에서 *authorized_keys* 라는 텍스트 파일에 공개 키를 서버에 배치 해야 합니다. OpenSSH 도구에는이를 도와 주는 안전한 파일 전송 유틸리티인 scp가 포함 되어 있습니다.

공개 키 (~\.ssh\id_ed25519.pub)의 콘텐츠를 서버/호스트의 authorized_keys\.라는 텍스트 파일로 이동 합니다.

이 예제에서는 위의 지침에서 호스트에 이전에 설치 된 OpenSSHUtils 모듈의 AuthorizedKeyPermissions 함수를 사용 합니다.

```powershell
# Make sure that the .ssh directory exists in your server's home folder
ssh user1@domain1@contoso.com mkdir C:\users\user1\.ssh\

# Use scp to opy the public key file generated previously to authorized_keys on your server
scp C:\Users\user1\.ssh\id_ed25519.pub user1@domain1@contoso.com:C:\Users\user1\.ssh\authorized_keys

# Appropriately ACL the authorized_keys file on your server  
ssh --% user1@domain1@contoso.com powershell -c $ConfirmPreference = 'None'; Repair-AuthorizedKeyPermission C:\Users\user1\.ssh\authorized_keys
```

이러한 단계는 Windows에서 SSH를 사용 하 여 키 기반 인증을 사용 하는 데 필요한 구성을 완료 합니다.
그러면 사용자가 개인 키가 있는 모든 클라이언트에서 sshd 호스트에 연결할 수 있습니다.

