---
title: bitsadmin getnoprogresstimeout
description: 서비스에서 일시적인 오류가 발생 한 후 파일을 전송 하려고 시도 하는 시간 (초)을 검색 하는 **bitsadmin getnoprogresstimeout**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9cd9b19b-cbb4-4352-8419-978080f016b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cf2cfd77b494e221b60c8816ff46eed5f9252f39
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850606"
---
# <a name="bitsadmin-getnoprogresstimeout"></a>bitsadmin getnoprogresstimeout

일시적인 오류가 발생 한 후 서비스에서 파일을 전송 하려고 시도 하는 시간 (초)을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getnoprogresstimeout <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 진행률 제한 시간 값을 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /getnoprogresstimeout myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)