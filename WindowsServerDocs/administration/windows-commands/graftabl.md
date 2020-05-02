---
title: graftabl
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b08351d4-3d24-490c-86f6-1252da11d923
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b3815b85da163c03dea7bd2619d4647454d3ebd7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724922"
---
# <a name="graftabl"></a>graftabl



Windows 운영 체제에서 그래픽 모드로 확장 문자 집합을 표시할 수 있도록 합니다. 매개 변수 없이 사용 하는 경우 **graftabl** 는 이전 및 현재 코드 페이지를 표시 합니다.



## <a name="syntax"></a>구문

```
graftabl <CodePage>
graftabl /status
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<코드 페이지>|그래픽 모드에서 확장 문자의 모양을 정의 하는 코드 페이지를 지정 합니다.</br>유효한 코드 페이지 id 번호는 다음과 같습니다.</br>437: United States</br>850: 다국어 (라틴어 I)</br>852: 슬라브어 (라틴어 II)</br>855: 키릴 자모 (러시아어)</br>857: 터키어</br>860: 포르투갈어</br>861: 아이슬란드어</br>863: 캐나다-프랑스어</br>865: 북유럽어</br>866: 러시아어</br>869: 현대 그리스어|
|/status|**Graftabl** 가 사용 하는 현재 코드 페이지를 표시 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   **Graftabl** 는 지정한 코드 페이지의 확장 된 문자 모니터 표시에만 영향을 줍니다. 실제 콘솔 입력 코드 페이지는 변경 되지 않습니다. 콘솔 입력 코드 페이지를 변경 하려면 **모드** 또는 **chcp** 명령을 사용 합니다.
-   다음 표에는 각 종료 코드와 그에 대 한 간략 한 설명이 나와 있습니다.  
    |종료 코드|설명|
    |---------|-----------|
    |0|문자 집합을 로드 했습니다. 이전 코드 페이지가 로드 되지 않았습니다.|
    |1|잘못 된 매개 변수가 지정 되었습니다. 아무 조치도 취하지 않았습니다.|
    |2|파일 오류가 발생 했습니다.|
-   일괄 처리 프로그램에서 ERRORLEVEL 환경 변수를 사용 하 여 **graftabl**에서 반환 하는 종료 코드를 처리할 수 있습니다.

## <a name="examples"></a>예

**Graftabl**에서 사용 하는 현재 코드 페이지를 보려면 다음을 입력 합니다.
```
graftabl /status
```
코드 페이지 437 (미국)에 대 한 그래픽 문자 집합을 메모리에 로드 하려면 다음을 입력 합니다.
```
graftabl 437
```
코드 페이지 850 (다국어)의 그래픽 문자 집합을 메모리로 로드 하려면 다음을 입력 합니다.
```
graftabl 850
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

[Freedisk](freedisk.md)

[Chcp](chcp.md)