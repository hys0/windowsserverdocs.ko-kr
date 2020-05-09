---
title: date
description: 시스템 날짜를 표시 하거나 설정 하는 date 명령에 대 한 참조 항목입니다. 매개 변수 없이 사용 하는 경우
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce6700fb-32f9-4350-a1af-5aee61d4448c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 64d0d94061e1b5c7891b364f4c0fe153b44a564e
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993198"
---
# <a name="date"></a>date

표시 하거나 시스템 날짜를 설정 합니다. 매개 변수 없이 사용 하는 경우 **날짜** 설정 현재 시스템 날짜를 표시 하 고 새 날짜를 입력 하 라는 메시지가 표시 됩니다.

>[!IMPORTANT]
> 이 명령을 사용 하려면 관리자 여야 합니다.

## <a name="syntax"></a>구문

```
date [/t | <month-day-year>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| `<month-day-year>` | 지정 된 날짜를 설정 합니다. 여기서 *month* 는 월 (1 ~ 12 값을 포함 하는 하나 또는 두 개의 숫자), *day* 는 일 (1부터 31 까지의 값을 포함 하는 하나 또는 두 개의 숫자), *year* 는 연도 (00-99 또는 1980 ~ 2099 값을 포함 하 여 두 자리 또는 네 자리)를 설정 합니다. *월*, *일*및 *연도* 에 대 한 값을 마침표 (.), 하이픈 (-) 또는 슬래시 (/)로 구분 해야 합니다.<p>**참고:** 두 자릿수를 사용 하 여 연도를 나타내는 경우 값 80-99은 1980 ~ 1999에 해당 합니다. |
| /t | 입력 하 라는 새로운 날짜 없이 현재 날짜를 표시 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

명령 확장을 사용 하는 경우 현재 시스템 날짜를 표시 하려면 입력 합니다.

```
date /t
```

2007 년 8 월 3 일을 현재 시스템 날짜를 변경 하려면 다음 중 하나를 입력할 수 있습니다.

```
date 08.03.2007
date 08-03-07
date 8/3/07
```

뒤에 새 날짜를 입력 하 라는 메시지가 현재 시스템 날짜를 표시 하려면 다음을 입력 합니다.

```
The current date is: Mon 04/02/2007
Enter the new date: (mm-dd-yyyy)
```

현재 날짜를 유지 하 고 명령 프롬프트로 돌아가려면 **enter**키를 누릅니다. 현재 날짜를 변경 하려면 새 날짜를 입력 한 다음 **enter**키를 누릅니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)