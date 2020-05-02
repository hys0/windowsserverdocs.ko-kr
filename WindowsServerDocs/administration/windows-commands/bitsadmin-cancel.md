---
title: bitsadmin cancel
description: 전송 큐에서 작업을 제거 하 고 작업과 연결 된 모든 임시 파일을 삭제 하는 bitsadmin cancel 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 95fefbc4a9731c2ccbac22adc27f8231a7f36138
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718261"
---
# <a name="bitsadmin-cancel"></a>bitsadmin cancel

작업 전송 큐에서 제거 하 고 작업과 연결 된 모든 임시 파일을 삭제 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /cancel <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

전송 큐에서 *Mydownloadjob* 작업을 제거 하려면 다음을 수행 합니다.

```
bitsadmin /cancel myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
