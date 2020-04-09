---
title: bitsadmin nowrap
description: '**Bitsadmin nowrap**에 대 한 Windows 명령 항목으로, 명령 창의 가장 오른쪽 가장자리를 벗어나 확장 되는 출력 텍스트 줄을 자릅니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f9f1db370d8a8917aa03a414a27623a1024df192
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850186"
---
# <a name="bitsadmin-nowrap"></a>bitsadmin nowrap

명령 창에서 가장 오른쪽 가장자리를 벗어나 확장 되는 출력 텍스트 줄을 자릅니다. 기본적으로 **모니터** 스위치를 제외한 모든 스위치는 출력을 래핑합니다. 다른 스위치 앞에 **nowrap** 스위치를 지정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /nowrap
```

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 이름이 *Mydownloadjob* 인 작업의 상태를 검색 하 고 출력을 줄 바꿈하지 않습니다.

```
C:\>bitsadmin /nowrap /getstate myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)