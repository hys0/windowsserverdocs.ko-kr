---
title: exec
description: 로컬 컴퓨터에서 스크립트 파일을 실행 하는 exec 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 956f3d4a7c5992980aea0fc0f5933ee7def48381
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436109"
---
# <a name="exec"></a>exec

로컬 컴퓨터에서 스크립트 파일을 실행 합니다. 또한이 명령은 백업 또는 복원 시퀀스의 일부로 데이터를 복제 하거나 복원 합니다. 스크립트가 실패할 경우 오류가 반환 되 고 DiskShadow 종료 됩니다.

파일 일 수는 **cmd** 스크립트입니다.

## <a name="syntax"></a>구문

```
exec <scriptfile.cmd>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<scriptfile.cmd>` | 실행할 스크립트 파일을 지정 합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [diskshadow 명령](diskshadow.md)
