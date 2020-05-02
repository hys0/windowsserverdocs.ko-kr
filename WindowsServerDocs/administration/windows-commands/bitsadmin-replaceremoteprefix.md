---
title: bitsadmin replaceremoteprefix
description: 필요에 따라 작업의 모든 파일에 대 한 원격 URL을 *oldprefix* 에서 *oldprefix*로 변경 하는 bitsadmin replaceremoteprefix 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 745d026513413db799e86df3422d5ee19c89274f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717032"
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

*Mydownloadjob*이라는 작업의 모든 파일에 대 한 원격 URL을에서 *http://stageserver* 로 *http://prodserver*변경 합니다.

```
bitsadmin /replaceremoteprefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>추가 정보

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
