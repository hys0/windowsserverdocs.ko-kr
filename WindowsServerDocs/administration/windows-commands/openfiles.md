---
title: openfiles
description: 관리자가 시스템에서 열려 있는 파일과 디렉터리를 쿼리, 표시 또는 연결을 끊을 수 있도록 하는 openfiles 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c3be561d-a11f-4bf1-9835-8e4e96fe98ec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e55dd88052f1bbfdebb02d1fb6d6f48261643c5c
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472599"
---
# <a name="openfiles"></a>openfiles

관리자가 쿼리, 표시 또는 파일 및 디렉터리는 시스템에서 열려 있는 연결을 끊을 수 있습니다. 또한이 명령을 사용 하면 시스템 **유지 관리 개체 목록** 전역 플래그를 사용 하거나 사용 하지 않도록 설정할 수 있습니다.

## <a name="openfiles-disconnect"></a>openfiles / 연결 끊기

관리자가 파일 및 폴더를 공유 폴더를 통해 원격으로 열린 연결을 끊을 수 있습니다.

### <a name="syntax"></a>구문

```
openfiles /disconnect [/s <system> [/u [<domain>\]<username> [/p [<password>]]]] {[/id <openfileID>] | [/a <accessedby>] | [/o {read | write | read/write}]} [/op <openfile>]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| /s`<system>` | 원격 시스템에 연결 (이름 또는 IP 주소)을 지정 합니다. 백슬래시를 사용 하지 마십시오. **/S** 옵션을 사용 하지 않으면 기본적으로 로컬 컴퓨터에서 명령이 실행 됩니다. 이 매개 변수는 모든 파일 및 명령에 지정 된 폴더에 적용 됩니다. |
| /u`[<domain>\]<username>` | 지정 된 사용자 계정의 사용 권한을 사용 하 여 명령을 실행 합니다. **/U** 옵션을 사용 하지 않으면 기본적으로 시스템 권한이 사용 됩니다. |
| /p`[<password>]` | 에 지정 된 사용자 계정의 암호를 지정 된 **/u** 옵션입니다. **/P** 옵션을 사용 하지 않으면 명령이 실행 될 때 암호 프롬프트가 표시 됩니다. |
| 더불어`<openfileID>` | 지정 된 파일 ID가 열려 있는 파일의 연결을 끊습니다. 이 매개 변수와 함께 와일드 카드 문자 (**&#42;**)를 사용할 수 있습니다.<p>참고: 사용할 수는 **openfiles /query** 파일 ID를 찾으려면 명령을 |
| 없음을`<accessedby>` | *Accessedby* 매개 변수에 지정 된 사용자 이름과 관련 된 열려 있는 모든 파일의 연결을 끊습니다. 이 매개 변수와 함께 와일드 카드 문자 (**&#42;**)를 사용할 수 있습니다. |
| /o`{read | write | read/write}` | 지정 된 열려 있는 모드 값을 사용 하 여 열려 있는 모든 파일의 연결을 끊습니다. 유효한 값은 **읽기**, **쓰기**또는 **읽기/쓰기**입니다. 이 매개 변수와 함께 와일드 카드 문자 (**&#42;**)를 사용할 수 있습니다. |
| /op`<openfile>` | 열려 있는 특정 파일 이름으로 만들어진 모든 열려 있는 파일 연결을 끊습니다. 이 매개 변수와 함께 와일드 카드 문자 (**&#42;**)를 사용할 수 있습니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예제

*파일 ID가 26843578*인 열려 있는 모든 파일의 연결을 끊으려면 다음을 입력 합니다.

```
openfiles /disconnect /id 26843578
```

사용자 *hiropln*에서 액세스 하는 열려 있는 모든 파일 및 디렉터리의 연결을 끊으려면 다음을 입력 합니다.

```
openfiles /disconnect /a hiropln
```

*읽기/쓰기 모드*를 사용 하 여 열려 있는 모든 파일과 디렉터리의 연결을 끊으려면 다음을 입력 합니다.

```
openfiles /disconnect /o read/write
```

파일에 액세스 하는 사용자에 관계 없이 열린 파일 이름 * C:\testshare을 사용 하 여 디렉터리의 연결을 끊으려면 \* 다음을 입력 합니다.

```
openfiles /disconnect /a * /op c:\testshare\
```

사용자 *hiropln*가 액세스 하는 원격 컴퓨터 *srvmain* 에서 열려 있는 모든 파일의 연결을 끊으려면 다음을 입력 합니다.

```
openfiles /disconnect /s srvmain /u maindom\hiropln /id *
```

## <a name="openfiles-query"></a>openfiles/쿼리

쿼리하고 열려 있는 모든 파일을 표시 합니다.

### <a name="syntax"></a>구문

```
openfiles /query [/s <system> [/u [<domain>\]<username> [/p [<password>]]]] [/fo {TABLE | LIST | CSV}] [/nh] [/v]
```

#### <a name="parameters"></a>매개 변수


| 매개 변수 | 설명 |
|--|--|
| /s`<system>` | 원격 시스템에 연결 (이름 또는 IP 주소)을 지정 합니다. 백슬래시를 사용 하지 마십시오. **/S** 옵션을 사용 하지 않으면 기본적으로 로컬 컴퓨터에서 명령이 실행 됩니다. 이 매개 변수는 모든 파일 및 명령에 지정 된 폴더에 적용 됩니다. |
| /u`[<domain>\]<username>` | 지정 된 사용자 계정의 사용 권한을 사용 하 여 명령을 실행 합니다. **/U** 옵션을 사용 하지 않으면 기본적으로 시스템 권한이 사용 됩니다. |
| /p`[<password>]` | 에 지정 된 사용자 계정의 암호를 지정 된 **/u** 옵션입니다. **/P** 옵션을 사용 하지 않으면 명령이 실행 될 때 암호 프롬프트가 표시 됩니다. |
| [/fo `{TABLE | LIST | CSV}` ] | 지정된 된 형식으로 출력을 표시합니다. 유효한 값은 다음과 같습니다.<ul><li>**테이블** -테이블에 출력을 표시 합니다.</li><li>**List** -목록에 출력을 표시 합니다.</li><li>**Csv** -Csv (쉼표로 구분 된 값) 형식으로 출력을 표시 합니다.</li></ul> |
| /nh | 출력에서 열 머리글을 표시 하지 않습니다. 경우에만 유효는 **/fo** 매개 변수는 설정 **테이블** 또는 **CSV**합니다. |
| /v | 세부 정보 (자세한 정보 표시)를 출력에 표시 하도록 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예제

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

*Maindom* 도메인에서 사용자 *hiropln* 에 대 한 자격 증명을 사용 하 여 원격 시스템 *srvmain* 에서 열려 있는 모든 파일을 쿼리하고 표시 하려면 다음을 입력 합니다.

```
openfiles /query /s srvmain /u maindom\hiropln /p p@ssW23
```

> [!NOTE]
> 이 예제에서는 암호를 명령줄에 제공 합니다. 암호 표시를 방지 하려면 생략 된 **/p** 옵션입니다. 화면에 에코 되지 않는 암호를 입력 하 라는 메시지가 표시 됩니다.

## <a name="openfiles-local"></a>openfiles /local

시스템 **유지 관리 개체 목록** 전역 플래그를 사용 하거나 사용 하지 않도록 설정 합니다. 매개 변수 없이 사용 하는 경우 **openfiles/local** 는 **개체 목록 유지 관리** 전역 플래그의 현재 상태를 표시 합니다.

> [!NOTE]
> **설정** 또는 **해제** 옵션을 사용 하 여 변경한 내용은 시스템을 다시 시작할 때까지 적용 되지 않습니다. **개체 목록 유지 관리** 전역 플래그를 사용 하도록 설정 하면 시스템의 속도가 느려질 수 있습니다.

### <a name="syntax"></a>구문

```
openfiles /local [on | off]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| `[on | off]` | 로컬 파일 핸들을 추적 하는 시스템 **유지 관리 개체 목록** 전역 플래그를 사용 하거나 사용 하지 않도록 설정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예제

**개체 목록 유지 관리** 전역 플래그의 현재 상태를 확인 하려면 다음을 입력 합니다.

```
openfiles /local
```

기본적으로 **개체 목록 유지 관리** 전역 플래그는 사용 하지 않도록 설정 되 고 다음과 같은 메시지가 나타납니다.`INFO: The system global flag 'maintain objects list' is currently disabled.`

**개체 목록 유지 관리** 전역 플래그를 사용 하려면 다음을 입력 합니다.

```
openfiles /local on
```

전역 플래그를 사용 하는 경우 다음과 같은 메시지가 나타납니다.`SUCCESS: The system global flag 'maintain objects list' is enabled. This will take effect after the system is restarted.`

**개체 목록 유지 관리** 전역 플래그를 사용 하지 않도록 설정 하려면 다음을 입력 합니다.

```
openfiles /local off
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
