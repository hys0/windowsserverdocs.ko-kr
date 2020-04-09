---
title: bitsadmin gettemporaryname
description: 작업 내에서 지정 된 파일의 임시 파일 이름을 보고 하는 **bitsadmin gettemporaryname**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c331ecf12cb02d34c76692158c79eafbe5691c5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850456"
---
# <a name="bitsadmin-gettemporaryname"></a>bitsadmin gettemporaryname

작업 내에서 지정된 된 파일의 임시 파일 이름을 보고합니다.

## <a name="syntax"></a>구문

```
bitsadmin /gettemporaryname <job> <file_index>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| file_index | 0부터 시작 합니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예에서는 이름이 *Mydownloadjob*인 작업에 대 한 파일 2의 임시 파일 이름을 보고 합니다.

```
C:\>bitsadmin /gettemporaryname myDownloadJob 1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)