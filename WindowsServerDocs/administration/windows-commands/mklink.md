---
title: mklink
description: 디렉터리 또는 파일 기호화 된 링크나 하드 링크를 만드는 mklink 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cb8339f7dcb2f397d6b90105e2ccd9bdc8cc07a5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928537"
---
# <a name="mklink"></a>mklink

디렉터리 또는 파일 기호화 된 또는 하드 링크를 만듭니다.

## <a name="syntax"></a>구문

```
mklink [[/d] | [/h] | [/j]] <link> <target>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /d | 디렉터리 기호화 된 링크를 만듭니다. 기본적으로이 명령은 파일 기호화 된 링크를 만듭니다. |
| /h | 대신 바로 가기 링크를 하드 링크를 만듭니다. |
| /j | 디렉터리 연결을 만듭니다. |
| `<link>` | 만들려는 기호화 된 링크의 이름을 지정 합니다. |
| `<target>` | 새 바로 가기 링크를 참조 하는 경로 (상대 또는 절대)를 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

루트 디렉터리에서 \Users\User1\Documents 디렉터리에 있는 MyFolder 및 Myfile 이라는 기호화 된 링크를 만들고 제거 하려면 다음을 입력 합니다.

```
mklink /d \MyFolder \Users\User1\Documents
mklink /h \MyFile.file \User1\Documents\example.file
rd \MyFolder
del \MyFile.file
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [del 명령](del.md)

- [rd 명령](rd.md)

- [Windows PowerShell의 새 항목](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
