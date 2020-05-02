---
title: bitsadmin suspend
description: 지정 된 작업을 일시 중단 하는 bitsadmin suspend 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f9d42500-7bea-4aa8-a9f0-c22f6ed3e73b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8117cf9f4286994847e53dca8065da6821d47c5d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720447"
---
# <a name="bitsadmin-suspend"></a>bitsadmin suspend

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 작업을 일시 중단합니다. 작업을 실수로 일시 중단 한 경우 [bitsadmin resume](bitsadmin-resume.md) 스위치를 사용 하 여 작업을 다시 시작할 수 있습니다.

## <a name="syntax"></a>구문

```
bitsadmin /suspend <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ---------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="example"></a>예제

*Mydownloadjob*이라는 작업을 일시 중지 하려면:


```
bitsadmin /suspend myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin resume 명령](bitsadmin-resume.md)

- [bitsadmin 명령](bitsadmin.md)
