---
title: title
description: 제목에 대 한 참조 문서로, 명령 프롬프트 창의 제목을 만듭니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0bbe8bd-201a-4b6c-b617-5d9809881dc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 732a0de30b9495e6281248120d2a90f85734ad8b
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930066"
---
# <a name="title"></a>title

명령 프롬프트 창에 대 한 제목을 만듭니다.



## <a name="syntax"></a>구문

```
title [<String>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<String>|명령 프롬프트 창의 제목을 지정합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   창 제목 배치 프로그램을 만들려는 포함는 **제목** 일괄 프로그램의 시작 부분에 명령 합니다.
-   창 제목, 설정한 후만 사용 하 여 재설정할 수 있습니다는 **제목** 명령입니다.

## <a name="examples"></a>예

다음 샘플 스크립트에서는 배치 파일이 **복사** 명령을 실행 하는 동안 명령 프롬프트 창의 제목이 파일 업데이트로 변경 됩니다. 명령이 실행 된 후 텍스트가 `Files Updated` 표시 되 고 명령 프롬프트 창의 제목이 명령 프롬프트로 다시 변경 됩니다.
```
@echo off
title Updating Files
copy \\server\share\*.xls c:\users\common\*.xls
echo Files Updated.
title Command Prompt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)