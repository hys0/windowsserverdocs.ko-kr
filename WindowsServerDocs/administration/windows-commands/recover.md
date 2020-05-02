---
title: recover
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cf9be2e3-90c8-4773-a201-dc503b91948e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b316ed26f008a62f88aaeb4a7a7f3030d08f1588
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722621"
---
# <a name="recover"></a>recover



잘못 된 이거나 결함이 있는 디스크에서 읽을 수 있는 정보를 복구합니다.



## <a name="syntax"></a>구문

```
recover [<Drive>:][<Path>]<FileName>
```

### <a name="parameters"></a>매개 변수

|           매개 변수           |                                          설명                                          |
|-------------------------------|-----------------------------------------------------------------------------------------------|
| [\<드라이브>:] [<Path>]<FileName> | 복구 하려는 파일의 이름과 위치를 지정 합니다. *FileName* 가 필요 합니다. |
|              /?               |                             명령 프롬프트에 도움말을 표시합니다.                              |

## <a name="remarks"></a>설명

-   **복구** 명령 파일을 섹터 단위로 읽고 좋은 섹터에서 데이터를 복구 합니다. 불량 섹터의 데이터가 손실 됩니다.
-   디스크를 작업에 사용할 준비가 되 면 **chkdsk** 에서 보고 한 불량 섹터가 잘못 된 것으로 표시 되었습니다. 위험 하지, 및 **복구** 에 영향을 주지 않습니다.
-   불량 섹터의 모든 데이터가 손실 되는 파일을 복구 하는 경우 한 번에 하나의 파일을 복구할 해야 있습니다.
-   **복구** 명령에는 와일드 카드 문자 (**&#42;** 및 **?**)를 사용할 수 없습니다. 파일 (및 현재 디렉터리에 없는 경우 파일의 위치)를 지정 해야 합니다.

## <a name="examples"></a>예

D 드라이브 \Fiction 디렉터리에 Story.txt 파일을 복구 하려면 다음을 입력 합니다.
```
recover d:\fiction\story.txt 
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)