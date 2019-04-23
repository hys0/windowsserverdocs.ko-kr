---
title: ren
description: 파일 또는 ren 명령 사용 하 여 디렉터리의 이름을 바꾸는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60398e12-a05d-4524-a73a-0a925943e21d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: c239dd1f1f8d03d761e45505634da10f19ed08cf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842024"
---
# <a name="ren"></a>ren

파일 또는 디렉터리의 이름을 바꿉니다. 이 명령은 같습니다는 **이름 바꾸기** 명령입니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
ren [<Drive>:][<Path>]<FileName1> <FileName2>
rename [<Drive>:][<Path>]<FileName1> <FileName2>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[\<Drive>:][\<Path>]\<FileName1>|파일의 이름 또는 집합 이름을 바꿀 파일의 위치를 지정 합니다. *FileName1* 와일드 카드 문자를 포함할 수 있습니다 (**&#42;** 하 고 **?**).|
|\<FileName2>|파일에 대 한 새 이름을 지정합니다. 여러 파일에 대 한 새 이름을 지정 하려면 와일드 카드 문자를 사용할 수 있습니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   파일 이름을 바꿀 때 새 드라이브 또는 경로 지정할 수 없습니다.
-   사용할 수 없습니다는 **ren** 드라이브 간에 파일 이름을 변경 하거나 다른 디렉터리에 파일을 이동 하는 명령입니다.
-   와일드 카드 문자를 사용할 수 있습니다 (**&#42;** 하 고 **?**) 중 하나에서 *FileName* 매개 변수입니다. 에 와일드 카드 문자로 표현 된 문자를 *FileName2* 해당 문자에 동일 *FileName1*합니다.
-   *FileName2* 고유한 파일 이름 이어야 합니다. 경우 *FileName2* 기존 파일 이름과 일치 하는 **ren** 다음 메시지가 표시 됩니다.  
    ```
    Duplicate file name or file not found
    ```

## <a name="BKMK_examples"></a>예제

현재 디렉터리의 모든.txt 파일의 이름 확장명.doc 확장명을 변경 하려면 다음을 입력 합니다.
```
ren *.txt *.doc 
```
Part10에 Chap10에서 디렉터리의 이름을 변경 하려면 다음을 입력 합니다.
```
ren chap10 part10 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)