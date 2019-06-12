---
title: diskcomp
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: ccd1a347f9ac51fc98c963dedb1c0ab3fcd27d41
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439594"
---
# <a name="diskcomp"></a>diskcomp



두 개의 플로피 디스크의 내용을 비교 합니다. 매개 변수 없이 사용 하는 경우 **diskcomp** 현재 드라이브를 사용 하 여 두 디스크를 비교 합니다. 이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.

## <a name="syntax"></a>구문

```
diskcomp [<Drive1>: [<Drive2>:]]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<Drive1>|플로피 디스크 중 하나를 포함 하는 드라이브를 지정 합니다.|
|\<Drive2>|다른 플로피 디스크를 포함 하는 드라이브를 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

- 디스크를 사용 하 여

  합니다 **diskcomp** 명령 플로피 디스크 에서만 작동 합니다. 사용할 수 없습니다 **diskcomp** 하드 디스크를 사용 합니다. 에 대 한 하드 디스크 드라이브를 지정 하는 경우 *Drive1* 또는 *드라이브 2*합니다 **diskcomp** 다음 오류 메시지가 표시 됩니다.  
  ```
  Invalid drive specification
  Specified drive does not exist
  or is nonremovable
  ```  
- 디스크 비교

  비교할 두 개의 디스크에 모든 트랙 동일한 경우 **diskcomp** 다음 메시지가 표시 됩니다.  
  ```
  Compare OK
  ```  
  없으면 트랙 동일 **diskcomp** 다음과 유사한 메시지가 표시 됩니다.  
  ```
  Compare error on
  side 1, track 2
  ```  
  때 **diskcomp** 비교를 완료 합니다. 다음 메시지를 표시 합니다.  
  ```
  Compare another diskette (Y/N)?
  ```  
  Y 키를 누르면 **diskcomp** 다음 비교에 대 한 디스크를 삽입 하 라는 메시지가 표시 됩니다. 키를 누르면 N **diskcomp** 비교를 중지 합니다.

  때 **diskcomp** 비교를 사용 하면 디스크의 볼륨 번호를 무시 합니다.
- 드라이브 매개 변수를 생략합니다.

  생략 하면 합니다 *드라이브 2* 매개 변수 **diskcomp** 에 대 한 현재 드라이브를 사용 하 여 *드라이브 2*합니다. 두 드라이브 매개 변수를 생략 **diskcomp** 둘 다에 대 한 현재 드라이브를 사용 합니다. 현재 드라이브와 같으면 *Drive1*를 **diskcomp** 필요에 따라 디스크를 교환 하 라는 메시지가 표시 됩니다.
- Onedrive를 사용 하 여

  에 대 한 동일한 플로피 디스크 드라이브를 지정 하는 경우 *Drive1* 하 고 *드라이브 2*를 **diskcomp** onedrive를 사용 하 여 비교 하 고 필요에 따라 디스크를 삽입 하 라는 메시지가 표시 됩니다. 사용 가능한 메모리의 양과 디스크의 용량에 따라 디스크를 두 번 이상 교환 해야 합니다.
- 다양 한 유형의 디스크를 비교합니다.

  **Diskcomp** 양면 디스크 하거나 고밀도 배 밀도 디스크를 사용 하 여 디스크를 사용 하 여 단면 디스크를 비교할 수 없습니다. 경우에서 디스크 *Drive1* 의 디스크와 동일한 형식이 아닙니다 *드라이브 2*, **diskcomp** 다음 메시지가 표시 됩니다.  
  ```
  Drive types or diskette types not compatible
  ```  
- 사용 하 여 **diskcomp** 네트워크 및 리디렉션된 드라이브를 사용 하 여

  **Diskcomp** 에서 만든 드라이브 또는 네트워크 드라이브에서 작동 하지 않습니다 합니다 **subst** 명령입니다. 사용 하려는 경우 **diskcomp** 이러한 형식의 모든 드라이브를 사용 하 여 **diskcomp** 다음 오류 메시지가 표시 됩니다.  
  ```
  Invalid drive specification
  ```  
- 복사본을 사용 하 여 원래 디스크 비교

  사용 하는 경우 **diskcomp** 사용 하 여 만든 디스크를 사용 하 여 **복사본**를 **diskcomp** 다음과 유사한 메시지가 표시 될 수 있습니다.  
  ```
  Compare error on 
  side 0, track 0
  ```  
  디스크에서 파일이 동일한 경우에 이러한 유형의 오류가 발생할 수 있습니다. 하지만 **복사** 내용은 중복 반드시 두지 않습니다 해당 대상 디스크에 동일한 위치에 있습니다.
- 이해 **diskcomp** 종료 코드

  다음 표에서 각 종료 코드를 보여 줍니다.  

  |종료 코드|설명|
  |---------|-----------|
  |0|디스크가 같습니다.|
  |1|차이 찾을 수 있습니다.|
  |3|하드 오류가 발생 했습니다.|
  |4|초기화 오류가 발생 했습니다.|

  반환 되는 프로세스 종료 코드를 **diskcomp**에서 ERRORLEVEL 환경 변수를 사용할 수 있습니다 합니다 **경우** 일괄 프로그램에서 명령줄입니다.

## <a name="BKMK_examples"></a>예제

컴퓨터에 하나의 플로피 디스크 드라이브 (예를 들어 드라이브 A), 두 개의 디스크를 비교 하려면을 입력 합니다.
```
diskcomp a: a:
```
**Diskcomp** 필요에 따라 각 디스크를 삽입 하 라는 메시지가 나타납니다.

다음 예제에서는 처리 하는 방법을 보여 줍니다는 **diskcomp** 일괄 프로그램에서 ERRORLEVEL 환경 변수를 사용 하는 코드를 종료 합니다 **경우** 명령줄:
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
