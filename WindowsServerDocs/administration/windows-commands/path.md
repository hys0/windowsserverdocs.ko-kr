---
title: 경로
description: PATH 환경 변수에서 명령 경로를 설정 하는 방법에 대 한 참조 항목으로, 실행 파일 (.exe)을 검색 하는 데 사용 되는 디렉터리 집합을 지정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1bfa1349-e79a-472b-a9e6-d7a91149ae8f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6fadeb2108f0e59ee2f45f3cf45338046a345006
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472569"
---
# <a name="path"></a>경로

PATH 환경 변수에서 명령 경로를 설정 하 여 실행 파일 (.exe)을 검색 하는 데 사용 되는 디렉터리 집합을 지정 합니다. 매개 변수 없이 사용 하는 경우이 명령은 현재 명령 경로를 표시 합니다.

## <a name="syntax"></a>구문

```
path [[<drive>:]<path>[;...][;%PATH%]]
path ;
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| `[<drive>:]<path>` | 드라이브와 명령 경로에 설정 하는 디렉터리를 지정 합니다. 현재 디렉터리를 명령 경로에 지정 된 디렉터리 하기 전에 항상 검색 됩니다. |
| ; | 명령 경로에서 디렉터리를 구분 합니다. 다른 매개 변수 없이 사용 하는 경우 **;** 기존 명령 경로 PATH 환경 변수를 지우고 Cmd.exe 현재 디렉터리 에서만에서 검색 하도록 지시 합니다. |
| `%PATH%` | PATH 환경 변수에 나열 된 디렉터리의 기존 집합에 명령 경로 추가 합니다. 이 매개 변수를 포함 하는 경우 Cmd.exe은 PATH 환경 변수에 있는 명령 경로 값으로 대체 하 여 명령 프롬프트에서 이러한 값을 수동으로 입력 하지 않아도 됩니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="remarks"></a>설명


- Windows 운영 체제는 기본 파일 이름 확장명을 사용 하 여 다음과 같은 우선 순위를 갖습니다. .exe, .com, .bat 및 .cmd로 검색 합니다. 즉, acct.bat 이라는 배치 파일을 찾고 있지만 동일한 디렉터리에 acct.exe 라는 응용 프로그램이 있는 경우 명령 프롬프트에 .bat 확장명을 포함 해야 합니다.

- 명령 경로에 있는 둘 이상의 파일에 동일한 파일 이름과 확장명이 있는 경우이 명령은 먼저 현재 디렉터리에서 지정 된 파일 이름을 검색 합니다. 그런 다음 PATH 환경 변수에 나열 된 순서 대로 명령 경로의 디렉터리를 검색 합니다.

- 배치 하는 경우는 **경로** Windows 운영 체제는 자동으로 지정된 된 MS-DOS 하위 시스템 검색 경로 추가 컴퓨터에 로그온 할 때마다 Autoexec.nt 파일에 명령 합니다. Cmd.exe는 Autoexec.nt 파일을 사용 하지 않습니다. 바로 가기에서 시작할 때 Cmd.exe 내 컴퓨터/속성/고급/환경에 설정 된 환경 변수를 상속 합니다.

## <a name="examples"></a>예제

외부 명령에 대 한 *c:\user\taxes*, *b:\user\invest*및 *b:\bin* 경로를 검색 하려면 다음을 입력 합니다.

```
path c:\user\taxes;b:\user\invest;b:\bin
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
