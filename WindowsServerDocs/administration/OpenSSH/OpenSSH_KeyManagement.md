---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH, SSH, SSHD, 설치, 설정
contributor: maertendMSFT
author: maertendMSFT
title: Windows용 OpenSSH 서버 구성
ms.product: w10
ms.openlocfilehash: fa3d40617a04c092403d9d2e018bd2eb82d20cd9
ms.sourcegitcommit: effbc183bf4b370905d95c975626c1ccde057401
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2019
ms.locfileid: "74781320"
---
# <a name="openssh-key-management"></a>OpenSSH 키 관리

Windows 환경에서 대부분의 인증은 사용자 이름-암호 쌍으로 수행됩니다.
이 방식은 공통 도메인을 공유하는 시스템에서 효과적입니다. 온프레미스와 클라우드에서 호스팅되는 시스템 사이와 같이 도메인 간 작업을 수행할 때는 더 어려워집니다.

이와 달리 Linux 환경은 일반적으로 공개 키/프라이빗 키 쌍을 사용하여 인증을 구동합니다.
OpenSSH에는 이를 돕기 위한 다음과 같은 도구가 포함되어 있습니다.

* 보안 키 생성을 위한 __ssh-keygen__
* 프라이빗 키를 안전하게 저장하기 위한 __ssh-agent__ 및 __ssh-add__
* 서버 초기 사용 중 공개 키 파일을 안전하게 복사하기 위한 __scp__ 및 __sftp__

이 문서에서는 Windows에서 이러한 도구들로 SSH 키 인증 사용을 시작하는 방법에 대한 개요를 제공합니다. SSH 키 관리에 익숙하지 않으면 "SSH(Secure Shell)를 사용한 대화형 및 자동화된 액세스 관리 보안"이라는 제목의 [NIST document IR 7966](http://nvlpubs.nist.gov/nistpubs/ir/2015/NIST.IR.7966.pdf)을 검토하는 것이 좋습니다.

## <a name="about-key-pairs"></a>키 쌍 정보

키 쌍은 특정 인증 프로토콜에 사용되는 공개 키 및 프라이빗 키 파일을 나타냅니다. 

SSH 공개 키 인증은 비동기 암호화 알고리즘을 사용하여 "프라이빗" 키와 "공개" 키라는 두 가지 키 파일을 생성합니다. 프라이빗 키 파일은 암호와 동일하며, 모든 상황에서 보호되어야 합니다. 다른 사람이 사용자의 프라이빗 키를 획득하면 사용자가 액세스할 수 있는 모든 SSH 서버에 사용자의 이름으로 로그인할 수 있습니다. 공개 키는 SSH 서버에 배치되며, 공유되더라도 프라이빗 키를 훼손하지 않습니다.

SSH 서버에서 키 인증을 사용할 때 SSH 서버와 클라이언트는 제공된 사용자 이름의 공개 키를 프라이빗 키와 비교합니다. 클라이언트 쪽 프라이빗 키로 공개 키의 유효성 검사를 수행할 수 없으면 인증이 실패합니다. 

키 쌍이 생성될 때 암호를 제공하도록 요구함으로써 키 쌍으로 다단계 인증을 구현할 수 있습니다(아래의 키 생성 참조). 인증 시 사용자는 사용자 인증을 위해 SSH 클라이언트에서 프라이빗 키와 함께 사용되는 암호를 입력해야 합니다. 

## <a name="host-key-generation"></a>호스트 키 생성

공개 키에는 Windows에서 관리자 및 시스템에 대해서만 액세스를 허용하는 것과 동일한 특별한 ACL 요구 사항이 있습니다. 이를 더 쉽게 수행하기 위해, 

* 키 ACL을 올바르게 설정하도록 OpenSSHUtils PowerShell 모듈이 생성되었으며, 이를 서버에 설치해야 합니다.
* sshd를 처음 사용할 때 호스트에 대한 키 쌍이 자동으로 생성됩니다. ssh-agent가 실행되면 키가 로컬 저장소에 자동으로 추가됩니다. 

SSH 서버에서 키 인증을 쉽게 수행하려면 권한을 높인 PowerShell 프롬프트에서 다음 명령을 수행합니다.

```powershell

# Install the OpenSSHUtils module to the server. This will be valuable when deploying user keys.
Install-Module -Force OpenSSHUtils -Scope AllUsers

# Start the ssh-agent service to preserve the server keys
Start-Service ssh-agent

# Now start the sshd service
Start-Service sshd
```

sshd 서비스와 연결된 사용자가 없기 때문에 호스트 키가 \ProgramData\ssh 아래에 저장됩니다.


## <a name="user-key-generation"></a>사용자 키 생성

키 기반 인증을 사용하려면 먼저 클라이언트에 대해 공개/프라이빗 키 쌍을 생성해야 합니다. PowerShell 또는 cmd에서 ssh-keygen을 사용하여 키 파일을 생성합니다.

```powershell
cd ~\.ssh\
ssh-keygen
```

결과는 다음과 같이 표시됩니다(여기서 "username"은 사용자 이름으로 대체됨).

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (C:\Users\username\.ssh\id_ed25519):
```

Enter 키를 눌러 기본값을 적용하거나 키를 생성할 경로를 지정할 수 있습니다. 그러면 프라이빗 키 파일 암호화를 위해 암호를 사용하라는 메시지가 표시됩니다.
암호는 키 파일과 함께 사용되어 2단계 인증을 제공합니다. 이 예제에서는 암호를 비워 둡니다. 

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

이제 공개/프라이빗 ED25519 키 쌍이 준비되었습니다. .pub 파일은 공개 키이고 나머지는 프라이빗 키입니다.

```
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/28/2018  11:09 AM           1679 id_ed25519
-a----        9/28/2018  11:09 AM            414 id_ed25519.pub
```

프라이빗 키 파일은 암호화 동일하며, 암호와 동일한 방법으로 보호되어야 합니다.
이를 돕기 위해서는 ssh-agent를 사용하여 Windows 로그인과 연결된 Windows 보안 컨텍스트 내에서 프라이빗 키를 안전하게 저장합니다. 이렇게 하려면 관리자 권한으로 ssh-agent 서비스를 시작하고 ssh-add를 사용하여 프라이빗 키를 저장합니다. 

```powershell
# Make sure you're running as an Administrator
Start-Service ssh-agent

# This should return a status of Running
Get-Service ssh-agent

# Now load your key files into ssh-agent
ssh-add ~\.ssh\id_ed25519

```

이러한 단계를 완료한 후에는 이 클라이언트에서 인증을 수행하기 위해 프라이빗 키가 필요할 때마다 ssh-agent가 자동으로 로컬 프라이빗 키를 검색하고 이를 SSH 클라이언트로 전달합니다.

> [!NOTE]
> 프라이빗 키를 안전한 위치에 백업한 다음에는 이를 ssh-agent에 추가한 *후*, 로컬 시스템에서 삭제하는 것이 좋습니다.
> 프라이빗 키는 에이전트에서 검색될 수 없습니다.
> 프라이빗 키에 대한 액세스 권한이 손실되면, 새 키 쌍을 만들고 사용하는 모든 시스템에서 공개 키를 업데이트해야 합니다.

## <a name="deploying-the-public-key"></a>공개 키 배포

위에서 만든 사용자 키를 사용하려면 공개 키를 서버의 users\username\.ssh\.에 있는 *authorized_keys*라는 텍스트 파일에 배치해야 합니다. OpenSSH 도구에는 이를 돕기 위한 보안 파일 전송 유틸리티인 scp가 포함되어 있습니다.

공개 키 콘텐츠(~\.ssh\id_ed25519.pub)를 ~\.ssh\ on your server/host의 authorized_keys라는 텍스트 파일로 이동합니다.

이 예제에서는 OpenSSHUtils 모듈에서 위 지침에 따라 호스트에 이전에 설치된 Repair-AuthorizedKeyPermissions 함수가 사용됩니다.

```powershell
# Make sure that the .ssh directory exists in your server's home folder
ssh user1@domain1@contoso.com mkdir C:\users\user1\.ssh\

# Use scp to opy the public key file generated previously to authorized_keys on your server
scp C:\Users\user1\.ssh\id_ed25519.pub user1@domain1@contoso.com:C:\Users\user1\.ssh\authorized_keys

# Appropriately ACL the authorized_keys file on your server  
ssh --% user1@domain1@contoso.com powershell -c $ConfirmPreference = 'None'; Repair-AuthorizedKeyPermission C:\Users\user1\.ssh\authorized_keys
```

이러한 단계에서는 Windows에서 키 기반 SSH 인증을 사용하기 위해 필요한 구성을 완료합니다.
그런 후에는 사용자가 프라이빗 키가 있는 어떤 클라이언트에서도 sshd 호스트에 연결할 수 있습니다.

