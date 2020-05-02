---
title: macfile
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e2ce586c-b316-41d3-90f8-4be0d074cc0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4384ce8d4f23966aea278e90b9ddddc42da6e77
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724230"
---
# <a name="macfile"></a>macfile

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Macintosh 서버, 볼륨, 디렉터리 및 파일에 대 한 파일 서버를 관리합니다. 미리 정해진 시간에 또는 배치 파일에는 일련의 명령 포함 하 고 수동으로 시작 되 게 여 관리 작업을 자동화할 수 있습니다. 
-   [Macintosh에서 액세스할 수 있는 볼륨의 디렉터리를 수정 하려면](#BKMK_Moddirs)
-   [Macintosh 파일의 데이터 및 리소스 포크 조인 하려면](#BKMK_Joinforks)
-   [로그온 메시지를 변경 하 고 세션 제한 하려면](#BKMK_LogonLimit)
-   [추가, 변경 또는 Macintosh에서 액세스할 수 있는 볼륨을 제거 하려면](#BKMK_addvol)

## <a name="to-modify-directories-in-macintosh-accessible-volumes"></a><a name=BKMK_Moddirs></a>Macintosh에서 액세스할 수 있는 볼륨의 디렉터리를 수정 하려면

### <a name="syntax"></a>구문
```
macfile directory[/server:\\<computerName>] /path:<directory> [/owner:<OwnerName>] [/group:<GroupName>] [/permissions:<Permissions>]
```

#### <a name="parameters"></a>매개 변수
-   /server:\\ \\ <computerName> 디렉터리를 변경할 서버를 지정 합니다. 생략 하면 로컬 컴퓨터에서 작업이 수행 됩니다.
-   /path:<directory> 필요 합니다. 변경 하려는 디렉터리의 경로를 지정 합니다. 디렉터리가 있어야 합니다. **macfile 디렉터리** 는 디렉터리를 만들지 않습니다.
-   /owner:<OwnerName> 디렉터리의 소유자를 변경 합니다. 생략 하면 소유자 변경 되지 않습니다.
-   그룹 /:<GroupName> 디렉터리와 연결 된 지정 또는 변경 내용을 기본 Macintosh 그룹입니다. 생략 하면 주 그룹 변경 되지 않습니다.
-   /permissions:<Permissions> 소유자, 주 그룹 및 전역 (모든 사람)에 대 한 디렉터리 사용 권한을 설정 합니다. 11 자리 수는 사용 권한을 설정 하는 데 사용 됩니다. 숫자 1에 권한을 부여 하 고 0 해지 권한 (예를 들어 11111011000) 키를 누릅니다. 생략 하면 사용 권한을 그대로 유지 됩니다.
    숫자의 위치는 다음 표에 설명 된 대로 어떤 사용 권한이 설정 되어를 결정 합니다.

    |위치|에 대 한 권한을 설정합니다.|
    |------|------------|
    |처음|OwnerSeeFiles|
    |초|OwnerSeeFolders|
    |셋째|OwnerMakechanges|
    |넷째|GroupSeeFiles|
    |다섯 번째|GroupSeeFolders|
    |여섯 번째|GroupMakechanges|
    |일곱 번째|WorldSeeFiles|
    |여덟 번째|WorldSeeFolders|
    |아홉 번째|WorldMakechanges|
    |열 번째|디렉터리 이름이 이동 하거나 삭제할 수 없습니다.|
    |열 한 번째|현재 디렉터리와 모든 하위 디렉터리에 변경 내용을 적용 합니다.|

-   /?
    명령 프롬프트에 도움말을 표시합니다.

### <a name="remarks"></a>설명
- 사용자가 제공 하는 정보에 공백이 나 특수 문자가 포함 된 경우 텍스트 주위에 따옴표를 사용 합니다 (예: * * * *<em>컴퓨터 이름</em>* * * *).
- 사용 하 여 **macfiledirectory** 기존 디렉터리 Macintosh에서 액세스할 수 있는 볼륨에서 사용할 수 있도록 Macintosh 사용자에 게 있습니다. **macfiledirectory** 명령은 디렉터리를 만들지 않습니다. 파일 관리자 명령 프롬프트를 사용 하 여 또는 **macintosh 새 폴더** 명령을 사용 하기 전에 Macintosh에서 액세스할 수 있는 볼륨의 디렉터리를 만들 수는 **macfile 디렉터리** 명령입니다.
  ### <a name="examples"></a>예
  하위 디렉터리의 사용 권한을 변경 하려면 Macintosh에서 액세스할 수 있는 볼륨 통계에서 로컬 서버의 E 드라이브에 있습니다. 이 예에서는 파일을 할당 하 고, 폴더를 참조 하 고, 소유자에 게 변경 권한을 부여 하 고, 디렉터리의 이름을 바꾸거나, 이동 하거나, 삭제 하지 못하게 하는 동시에 다른 모든 사용자에 대 한 파일 및 폴더 사용 권한을 할당 합니다.
  ```
  macfile directory /path:e:\statistics\may sales /permissions:11111011000
  ```

## <a name="to-join-a-macintosh-files-data-and-resource-forks"></a><a name=BKMK_Joinforks></a>Macintosh 파일의 데이터 및 리소스 포크 조인 하려면

### <a name="syntax"></a>구문
```
macfile forkize[/server:\\<computerName>] [/creator:<CreatorName>] [/type:<typeName>]  [/datafork:<Filepath>] [/resourcefork:<Filepath>] /targetfile:<Filepath>
```

#### <a name="parameters"></a>매개 변수

|         매개 변수          |                                                                                                           설명                                                                                                            |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /server\\\\<computerName> |                                                            조인할 파일 서버를 지정 합니다. 생략 하면 로컬 컴퓨터에서 작업이 수행 됩니다.                                                            |
|   만든<CreatorName>   |                                      파일의 작성자를 지정 합니다. Macintosh finder는 **/sourceo** 명령줄 옵션을 사용 하 여 파일을 만든 응용 프로그램을 확인 합니다.                                       |
|      /type<typeName>      |                                 파일의 유형을 지정합니다. Macintosh finder는 **/type** 명령줄 옵션을 사용 하 여 파일을 만든 응용 프로그램 내의 파일 형식을 확인 합니다.                                 |
|    /datafork:<Filepath>    |                                                                   조인 되는 데이터 포크의 위치를 지정 합니다. 원격 경로 지정할 수 있습니다.                                                                   |
|  /resourcefork:<Filepath>  |                                                                 조인 되는 리소스 포크의 위치를 지정 합니다. 원격 경로 지정할 수 있습니다.                                                                 |
|   targetfile<Filepath>   | 필수 사항입니다. 데이터 포크 및 리소스 포크를 결합 하 여 만든 파일의 위치를 지정 하거나 해당 형식 또는 만든이를 변경할 파일의 위치를 지정 합니다. 지정된 된 서버에서 파일 이어야 합니다. |
|             /?             |                                                                                               명령 프롬프트에 도움말을 표시합니다.                                                                                               |

### <a name="remarks"></a>설명
- 사용자가 제공 하는 정보에 공백이 나 특수 문자가 포함 된 경우 텍스트 주위에 따옴표를 사용 합니다 (예: * * * *<em>컴퓨터 이름</em>* * * *).

### <a name="examples"></a>예
Macintosh에서 액세스할 수 있는 볼륨 D:\Release에 treeapp 파일을 만들고 리소스 포크 C:\Cross\Mac\Appcode를 사용 하 여이 새 파일이 Macintosh 클라이언트에 응용 프로그램으로 표시 되도록 하려면 (Macintosh 응용 프로그램에서 APPL 형식 사용) 작성자 (서명)를 목련로 설정 하 고 다음을 입력 합니다.
```
macfile forkize /resourcefork:c:\cross\mac\appcode /type:APPL /creator:MAGNOLIA /targetfile:D:\Release\treeapp
```
파일 작성자를 Microsoft Word 5.1으로 변경 하려면 \SERverA 파일 디렉터리의 파일에서 .txt 파일에 대해 서버 \\에서 다음을 입력 합니다.
```
macfile forkize /server:\\servera /creator:MSWD /type:TEXT /targetfile:d:\Word documents\Group files\Word.txt
```

## <a name="to-change-the-logon-message-and-limit-sessions"></a><a name=BKMK_LogonLimit></a>로그온 메시지를 변경 하 고 세션 제한 하려면
### <a name="syntax"></a>구문
```
macfile server [/server:\\<computerName>] [/maxsessions:{Number | unlimited}] [/loginmessage:<Message>]
```

#### <a name="parameters"></a>매개 변수

|               매개 변수                |                                                                                                                                                                           설명                                                                                                                                                                            |
|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /server\\\\<computerName>       |                                                                                                                        매개 변수를 변경 하려는 서버를 지정 합니다. 생략 하면 로컬 컴퓨터에서 작업이 수행 됩니다.                                                                                                                         |
| /maxsessions: {번호 & #124; 무제한} |                                                                                         Macintosh 용 파일 및 인쇄 서버를 동시에 사용할 수 있는 최대 사용자 수를 지정 합니다. 생략 한 경우는 **maxsessions** 를 설정 하는 서버 그대로 유지 됩니다.                                                                                         |
|        /loginmessage:<Message>         | macintosh 용 파일 서버 서버에 로그온 할 때 Macintosh 사용자에 게 표시 되는 메시지를 변경 합니다. 로그온 메시지에 대 한 문자의 최대 수는 199입니다. 생략 한 경우는 **loginmessage** 서버 그대로 유지에 대 한 메시지입니다. 기존 로그온 메시지를 제거 하려면 포함는 **/loginmessage** 하지 않으면 매개 변수는 *메시지* 빈 변수. |
|                   /?                   |                                                                                                                                                               명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                               |

### <a name="remarks"></a>설명
- 사용자가 제공 하는 정보에 공백이 나 특수 문자가 포함 된 경우 텍스트 주위에 따옴표를 사용 합니다 (예: * * * *<em>컴퓨터 이름</em>* * * *).

### <a name="examples"></a>예
로컬 서버에서 허용 되는 Macintosh 세션의 파일 및 인쇄 서버 수를 현재 설정에서 5 개의 세션으로 변경 하 고, 완료 되 면 Macintosh 용 서버에서 로그온 메시지 로그를 추가 하려면 다음을 입력 합니다.
```
macfile server /maxsessions:5 /loginmessage:Log off from Server for Macintosh when you are finished.
```

## <a name="to-add-change-or-remove-macintosh-accessible-volumes"></a><a name=BKMK_addvol></a>추가, 변경 또는 Macintosh에서 액세스할 수 있는 볼륨을 제거 하려면
### <a name="syntax"></a>구문
```
macfile volume {/add|/set} [/server:\\<computerName>] /name:<volumeName>/path:<directory>[/readonly:{true | false}] [/guestsallowed:{true | false}] [/password:<Password>] [/maxusers:{<Number>>|unlimited}]
macfile volume /remove[/server:\\<computerName>] /name:<volumeName>
```

#### <a name="parameters"></a>매개 변수

|              매개 변수               |                                                                                                                                                                       설명                                                                                                                                                                        |
|--------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          {/ 추가 (& a) #124; /set}          |                                                                                                                      추가 하거나 Macintosh에서 액세스할 수 있는 볼륨을 변경 하는 경우 필요 합니다. 지정 된 볼륨을 추가 하거나 변경 합니다.                                                                                                                       |
|      /server\\\\<computerName>      |                                                                                                             서버를 추가, 변경 또는 볼륨 제거를 지정 합니다. 생략 하면 로컬 컴퓨터에서 작업이 수행 됩니다.                                                                                                              |
|          /name<volumeName>          |                                                                                                                                          필수 사항입니다. 추가, 변경 또는 제거 된 볼륨 이름을 지정 합니다.                                                                                                                                           |
|          /path<directory>           |                                                                                                                필수 및 볼륨을 추가 하는 경우에 유효 합니다. 추가 될 때 변환할 볼륨의 루트 디렉터리의 경로를 지정 합니다.                                                                                                                 |
|    /readonly: {true & #124; false}     | 사용자가 볼륨의 파일을 변경할 수 있는지 여부를 지정 합니다. 사용자가 볼륨의 파일을 변경할 수 없도록 지정 하려면 true를 입력 합니다. 사용자가 볼륨의 파일을 변경할 수 있도록 지정 하려면 false를 입력 합니다. 볼륨을 추가 하는 경우를 지정 하지 않으면 파일에는 변경이 허용 됩니다. 볼륨을 변경 하는 경우를 생략 하는 경우는 **readonly** 를 설정 하는 볼륨 그대로 유지 됩니다. |
|  /guestsallowed: {true & #124; false}  |      로그온 사용자에 게 게스트로 볼륨을 사용할 수 있는지 여부를 지정 합니다. 게스트가 볼륨을 사용할 수 있도록 지정 하려면 true를 입력 합니다. 게스트가 볼륨을 사용할 수 없도록 지정 하려면 false를 입력 합니다. 볼륨을 추가 하는 경우를 생략 하면 게스트가 볼륨을 사용할 수 있습니다. 볼륨을 변경 하는 경우를 생략 하는 경우는 **guestsallowed** 를 설정 하는 볼륨 그대로 유지 됩니다.       |
|         /password<Password>         |                                                                               볼륨에 액세스 하는 데 필요한는 암호를 지정 합니다. 볼륨을 추가 하는 경우를 생략 하면 암호를 만들지 않습니다. 볼륨을 변경 하는 경우를 생략 하면 암호가 변경 되지 않습니다.                                                                               |
| /maxusers: {<Number>> & #124 무제한;} |                                                 볼륨에서 파일을 동시에 사용할 수 있는 사용자의 최대 수를 지정 합니다. 볼륨을 추가 하는 경우를 지정 하지 않으면 사용자의 무제한 볼륨을 사용할 수 있습니다. 볼륨을 변경 하는 경우를 생략 하는 경우는 **maxusers** 값 변경 되지 않습니다.                                                 |
|               /remove                |                                                                                                                                Macintosh에서 액세스할 볼륨을 제거 하는 경우 필요 합니다. 지정 된 볼륨을 제거 합니다.                                                                                                                                |
|                  /?                  |                                                                                                                                                           명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                           |

### <a name="remarks"></a>설명
- 사용자가 제공 하는 정보에 공백이 나 특수 문자가 포함 된 경우 텍스트 주위에 따옴표를 사용 합니다 (예: * * * *<em>컴퓨터 이름</em>* * * *).

### <a name="examples"></a>예
볼륨을 만들려면 미국 마케팅 통계 통계 디렉터리를 사용 하 여 E 드라이브에 로컬 서버에서 호출 하 고 게스트에서 볼륨을 액세스할 수 없는 지정 하려면 다음을 입력 합니다.
```
macfile volume /add /name:US Marketing Statistics /guestsallowed:false /path:e:\Stats
```
볼륨을 변경 하려면 위에서 만든 읽기 전용으로 암호를 요구 하 고 5, 형식에 최대 사용자 수를 설정 하려면:
```
macfile volume /set /name:US Marketing Statistics /readonly:true /password:saturn /maxusers:5
```
서버 \\\Magnolia에서 E 드라이브의 트리 디렉터리를 사용 하 여 가로 디자인 이라는 볼륨을 추가 하 고 게스트에서 볼륨에 액세스할 수 있도록 지정 하려면 다음을 입력 합니다.
```
macfile volume /add /server:\\Magnolia /name:Landscape Design /path:e:\trees
```
로컬 서버에서 판매 보고서를 호출 하는 볼륨을 제거 하려면 다음을 입력 합니다.
```
macfile volume /remove /name:Sales Reports
```

## <a name="additional-references"></a>추가 참조
-   - [명령줄 구문 키](command-line-syntax-key.md)
