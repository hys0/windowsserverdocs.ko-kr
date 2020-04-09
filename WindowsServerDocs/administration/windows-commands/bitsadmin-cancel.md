---
title: bitsadmin cancel
description: '**Bitsadmin cancel**의 Windows 명령 항목은 전송 큐에서 작업을 제거 하 고 작업과 연결 된 모든 임시 파일을 삭제 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5c2bdeef824bc269671cc5ae926fb77cd5726c58
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850836"
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
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 제거 된 *myDownloadJob* 전송 큐에서 작업 합니다.

```
C:\>bitsadmin /cancel myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)