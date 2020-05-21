---
title: forfiles
description: 파일이 나 파일 집합에 대 한 명령을 선택 하 고 실행 하는 하위 폴더 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 43f6b004-446d-4fdd-91c5-5653613524a4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/20/2020
ms.openlocfilehash: 96ef7d016bd13961a4814ba4cd09095aed4f0e97
ms.sourcegitcommit: 29f7a4811b4d36d60b8b7c55ce57d4ee7d52e263
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83716848"
---
# <a name="forfiles"></a>forfiles

파일이 나 파일 집합에 대 한 명령을 선택 하 고 실행 합니다. 이 명령은 배치 파일에서 가장 일반적으로 사용 됩니다.

## <a name="syntax"></a>구문

```
forfiles [/P pathname] [/M searchmask] [/S] [/C command] [/D [+ | -] [{<date> | <days>}]]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /P`<pathname>` | 검색을 시작 하는 경로 지정 합니다. 기본적으로 현재 작업 디렉터리에서 시작 검색 합니다. |
| 연속`<searchmask>` | 지정 된 검색 마스크에 따라 파일을 검색합니다. 기본 searchmask은 `*` 입니다. |
| /S | 하위 디렉터리를 재귀적으로 검색 하도록 **하위 폴더** 명령을 지시 합니다. |
| /C`<command>` | 각 파일에 지정된 된 명령을 실행합니다. 명령 문자열은 큰따옴표로 묶어야 합니다. 기본 명령은 `"cmd /c echo @file"` 입니다. |
| D`[{+\|-}][{<date> | <days>}]` | 지정 된 시간 프레임 내에 마지막으로 수정한 날짜를 사용 하 여 파일을 선택 합니다.<ul><li>마지막으로 수정한 날짜 보다 이후 또는 같음 () **+** 또는 이전 또는 같음 () 지정 된 날짜로 파일을 선택 **-** 합니다. 여기서 *날짜* 는 MM/DD/YYYY 형식입니다.</li><li>마지막으로 수정한 날짜 보다 이후 또는 같음 ( **+** ) 현재 날짜에 지정 된 일 수를 더한 날짜를 선택 하거나, **-** 현재 날짜에서 지정 된 일 수를 뺀 값 ()을 사용 하 여 파일을 선택 합니다.</li><li>유효한 *날짜* 값에는 0 – 32768 범위의 숫자가 포함 됩니다. 부호가 지정 되지 않은 경우 **+** 기본적으로가 사용 됩니다.</li></ul> |
| /? | Cmd 창에 도움말 텍스트를 표시 합니다. |

#### <a name="remarks"></a>설명

- `forfiles /S`명령은와 비슷합니다 `dir /S` .

- 명령 문자열에서 다음 변수를 사용 하 여 **/c** 명령줄 옵션으로 지정할 수 있습니다.

    | 변수 | Description |
    | -------- | ----------- |
    | @FILE | 파일 이름. |
    | @FNAME | 확장명 없이 파일 이름입니다. |
    | @EXT | 파일 이름 확장명입니다. |
    | @PATH | 파일의 전체 경로입니다. |
    | @RELPATH | 파일의 상대 경로입니다. |
    | @ISDIR | 파일 형식을 디렉터리 이면 TRUE로 평가 합니다. 그렇지 않은 경우이 변수를 FALSE로 평가합니다. |
    | @FSIZE | 파일 크기 (바이트)에서입니다. |
    | @FDATE | 파일에 마지막으로 수정한 날짜 스탬프입니다. |
    | @FTIME | 파일의 마지막 수정된 타임 스탬프입니다. |

- **하위 폴더** 명령을 사용 하 여 명령을 실행 하거나 여러 파일에 인수를 전달할 수 있습니다. 예를 들어, 실행할 수는 **형식** .txt 파일 이름 확장명을 사용 하 여 트리의 모든 파일에서 명령입니다. 또는 파일 이름 Myinput을 첫 번째 인수로 사용 하 여 C 드라이브에서 모든 배치 파일 (* .bat)을 실행할 수 있습니다.

- 이 명령은 다음 작업을 수행할 수 있습니다.

    - 파일을 사용 하 여 절대 날짜 또는 상대 날짜 선택은 **/d** 매개 변수입니다.

    - 및와 같은 변수를 사용 하 여 파일의 보관 트리를 빌드합니다 @FSIZE @FDATE .

    - 변수를 사용 하 여 디렉터리와 파일을 구분 @ISDIR 합니다.

    - 문자, 0 x에 대 한 16 진수 코드를 사용 하 여 명령줄에 특수 문자를 포함*HH* 형식 (예: 탭에는 0x09).

- 이 명령은 `recurse subdirectories` 단일 파일만 처리 하도록 설계 된 도구에서 플래그를 구현 하는 방식으로 작동 합니다.

### <a name="examples"></a>예

C 드라이브에 배치 파일의 모든를 나열 하려면 다음을 입력 합니다.

```
forfiles /P c:\ /S /M *.bat /C "cmd /c echo @file is a batch file"
```

C 드라이브에 있는 디렉터리를 나열 하려면 다음을 입력 합니다.

```
forfiles /P c:\ /S /M *.* /C "cmd /c if @isdir==TRUE echo @file is a directory"
```

현재 디렉터리에 있는 파일을 적어도 1 년 전의 모든를 나열 하려면 다음을 입력 합니다.

```
forfiles /S /M *.* /D -365 /C "cmd /c echo @file is at least one year old."
```

2007 년 1 월 1 일 보다 오래 된 현재 디렉터리에 있는 각 파일에 대해 텍스트 *파일* 의 기한이 오래 된 경우 다음을 입력 합니다.

```
forfiles /S /M *.* /D -01/01/2007 /C "cmd /c echo @file is outdated."
```

열 형식으로 현재 디렉터리에 있는 모든 파일의 파일 이름 확장명을 나열 하 고 확장명 앞에 탭 추가 하려면 다음을 입력 합니다.

```
forfiles /S /M *.* /C "cmd /c echo The extension of @file is 0x09@ext"
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
