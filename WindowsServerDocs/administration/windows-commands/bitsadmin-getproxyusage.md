---
title: bitsadmin getproxyusage
description: 지정 된 작업에 대 한 프록시 사용 설정을 검색 하는 bitsadmin getproxyusage 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad1ffe5786202d6fecc0d65a719c9d6be0f5609e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926784"
---
# <a name="bitsadmin-getproxyusage"></a>bitsadmin getproxyusage

지정된 된 작업에 대 한 프록시 사용 설정을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getproxyusage <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

#### <a name="output"></a>출력

반환 된 프록시 사용 값은 다음과 같을 수 있습니다.

- **사전 구성** -소유자의 Internet Explorer 기본값을 사용 합니다.

- **No_Proxy** -프록시 서버를 사용 하지 않습니다.

- **Override** -명시적 프록시 목록을 사용 합니다.

- 자동 **검색-프록시 설정을 자동으로 검색** 합니다.

## <a name="examples"></a>예

이름이 *Mydownloadjob*인 작업에 대 한 프록시 사용을 검색 하려면:

```
bitsadmin /getproxyusage myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
