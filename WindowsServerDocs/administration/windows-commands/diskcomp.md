---
title: diskcomp
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f56f534-a356-4daa-8b4f-38e089341e42
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca5ea0f4587b21b2a274c772aab239668b7868b4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377875"
---
# <a name="diskcomp"></a>diskcomp



두 플로피 디스크의 내용을 비교 합니다. 매개 변수 없이 사용 하는 경우 **diskcomp** 는 현재 드라이브를 사용 하 여 두 디스크를 비교 합니다. 이 명령을 사용 하는 방법에 대 한 예는 [예제](#BKMK_examples)를 참조 하세요.

## <a name="syntax"></a>구문

```
diskcomp [<Drive1>: [<Drive2>:]]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<드라이브 1 >|플로피 디스크 중 하나를 포함 하는 드라이브를 지정 합니다.|
|\<Drive2 >|다른 플로피 디스크를 포함 하는 드라이브를 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

- 디스크 사용

  **Diskcomp** 명령은 플로피 디스크 에서만 작동 합니다. **Diskcomp** 는 하드 디스크에 사용할 수 없습니다. *Drive1* 또는 *Drive2*에 대 한 하드 디스크 드라이브를 지정 하는 경우 **diskcomp** 는 다음 오류 메시지를 표시 합니다.  
  ```
  Invalid drive specification
  Specified drive does not exist
  or is nonremovable
  ```  
- 디스크 비교

  비교 하는 두 디스크의 모든 트랙이 동일 하면 **diskcomp** 는 다음과 같은 메시지를 표시 합니다.  
  ```
  Compare OK
  ```  
  트랙이 동일 하지 않으면 **diskcomp** 는 다음과 유사한 메시지를 표시 합니다.  
  ```
  Compare error on
  side 1, track 2
  ```  
  **Diskcomp** 비교가 완료 되 면 다음 메시지가 표시 됩니다.  
  ```
  Compare another diskette (Y/N)?
  ```  
  Y 키를 누르면 **diskcomp** 는 다음 비교를 위해 디스크를 삽입 하 라는 메시지를 표시 합니다. N 키를 누르면 **diskcomp** 는 비교를 중지 합니다.

  **Diskcomp** 는 비교를 수행 하는 경우 디스크의 볼륨 번호를 무시 합니다.
- 드라이브 매개 변수 생략

  *Drive2* 매개 변수를 생략 하면 **diskcomp** 는 *Drive2*에 대 한 현재 드라이브를 사용 합니다. 두 드라이브 매개 변수를 모두 생략 하면 **diskcomp** 는 두 가지 모두에 대해 현재 드라이브를 사용 합니다. 현재 드라이브가 *Drive1*와 동일 하면 **diskcomp** 는 필요에 따라 디스크를 교환 하 라는 메시지를 표시 합니다.
- 드라이브 하나 사용

  *Drive1* 및 *Drive2*에 대해 동일한 플로피 디스크 드라이브를 지정 하면 **diskcomp** 는 드라이브 하나를 사용 하 여 비교 하 고 필요에 따라 디스크를 넣으라는 메시지를 표시 합니다. 디스크 용량 및 사용 가능한 메모리 양에 따라 디스크를 두 번 이상 교환 해야 할 수도 있습니다.
- 여러 유형의 디스크 비교

  **Diskcomp** 는 양면 디스크와 더블 밀도 디스크를 사용 하는 고밀도 디스크를 비교할 수 없습니다. *Drive1* 의 디스크가 *Drive2*의 디스크와 동일한 유형이 아니면 **diskcomp** 는 다음 메시지를 표시 합니다.  
  ```
  Drive types or diskette types not compatible
  ```  
- 네트워크 및 리디렉션된 드라이브에 **diskcomp** 사용

  **Diskcomp** 는 네트워크 드라이브 또는 **subst** 명령으로 만든 드라이브에서 작동 하지 않습니다. 이러한 유형의 드라이브에 **diskcomp** 를 사용 하려고 하면 **diskcomp** 는 다음 오류 메시지를 표시 합니다.  
  ```
  Invalid drive specification
  ```  
- 원본 디스크와 복사본 비교

  **Copy**를 사용 하 여 만든 디스크에 **diskcomp** 를 사용 하는 경우 **diskcomp** 는 다음과 유사한 메시지를 표시할 수 있습니다.  
  ```
  Compare error on 
  side 0, track 0
  ```  
  이 유형의 오류는 디스크의 파일이 동일한 경우에도 발생할 수 있습니다. **복사** 는 중복 된 정보를 대상 디스크의 동일한 위치에 배치 하지 않을 수도 있습니다.
- **Diskcomp** 종료 코드 이해

  다음 표에서는 각 종료 코드에 대해 설명 합니다.  

  |종료 코드|설명|
  |---------|-----------|
  |0|디스크가 동일 합니다.|
  |1|차이점 발견|
  |3|하드 오류가 발생 했습니다.|
  |4|초기화 오류가 발생 했습니다.|

  **Diskcomp**에서 반환 하는 종료 코드를 처리 하려면 일괄 처리 프로그램의 **IF** 명령줄에서 ERRORLEVEL 환경 변수를 사용할 수 있습니다.

## <a name="BKMK_examples"></a>예와

컴퓨터에 플로피 디스크 드라이브가 하나만 있는 경우 (예: 드라이브 A) 두 개의 디스크를 비교 하려면 다음을 입력 합니다.
```
diskcomp a: a:
```
**Diskcomp** 는 필요에 따라 각 디스크를 삽입 하 라는 메시지를 표시 합니다.

다음 예제에서는 **if** 명령줄에서 ERRORLEVEL 환경 변수를 사용 하는 일괄 처리 프로그램에서 **diskcomp** 종료 코드를 처리 하는 방법을 보여 줍니다.
```
rem Checkout.bat compares the disks in drive A and B 
echo off 
diskcomp a: b: 
if errorlevel 4 goto ini_error 
if errorlevel 3 goto hard_error 
if errorlevel 1 goto no_compare
if errorlevel 0 goto compare_ok 
:ini_error 
echo ERROR: Insufficient memory or command invalid 
goto exit 
:hard_error 
echo ERROR: An irrecoverable error occurred 
goto exit 
:break 
echo "You just pressed CTRL+C" to stop the comparison 
goto exit 
:no_compare 
echo Disks are not the same 
goto exit 
:compare_ok 
echo The comparison was successful; the disks are the same 
goto exit 
:exit
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
