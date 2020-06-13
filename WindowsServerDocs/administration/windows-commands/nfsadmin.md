---
title: nfsadmin
description: NFS 용 서버와 NFS 용 클라이언트를 모두 관리 하는 nfsadmin 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7375b2cf-c6b8-45b5-abf6-6c10e462defd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c122577758dd28d11d25445ca9dc98ed03024c77
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721536"
---
# <a name="nfsadmin"></a>nfsadmin

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nfs (네트워크 파일 시스템) 용 Microsoft 서비스를 실행 하는 로컬 또는 원격 컴퓨터에서 nfs 용 서버 또는 nfs 용 클라이언트를 관리 하는 명령줄 유틸리티입니다. 매개 변수 없이 사용 하는 경우 nfsadmin server NFS 구성 설정에 대 한 현재 서버를 표시 하 고, nfsadmin client NFS 용 현재 클라이언트 구성 설정을 표시 합니다.

## <a name="syntax"></a>구문

```
nfsadmin server [computername] [-u Username [-p Password]] -l
nfsadmin server [computername] [-u Username [-p Password]] -r {client | all}
nfsadmin server [computername] [-u Username [-p Password]] {start | stop}
nfsadmin server [computername] [-u Username [-p Password]] config option[...]
nfsadmin server [computername] [-u Username [-p Password]] creategroup <name>
nfsadmin server [computername] [-u Username [-p Password]] listgroups
nfsadmin server [computername] [-u Username [-p Password]] deletegroup <name>
nfsadmin server [computername] [-u Username [-p Password]] renamegroup <oldname> <newname>
nfsadmin server [computername] [-u Username [-p Password]] addmembers <hostname>[...]
nfsadmin server [computername] [-u Username [-p Password]] listmembers
nfsadmin server [computername] [-u Username [-p Password]] deletemembers <hostname><groupname>[...]
nfsadmin client [computername] [-u Username [-p Password]] {start | stop}
nfsadmin client [computername] [-u Username [-p Password]] config option[...]
```

### <a name="general-parameters"></a>일반 매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| 컴퓨터 이름 | 관리 하려는 원격 컴퓨터를 지정 합니다. 인터넷 이름 서비스 WINS (Windows) 이름 또는 도메인 이름 시스템 (DNS) 이름을 사용 하 여 컴퓨터를 지정 하거나 하 여 IP (인터넷 프로토콜) 주소 수 있습니다. |
| -u 사용자 이름 | 자격 증명에 사용 하려는 사용자의 사용자 이름을 지정 합니다. 사용자 이름에 도메인 이름을 *domain\username*형식으로 추가 해야 할 수도 있습니다. |
| -p 암호 | **-U** 옵션을 사용 하 여 지정 된 사용자의 암호를 지정 합니다. 지정 하는 경우는 **-u** 옵션은 있 생략 된 **-p** 옵션을 사용자의 암호를 묻는 메시지가 나타납니다. |

### <a name="server-for-nfs-related-parameters"></a>NFS 관련 매개 변수에 대 한 서버

| 매개 변수 | Description |
| --------- | ----------- |
| -l | 클라이언트에서 보유 한 모든 잠금을 나열 합니다. |
| -r`{client|all}` | 지정한 잠금을 해제 한 클라이언트 또는 모든 모든 클라이언트에 의해 지정 됩니다. |
| start | NFS 용 서버를 시작합니다. |
| stop(정지) | NFS 용 서버를 중지합니다. |
| config | NFS 용 서버에 대 한 일반 설정을 지정합니다. 하나 이상의 다음 옵션을 제공 해야는 **config** 인수:<ul><li>**mapsvr = `<server>` ** -서버를 NFS 용 서버에 대 한 사용자 이름 매핑 서버로 설정 합니다. 이 옵션을 이전 버전과 호환성에 대 한 지원 계속 있지만 사용 해야는 sfuadmin 유틸리티 대신 합니다.</li><li>**auditlocation = `{eventlog|file|both|none}` ** -이벤트를 감사할지 여부와 이벤트를 기록할지 여부를 지정 합니다. 다음 인수 중 하나가 필요 합니다.<ul><li>**eventlog** -감사 된 이벤트를 이벤트 뷰어 응용 프로그램 로그에만 기록 하도록 지정 합니다.</li><li>**file** -감사 된 이벤트를에 지정 된 파일에만 기록 하도록 지정 합니다 `config fname` .</li><li>**both** -감사 된 이벤트를 이벤트 뷰어 응용 프로그램 로그 및에 지정 된 파일에 기록 하도록 지정 합니다 `config fname` .</li><li>**none** -이벤트가 감사 되지 않도록 지정 합니다.</li></ul><li>**fname = `<file>` ** -파일에 지정 된 파일을 감사 파일로 설정 합니다. 기본값은 **%sfudir%\log \\ nfssvr**입니다.</li><li>**fsize = `<size>` ** -크기를 감사 파일의 최대 크기 (mb)로 설정 합니다. 기본 최대 크기는 **7MB**입니다.</li><li>**`audit=[+|-]mount [+|-]read [+|-]write [+|-]create [+|-]delete [+|-]locking [+|-]all`**-로깅할 이벤트를 지정 합니다. 이벤트 로깅을 시작 하려면 이벤트 이름 앞에 더하기 기호 ()를 입력 하 **+** 고 이벤트 로깅을 중지 하려면 이벤트 이름 앞에 빼기 기호 ()를 입력 **-** 합니다. 기호를 생략 하면 **+** 부호가 가정 됩니다. 다른 이벤트 이름과 함께 **all** 을 사용 하지 마세요.</li><li>**lockperiod = `<seconds>` ** -Nfs 용 서버에 대 한 연결이 끊어진 후 또는 nfs 용 서버 서비스를 다시 시작한 후 NFS 용 서버에서 잠금을 회수 하기 위해 대기 하는 시간 (초)을 지정 합니다.</li><li>**portmapprotocol = `{TCP|UDP|TCP+UDP}` ** -Portmap에서 지 원하는 전송 프로토콜을 지정 합니다. 기본 설정은 **TCP + UDP**입니다.</li><li>**mountprotocol = `{TCP|UDP|TCP+UDP}` ** -탑재에서 지 원하는 전송 프로토콜을 지정 합니다. 기본 설정은 **TCP + UDP**입니다.</li><li>**nfsprotocol = `{TCP|UDP|TCP+UDP}` ** -NFS (네트워크 파일 시스템)에서 지 원하는 전송 프로토콜을 지정 합니다. 기본 설정은 **TCP + UDP** 입니다.</li><li>**nlmprotocol = `{TCP|UDP|TCP+UDP}` ** -NLM (네트워크 잠금 관리자)에서 지 원하는 전송 프로토콜을 지정 합니다. 기본 설정은 **TCP + UDP**입니다.</li><li>**nsmprotocol = `{TCP|UDP|TCP+UDP}` ** -NSM (네트워크 상태 관리자)에서 지 원하는 전송 프로토콜을 지정 합니다. 기본 설정은 **TCP + UDP**입니다.</li><li>**enableV3 = `{yes|no}` ** -NFS 버전 3 프로토콜을 지원 하는지 여부를 지정 합니다. 기본 설정은 **예**입니다.</li><li>**renewauth = `{yes|no}` ** -구성 renewauthinterval에 지정 된 기간 후 클라이언트 연결을 다시 인증 해야 하는지 여부를 지정 합니다. 기본 설정은 **아니요**입니다.</li><li>**renewauthinterval = `<seconds>` ** - `config renewauth` 가 **예**로 설정 된 경우 클라이언트를 다시 인증 하는 데 걸리는 시간 (초)을 지정 합니다. 기본값은 **600 초**입니다.</li><li>**dicache = `<size>` ** -디렉터리 캐시의 크기 (kb)를 지정 합니다. 로 지정 된 숫자 크기 4와 128 사이의 4의 배수 여야 합니다. 기본 디렉터리 캐시 크기는 **128 KB**입니다.</li><li>**translationfile = `<file>` ** -Windows 기반 파일 시스템에서 UNIX 기반 파일 시스템으로 이동할 때 파일 이름에서 문자를 바꾸기 위한 매핑 정보를 포함 하는 파일을 지정 합니다. 경우 파일 를 지정 하지 않으면 파일 이름 문자 변환을 사용할 수 없습니다. 하는 경우의 값 **translationfile** 은 변경, 다시 시작 해야 변경 내용이 적용에 대 한 서버입니다.</li><li>**dotfileshidden = `{yes|no}` ** -이름이 마침표 (.)로 시작 하는 파일이 Windows 파일 시스템에서 숨김 상태로 표시 되 고 그에 따라 NFS 클라이언트에서 숨겨져 있는지 여부를 지정 합니다. 기본 설정은 **아니요**입니다.</li><li>**casesensitivelookups = `{yes|no}` ** -디렉터리 조회가 대/소문자를 구분 하는지 여부를 지정 합니다 (문자 대/소문자를 정확 하 게 일치 해야 함).<p>대/소문자를 구분 하는 파일 이름을 지원 하려면 Windows 커널 대/소문자 구분 안 함도 사용 하지 않도록 설정 해야 합니다. 대/소문자 구분을 지원 하려면 레지스트리 키의 **DWord** 값을 `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\kernel` **0**으로 변경 합니다.</li><li>**ntfscase = `{lower|upper|preserve}` ** -NTFS 파일 시스템의 파일 이름에 있는 문자의 대/소문자를 소문자, 대문자 또는 디렉터리에 저장 된 형식으로 반환할지 여부를 지정 합니다. 기본 설정은 **유지**합니다. **Casesensitivelookups** 가 **yes**로 설정 된 경우에는이 설정을 변경할 수 없습니다.</li></ul> |
| creategroup`<name>` | 제공 하 여 지정 된 새 클라이언트 그룹을 만듭니다 이름합니다. |
| listgroups | 모든 클라이언트 그룹의 이름을 표시합니다. |
| 주로`<name>` | 지정한 클라이언트 그룹 제거 이름합니다. |
| renamegroup `<oldname>``<newname>` | *Oldname* 에 지정 된 클라이언트 그룹의 이름을 *newname*으로 변경 합니다. |
| addmembers`<hostname>[...]` | *이름*으로 지정 된 클라이언트 그룹에 *호스트* 를 추가 합니다. |
| listmembers`<name>` | *이름*으로 지정 된 클라이언트 그룹의 호스트 컴퓨터를 나열 합니다. |
| deletemembers`<hostname><groupname>[...]` | *그룹*으로 지정 된 클라이언트 그룹에서 *호스트로* 지정 된 클라이언트를 제거 합니다. |

### <a name="client-for-nfs-related-parameters"></a>NFS 관련 매개 변수에 대 한 클라이언트

| 매개 변수 | Description |
| --------- | ----------- |
| start | NFS 용 클라이언트 서비스를 시작합니다. |
| stop(정지) | NFS 용 클라이언트 서비스를 중지합니다. |
| config | NFS 용 클라이언트에 대 한 일반 설정을 지정합니다. 하나 이상의 다음 옵션을 제공 해야는 **config** 인수:<ul><li>**fileaccess = `<mode>` ** -NFS (네트워크 파일 시스템) 서버에서 만든 파일에 대 한 기본 사용 권한 모드를 지정 합니다. **Mode** 인수는 0에서 7 (포함) 사이의 세 자리 숫자로 구성 되며 사용자, 그룹 및 다른 사용자에 게 부여 된 기본 사용 권한을 나타냅니다. 숫자는 다음과 같이 UNIX 스타일 사용 권한으로 변환 됩니다. *0 = 없음*, *1 = x (실행)*, *2 = w (쓰기 전용)*, *3 = wx (쓰기 및 실행*), *4 = r (읽기 전용)*, *5 = rx (읽기 및 실행)*, *6 = rw (읽기 및 쓰기)* 및 *7 = rwx (읽기, 쓰기 및 실행)*. 예를 들어는 `fileaccess=750` 소유자에 대 한 읽기, 쓰기 및 실행 권한을 부여 하 고, 그룹에 대 한 읽기 및 실행 권한을 부여 하 고, 다른 사용자에 게 액세스 권한을 부여 하지 않습니다.</li><li>**mapsvr = `<server>` ** -서버를 NFS 용 클라이언트에 대 한 사용자 이름 매핑 서버로 설정 합니다. 이 옵션을 이전 버전과 호환성에 대 한 지원 계속 있지만 사용 해야는 sfuadmin 유틸리티 대신 합니다.</li><li>**mtype = `{hard|soft}` ** -기본 탑재 유형을 지정 합니다. 하드 탑재에 대 한 NFS 용 클라이언트 계속 성공할 때까지 실패 한 RPC를 다시 시도 합니다. 소프트 탑재를 위해 NFS 용 클라이언트 수를 반환 실패 한 호출을 다시 시도한 후 호출 애플리케이션에 지정 된 횟수는 다시 시도 옵션입니다.</li><li>**retry = `<number>` ** -소프트 탑재에 대 한 연결을 시도 하는 횟수를 지정 합니다. 이 값은 1에서 10 (포함) 여야 합니다. 기본값은 **1**입니다.</li><li>**시간 제한 `<seconds>` =** -연결을 대기할 시간 (초)을 지정 합니다 (원격 프로시저 호출). 이 값은 *0.8*, *0.9*또는 *1에서 60*(포함) 사이의 정수 여야 합니다. 기본값은 **0.8**입니다.</li><li>**프로토콜 = `{TCP|UDP|TCP+UDP}` ** -클라이언트가 지 원하는 전송 프로토콜을 지정 합니다. 기본 설정은 **TCP + UDP**입니다.</li><li>**rsize = `<size>` ** -읽기 버퍼의 크기 (kb)를 지정 합니다. 이 값은 *0.5, 1, 2, 4, 8, 16* 또는 *32*일 수 있습니다. 기본값은 **32**입니다.</li><li>**wsize = `<size>` ** -쓰기 버퍼의 크기 (kb)를 지정 합니다. 이 값은 *0.5, 1, 2, 4, 8, 16* 또는 *32*일 수 있습니다. 기본값은 **32**입니다.</li><li>**perf = default** -다음 성능 설정을 기본값 ( *mtype*, *retry*, *timeout*, *rsize*또는 *wsize*)으로 복원 합니다. |

### <a name="examples"></a>예제

Nfs 용 서버나 NFS 용 클라이언트를 중지 하려면 다음을 입력 합니다.

```
nfsadmin server stop
nfsadmin client stop
```

Nfs 용 서버나 NFS 용 클라이언트를 시작 하려면 다음을 입력 합니다.

```
nfsadmin server start
nfsadmin client start
```

NFS 용 서버에서 대/소문자를 구분 하지 않도록 설정 하려면 다음을 입력 합니다.

```
nfsadmin server config casesensitive=no
```

NFS 용 클라이언트를 대/소문자를 구분 하도록 설정 하려면 다음을 입력 합니다.

```
nfsadmin client config casesensitive=yes
```

NFS 용 현재 서버 또는 NFS 용 클라이언트 옵션을 모두 표시 하려면 다음을 입력 합니다.

```
nfsadmin server config
nfsadmin client config
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [NFS cmdlet 참조](https://docs.microsoft.com/powershell/module/nfs)
