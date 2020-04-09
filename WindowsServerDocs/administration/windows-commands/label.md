---
title: 레이블
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bbae8bdd-97d4-4566-9118-7c95aa07645f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7ccb86e2167682e1048161f2d5f5386a8b5cf6ed
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841176"
---
# <a name="label"></a>레이블



만들고, 변경 또는 디스크의 볼륨 레이블 (이름)을 삭제 합니다. 매개 변수 없이 사용 되는 **레이블** 명령을 현재 볼륨 레이블을 변경 하거나 기존 레이블을 삭제 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
label [/mp] [<Volume>] [<Label>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/mp|볼륨 탑재 지점 또는 볼륨 이름으로 처리 해야 함을 지정 합니다.|
|볼륨 > \<|(콜론) 드라이브 문자 지정 탑재 지점 또는 볼륨 이름입니다. 볼륨 이름을 지정 하는 경우는 **/mp** 매개 변수가 필요 하지 않습니다.|
|\<레이블 >|볼륨에 대 한 레이블을 지정합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의

- Windows 볼륨 레이블 및 일련 번호 (있으면)의 일부분으로 표시 디렉터리 목록입니다.
- NTFS 볼륨 레이블의 공백을 포함 하 여 길이가 최대 32 자를 수 있습니다. NTFS 볼륨 레이블 유지 및 레이블을 만들 때 사용 된 사례를 표시 합니다.
- 에 대 한 값을 지정 하지 않으면 경우는 **레이블** 매개 변수를는 **레이블** 명령은 다음과 같은 형식으로 출력을 표시 합니다.  
  ```
  Volume in drive C: xxxxxxxxxxx 
  Volume Serial Number is xxxx-xxxx 
  Volume label (32 characters, ENTER for none)?
  ```  
  새 볼륨 레이블을 입력 하거나 enter 키를 눌러 현재 레이블을 그대로 수 있습니다. ENTER 키를 누르면 하 고 볼륨 레이블을 현재 보유 하는 경우는 **레이블** 명령은 다음과 같은 메시지가 묻는 메시지를 표시 합니다.  
  ```
  Delete current volume label (Y/N)?
  ```  
  레이블을 삭제 하려면 Y 키 또는 레이블을 변경 하지 않으려면 N 키를 누릅니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

7 월에 대 한 판매 정보를 포함 하는 드라이브의 디스크에에서 레이블을 입력 합니다.
```
label a:sales-july
```
C 드라이브에 대 한 현재 레이블을 삭제 하려면 다음이 단계를 따르십시오.
1. 명령 프롬프트에서 다음을 입력합니다.  
   ```
   Label
   ```  
   다음과 유사한 출력이 표시 됩니다.  
   ```
   Volume in drive C: is Main Disk
   Volume Serial Number is 6789-ABCD
   Volume label (32 characters, ENTER for none)?
   ```  
2. Enter 키를 누릅니다. 다음과 같은 메시지가 표시 됩니다.  
   ```
   Delete current volume label (Y/N)?
   ```  
3. 현재 레이블을 삭제 하려면 Y 누릅니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)