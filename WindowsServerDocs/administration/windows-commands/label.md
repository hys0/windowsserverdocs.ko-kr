---
title: label
description: 디스크의 볼륨 레이블 (즉, 이름)을 만들거나 변경 하거나 삭제 하는 label 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bbae8bdd-97d4-4566-9118-7c95aa07645f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f2d09328f79215c497bcb0ea4549b1f6ac227994
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817263"
---
# <a name="label"></a>label

만들고, 변경 또는 디스크의 볼륨 레이블 (이름)을 삭제 합니다. 매개 변수 없이 사용 되는 **레이블** 명령을 현재 볼륨 레이블을 변경 하거나 기존 레이블을 삭제 합니다.

## <a name="syntax"></a>구문

```
label [/mp] [<volume>] [<label>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /mp | 볼륨 탑재 지점 또는 볼륨 이름으로 처리 해야 함을 지정 합니다. |
| `<volume>` | (콜론) 드라이브 문자 지정 탑재 지점 또는 볼륨 이름입니다. 볼륨 이름을 지정 하는 경우는 **/mp** 매개 변수가 필요 하지 않습니다. |
| `<label>` | 볼륨에 대 한 레이블을 지정합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="remarks"></a>설명

- Windows 볼륨 레이블 및 일련 번호 (있으면)의 일부분으로 표시 디렉터리 목록입니다.

- NTFS 볼륨 레이블의 공백을 포함 하 여 길이가 최대 32 자를 수 있습니다. NTFS 볼륨 레이블 유지 및 레이블을 만들 때 사용 된 사례를 표시 합니다.

## <a name="examples"></a>예

7 월에 대 한 판매 정보를 포함 하는 드라이브의 디스크에에서 레이블을 입력 합니다.

```
label a:sales-july
```

C 드라이브에 대 한 현재 레이블을 보고 삭제 하려면 다음 단계를 수행 합니다.

1. 명령 프롬프트에 다음을 입력합니다.

   ```
   label
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

3. 현재 레이블을 삭제 하려면 **Y** 를 누르고, 기존 레이블을 유지 하려면 **N** 을 누릅니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)