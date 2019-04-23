---
title: attrib
description: Windows 명령 항목에 대 한 **attrib** -파일 또는 디렉터리를 표시, 집합 또는 제거 특성에 할당 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e763ca5-21a2-45d2-b26d-a9c44c99091a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0f640af2c7957e43dd3f31dfa732bfc887112651
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841094"
---
# <a name="attrib"></a>attrib



표시 설정 하거나 파일 또는 디렉터리에 할당 된 특성을 제거 합니다. 매개 변수 없이 사용 하는 경우 **attrib** 현재 디렉터리에 있는 모든 파일의 속성을 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
attrib [{+|-}r] [{+|-}a] [{+|-}s] [{+|-}h] [{+|-}i] [<Drive>:][<Path>][<FileName>] [/s [/d] [/l]]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|{+\|-}r|집합 (**+**)을 선택 하거나 취소 (**-**) 읽기 전용 파일 특성입니다.|
|{+\|-}a|집합 (**+**)을 선택 하거나 취소 (**-**) 보관 파일 특성입니다.|
|{+\|-}s|집합 (**+**)을 선택 하거나 취소 (**-**) 시스템 파일 특성입니다.|
|{+\|-}h|집합 (**+**)을 선택 하거나 취소 (**-**) 숨김 파일 특성입니다.|
|{+\|-}i|집합 (**+**)을 선택 하거나 취소 (**-**) 콘텐츠 인덱싱되지 파일 특성입니다.|
|[\<Drive>:][<Path>][<FileName>]|디렉터리, 파일 또는 파일을 표시 하거나 특성을 변경 하려면 원하는 그룹의 이름과 위치를 지정 합니다. 사용할 수는 **?** 및 **&#42;** 와일드 카드 문자는 *FileName* 매개 변수를 표시 하거나 파일 그룹에 대 한 특성을 변경 합니다.|
|/s|적용 대상 **attrib** 현재 디렉터리에 일치 하는 파일에 명령줄 옵션 및 모든 하위 디렉터리 및입니다.|
|/d|적용 대상 **attrib** 와 디렉터리에 명령줄 옵션입니다.|
|/l|적용 대상 **attrib** 와 기호화 된 링크의 대상이 아닌 기호화 된 링크에 명령줄 옵션입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   와일드 카드 문자를 사용할 수 있습니다 (**?** 및 **&#42;**)와 *FileName* 매개 변수를 표시 하거나 파일 그룹에 대 한 특성을 변경 합니다.
-   파일에 있는 경우 시스템 (**s**) 또는 숨김 (**h**) 특성 집합을 해제 해야 특성 해당 파일에 대 한 다른 특성을 변경할 수 있습니다.
-   Archive 특성 (**는**) 마지막으로 백업한 이후 변경 된 파일을 표시 합니다. 유의 합니다 **xcopy** 명령을 사용 하 여 특성을 보관 합니다.

## <a name="BKMK_examples"></a>예제

현재 디렉터리에 있는 News86 라는 파일의 특성을 표시 하려면 다음을 입력 합니다.
```
attrib news86 
```
Report.txt 라는 파일에 읽기 전용 특성을 할당 하려면 다음을 입력 합니다.
```
attrib +r report.txt 
```
B 드라이브의 디스크에서 공용 디렉터리 및 하위 디렉터리에 있는 파일에서 읽기 전용 특성을 제거 하려면 다음을 입력 합니다.
```
attrib -r b:\public\*.* /s 
```
A, 드라이브에 있는 모든 파일에 대 한 기록 속성을 설정 하 고 확장명이.bak 인 파일에 대 한 보관 특성을 해제 하십시오, 다음을 입력 합니다.
```
attrib +a a:*.* & attrib -a a:*.bak 
```
