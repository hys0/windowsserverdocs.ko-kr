---
title: 일시 중지
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cab3afc3-d046-432f-a0bf-6282f0099032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6501859eacf30dd6c1e64f34eee29ff81bd78ec9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372366"
---
# <a name="pause"></a>일시 중지



일괄 처리 프로그램의 처리를 일시 중단 하 고 다음 메시지를 표시 합니다.
```
Press any key to continue . . .
```
이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
pause
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

- **일시 중지** 명령을 실행 하면 다음과 같은 메시지가 나타납니다.  
  ```
  Press any key to continue . . .
  ```  
- CTRL + C를 눌러 일괄 처리 프로그램을 중지 하면 다음과 같은 메시지가 나타납니다.  
  ```
  Terminate batch job (Y/N)?
  ```  
  이 메시지에 대 한 응답으로 Y (예의 경우)를 누르면 일괄 처리 프로그램이 종료 되 고 운영 체제에 대 한 제어가 반환 됩니다.
- 처리 하지 않을 수 있는 배치 파일의 섹션 앞에 **일시 중지** 명령을 삽입할 수 있습니다. **일시 중지가** 일괄 처리 프로그램의 처리를 일시 중단 하면 Ctrl + C를 누른 다음 Y를 눌러 batch 프로그램을 중지할 수 있습니다.

## <a name="BKMK_examples"></a>예와

사용자에 게 드라이브 중 하나에서 디스크를 변경 하 라는 메시지를 표시 하는 일괄 처리 프로그램을 만들려면 다음을 입력 합니다.
```
@echo off 
:Begin 
copy a:*.* 
echo Put a new disk into drive A 
pause 
goto begin
```
이 예제에서는 드라이브 A에 있는 디스크의 모든 파일이 현재 디렉터리에 복사 됩니다. 메시지에 드라이브 A에 새 디스크를 추가 하 라는 메시지가 표시 되 면 **일시 중지** 명령은 디스크를 변경한 다음 아무 키나 눌러 처리를 다시 시작할 수 있도록 처리를 일시 중단 합니다. 이 일괄 처리 프로그램은 무한 루프로 실행 됩니다. **goto begin** 명령은 명령 인터프리터를 배치 파일의 시작 레이블로 보냅니다. 이 일괄 처리 프로그램을 중지 하려면 CTRL + C를 누른 다음 Y를 누릅니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)