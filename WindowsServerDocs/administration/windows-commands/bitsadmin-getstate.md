---
title: bitsadmin getstate
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1252d6cf-14ca-44df-beb2-930ff011f297
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55be37a6b1b44b81ed9002e5e3b9eb1fd46bd0dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381226"
---
# <a name="bitsadmin-getstate"></a>bitsadmin getstate



지정된 된 작업의 상태를 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetState <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

가능한 상태는.

|-----|-----| | 큐에 대기 | 작업이 실행 되기를 기다리고 있습니다. | | 연결 | BITS가 서버에 연결 하는 중입니다. | | 전송 중 | BITS가 데이터를 전송 하 고 있습니다. | | 일시 중단 됨 | 작업이 일시 중지 되었습니다. | | 오류 | 복구할 수 없는 오류가 발생 했습니다. 전송은 다시 시도 되지 않습니다. | | TRANSIENT_ERROR | 복구 가능한 오류가 발생 했습니다. 최소 다시 시도 지연이 만료 되 면 전송 다시 시도 됩니다. | | 승인 됨 | 작업이 완료 되었습니다. | | 취소 | 작업이 취소 되었습니다. |

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 상태를 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetState myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)