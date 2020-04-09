---
title: bitsadmin getvalidationstate
description: 작업 내에서 지정 된 파일의 콘텐츠 유효성 검사 상태를 보고 하는 **bitsadmin getvalidationstate**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 52d7d983cc7858607c350483ed81223d107cee25
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850436"
---
# <a name="bitsadmin-getvalidationstate"></a>bitsadmin getvalidationstate

작업 내에서 지정된 된 파일의 콘텐츠 유효성 검사 상태를 보고합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getvalidationstate <job> <file_index>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| file_index | 0부터 시작 합니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 이름이 *Mydownloadjob*인 작업 내에서 파일 2의 콘텐츠 유효성 검사 상태를 가져옵니다.

```
C:\>bitsadmin /getvalidationstate myDownloadJob 1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)