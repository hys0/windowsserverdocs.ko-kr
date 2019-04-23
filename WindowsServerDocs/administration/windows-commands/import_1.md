---
title: 가져오기
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b9d2751-7637-4738-83b0-8c578eb28f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 379d5923a9355db2965b56c27cedd207b1b63006
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885994"
---
# <a name="import"></a>가져오기



로컬 컴퓨터의 디스크 그룹에 외부 디스크 그룹을 가져옵니다.

## <a name="syntax"></a>구문

```
import [noerr]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|noerr|만 스크립팅 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|

## <a name="remarks"></a>설명

-   Import 명령 포커스가 있는 디스크와 동일한 그룹에 있는 모든 디스크를 가져옵니다.
-   이 작업이 성공 하기 위해 외부 디스크 그룹에서 동적 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="BKMK_examples"></a>예제

로컬 컴퓨터의 디스크 그룹에 포커스가 있는 디스크와 같은 디스크 그룹에 있는 모든 디스크를 가져오려면 다음을 입력 합니다.
```
import
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

