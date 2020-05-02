---
title: 오프 라인 볼륨
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b8f7192f-ea38-47d0-9d4e-58ef68336ae6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d17295f3367fed054a7f6a245bae44ea3494a4a8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723457"
---
# <a name="offline-volume"></a>오프 라인 볼륨



포커스가 있는 온라인 볼륨을 오프 라인 상태로 이동합니다.

> [!IMPORTANT]
> 이 DiskPart 명령을 Windows Vista의 모든 버전에서 사용할 수 없는 경우

## <a name="syntax"></a>구문

```
offline volume [noerr]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|noerr|스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|

## <a name="remarks"></a>설명

-   이것이 성공 하려면 볼륨을 선택 해야 합니다. 사용 하 여는 **볼륨 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="examples"></a>예

포커스가 있는 디스크를 오프 라인으로 다음을 입력 합니다.
```
offline volume
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

