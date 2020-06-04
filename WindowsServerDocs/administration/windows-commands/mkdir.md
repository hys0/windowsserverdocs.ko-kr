---
title: mkdir
description: 디렉터리 또는 하위 디렉터리를 만드는 mkdir 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 033a57a2-5deb-4c98-aa78-61ce8df2a330
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 921e369cb1550bca8e26cc0beada4c1f5c1c3d5b
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354603"
---
# <a name="mkdir"></a>mkdir

디렉터리 또는 하위 디렉터리를 만듭니다. 기본적으로 사용 하도록 설정 된 명령 확장을 사용 하면 단일 **mkdir** 명령을 사용 하 여 지정 된 경로에 중간 디렉터리를 만들 수 있습니다.

> [!NOTE]
> 이 명령은 [md 명령과](md.md)동일 합니다.

## <a name="syntax"></a>구문

```
mkdir [<drive>:]<path>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| `<drive>`: | 새 디렉터리를 만들고 원하는 드라이브를 지정 합니다. |
| `<path>` | 새 디렉터리의 위치와 이름을 지정합니다. 단일 경로의 최대 길이 파일 시스템에 의해 결정 됩니다. 필수 매개 변수입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

현재 디렉터리 내에 *Directory1* 라는 디렉터리를 만들려면 다음을 입력 합니다.

```
mkdir Directory1
```

명령 확장을 사용 하도록 설정 하 여 루트 디렉터리 내에 *Taxes\Property\Current* 디렉터리 트리를 만들려면 다음을 입력 합니다.

```
mkdir \Taxes\Property\Current
```

이전 예제와 같이 루트 디렉터리 내에 *Taxes\Property\Current* 디렉터리 트리를 만들 수 있지만 명령 확장을 사용 하지 않도록 설정 하려면 다음 명령 시퀀스를 입력 합니다.

```
mkdir \Taxes
mkdir \Taxes\Property
mkdir \Taxes\Property\Current
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [md 명령](md.md)