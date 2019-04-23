---
title: exec
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: ecdfd05b8abefb35946b783daaa3220a6713a38d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882924"
---
# <a name="exec"></a>exec



로컬 컴퓨터에서 파일을 실행합니다. 파일 일 수는 **cmd** 스크립트입니다.

## <a name="syntax"></a>구문

```
exec <ScriptFile.cmd>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<ScriptFile.cmd>|실행할 스크립트 파일을 지정 합니다.|

## <a name="remarks"></a>설명

-   이 명령은 중복 또는 백업의 일부로 데이터를 복원 하거나 복원 시퀀스에 사용 됩니다.
-   스크립트가 실패할 경우 오류가 반환 되 고 DiskShadow 종료 됩니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)