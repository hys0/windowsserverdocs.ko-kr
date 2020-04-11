---
title: bitsadmin setnotifyflags
description: '**Bitsadmin setnotifyflags**에 대 한 Windows 명령 항목으로, 지정 된 작업에 대 한 이벤트 알림 플래그를 설정 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73c088ce2bae8d2ad99b313417c14449ddd822b5
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122794"
---
# <a name="bitsadmin-setnotifyflags"></a>bitsadmin setnotifyflags

이벤트가 지정된 된 작업에 대 한 알림 플래그를 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setnotifyflags <job> <notifyflags>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| notifyflags | 다음과 같은 알림 플래그 중 하나 이상을 포함할 수 있습니다.<ul><li>**1.** 작업의 모든 파일이 전송 되 면 이벤트를 생성 합니다.</li><li>**2.** 오류가 발생 하면 이벤트를 생성 합니다.</li><li>**3.** 모든 파일 전송이 완료 되거나 오류가 발생할 때 이벤트를 생성 합니다.</li><li>**4.** 알림을 사용 하지 않도록 설정 합니다.</li></ul> |

## <a name="examples"></a>예

다음 예에서는 *Mydownloadjob*이라는 작업에 대해 오류가 발생할 때 이벤트를 생성 하도록 알림 플래그를 설정 합니다.

```
C:\>bitsadmin /setnotifyflags myDownloadJob 2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)