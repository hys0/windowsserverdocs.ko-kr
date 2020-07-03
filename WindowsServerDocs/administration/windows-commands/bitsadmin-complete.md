---
title: bitsadmin complete
description: 작업을 완료 하는 bitsadmin complete 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08fb74690f5a8f70611bb6ca52a291bec89d81e8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928357"
---
# <a name="bitsadmin-complete"></a>bitsadmin complete

작업을 완료합니다. 전송 된 상태로 이동 작업 후에이 스위치를 사용 합니다. 그렇지 않으면 성공적으로 전송 된 파일만 사용할 수 있습니다.

## <a name="syntax"></a>구문

```
bitsadmin /complete <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="example"></a>예제

상태에 도달한 후 *Mydownloadjob* 작업을 완료 하려면 다음을 수행 합니다 `TRANSFERRED` .

```
bitsadmin /complete myDownloadJob
```

여러 작업에서 *Mydownloadjob* 을 이름으로 사용 하는 경우 작업의 GUID를 사용 하 여 완료를 위해 고유 하 게 식별 해야 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
