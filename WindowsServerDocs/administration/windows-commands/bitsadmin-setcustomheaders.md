---
title: bitsadmin setcustomheaders
description: GET 요청에 사용자 지정 HTTP 헤더를 추가 하는 bitsadmin setcustomheaders 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 74a8c5f4aa464aa9f362a9761c9f1c449fbaad00
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927847"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders

HTTP 서버에 전송 되는 GET 요청에 사용자 지정 HTTP 헤더를 추가 합니다. GET 요청에 대 한 자세한 내용은 [메서드 정의](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3) 및 [헤더 필드 정의](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)를 참조 하세요.

## <a name="syntax"></a>구문

```
bitsadmin /setcustomheaders <job> <header1> <header2> <...>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| `<header1> <header2>`등 | 작업에 대 한 사용자 지정 헤더입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에 대 한 사용자 지정 HTTP 헤더를 추가 하려면 다음을 수행 합니다.

```
bitsadmin /setcustomheaders myDownloadJob accept-encoding:deflate/gzip
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
