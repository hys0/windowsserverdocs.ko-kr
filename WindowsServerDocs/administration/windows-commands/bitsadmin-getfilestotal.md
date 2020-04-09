---
title: bitsadmin getfilestotal
description: 지정 된 작업의 파일 수를 검색 하는 **bitsadmin getfilestotal**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bad42a8bef57ca4c4a1411a12f20979e4a95d178
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850686"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal

지정 된 작업의 파일 수를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getfilestotal <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 포함 된 파일의 수를 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /getfilestotal myDownloadJob
```

## <a name="see-also"></a>관련 항목

- [명령줄 구문 키](command-line-syntax-key.md)
