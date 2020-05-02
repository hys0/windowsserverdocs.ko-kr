---
title: mklink
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 83a607711f0abe51810aa5abf4eb731206d810c2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723972"
---
# <a name="mklink"></a>mklink
기호화 된 링크를 만듭니다.



## <a name="syntax"></a>구문

```
mklink [[/d] | [/h] | [/j]] <Link> <Target>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/d|디렉터리 기호화 된 링크를 만듭니다. 기본적으로 **mklink** 파일 바로 가기 링크를 만듭니다.|
|/h|대신 바로 가기 링크를 하드 링크를 만듭니다.|
|/j|디렉터리 연결을 만듭니다.|
|\<링크>|생성 중인 기호화 된 링크의 이름을 지정 합니다.|
|\<Target>|새 바로 가기 링크를 참조 하는 경로 (상대 또는 절대)를 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="examples"></a>예

루트 디렉터리에서 \Users\User1\Documents 디렉터리에 있는 MyFolder 및 MyFile 이라는 기호화 된 링크를 만들고 제거 하는 방법을 보여 주고 디렉터리 내에 있습니다.
```
mklink /d \MyFolder \Users\User1\Documents
mklink /h \MyFile.file \User1\Documents\example.file
rd \MyFolder
del \MyFile.file
```
## <a name="additional-references"></a>추가 참조
-   [새 항목](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
-   [del](https://docs.microsoft.com/windows-server/administration/windows-commands/del)
-   [rmdir](https://docs.microsoft.com/windows-server/administration/windows-commands/rd)
