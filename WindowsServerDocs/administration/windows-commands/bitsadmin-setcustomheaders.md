---
title: bitsadmin setcustomheaders
description: GET 요청에 사용자 지정 HTTP 헤더를 추가 하는 **bitsadmin setcustomheaders**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b5b1a28f03815a22a3f8d10b2c3d1d4a3a2ae635
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123023"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders

HTTP 서버에 전송 되는 GET 요청에 사용자 지정 HTTP 헤더를 추가 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setcustomheaders <job> <header1> <header2> <...>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| `<header1> <header2>` 등 | 작업에 대 한 사용자 지정 헤더입니다. |

## <a name="examples"></a>예

다음 예제에서는 명명 된 작업에 대 한 사용자 지정 HTTP 헤더 추가 *myDownloadJob*합니다. GET 요청에 대 한 자세한 내용은 [메서드 정의](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3) 및 [헤더 필드 정의](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)를 참조 하세요.

```
C:\>bitsadmin /setcustomheaders myDownloadJob accept-encoding:deflate/gzip
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)