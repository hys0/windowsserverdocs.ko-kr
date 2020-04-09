---
title: bitsadmin getowner
description: 지정 된 작업의 소유자를 검색 하는 bitsadmin **getowner**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e622c3759c9ec20867c693539c4481c70aa4f26
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850566"
---
# <a name="bitsadmin-getowner"></a>bitsadmin getowner

지정 된 작업의 소유자에 대 한 표시 이름 또는 GUID를 표시 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getowner <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예에서는 이름이 *Mydownloadjob*인 작업의 소유자를 표시 합니다.

```
C:\>bitsadmin /getowner myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)