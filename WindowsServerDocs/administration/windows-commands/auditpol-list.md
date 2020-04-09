---
title: auditpol 목록
description: Windows 명령 항목에서 감사 정책 범주 및 하위 범주를 나열 하거나 사용자 단위 감사 정책을 정의 하는 사용자를 나열 하는 **auditpol 목록**입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 45502abe-3d6e-4e13-94f0-8e6fcb6db860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e0aff46e62ea4e4259360b78aae223dfcd66ef7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851186"
---
# <a name="auditpol-list"></a>auditpol 목록

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

목록에는 정책 범주 및/또는 하위 범주, 또는 사용자 단위 감사 정책이 정의 되어 대상 목록 사용자가 감사 합니다.

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

## <a name="remarks"></a>주의

사용자 정책에 대 한 모든 목록 작업에 대 한 보안 설명자에 설정 된 해당 개체에 대 한 권한이 읽기 있어야 합니다. 처리 하는 개체로 목록 작업을 수행할 수도 있습니다는 **관리 감사 및 보안 로그** (SeSecurityPrivilege) 사용자 권한이 있습니다. 그러나이 오른쪽 목록 작업을 수행할 필요가 없는 추가 액세스를 허용 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

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
