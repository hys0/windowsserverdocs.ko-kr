---
title: bitsadmin setnotifyflags
description: 지정 된 작업에 대 한 이벤트 알림 플래그를 설정 하는 bitsadmin setnotifyflags 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 00b704bf0943790ef01bbfbdbcbbde4dfd1845c6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717277"
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
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| notifyflags | 다음과 같은 알림 플래그 중 하나 이상을 포함할 수 있습니다.<ul><li>**1.** 작업의 모든 파일이 전송 되 면 이벤트를 생성 합니다.</li><li>**2.** 오류가 발생 하면 이벤트를 생성 합니다.</li><li>**3.** 모든 파일 전송이 완료 되거나 오류가 발생할 때 이벤트를 생성 합니다.</li><li>**4.** 알림을 사용 하지 않도록 설정 합니다.</li></ul> |

## <a name="examples"></a>예

오류가 발생할 때 이벤트를 생성 하도록 알림 플래그를 설정 하려면 *Mydownloadjob*이라는 작업에 대해 다음을 수행 합니다.

```
bitsadmin /setnotifyflags myDownloadJob 2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
