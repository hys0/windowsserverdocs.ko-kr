---
title: bitsadmin replaceremoteprefix
description: 필요에 따라 작업의 모든 파일에 대 한 원격 URL을 *oldprefix* 에서 *oldprefix*로 변경 하는 bitsadmin replaceremoteprefix 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2453ac4c223baa049980578c81d9bc6539baac7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927972"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix

필요에 따라 작업의 모든 파일에 대 한 원격 URL을 *oldprefix* 에서 *oldprefix*로 변경 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /replaceremoteprefix <job> <oldprefix> <newprefix>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| oldprefix | 기존 URL 접두사입니다. |
| oldprefix | 새 URL 접두사입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업의 모든 파일에 대 한 원격 URL을에서로 변경 합니다 *http://stageserver* *http://prodserver* .

```
bitsadmin /replaceremoteprefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>추가 정보

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
