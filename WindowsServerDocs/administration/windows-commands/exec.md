---
title: 재시도
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 514503e4920e16ba6778185af32f925541805223
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377427"
---
# <a name="exec"></a>재시도



로컬 컴퓨터에서 파일을 실행합니다. 파일 일 수는 **cmd** 스크립트입니다.

## <a name="syntax"></a>구문

```
exec <ScriptFile.cmd>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-0ScriptFile > @no__t|실행할 스크립트 파일을 지정 합니다.|

## <a name="remarks"></a>설명

-   이 명령은 중복 또는 백업의 일부로 데이터를 복원 하거나 복원 시퀀스에 사용 됩니다.
-   스크립트가 실패할 경우 오류가 반환 되 고 DiskShadow 종료 됩니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)