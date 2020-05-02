---
title: convert basic
description: 빈 동적 디스크를 기본 디스크로 변환 하는 convert 기본 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 61329896-3b56-4959-8d58-45cbe18ba860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e44ecc9f5d18bbe426c63f8854e7c3347f418bb2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720789"
---
# <a name="convert-basic"></a>convert basic

빈 동적 디스크를 기본 디스크로 변환합니다. 이 작업이 성공 하기 위해 동적 디스크를 선택 해야 합니다. [디스크 선택 명령을](select-disk.md) 사용 하 여 동적 디스크를 선택 하 고 포커스를 이동 합니다.

> [!IMPORTANT]
> 디스크를 기본 디스크로 변환 하려면 비어 있어야 합니다. 데이터를 백업 하 고 디스크를 변환 하기 전에 모든 파티션 또는 볼륨을 삭제 합니다.

> [!NOTE]
> 이 명령을 사용 하는 방법에 대 한 지침은 [동적 디스크를 기본 디스크로 다시 변경](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755238(v=ws.11))을 참조 하세요.

## <a name="syntax"></a>구문

```
convert basic [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="examples"></a>예

기본으로 선택된 된 동적 디스크 변환 하려면 다음을 입력 합니다.

```
convert basic
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [convert 명령](convert.md)
