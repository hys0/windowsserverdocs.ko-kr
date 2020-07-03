---
title: auditpol clear
description: 모든 사용자에 대 한 사용자 단위 감사 정책을 삭제 하 고 모든 하위 범주에 대 한 시스템 감사 정책을 다시 설정 (해제) 하며 모든 감사 옵션을 사용 안 함으로 설정 하는 auditpol clear 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 05bfa218-2434-4ad1-b33c-e6fcfb2b4f67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 797f26ab9e191176808bbce917ca5ac0fa3d73a3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923796"
---
# <a name="auditpol-clear"></a>auditpol clear

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

모든 사용자를 다시 설정 (해제) 시스템 감사 정책 모든 하위 범주를 및 모든 감사를 사용 안 함으로 옵션 집합에 대 한 사용자 단위 감사 정책을 삭제 합니다.

*사용자* 및 *시스템* 정책에 대 한 *지우기* 작업을 수행 하려면 보안 설명자에 설정 된 해당 개체에 대 한 **쓰기** 또는 **모든 제어** 권한이 있어야 합니다. **감사 및 보안 로그 관리** (SeSecurityPrivilege) 사용자 권한이 있는 경우에도 *지우기* 작업을 수행할 수 있습니다. 그러나이 권한은 전체 *지우기* 작업을 수행 하는 데 필요 없는 추가 액세스를 허용 합니다.

## <a name="syntax"></a>구문

```
auditpol /clear [/y]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ----------- | --------------- |
| /y | 모든 감사 정책 설정을 지워야 하는 경우를 확인 하는 메시지를 표시 하지 않습니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

모든 사용자에 대 한 사용자 단위 감사 정책을 삭제 하려면 모든 (해제) 시스템 감사 정책 하위 범주를 다시 설정 하 고 모든 감사 정책 설정을 확인 메시지 형식에서 사용 안 함으로 설정 합니다.

```
auditpol /clear
```

모든 사용자에 대 한 사용자 단위 감사 정책을 삭제 하려면 모든 하위 범주에 대 한 시스템 감사 정책 설정을 다시 설정 하 고 모든 감사 정책 설정 유형 확인 메시지 없이 사용 안 함으로 설정:

```
auditpol /clear /y
```

> [!NOTE]
> 앞의 예제는이 작업을 수행 하는 스크립트를 사용 하는 경우에 유용 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [auditpol 명령](auditpol.md)
