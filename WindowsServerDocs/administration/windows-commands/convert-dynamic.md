---
title: 동적 변환
description: 기본 디스크를 동적 디스크로 변환 하는 동적 변환에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7b8fa4b1-850f-4e48-b05f-871c883ea33c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ad84cf2ecb6808b68110187b52f3fc13590b491
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847326"
---
# <a name="convert-dynamic"></a>동적 변환

기본 디스크를 동적 디스크로 변환합니다.

이 명령을 사용 하는 방법에 대 한 지침은 [기본 디스크를 동적 디스크로 변경](https://go.microsoft.com/fwlink/?LinkId=207047) (https://go.microsoft.com/fwlink/?LinkId=207047)을 참조 하세요.

## <a name="syntax"></a>구문

```
convert dynamic [noerr]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|noerr|스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|

## <a name="remarks"></a>주의

-   기본 디스크의 모든 기존 파티션은 단순 볼륨 사용 하는 것입니다.
-   이 작업을 수행 하려면 기본 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 기본 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

기본 디스크를 동적 디스크로 변환 하려면 다음을 입력 합니다.
```
convert dynamic
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

