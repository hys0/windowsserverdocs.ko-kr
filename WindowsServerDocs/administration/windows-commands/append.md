---
title: append
description: '에 대 한 Windows 명령을 항목 '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c3fea20-9502-40ad-a442-7a927aad88eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: abf7713b3fd5bbb6172969ca1cc39cbbbbafafc6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881984"
---
# <a name="append"></a>append



지정 된 디렉터리에 데이터 파일을 현재 디렉터리에 있는 것 처럼 열을 수 있습니다. 매개 변수 없이 사용 하는 경우 **추가** 추가 디렉터리 목록을 표시 합니다.

> [!NOTE]
> 이 명령은 Windows 10에서 지원 되지 않습니다.
>

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
append [[<Drive>:]<Path>[;...]] [/x[:on|:off]] [/path:[:on|:off] [/e] 
append ;
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[\<Drive>:]<Path>|드라이브와 추가할 디렉터리를 지정 합니다.|
|/ x:에|파일 검색 및 시작 응용 프로그램에 추가 된 디렉터리를 적용합니다.|
|/x: 해제|추가 된 디렉터리 요청 파일을 열에 적용 됩니다.</br>**/x: off** 기본 설정입니다.|
|/path:에|이미 경로 지정 하는 파일 요청에 추가 된 디렉터리를 적용 합니다. **/path:에** 기본 설정입니다.|
|/path: 해제|효과 해제 **/path:에**합니다.|
|/e|Append 환경 변수에 추가 디렉터리 목록의 복사본을 저장 합니다. **/e** 처음에 사용할 때만 사용할 수 있습니다 **추가** 시스템을 시작한 후입니다.|
|;|추가 디렉터리 목록을 지웁니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="BKMK_examples"></a>예제

추가 디렉터리 목록을 지우려면 다음을 입력 합니다.
```
append ;
```
Append 환경 변수에 추가 된 디렉터리의 복사본을 저장 하려면 다음을 입력 합니다.
```
append /e
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
