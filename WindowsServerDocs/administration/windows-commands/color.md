---
title: 색
description: 현재 세션에 대 한 명령 프롬프트 창의 전경색과 배경색을 변경 하는 color 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f5b67131-d196-45ec-a3f9-b5d9f091fd86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 93c51fdbf1909adfda06730c3a517f602f8024b8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929802"
---
# <a name="color"></a>색

현재 세션에 대 한 명령 프롬프트 창에서 전경색 및 배경색을 변경 합니다. 매개 변수 없이 사용 하는 경우 **색** 기본 명령 프롬프트 창 전경색 및 배경색을 복원 합니다.

## <a name="syntax"></a>구문

```
color [[<b>]<f>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<b>` | 배경색을 지정합니다. |
| `<f>` | 전경색을 지정합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

위치:

다음 표에서는 및에 대 한 값으로 사용할 수 있는 유효한 16 진수를 보여 줍니다 `<b>` `<f>` .

| 값 | 색상 |
| ----- | ----- |
| 0 | 검정 |
| 1 | 파랑 |
| 2 | 녹색 |
| 3 | Aqua |
| 4 | 빨강 |
| 5 | 보라 |
| 6 | 노랑 |
| 7 | 흰색 |
| 8 | 회색 |
| 9 | 연한 파랑 |
| a | 연한 녹색 |
| b | 연한 바다색 |
| c | 연한 빨강 |
| 일 | 연한 자주색 |
| e | 연한 노랑 |
| f | 밝은 흰색 |

#### <a name="remarks"></a>설명

- 및 사이에 공백 문자를 사용 하지 않습니다 `<b>` `<f>` .

- 16 진수를 하나만 지정 하는 경우 해당 색은 전경색으로 사용 되 고 배경색은 기본 색으로 설정 됩니다.

- 기본 명령 프롬프트 창 색을 설정 하려면 **명령 프롬프트** 창의 왼쪽 위 모퉁이를 선택 하 고, **기본값**을 선택 하 고, **색** 탭을 선택한 후 **화면 텍스트** 및 **화면 배경에**사용할 색을 선택 합니다.

- `<b>`및 `<f>` 가 동일한 색 값 이면 ERRORLEVEL은로 설정 되 `1` 고 전경색 또는 배경색은 변경 되지 않습니다.

## <a name="examples"></a>예

명령 프롬프트 창의 배경색을 회색으로 변경 하 고 전경색을 빨강으로 변경 하려면 다음을 입력 합니다.

```
color 84
```

명령 프롬프트 창의 전경색을 연한 노랑으로 변경 하려면 다음을 입력 합니다.

```
color e
```

> [!NOTE]
> 이 예제에서는 하나의 16 진수가 지정 되어 있으므로 배경은 기본 색으로 설정 됩니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
