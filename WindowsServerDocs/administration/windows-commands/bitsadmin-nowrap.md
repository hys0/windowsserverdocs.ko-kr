---
title: bitsadmin nowrap
description: 명령 창의 가장 오른쪽 가장자리를 벗어나 확장 되는 출력 텍스트 줄을 잘라내는 bitsadmin nowrap 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8f55faeea79e5f2cf02fde0732ed82ae13e902f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923027"
---
# <a name="bitsadmin-nowrap"></a>bitsadmin nowrap

명령 창에서 가장 오른쪽 가장자리를 벗어나 확장 되는 출력 텍스트 줄을 자릅니다. 기본적으로 **모니터** 스위치를 제외한 모든 스위치는 출력을 래핑합니다. 다른 스위치 앞에 **nowrap** 스위치를 지정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /nowrap
```

## <a name="examples"></a>예

출력을 래핑하는 동안 *Mydownloadjob* 이라는 작업 상태를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /nowrap /getstate myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
