---
title: bitsadmin getdisplayname
description: '**Bitsadmin getdisplayname**에 대 한 Windows 명령 항목으로, 지정 된 작업의 표시 이름을 검색 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6944dc2b7a63ca986fb285d26796f350c1052295
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850716"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname

지정 된 작업의 표시 이름을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getdisplayname <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 표시 이름을 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /getdisplayname myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)