---
title: bitsadmin getstate
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: f7ed7529fda264efaceb6b4b36e36e728c211f3f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889624"
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

|-----|-----| | 큐에 대기 | 작업 실행 되기를 기다리고 있습니다. | | 연결 | 비트에는 서버에 연결 됩니다. | | 전송 | 비트 데이터를 전송 합니다. | | 일시 중단 | 작업 일시 중지 됩니다. | | 오류 | 복구할 수 없는 오류가 발생 했습니다. 전송 재시도 되지 것입니다. | | TRANSIENT_ERROR | 복구 가능한 오류가 발생 했습니다. 최소 재시도 간격에서 만료 되 면 전송 재시도 합니다. | | 승인 | 작업이 완료 되었습니다. | | 취소 | 작업이 취소 되었습니다. |

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 상태를 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetState myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)