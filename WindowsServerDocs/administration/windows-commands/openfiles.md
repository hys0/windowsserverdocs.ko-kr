---
title: openfiles
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c3be561d-a11f-4bf1-9835-8e4e96fe98ec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38b1d27b86551c6d4cd9e6b1ad87bfc0e8dd221d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372504"
---
# <a name="openfiles"></a>openfiles



관리자가 쿼리, 표시 또는 파일 및 디렉터리는 시스템에서 열려 있는 연결을 끊을 수 있습니다. 또한 사용 하거나 시스템 개체 목록을 유지 관리 하려면 전역 플래그를 사용 하지 않도록 설정 합니다.

이 항목에는 다음 명령에 대 한 정보가 포함 됩니다.
-   [openfiles/disconnect](#BKMK_disconnect)
-   [openfiles/query](#BKMK_query)
-   [openfiles/local](#BKMK_local)

## <a name="BKMK_disconnect"></a>openfiles/disconnect

관리자가 파일 및 폴더를 공유 폴더를 통해 원격으로 열린 연결을 끊을 수 있습니다.

### <a name="syntax"></a>구문

```
openfiles /disconnect [/s <System> [/u [<Domain>\]<UserName> [/p [<Password>]]]] {[/id <OpenFileID>] | [/a <AccessedBy>] | [/o {read | write | read/write}]} [/op <OpenFile>]
```

### <a name="parameters"></a>매개 변수

|            매개 변수             |                                                                                                                                 설명                                                                                                                                  |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /s \<System >           | 원격 시스템에 연결 (이름 또는 IP 주소)을 지정 합니다. 백슬래시를 사용 하지 마십시오. 사용 하지 않는 경우는 **/s** 명령 옵션을 기본적으로 로컬 컴퓨터에서 실행 됩니다. 이 매개 변수는 모든 파일 및 명령에 지정 된 폴더에 적용 됩니다. |
|    /u [\<Domain > \] @ no__t-2     |                                                          지정 된 사용자 계정의 권한을 사용 하 여 명령을 실행 합니다. 사용 하지 않는 경우는 **/u** 옵션을 시스템 사용 권한을 기본적으로 사용 됩니다.                                                           |
|         /p [\<Password >]         |                                               에 지정 된 사용자 계정의 암호를 지정 된 **/u** 옵션입니다. 사용 하지 않는 경우는 **/p** 명령이 실행 되는 경우 옵션을 암호를 묻는 메시지가 나타납니다.                                                |
|        /id \<OpenFileID >         |                                       지정 된 파일 ID가 열려 있는 파일의 연결을 끊습니다. 이 매개 변수와 함께 **&#42;** 와일드 카드 문자 ()를 사용할 수 있습니다.</br>참고: **Openfiles/query** 명령을 사용 하 여 파일 ID를 찾을 수 있습니다.                                       |
|         /a \<AccessedBy >         |                                                에 지정 된 사용자 이름과 관련 된 열려 있는 모든 파일의 연결을 끊습니다는 *AccessedBy* 매개 변수입니다. 이 매개 변수와 함께 **&#42;** 와일드 카드 문자 ()를 사용할 수 있습니다.                                                 |
| /o {read \| 쓰기 \| 읽기/쓰기} |                                               지정 된 열려 있는 모드 값을 사용 하 여 열려 있는 모든 파일의 연결을 끊습니다. 유효한 값에는 읽기, 쓰기 또는 읽기/쓰기는입니다. 이 매개 변수와 함께 **&#42;** 와일드 카드 문자 ()를 사용할 수 있습니다.                                                |
|         /op \<OpenFile >          |                                                           열려 있는 특정 파일 이름으로 만들어진 모든 열려 있는 파일 연결을 끊습니다. 이 매개 변수와 함께 **&#42;** 와일드 카드 문자 ()를 사용할 수 있습니다.                                                           |
|                /?                |                                                                                                                     명령 프롬프트에 도움말을 표시합니다.                                                                                                                     |

### <a name="examples"></a>예

ID 26843578 파일을 사용 하 여 열려 있는 모든 파일 연결을 끊으려면 다음을 입력 합니다.
```
openfiles /disconnect /id 26843578
```
모든 열려 있는 파일 및 디렉터리 "hiropln" 사용자가 액세스 연결을 끊으려면 다음을 입력 합니다.
```
openfiles /disconnect /a hiropln
```
모든 열려 있는 파일 및 읽기/쓰기 모드를 사용 하 여 디렉터리 연결을 끊으려면 다음을 입력 합니다.
```
openfiles /disconnect /o read/write
```
파일에 액세스 하는 사용자에 관계 없이 열린 파일 이름 "C:\TestShare @ no__t-0"을 사용 하 여 디렉터리의 연결을 끊으려면 다음을 입력 합니다.
```
openfiles /disconnect /a * /op "c:\testshare\"
```
가 ID에 관계 없이 "srvmain" 원격 컴퓨터에서 "hiropln" 사용자가 액세스 하는 모든 열린 파일을 분리 하려면 다음을 입력 합니다.
```
openfiles /disconnect /s srvmain /u maindom\hiropln /id *
```

## <a name="BKMK_query"></a>openfiles/query

쿼리하고 열려 있는 모든 파일을 표시 합니다.

### <a name="syntax"></a>구문

```
openfiles /query [/s <System> [/u [<Domain>\]<UserName> [/p [<Password>]]]] [/fo {TABLE | LIST | CSV}] [/nh] [/v]
```

### <a name="parameters"></a>매개 변수

|          매개 변수           |                                                                                                                                 설명                                                                                                                                  |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         /s \<System >         | 원격 시스템에 연결 (이름 또는 IP 주소)을 지정 합니다. 백슬래시를 사용 하지 마십시오. 사용 하지 않는 경우는 **/s** 명령 옵션을 기본적으로 로컬 컴퓨터에서 실행 됩니다. 이 매개 변수는 모든 파일 및 명령에 지정 된 폴더에 적용 됩니다. |
|  /u [\<Domain > \] @ no__t-2   |                                                          지정 된 사용자 계정의 권한을 사용 하 여 명령을 실행 합니다. 사용 하지 않는 경우는 **/u** 옵션을 시스템 사용 권한을 기본적으로 사용 됩니다.                                                           |
|       /p [\<Password >]       |                                               에 지정 된 사용자 계정의 암호를 지정 된 **/u** 옵션입니다. 사용 하지 않는 경우는 **/p** 명령이 실행 되는 경우 옵션을 암호를 묻는 메시지가 나타납니다.                                                |
| [/fo {테이블 \| 목록 \| CSV}] |                             지정된 된 형식으로 출력을 표시합니다. 유효한 값에 대 한 *형식* 됩니다.</br>테이블  테이블에 출력을 표시 합니다.</br>은 목록에 출력을 표시 합니다.</br>CSV 쉼표로 구분 된 값 형식으로 출력을 표시 합니다.                              |
|             /nh              |                                                                                출력에 열 머리글을 표시 하지 않습니다. 경우에만 유효는 **/fo** 매개 변수는 설정 **테이블** 또는 **CSV**합니다.                                                                                 |
|              /v              |                                                                                                       자세한 정보는 출력에 표시를 지정 합니다.                                                                                                        |
|              /?              |                                                                                                                     명령 프롬프트에 도움말을 표시합니다.                                                                                                                     |

### <a name="examples"></a>예

쿼리하고 열려 있는 모든 파일을 표시 하려면 다음을 입력 합니다.
```
openfiles /query
```
쿼리하고 머리글이 없는 테이블 형식으로 열려 있는 모든 파일을 표시 하려면 다음을 입력 합니다.
```
openfiles /query /fo table /nh
```
쿼리 세부 정보를 목록 형식으로 열려 있는 모든 파일 표시를 입력 합니다.
```
openfiles /query /fo list /v
```
쿼리하고 "hiropln" "maindom" 도메인에서 사용자에 대 한 자격 증명을 사용 하 여 "srvmain" 원격 시스템에서 열려 있는 모든 파일을 표시 하려면 다음을 입력 합니다.
```
openfiles /query /s srvmain /u maindom\hiropln /p p@ssW23
```

> [!NOTE]
> 이 예제에서는 암호를 명령줄에 제공 합니다. 암호 표시를 방지 하려면 생략 된 **/p** 옵션입니다. 화면에 표시 되지 암호를 묻는 메시지가 나타납니다.

## <a name="BKMK_local"></a>openfiles/local

시스템 개체 목록을 유지 관리 하려면 전역 플래그를 사용 하지 않도록 설정 하거나 사용 합니다. 매개 변수 없이 사용 하는 경우 **openfiles /local** 개체 목록을 유지 관리 하려면 전역 플래그의 현재 상태를 표시 합니다.

### <a name="syntax"></a>구문

```
openfiles /local [on | off]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[on \| 해제]|사용 하거나 시스템 로컬 파일 핸들을 추적 하는 개체 목록을 유지 관리 전역 플래그를 사용 하지 않도록 설정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

### <a name="remarks"></a>설명

-   개체 목록을 유지 관리 하려면 전역 플래그를 사용 하도록 설정 하면 시스템 느려질 수 있습니다.
-   변경 내용을 사용 하 여는 **에** 또는 **오프** 시스템을 다시 시작 될 때까지 옵션 내용이 적용 되지 않습니다.

### <a name="examples"></a>예

개체 목록을 유지 관리 하려면 전역 플래그의 현재 상태를 확인 하려면 다음을 입력 합니다.
```
openfiles /local
```
기본적으로 개체 목록을 유지 관리 하려면 전역 플래그를 사용 하지 않도록 설정 하 고 다음과 같은 출력이 표시 됩니다.
```
INFO: The system global flag 'maintain objects list' is currently disabled.
```
개체 목록을 유지 관리 하려면 전역 플래그를 사용 하려면 다음을 입력 합니다.
```
openfiles /local on
```
전역 플래그를 설정 하는 경우 다음과 같은 메시지가 표시 됩니다.
```
SUCCESS: The system global flag 'maintain objects list' is enabled.
         This will take effect after the system is restarted.
```
개체 목록을 유지 관리 하려면 전역 플래그를 해제 하려면 다음을 입력 합니다.
```
openfiles /local off
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)