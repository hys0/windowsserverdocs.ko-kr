---
title: macfile
description: Macintosh 서버, 볼륨, 디렉터리 및 파일에 대 한 파일 서버를 관리 하는 macfile 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e2ce586c-b316-41d3-90f8-4be0d074cc0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6937e8bbf40ec9ce908be095e5de0e04f793f40e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933650"
---
# <a name="macfile"></a>macfile

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Macintosh 서버, 볼륨, 디렉터리 및 파일에 대 한 파일 서버를 관리합니다. 미리 정해진 시간에 또는 배치 파일에는 일련의 명령 포함 하 고 수동으로 시작 되 게 여 관리 작업을 자동화할 수 있습니다.

## <a name="modify-directories-in-macintosh-accessible-volumes"></a>Macintosh에서 액세스할 수 있는 볼륨의 디렉터리 수정

Macintosh에서 액세스할 수 있는 볼륨의 디렉터리 이름, 위치, 소유자, 그룹 및 사용 권한을 변경 합니다.

### <a name="syntax"></a>구문

```
macfile directory[/server:\\<computername>] /path:<directory> [/owner:<ownername>] [/group:<groupname>] [/permissions:<permissions>]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /server:`\\<computername>` | 디렉터리를 변경할 서버를 지정 합니다. 생략 하면 로컬 컴퓨터에서 작업이 수행 됩니다. |
| /path`<directory>` | 변경 하려는 디렉터리의 경로를 지정 합니다. 이 매개 변수는 필수입니다. **참고:** 디렉터리가 있어야 하 고, **macfile 디렉터리** 를 사용 하 여 디렉터리를 만들지 않습니다. |
| /owner`<ownername>` | 디렉터리의 소유자를 변경 합니다. 생략 하면 소유자 이름이 변경 되지 않습니다. |
| 그룹`<groupname>` | 디렉터리와 연결 된 Macintosh 주 그룹을 지정 하거나 변경 합니다. 생략 하면 주 그룹 변경 되지 않습니다. |
| 권한에`<permissions>` | 소유자, 주 그룹 및 세계 (everyone)의 디렉터리에 대 한 사용 권한을 설정 합니다. 숫자 1은 사용 권한을 부여 하 고 0은 사용 권한을 부여 하는 11 자리 숫자 여야 합니다 (예: 11111011000). 이 매개 변수를 생략 하면 사용 권한이 변경 되지 않은 상태로 유지 됩니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

##### <a name="position-of-permissions-digit"></a>사용 권한 숫자의 위치

사용 권한 숫자의 위치는 다음을 비롯 하 여 설정 된 사용 권한을 결정 합니다.

| 위치 | 권한 설정 |
| -------- | --------------- |
| 첫째 | OwnerSeeFiles |
| Second | OwnerSeeFolders |
| 셋째 | OwnerMakechanges |
| 넷째 | GroupSeeFiles |
| 다섯 번째 | GroupSeeFolders |
| 여섯 번째 | GroupMakechanges |
| 일곱 번째 | WorldSeeFiles |
| 여덟 번째 | WorldSeeFolders |
| 아홉 번째 | WorldMakechanges |
| 열 번째 | 디렉터리의 이름을 바꾸거나 이동 하거나 삭제할 수 없습니다. |
| 열 한 번째 | 현재 디렉터리와 모든 하위 디렉터리에 변경 내용을 적용 합니다. |

##### <a name="remarks"></a>설명

- 사용자가 제공 하는 정보에 공백이 나 특수 문자가 포함 된 경우 텍스트 주위에 따옴표를 사용 합니다 (예: " `<computer name>` ").

- **Macfile 디렉터리** 를 사용 하 여 macintosh 사용자가 사용할 수 있는 macintosh에서 액세스할 수 있는 볼륨의 기존 디렉터리를 만듭니다. **Macfile 디렉터리** 명령은 디렉터리를 만들지 않습니다.

- 파일 관리자 명령 프롬프트를 사용 하 여 또는 **macintosh 새 폴더** 명령을 사용 하기 전에 Macintosh에서 액세스할 수 있는 볼륨의 디렉터리를 만들 수는 **macfile 디렉터리** 명령입니다.

#### <a name="examples"></a>예

파일을 할당 하려면 *파일 보기*를 *참조*하 고, 소유자에 게 *변경* 권한을 부여 하 고, 다른 모든 사용자에 대 한 *폴더 권한 보기* 를 설정 하 고, 디렉터리의 이름을 변경 하거나, 이동 하거나, 삭제 하지 않도록 하려면 다음을 입력 합니다.

```
macfile directory /path:e:\statistics\may sales /permissions:11111011000
```

여기서 하위 디렉터리는 E:\의 Macintosh에서 액세스할 수 있는 볼륨 *통계*에 있는 *Sales가 될 수 있습니다*. 로컬 서버의 드라이브입니다.

## <a name="join-a-macintosh-files-data-and-resource-forks"></a>Macintosh 파일의 데이터 및 리소스 포크 조인

파일이 가입 될 서버, 파일을 만든 사람, 데이터 분기가 있는 파일 형식, 리소스 분기가 있는 위치 및 출력 파일을 배치할 서버를 지정 합니다.

### <a name="syntax"></a>구문

```
macfile forkize[/server:\\<computername>] [/creator:<creatorname>] [/type:<typename>]  [/datafork:<filepath>] [/resourcefork:<filepath>] /targetfile:<filepath>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /server:`\\<computername>` | 조인할 파일 서버를 지정 합니다. 생략 하면 로컬 컴퓨터에서 작업이 수행 됩니다. |
| 만든`<creatorname>` | 파일의 작성자를 지정 합니다. Macintosh finder는 **/sourceo** 명령줄 옵션을 사용 하 여 파일을 만든 응용 프로그램을 확인 합니다. |
| /type`<typename>` | 파일의 유형을 지정합니다. Macintosh finder는 **/type** 명령줄 옵션을 사용 하 여 파일을 만든 응용 프로그램 내의 파일 형식을 확인 합니다. |
| /datafork:`<filepath>` | 조인 되는 데이터 포크의 위치를 지정 합니다. 원격 경로 지정할 수 있습니다. |
| /resourcefork:`<filepath>` | 조인 되는 리소스 포크의 위치를 지정 합니다. 원격 경로 지정할 수 있습니다. |
| targetfile`<filepath>` | 데이터 포크 및 리소스 포크를 조인 하 여 만든 파일의 위치를 지정 하거나, 해당 형식이 나 작성자가 변경할 파일의 위치를 지정 합니다. 지정된 된 서버에서 파일 이어야 합니다. 이 매개 변수는 필수입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

##### <a name="remarks"></a>설명

- 사용자가 제공 하는 정보에 공백이 나 특수 문자가 포함 된 경우 텍스트 주위에 따옴표를 사용 합니다 (예: " `<computer name>` ").

#### <a name="examples"></a>예

Macintosh에서 액세스할 수 있는 볼륨 *D:\release*에서 파일 *tree_app* 를 만들고 리소스 포크 *C:\cross\mac\appcode*를 사용 하 여이 새 파일을 macintosh 클라이언트에 응용 프로그램으로 표시 하는 경우 (macintosh 응용 프로그램에서 *appl*형식 사용) 작성자 (서명)를 *목련*로 설정 하 고 다음을 입력 합니다.

```
macfile forkize /resourcefork:c:\cross\mac\appcode /type:APPL /creator:MAGNOLIA /targetfile:D:\Release\tree_app
```

파일 작성자를 *Microsoft Word 5.1*으로 변경 하려면 * \\ 서버 a*디렉터리의 파일 *Word.txt* 에 대해 서버에서 *다음을 입력*합니다.

```
macfile forkize /server:\\ServerA /creator:MSWD /type:TEXT /targetfile:d:\Word documents\Group files\Word.txt
```

## <a name="change-the-sign-in-message-and-limit-sessions"></a>로그인 메시지 변경 및 세션 제한

사용자가 Macintosh 용 파일 서버 서버에 로그인 할 때 표시 되는 로그온 메시지를 변경 하 고 Macintosh 용 파일 및 인쇄 서버를 동시에 사용할 수 있는 사용자 수를 제한 하려면입니다.

### <a name="syntax"></a>구문

```
macfile server [/server:\\<computername>] [/maxsessions:{number | unlimited}] [/loginmessage:<message>]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- |------------ |
| /server:`\\<computername>` | 매개 변수를 변경 하려는 서버를 지정 합니다. 생략 하면 로컬 컴퓨터에서 작업이 수행 됩니다. |
| maxsessions`{number | unlimited}` | Macintosh 용 파일 및 인쇄 서버를 동시에 사용할 수 있는 최대 사용자 수를 지정 합니다. 생략 한 경우는 **maxsessions** 를 설정 하는 서버 그대로 유지 됩니다. |
| /loginmessage:`<message>` | Macintosh 용 파일 서버 서버에 로그인 할 때 Macintosh 사용자에 게 표시 되는 메시지를 변경 합니다. 로그인 메시지의 최대 문자 수는 199입니다. 생략 한 경우는 **loginmessage** 서버 그대로 유지에 대 한 메시지입니다. 기존 로그인 메시지를 제거 하려면 **/loginmessage** 매개 변수를 포함 하 되 *메시지* 변수는 비워 둡니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

##### <a name="remarks"></a>설명

- 사용자가 제공 하는 정보에 공백이 나 특수 문자가 포함 된 경우 텍스트 주위에 따옴표를 사용 합니다 (예: " `<computer name>` ").

#### <a name="examples"></a>예

로컬 서버에서 허용 되는 파일 및 Macintosh 세션의 인쇄 서버 수를 5 개 세션으로 변경 하 고 로그인 메시지 "작업을 완료할 때 Macintosh 용 서버에서 로그 오프"를 추가 하려면 다음을 입력 합니다.

```
macfile server /maxsessions:5 /loginmessage:Sign off from Server for Macintosh when you are finished
```

## <a name="add-change-or-remove-macintosh-accessible-volumes"></a>Macintosh에서 액세스할 수 있는 볼륨 추가, 변경 또는 제거

Macintosh에서 액세스할 수 있는 볼륨을 추가, 변경 또는 제거 합니다.

### <a name="syntax"></a>구문

```
macfile volume {/add|/set} [/server:\\<computername>] /name:<volumename>/path:<directory>[/readonly:{true | false}] [/guestsallowed:{true | false}] [/password:<password>] [/maxusers:{<number>>|unlimited}]
macfile volume /remove[/server:\\<computername>] /name:<volumename>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{/add | /set}` | Macintosh에서 액세스할 수 있는 볼륨을 추가 하거나 변경할 때 필요 합니다. 추가 하거나 지정된 된 볼륨을 변경 합니다. |
| /server:`\\<computername>` | 서버를 추가, 변경 또는 볼륨 제거를 지정 합니다. 생략 하면 로컬 컴퓨터에서 작업이 수행 됩니다. |
| /name`<volumename>` | 필수 요소. 추가, 변경 또는 제거 된 볼륨 이름을 지정 합니다. |
| /path`<directory>` | 필수 및 볼륨을 추가 하는 경우에 유효 합니다. 추가 될 때 변환할 볼륨의 루트 디렉터리의 경로를 지정 합니다. |
| readonly`{true | false}` | 사용자가 볼륨의 파일을 변경할 수 있는지 여부를 지정 합니다. 사용자가 볼륨의 파일을 변경할 수 없도록 지정 하려면 **True** 를 사용 합니다. 사용자가 볼륨의 파일을 변경할 수 있도록 지정 하려면 **False** 를 사용 합니다. 볼륨을 추가 하는 경우를 지정 하지 않으면 파일에는 변경이 허용 됩니다. 볼륨을 변경 하는 경우를 생략 하는 경우는 **readonly** 를 설정 하는 볼륨 그대로 유지 됩니다. |
| /guestsallowed:`{true | false}` | 로그온 사용자에 게 게스트로 볼륨을 사용할 수 있는지 여부를 지정 합니다. 게스트가 볼륨을 사용할 수 있도록 지정 하려면 **True** 를 사용 합니다. 게스트가 볼륨을 사용할 수 없도록 지정 하려면 **False** 를 사용 합니다. 볼륨을 추가 하는 경우를 생략 하면 게스트가 볼륨을 사용할 수 있습니다. 볼륨을 변경 하는 경우를 생략 하는 경우는 **guestsallowed** 를 설정 하는 볼륨 그대로 유지 됩니다. |
| /password`<password>` | 볼륨에 액세스 하는 데 필요한는 암호를 지정 합니다. 볼륨을 추가 하는 경우를 생략 하면 암호를 만들지 않습니다. 볼륨을 변경 하는 경우를 생략 하면 암호가 변경 되지 않습니다. |
| /maxusers:`{<number>> | unlimited}` | 볼륨에서 파일을 동시에 사용할 수 있는 사용자의 최대 수를 지정 합니다. 볼륨을 추가 하는 경우를 지정 하지 않으면 사용자의 무제한 볼륨을 사용할 수 있습니다. 볼륨을 변경 하는 경우를 생략 하는 경우는 **maxusers** 값 변경 되지 않습니다.                                                 |
| /remove | Macintosh에서 액세스할 수 있는 볼륨을 제거 하는 경우에 필요 합니다. 지정 된 볼륨을 제거 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

##### <a name="remarks"></a>설명

- 사용자가 제공 하는 정보에 공백이 나 특수 문자가 포함 된 경우 텍스트 주위에 따옴표를 사용 합니다 (예: " `<computer name>` ").

#### <a name="examples"></a>예

로컬 서버에서 *미국 마케팅 통계* 라는 볼륨을 만들고, E 드라이브의 *Stats* 디렉터리를 사용 하 고, 게스트에서 볼륨에 액세스할 수 없도록 지정 하려면 다음을 입력 합니다.

```
macfile volume /add /name:US Marketing Statistics /guestsallowed:false /path:e:\Stats
```

위에서 만든 볼륨을 읽기 전용으로 변경 하 고, 암호를 요구 하 고, 최대 사용자 수를 5로 설정 하려면 다음을 입력 합니다.

```
macfile volume /set /name:US Marketing Statistics /readonly:true /password:saturn /maxusers:5
```

서버 * \\ 목련*에서 E 드라이브의 *트리* 디렉터리를 사용 하 여 *가로 디자인*이라는 볼륨을 추가 하 고 게스트에서 볼륨에 액세스할 수 있도록 지정 하려면 다음을 입력 합니다.

```
macfile volume /add /server:\\Magnolia /name:Landscape Design /path:e:\trees
```

로컬 서버에서 *Sales Reports* 라는 볼륨을 제거 하려면 다음을 입력 합니다.

```
macfile volume /remove /name:Sales Reports
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
