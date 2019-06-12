---
title: cd
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 932d9cc1-3dff-40da-835c-1cb0894874f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 53340612d26eaa7c4ae6fd977a0eac573f91881d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434605"
---
# <a name="cd"></a>cd



이름을 표시 하거나 현재 디렉터리를 변경 합니다. 드라이브 문자로 사용 하는 경우 (예를 들어 `cd C:`), **cd** 지정된 된 드라이브의 현재 디렉터리의 이름을 표시 합니다. 매개 변수 없이 사용 하는 경우 **cd** 디렉터리와 현재 드라이브를 표시 합니다.

> [!NOTE]
> 이 명령은 같습니다는 **chdir** 명령입니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
cd [/d] [<Drive>:][<Path>]
cd [..]
chdir [/d] [<Drive>:][<Path>]
chdir [..]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/d|드라이브에 대 한 현재 디렉터리와 현재 드라이브를 변경합니다.|
|\<Drive>:|표시 하거나 (다른 경우 현재 드라이브)를 변경 하려면 드라이브를 지정 합니다.|
|\<Path>|표시 하거나 변경 하려는 디렉터리의 경로를 지정 합니다.|
|[..]|상위 폴더를 변경 하려면 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

다음과 같은 명령 확장을 사용 하는 경우에 적용 된 **cd** 명령:
- 디스크의 이름으로는 대/소문자를 사용 하 여 현재 디렉터리 문자열 변환 됩니다. 예를 들어 `cd C:\TEMP` 되어 디스크의 경우에는 현재 디렉터리를 C:\Temp로 설정 합니다.
- 공백 처리 하지 않을 구분 기호로 하므로 *경로* 인용 부호를 포함 하지 않고 공백을 포함할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  ```
  cd username\programs\start menu
  ```  
  와 같습니다.  
  ```
  cd "username\programs\start menu"
  ```  
  확장을 사용할 수 있는 경우 따옴표, 필요한 경우은 없습니다.

명령 확장을 사용 하지 않으려면 다음을 입력 합니다.
```
cmd /e:off
```

## <a name="BKMK_examples"></a>예제

루트 디렉터리는 드라이브에 대 한 디렉터리 계층의 맨 위에 있습니다. 루트 디렉터리를 반환 하려면 다음을 입력 합니다.
```
cd\
```
에 있는 것과에서 다른 드라이브의 기본 디렉터리를 변경 하려면 다음을 입력 합니다.
```
cd [<Drive>:\[<Directory>]]
```
디렉터리 변경을 확인 하려면 다음을 입력 합니다.
```
cd [<Drive>:]
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)