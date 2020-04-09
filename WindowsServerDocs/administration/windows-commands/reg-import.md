---
title: reg 가져오기
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0be103de-08fc-4f02-b590-361782680b3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0816297e837bbce91ca069e3506405cbdb53c51a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836426"
---
# <a name="reg-import"></a>reg 가져오기



포함 된 파일의 내용을 복사 하는 로컬 컴퓨터의 레지스트리로 레지스트리 하위 키, 항목 및 값을 내보냅니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
Reg import FileName
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<파일 이름 >|로컬 컴퓨터의 레지스트리로 복사 되는 콘텐츠를 포함 하는 파일의 경로 이름을 지정 합니다. 이 파일을 사용 하 여 사전에 만들 수 있어야 **reg 내보내기**합니다.|
|/?|에 대 한 도움말을 표시 **reg 가져오기** 명령 프롬프트입니다.|

## <a name="remarks"></a>주의

다음 표에 대 한 반환 값은 **reg 가져오기** 작업 합니다.

|값|설명|
|-----|-----------|
|0|성공|
|1|실패|

## <a name="examples"></a><a name=BKMK_examples></a>예와

레지스트리 항목에서 AppBkUp.reg 라는 파일을 가져오려면 다음을 입력 합니다.
```
reg import AppBkUp.reg
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)