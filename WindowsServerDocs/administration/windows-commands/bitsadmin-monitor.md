---
title: bitsadmin monitor
description: 현재 사용자가 소유 하는 전송 큐의 작업을 모니터링 하는 bitsadmin monitor 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7ce08eccf46fc17086d216bc6797bec451ace7eb
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926491"
---
# <a name="bitsadmin-monitor"></a>bitsadmin monitor

현재 사용자가 소유 하는 전송 큐의 작업을 모니터링 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /monitor [/allusers] [/refresh <seconds>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| /allusers | 선택 사항입니다. 모든 사용자에 대 한 작업을 모니터링 합니다. 이 매개 변수를 사용 하려면 관리자 권한이 있어야 합니다. |
| /새로 고침 | 선택 사항입니다. 로 지정 된 간격으로 데이터를 새로 고칩니다 `<seconds>` . 기본 새로 고침 간격은 5 초입니다. 새로 고침을 중지 하려면 CTRL + C를 누릅니다. |

## <a name="examples"></a>예

현재 사용자가 소유 하 고 있는 작업에 대 한 전송 큐를 모니터링 하 고 60 초 마다 정보를 새로 고칩니다.

```
bitsadmin /monitor /refresh 60
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
