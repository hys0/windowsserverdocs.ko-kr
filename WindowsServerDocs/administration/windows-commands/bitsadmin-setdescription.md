---
title: bitsadmin setdescription
description: '**Bitsadmin setdescription**에 대 한 Windows 명령 항목으로, 지정 된 작업에 대 한 설명을 설정 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b62e6b030c23c475418cd6f2c63f04edba1acff
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123010"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin setdescription

지정 된 작업에 대 한 설명을 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setdescription <job> <description>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| description | 작업에 설명 하는 데 사용 하는 텍스트입니다. |

## <a name="examples"></a>예

다음 예제에서는 명명 된 작업에 대 한 설명을 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /setdescription myDownloadJob music_downloads
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)