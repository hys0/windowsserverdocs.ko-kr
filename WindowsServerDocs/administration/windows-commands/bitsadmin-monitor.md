---
title: bitsadmin monitor
description: '**Bitsadmin 모니터**에 대 한 Windows 명령 항목으로, 현재 사용자가 소유 하는 전송 큐의 작업을 모니터링 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bda268afd5fda24bba2afb04b32bac9cda9a05bb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850216"
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
| /allusers | (선택 사항) 모든 사용자에 대 한 작업을 모니터링 합니다. 이 매개 변수를 사용 하려면 관리자 권한이 있어야 합니다. |
| /새로 고침 | (선택 사항) `<seconds>`에 지정 된 간격으로 데이터를 새로 고칩니다. 기본 새로 고침 간격은 5 초입니다. 새로 고침을 중지 하려면 CTRL + C를 누릅니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 현재 사용자가 소유한 작업에 대 한 전송 큐를 모니터링 하 고 60 초 마다 정보를 새로 고칩니다.

```
C:\>bitsadmin /monitor /refresh 60
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)