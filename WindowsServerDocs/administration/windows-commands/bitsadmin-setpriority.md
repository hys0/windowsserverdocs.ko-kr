---
title: bitsadmin setpriority
description: 지정 된 작업의 우선 순위를 설정 하는 **bitsadmin setpriority**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9348680a61649b938267b3277de9aa5aa521361f
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122764"
---
# <a name="bitsadmin-setpriority"></a>bitsadmin setpriority

지정된 된 작업의 우선 순위를 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setpriority <job> <priority>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| priority | 다음을 포함 하 여 작업의 우선 순위를 설정 합니다.<ul><li>FOREGROUND</li><li>HIGH</li><li>NORMAL</li><li>LOW</li></ul> |

## <a name="examples"></a>예

다음 예제에서는 명명 된 작업에 대 한 우선 순위 설정 *myDownloadJob* 정상입니다.

```
C:\>bitsadmin /setpriority myDownloadJob NORMAL
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)