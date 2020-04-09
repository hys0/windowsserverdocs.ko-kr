---
title: mklink
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3d6328d972b07b1bebd272788b896fd491e47380
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839556"
---
# <a name="mklink"></a>mklink
기호화 된 링크를 만듭니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

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
|\<링크 >|생성 중인 기호화 된 링크의 이름을 지정 합니다.|
|\<대상 >|새 바로 가기 링크를 참조 하는 경로 (상대 또는 절대)를 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 루트 디렉터리에서 \Users\User1\Documents 디렉터리에 있는 MyFolder 및 MyFile 이라는 기호화 된 링크를 만들고 제거 하는 방법을 보여 줍니다.
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
