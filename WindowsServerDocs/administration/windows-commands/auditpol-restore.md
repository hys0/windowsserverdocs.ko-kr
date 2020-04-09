---
title: auditpol 복원
description: '**Auditpol 복원**에 대 한 Windows 명령 항목은 시스템 감사 정책 설정, 모든 사용자에 대 한 사용자별 감사 정책 설정 및/backup 옵션에 사용 되는 쉼표로 구분 된 값 (CSV) 파일 형식과 구문적으로 일치 하는 파일의 모든 감사 옵션을 복원 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ad73e520-484f-4cf1-a7f9-ae7488e9edf6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd166ca6f3a268015e5cd25bd1fbdd78e1a9eed7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851166"
---
# <a name="auditpol-restore"></a>auditpol 복원

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

시스템 감사 정책 설정, 모든 사용자 및 모든 감사 옵션에 대 한 사용자 단위 감사 정책 설정을 차례로 사용 하는 쉼표로 구분 된 값 (CSV) 파일 형식을와 구문적으로 일치 하는 파일에서 복원 하는 옵션입니다.

## <a name="syntax"></a>구문

```
auditpol /restore /file:<filename>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ------- | -------- |
| /file | 감사 정책을 복원할 파일을 지정 합니다. 파일에서 차례로 사용 하 여 만든 것 이어야 옵션을 선택 하거나 구문상와 일치 해야는 /backup에서 사용 하는 CSV 파일 형식 옵션입니다. |
| /? |명령 프롬프트에 도움말을 표시합니다. |

## <a name="remarks"></a>주의

사용자 정책 및 시스템 정책에 대 한 복원 작업에 대 한 작성 한 해야 하거나 보안 설명자에 있는 해당 개체에 대 한 모든 권한을 설정 합니다. 소유 하 여 복원 작업을 수행할 수도 있습니다는 **관리 감사 및 보안 로그** (SeSecurityPrivilege) 사용자 권한이 있습니다. SeSecurityPrivilege 의도 하지 않은 오류 또는 악의적인 공격이 발생할 경우의 보안 설명자를 복원 하는 경우에 유용 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

시스템 감사 정책 설정, 모든 사용자에 대 한 사용자 단위 감사 정책 설정 및/backup 명령을 사용 하 여 만든 auditpolicy .csv 라는 파일의 모든 감사 옵션을 복원 하려면 다음을 입력 합니다.

```
auditpol /restore /file:c:\auditpolicy.csv
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [auditpol 백업](auditpol-backup.md) '    '    