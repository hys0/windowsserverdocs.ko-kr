---
title: convert dynamic
description: 기본 디스크를 동적 디스크로 변환 하는 convert 동적 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7b8fa4b1-850f-4e48-b05f-871c883ea33c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3474da8c1f4a3e58d9e77c36abe4390ec2f5b731
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928971"
---
# <a name="convert-dynamic"></a>convert dynamic

기본 디스크를 동적 디스크로 변환합니다. 이 작업을 수행 하려면 기본 디스크를 선택 해야 합니다. [디스크 선택 명령을](select-disk.md) 사용 하 여 기본 디스크를 선택 하 고 포커스를 이동 합니다.

> [!NOTE]
> 이 명령을 사용 하는 방법에 대 한 지침은 [동적 디스크를 기본 디스크로 다시 변경](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755238(v=ws.11))을 참조 하세요.

## <a name="syntax"></a>구문

```
convert dynamic [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

#### <a name="remarks"></a>설명

- 기본 디스크의 모든 기존 파티션은 단순 볼륨 사용 하는 것입니다.

## <a name="examples"></a>예

기본 디스크를 동적 디스크로 변환 하려면 다음을 입력 합니다.

```
convert dynamic
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [convert 명령](convert.md)
