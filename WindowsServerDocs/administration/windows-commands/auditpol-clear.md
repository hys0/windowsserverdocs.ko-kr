---
title: auditpol 지우기
description: Windows 명령 항목-모든 사용자에 대 한 사용자 단위 감사 정책을 삭제 하 고 모든 하위 범주에 대 한 시스템 감사 정책을 다시 설정 (해제) 하며 모든 감사 옵션을 사용 안 **함으로 설정**합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 05bfa218-2434-4ad1-b33c-e6fcfb2b4f67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 971f4ba54d787be29cb9e7d710f556c50c69a8dc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851206"
---
# <a name="auditpol-clear"></a>auditpol 지우기

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

모든 사용자를 다시 설정 (해제) 시스템 감사 정책 모든 하위 범주를 및 모든 감사를 사용 안 함으로 옵션 집합에 대 한 사용자 단위 감사 정책을 삭제 합니다.

## <a name="syntax"></a>구문

```
auditpol /clear [/y]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ----------- | --------------- |
| /y | 모든 감사 정책 설정을 지워야 하는 경우를 확인 하는 메시지를 표시 하지 않습니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="remarks"></a>주의

사용자 정책 및 시스템 정책에 대 한 일반 작업에 대 한 작성 한 해야 하거나 보안 설명자에 있는 해당 개체에 대 한 모든 권한을 설정 합니다. 처리 하는 개체로 지우기 작업을 수행할 수도 있습니다는 **관리 감사 및 보안 로그** (SeSecurityPrivilege) 사용자 권한이 있습니다. 그러나이 권한을 지우기 작업을 수행할 필요가 없는 추가 액세스를 허용 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

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
