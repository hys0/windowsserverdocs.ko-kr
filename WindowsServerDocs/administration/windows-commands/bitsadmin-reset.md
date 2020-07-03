---
title: bitsadmin reset
description: 현재 사용자가 소유한 전송 큐의 모든 작업을 취소 하는 bitsadmin reset 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0e4f9d1d-072c-493f-8d7a-f6d713c3ef29
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc8faf10f991f06609d653c8cb7a1dc89de2fa8a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926397"
---
# <a name="bitsadmin-reset"></a>bitsadmin reset

현재 사용자가 소유 하 고 있는 전송 큐의 모든 작업을 취소 합니다. 로컬 시스템에서 만든 작업은 다시 설정할 수 없습니다. 대신 관리자 이며 작업 스케줄러를 사용 하 여 로컬 시스템 자격 증명을 사용 하 여이 명령을 작업으로 예약 해야 합니다.

> [!NOTE]
> BITSAdmin 1.5 이전 버전에서 관리자 권한이 있는 경우/reset 스위치는 큐에 있는 모든 작업을 취소 합니다. 또한/allusers 옵션은 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /reset [/allusers]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| /allusers | 선택 사항입니다. 현재 사용자가 소유 하 고 있는 큐의 모든 작업을 취소 합니다. 이 매개 변수를 사용 하려면 관리자 권한이 있어야 합니다. |

## <a name="examples"></a>예

현재 사용자에 대 한 전송 큐의 모든 작업을 취소 합니다.

```
bitsadmin /reset
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
