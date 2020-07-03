---
title: md
description: 디렉터리 또는 하위 디렉터리를 만드는 md 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 82162d00-cc34-4776-9e55-4b4836dbd6a9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e7d5dac14572bfe53f92333cddcdc68bfa0aab1a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922094"
---
# <a name="md"></a>md

디렉터리 또는 하위 디렉터리를 만듭니다. 기본적으로 사용 하도록 설정 된 명령 확장을 사용 하면 단일을 사용할 수 있도록 **md** 지정된 된 경로에서 중간 디렉터리를 만드는 명령입니다.

> [!NOTE]
> 이 명령은 [mkdir 명령과](mkdir.md)동일 합니다.

## <a name="syntax"></a>구문

```
md [<drive>:]<path>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<drive>`: | 새 디렉터리를 만들고 원하는 드라이브를 지정 합니다. |
| `<path>` | 새 디렉터리의 위치와 이름을 지정합니다. 단일 경로의 최대 길이 파일 시스템에 의해 결정 됩니다. 필수 매개 변수입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

현재 디렉터리 내에 *Directory1* 라는 디렉터리를 만들려면 다음을 입력 합니다.

```
md Directory1
```

명령 확장을 사용 하도록 설정 하 여 루트 디렉터리 내에 *Taxes\Property\Current* 디렉터리 트리를 만들려면 다음을 입력 합니다.

```
md \Taxes\Property\Current
```

이전 예제와 같이 루트 디렉터리 내에 *Taxes\Property\Current* 디렉터리 트리를 만들 수 있지만 명령 확장을 사용 하지 않도록 설정 하려면 다음 명령 시퀀스를 입력 합니다.

```
md \Taxes
md \Taxes\Property
md \Taxes\Property\Current
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [mkdir 명령](mkdir.md)