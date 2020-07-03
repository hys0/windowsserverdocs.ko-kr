---
title: auditpol list
description: 감사 정책 범주 및 하위 범주를 나열 하거나 사용자 단위 감사 정책을 정의한 사용자를 나열 하는 auditpol list 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 45502abe-3d6e-4e13-94f0-8e6fcb6db860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a0ce67b9907fa4c5207d75422dc972d70f5e6eea
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923716"
---
# <a name="auditpol-list"></a>auditpol list

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

감사 정책 범주 및 하위 범주를 나열 하거나 사용자 단위 감사 정책을 정의한 사용자를 나열 합니다.

*사용자별* 정책에 대해 *목록* 작업을 수행 하려면 보안 설명자에 설정 된 해당 개체에 대 한 **읽기** 권한이 있어야 합니다. **감사 및 보안 로그 관리** (SeSecurityPrivilege) 사용자 권한이 있는 경우에도 *목록* 작업을 수행할 수 있습니다. 그러나이 권한은 전체 *목록* 작업을 수행할 필요가 없는 추가 액세스를 허용 합니다.

## <a name="syntax"></a>구문

```
auditpol /list
[/user|/category|subcategory[:<categoryname>|<{guid}>|*]]
[/v] [/r]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ------- | -------- |
| /user | 사용자 단위 감사 정책에 정의 된 모든 사용자를 검색 합니다. /V 매개 변수를 사용할 경우 사용자의 보안 식별자 (SID)도 표시 됩니다. |
| /category | 시스템에서 인식 하는 범주의 이름을 표시 합니다. /V 매개 변수를 사용할 경우 범주 전역 고유 식별자 (GUID)도 표시 됩니다. |
| /subcategory | 하위 범주 및 관련된 GUID가의 이름을 표시합니다. |
| /v | 범주 또는 하위 범주, GUID 또는 /user와 함께 사용 하는 경우 각 사용자의 SID를 표시 합니다. |
| /r | 보고서를 쉼표로 구분 된 값 (CSV) 형식으로 출력을 표시합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

정의 된 감사 정책에 있는 모든 사용자를 나열 하려면 다음을 입력 합니다.

```
auditpol /list /user
```

정의 된 감사 정책 및 연결 된 해당 SID를 가진 모든 사용자를 나열 하려면 다음을 입력 합니다.

```
auditpol /list /user /v
```

모든 범주 및 하위 보고서 형식에서를 나열 하려면 다음을 입력 합니다.

```
auditpol /list /subcategory:* /r
```

자세한 추적 및 DS 액세스 범주의 하위 범주를 나열 하려면 다음을 입력 합니다.

```
auditpol /list /subcategory:detailed Tracking,DS Access
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [auditpol 명령](auditpol.md)
