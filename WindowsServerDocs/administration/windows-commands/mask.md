---
title: 마스크
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 816bcd932091b33ed897add5a13603e3a1eea925
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724013"
---
# <a name="mask"></a>마스크



제거를 사용 하 여 가져온 하드웨어 섀도 복사본은 **가져올** 명령입니다.



## <a name="syntax"></a>구문

```
mask <ShadowSetID>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|ShadowSetID|제거 섀도 복사본에 지정 된 섀도 복사본 세트 ID에 속하는|

## <a name="remarks"></a>설명

-   기존 별칭 또는 환경 변수 대신 사용할 수 있습니다 *ShadowSetID*합니다. 사용 하 여 **추가** 매개 변수 없이 기존 별칭을 참조 하십시오.

## <a name="examples"></a>예

가져온 섀도 복사본% Import_1%를 제거 하려면 다음을 입력 합니다.
```
mask %Import_1%
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)