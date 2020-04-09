---
title: bitsadmin getdescription
description: '**Bitsadmin getdescription**에 대 한 Windows 명령 항목으로, 지정 된 작업에 대 한 설명을 검색 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f3974603-ebbe-4d31-8217-040fe2d90c85
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ff1638cf634d76001042691fd890dfe41f9ae0b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850726"
---
# <a name="bitsadmin-getdescription"></a>bitsadmin getdescription

지정 된 작업에 대 한 설명을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getdescription <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 설명을 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /getdescription myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)