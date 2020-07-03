---
title: bitsadmin resume
description: 전송 큐에서 새 작업이 나 일시 중단 된 작업을 활성화 하는 bitsadmin resume 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd2a8dcb486c584ef4adaf96a5288a9db32d4553
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927968"
---
# <a name="bitsadmin-resume"></a>bitsadmin resume

전송 큐에 새로운 또는 일시 중단 된 작업을 활성화합니다. 실수로 작업을 다시 시작 하거나 작업을 일시 중단 해야 하는 경우 [bitsadmin suspend](bitsadmin-suspend.md) 스위치를 사용 하 여 작업을 일시 중단할 수 있습니다.

## <a name="syntax"></a>구문

```
bitsadmin /resume <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업을 다시 시작 하려면 다음을 수행 합니다.

```
bitsadmin /resume myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin suspend 명령](bitsadmin-suspend.md)

- [bitsadmin 명령](bitsadmin.md)
