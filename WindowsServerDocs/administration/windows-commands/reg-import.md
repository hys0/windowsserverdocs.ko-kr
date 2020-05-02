---
title: reg 가져오기
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0be103de-08fc-4f02-b590-361782680b3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e7e033091752f97086fd27fcb94e62469f0cced
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722548"
---
# <a name="reg-import"></a>reg 가져오기



포함 된 파일의 내용을 복사 하는 로컬 컴퓨터의 레지스트리로 레지스트리 하위 키, 항목 및 값을 내보냅니다.



## <a name="syntax"></a>구문

```
Reg import FileName
```

### <a name="parameters"></a>매개 변수

|매개 변수|Description|
|---------|-----------|
|\<파일 이름>|로컬 컴퓨터의 레지스트리로 복사 되는 콘텐츠를 포함 하는 파일의 경로 이름을 지정 합니다. 이 파일을 사용 하 여 사전에 만들 수 있어야 **reg 내보내기**합니다.|
|/?|에 대 한 도움말을 표시 **reg 가져오기** 명령 프롬프트입니다.|

## <a name="remarks"></a>설명

다음 표에 대 한 반환 값은 **reg 가져오기** 작업 합니다.

|값|설명|
|-----|-----------|
|0|Success|
|1|실패|

## <a name="examples"></a>예

레지스트리 항목에서 AppBkUp.reg 라는 파일을 가져오려면 다음을 입력 합니다.
```
reg import AppBkUp.reg
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)