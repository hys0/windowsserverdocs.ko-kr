---
title: graftabl
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b08351d4-3d24-490c-86f6-1252da11d923
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 395873cf3dbeb574dd9abc69f45b410bece80c25
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848444"
---
# <a name="graftabl"></a>graftabl



Windows 운영 체제 그래픽 모드에서 설정 하는 확장 된 문자를 표시할 수 있습니다. 매개 변수 없이 사용 하는 경우 **graftabl** 이전 및 현재 코드 페이지를 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
graftabl <CodePage>
graftabl /status
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<CodePage>|그래픽 모드에서 확장 문자 모양을 정의 하는 코드 페이지를 지정 합니다.</br>유효한 코드 페이지 id 다음과 같습니다.</br>437: 미국</br>850: 다국어 (라틴어 I)</br>852: 슬라브어 (라틴어 II)</br>855: 키릴 자모 (러시아어)</br>857: 터키어</br>860: 포르투갈어</br>861: 아이슬란드어</br>863: 프랑스어 (캐나다)</br>865: 북유럽</br>866: 러시아어</br>869: 현대 그리스어|
|/status|현재 표시 하는 코드 페이지 **graftabl** 사용 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   **Graftabl** 지정 하는 코드 페이지의 확장 문자가 모니터 표시에만 영향을 줍니다. 실제 콘솔 입력된 코드 페이지는 변경 되지 않습니다. 콘솔 입력된 코드 페이지를 변경 하려면 사용 합니다 **모드** 또는 **chcp** 명령입니다.
-   다음 표에 각 종료 코드 및 간략 한 설명이 있습니다.  
    |종료 코드|설명|
    |---------|-----------|
    |0|문자 집합을 로드 했습니다. 이전 코드 페이지가 없습니다. 로드 되었습니다.|
    |1|잘못 된 매개 변수를 지정 했습니다. 아무 조치도 취하지 않았습니다.|
    |2|파일 오류가 발생 했습니다.|
-   반환 되는 프로세스 종료 코드를 일괄 프로그램에서 ERRORLEVEL 환경 변수를 사용할 수 있습니다 **graftabl**합니다.

## <a name="BKMK_examples"></a>예제

사용 하는 현재 코드 페이지를 보려는 **graftabl**, 유형:
```
graftabl /status
```
그래픽 문자 집합을 메모리로 코드 페이지 437 (미국)를 로드 하려면 다음을 입력 합니다.
```
graftabl 437
```
그래픽 문자 집합을 코드 페이지 850 (다국어) 메모리에 로드 하려면 다음을 입력 합니다.
```
graftabl 850
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

[Freedisk](freedisk.md)

[Chcp](chcp.md)