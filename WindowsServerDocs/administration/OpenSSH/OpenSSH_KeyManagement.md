---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH SSH, SSHD, 설치, 설정
contributor: maertendMSFT
author: maertendMSFT
title: Windows 용 OpenSSH 서버 구성
ms.product: w10
ms.openlocfilehash: 3e2981cbbdfe34bf28a77d5121bff0b663e0d3bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837154"
---
# <a name="openssh-key-management"></a>OpenSSH 키 관리

Windows 환경에서 대부분의 인증은 사용자 이름 / 암호 쌍을 사용 하 여 수행 됩니다.
이 공용 도메인을 공유 하는 시스템에 적합 합니다. 도메인에 걸쳐 작동 하는 경우와 같은 온-프레미스와 클라우드에 호스트 된 시스템 간에 더 어려워집니다.

비교를 Linux 환경을 일반적으로 드라이브 인증으로 공개 키/개인 키 쌍을 사용 합니다.
OpenSSH는 구체적으로이 지원할 수 있도록 도구가 포함 되어 있습니다.

* __ssh-keygen__ 보안 키를 생성 합니다.
* __ssh 에이전트__ 하 고 __ssh 추가__ 개인 키를 안전 하 게 저장
* __scp__ 하 고 __sftp__ 안전 하 게 서버를 처음 사용 하는 동안 공용 키 파일을 복사 하려면

이 문서에서는 Windows에서 이러한 도구를 사용 하 여 SSH 키 인증 사용을 시작 하는 방법의 개요를 제공 합니다. SSH 키 관리를 사용 하 여 잘 모르는 경우 강력한 검토 좋습니다 [NIST 문서 IR 7966](http://nvlpubs.nist.gov/nistpubs/ir/2015/NIST.IR.7966.pdf) "대화형 및 자동화 된 액세스 관리를 사용 하 여 SSH (보안 셸)의 보안입니다." 라는

## <a name="about-key-pairs"></a>키 쌍에 대 한

키 쌍은 특정 인증 프로토콜에서 사용 하는 공용 및 개인 키 파일을 가리킵니다. 

SSH 공개 키 인증 비대칭 암호화 알고리즘 사용 하 여 두 개의 키 파일이 – "개인" 및 "공개"를 생성 합니다. 개인 키 파일을 암호를 동일 하 고 모든 상황에서 보호 해야 합니다. 누군가가 사용자의 개인 키를 획득 하 고 하는 경우 수 로그인 할 때 모든 SSH 서버에 액세스할 수 있습니다. 공개 키에는 SSH 서버에 위치한를 만들고 개인 키를 손상 시 키 지 않고 공유 될 수 있습니다.

키 인증을 사용 하 여 SSH 서버를 사용 하 여, SSH 서버와 클라이언트는 개인 키에 대해 제공 하는 사용자 이름에 대 한 공개 키를 비교 합니다. 클라이언트 쪽 개인 키에 대 한 공개 키를 확인할 수 없으면 인증이 실패 합니다. 

Multi-factor authentication 인증 키 쌍 생성 되 면 암호를 제공 하도록 요구 하 여 키 쌍을 사용 하 여 구현 될 수 있습니다 (키 생성 아래 참조). 암호에 대 한 메시지가 표시 됩니다 인증 하는 동안 사용자를 인증 하는 SSH 클라이언트에서 개인 키의 존재와 함께 사용 됩니다. 

## <a name="host-key-generation"></a>호스트 키 생성

공개 키 ACL는 특정 요구 사항이, Windows에서 결과가 관리자와 시스템에 대 한 액세스를 허용 하 합니다. 이 쉽게 

* OpenSSHUtils PowerShell 모듈을 제대로 키 Acl을 설정 하려면 만든 및 서버에 설치 해야
* Sshd의 처음 사용할 때 호스트에 대 한 키 쌍 자동으로 생성 됩니다. Ssh 에이전트를 실행 하는 경우 로컬 저장소에 키를 자동으로 추가 됩니다. 

키 인증을 더 쉽게 SSH 서버를 사용 하 여 관리자 권한 PowerShell 프롬프트에서 다음 명령을 실행 합니다.

```powershell

# Install the OpenSSHUtils module to the server. This will be valuable when deploying user keys.
Install-Module -Force OpenSSHUtils -Scope AllUsers

# Start the ssh-agent service to preserve the server keys
Start-Service ssh-agent

# Now start the sshd service
Start-Service sshd
```

Sshd 서비스를 사용 하 여 연결 된 사용자 이므로 \ProgramData\ssh 아래 호스트 키에 저장 됩니다.


## <a name="user-key-generation"></a>사용자 키 생성

키 기반 인증을 사용 하려면 먼저 클라이언트에 대 한 일부 공개/개인 키 쌍을 생성 해야 합니다. PowerShell 또는 cmd에서 ssh-keygen 사용 하 여 일부 키 파일을 생성 합니다.

```powershell
cd ~\.ssh\
ssh-keygen
```

그러면 (여기서 "username"으로 바뀝니다 사용자 이름) 다음과 같이 표시 됩니다

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (C:\Users\username\.ssh\id_ed25519):
```

기본값을 적용 하려면 Enter 키를 눌러 하거나 키를 생성 하려는 경로 지정할 수 있습니다. 이 시점에서 암호를 사용 하 여 개인 키 파일을 암호화 하 라는 메시지가 됩니다.
암호는 2 단계 인증을 제공 하는 키 파일을 사용 하 여 작동 합니다. 예를 들어 것은 암호를 비워 두면 됩니다. 

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

이제 공개/개인 ED25519 키 쌍 (.pub 파일은 공개 키 및 나머지는 개인 키):

```
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/28/2018  11:09 AM           1679 id_ed25519
-a----        9/28/2018  11:09 AM            414 id_ed25519.pub
```

개인 키 파일을 암호에 해당 하는 동일한 방식으로 암호를 보호 하는 보호 해야 합니다.
돕기 위해 ssh 에이전트를 사용 하 여 Windows 로그인과 연결 된 Windows 보안 컨텍스트 내에서 개인 키를 안전 하 게 저장 합니다. 이렇게 하려면 관리자 권한으로 ssh 에이전트 서비스를 시작 및 사용 하 여 ssh 부가 개인 키를 저장 합니다. 

```powershell
# Make sure you're running as an Administrator
Start-Service ssh-agent

# This should return a status of Running
Get-Service ssh-agent

# Now load your key files into ssh-agent
ssh-add ~\.ssh\id_ed25519

```

다음이 단계를 완료 한 후이 클라이언트에서 인증에 대 한 개인 키가 필요할 때마다 ssh 에이전트 자동으로 로컬 개인 키를 검색할를 SSH 클라이언트에 전달 합니다.

> [!NOTE]
> 개인 키를 안전한 위치에 다음 로컬 시스템에서 삭제 하는 것이 좋습니다 *후* ssh 에이전트에 추가 합니다.
> 에이전트에서 개인 키를 검색할 수 없습니다.
> 개인 키에 액세스할 수 없는 경우 새 키 쌍을 작성 하 고 상호 작용할 모든 시스템에 있는 공개 키를 업데이트 해야 합니다.

## <a name="deploying-the-public-key"></a>공개 키를 배포합니다.

위에서 만든 사용자 키를 사용 하려면 공개 키 라는 텍스트 파일에 서버에 배치 해야 *authorized_keys* users\username\ssh 아래. OpenSSH 도구에는 scp를 보안 파일 전송 유틸리티를 위해이 포함 됩니다.

공개 키의 내용을 이동 (~\.ssh\id_ed25519.pub)에서 파일 이라는 authorized_keys 텍스트 ~\.ssh\ 서버/호스트에서.

이 예제에서는 위의 지침에 따라 호스트에 이전에 설치한 OpenSSHUtils 모듈에서 복구 AuthorizedKeyPermissions 함수를 사용 합니다.

```powershell
# Make sure that the .ssh directory exists in your server's home folder
ssh user1@domain1@contoso.com mkdir C:\users\user1\.ssh\

# Use scp to opy the public key file generated previously to authorized_keys on your server
scp C:\Users\user1\.ssh\id_ed25519.pub user1@domain1@contoso.com:C:\Users\user1\.ssh\authorized_keys

# Appropriately ACL the authorized_keys file on your server  
ssh --% user1@domain1@contoso.com powershell -c $ConfirmPreference = 'None'; Repair-AuthorizedKeyPermission C:\Users\user1\.ssh\authorized_keys
```

Windows의 SSH 키 기반 인증을 사용 하는 데 필요한 구성을 완료 하는이 단계입니다.
그러면 사용자 개인 키가 있는 모든 클라이언트에서 sshd 호스트에 연결할 수 있습니다.

