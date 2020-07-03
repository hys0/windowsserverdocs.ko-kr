---
title: recover
description: 불량 하거나 결함이 있는 디스크에서 읽을 수 있는 정보를 복구 하는 복구 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cf9be2e3-90c8-4773-a201-dc503b91948e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ab7f502b046bf30a40b1fdd386c7faddc5c8f15a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931934"
---
# <a name="recover"></a>recover

잘못 된 이거나 결함이 있는 디스크에서 읽을 수 있는 정보를 복구합니다. 이 명령은 섹터 단위로 파일을 읽고 양호한 섹터에서 데이터를 복구 합니다. 불량 섹터의 데이터가 손실 됩니다. 불량 섹터의 모든 데이터가 손실 되는 파일을 복구 하는 경우 한 번에 하나의 파일을 복구할 해야 있습니다.

디스크를 작업에 사용할 준비가 되 면 **chkdsk** 명령에 의해 보고 된 불량 섹터가 잘못 된 것으로 표시 되었습니다. 위험 하지, 및 **복구** 에 영향을 주지 않습니다.

## <a name="syntax"></a>구문

```
recover [<drive>:][<path>]<filename>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| `[<drive>:][<path>]<filename>` | 복구 하려는 파일 이름 및 파일의 위치 (현재 디렉터리에 없는 경우)를 지정 합니다. *Filename* 은 필수 이며 와일드 카드는 지원 되지 않습니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

D 드라이브의 *\fiction* 디렉터리에 있는 파일 *story.txt* 를 복구 하려면 다음을 입력 합니다.

```
recover d:\fiction\story.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
