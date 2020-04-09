---
title: bitsadmin getcustomheaders
description: 작업에서 사용자 지정 HTTP 헤더를 검색 하는 **bitsadmin getcustomheaders**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 80a3d1230fd541f0b986434ce373da4c8bb0c761
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850736"
---
# <a name="bitsadmin-getcustomheaders"></a>bitsadmin getcustomheaders

작업에서 사용자 지정 HTTP 헤더를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getcustomheaders <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 이름이 *Mydownloadjob*인 작업에 대 한 사용자 지정 헤더를 가져옵니다.

```
C:\>bitsadmin /getcustomheaders myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)