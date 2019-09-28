---
title: convert basic
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61329896-3b56-4959-8d58-45cbe18ba860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4b81126f4a623d841bb5868f786678d7b093581
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379135"
---
# <a name="convert-basic"></a>convert basic



빈 동적 디스크를 기본 디스크로 변환합니다.

이 명령을 사용 하는 방법에 대 한 지침은 [동적 디스크를 기본 디스크로 다시 변경](https://go.microsoft.com/fwlink/?LinkId=207048) (https://go.microsoft.com/fwlink/?LinkId=207048) 을 참조 하세요.

## <a name="syntax"></a>구문

```
convert basic [noerr]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|noerr|스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|

## <a name="remarks"></a>설명

> [!IMPORTANT]
> 디스크를 기본 디스크로 변환 하려면 비어 있어야 합니다. 데이터를 백업 하 고 디스크를 변환 하기 전에 모든 파티션 또는 볼륨을 삭제 합니다.
> -   이 작업이 성공 하기 위해 동적 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 동적 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="BKMK_examples"></a>예와

기본으로 선택된 된 동적 디스크 변환 하려면 다음을 입력 합니다.
```
convert basic
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

