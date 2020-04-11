---
title: bitsadmin setdisplayname
description: 지정 된 작업의 표시 이름을 설정 하는 **bitsadmin setdisplayname**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b1086903dd130392800f325c451bb4750fbf8fa
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123002"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

지정 된 작업에 대 한 표시 이름을 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setdisplayname <job> <display_name>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| display_name | 특정 작업에 대해 표시 된 이름으로 사용 되는 텍스트입니다. |

## <a name="examples"></a>예

다음 예에서는 작업의 표시 이름을 *Mydownloadjob*로 설정 합니다.

```
C:\>bitsadmin /setdisplayname myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)