---
title: 편집
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4e0ff2e8-3518-47c1-8c69-5e93f895fa0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c77941d39118554b6b59e436e63d67a4a1f7c8cb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720858"
---
# <a name="edit"></a>편집



만들고 ASCII 텍스트 파일을 변경 하는 MS-DOS 편집기를 시작 합니다.



## <a name="syntax"></a>구문

```
edit [/b] [/h] [/r] [/s] [/<NNN>] [[<Drive>:][<Path>]<FileName> [<FileName2> [...]]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[\<드라이브>:] [<Path>]<FileName> [<FileName2> [...]]|하나 이상의 ASCII 텍스트 파일의 이름과 위치를 지정합니다. 파일이 없으면 MS-DOS 편집기를 만듭니다. 파일이 있으면 MS-DOS 것 열리고 해당 내용을 화면에 표시 됩니다. *파일 이름* 에는 와일드 카드 문자 (**&#42;** 및 **?**)를 사용할 수 있습니다. 여러 파일 이름을 공백으로 구분 합니다.|
|/b|강제로 흑백 모드 흑백으로 해당 MS-DOS 편집기를 표시 합니다.|
|/h|현재 모니터에 대 한 줄의 가능한 최대 수를 표시합니다.|
|/r|읽기 전용 모드에서 파일을 로드합니다.|
|/s|짧은 파일 이름 사용 하도록 강제 합니다.|
|\<NNN>|줄을 배치 하는 이진 파일을 로드 *NNN* 문자 너비입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   자세한 도움말을 보려면 MS-DOS 편집기를 열고 F1 키를 누릅니다.
-   일부 모니터는 기본적으로 바로 가기 키의 표시를 지원 하지 않습니다. 모니터가 바로 가기 키를 표시 하지 않는 경우 사용 하 여 **/b**합니다.

## <a name="examples"></a>예

MS-DOS 편집기를 열려면 다음을 입력 합니다.
```
edit
```
을 만들고 현재 디렉터리에 newtextfile.txt 라는 파일을 편집 하려면 다음을 입력 합니다.
```
edit newtextfile.txt
```