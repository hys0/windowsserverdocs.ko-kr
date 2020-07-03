---
title: reg
description: 레지스트리 하위 키 정보 및 레지스트리 항목의 값에 대 한 작업을 수행 하는 reg 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c97496b2-d1ff-4887-b5d2-6e1524be465a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 47ceea315b3d172c766e749e3447f56907eab945
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931023"
---
# <a name="reg"></a>reg

레지스트리 항목의 값과 레지스트리 하위 키 정보에 대 한 작업을 수행합니다.

일부 작업을 통해 로컬 컴퓨터 또는 원격 컴퓨터에서 레지스트리 항목을 보거나 구성할 수 있으며, 다른 작업을 통해 로컬 컴퓨터만 구성할 수 있습니다. 사용 하 여 **reg** 제한 일부 작업에서 사용할 수 있는 매개 변수를 컴퓨터의 원격 레지스트리를 구성 합니다. 각 작업에 대 한 구문 및 매개 변수를 확인 하 여 원격 컴퓨터에서 사용할 수 있는지 확인 합니다.

> [!CAUTION]
> 대안이 없는 한 레지스트리를 직접 편집 하지 마십시오. 레지스트리 편집기의 성능이 저하, 하면 시스템이 손상 또는 Windows를 다시 설치 해야 할 수 있는 설정을 허용 표준 보호를 무시 합니다. 안전 하 게 제어판 또는 Microsoft Management Console (MMC)에서 프로그램을 사용 하 여 대부분의 레지스트리 설정을 변경할 수 있습니다. 레지스트리를 직접 편집 해야 하는 경우 먼저 백업 합니다.

## <a name="syntax"></a>구문

```
reg add
reg compare
reg copy
reg delete
reg export
reg import
reg load
reg query
reg restore
reg save
reg unload
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| [reg add](reg-add.md) | 새 하위 키 또는 항목을 레지스트리에 추가합니다. |
| [reg compare](reg-compare.md) | 비교 하 여 레지스트리 하위 키 또는 항목을 지정 합니다. |
| [reg copy](reg-copy.md) | 로컬 또는 원격 컴퓨터의 지정된 된 위치에 레지스트리 항목을 복사합니다. |
| [reg delete](reg-delete.md) | 레지스트리에서 하위 키 또는 항목을 삭제합니다. |
| [reg export](reg-export.md) | 다른 서버에 전송 하기 위해서는 파일에 지정 된 하위 키, 항목 및 로컬 컴퓨터의 값을 복사합니다. |
| [reg import](reg-import.md) | 포함 된 파일의 내용을 복사 하는 로컬 컴퓨터의 레지스트리로 레지스트리 하위 키, 항목 및 값을 내보냅니다. |
| [reg load](reg-load.md) | 쓰기 레지스트리에 하위 키와 다른 하위 키에 대 한 항목을 저장 합니다. |
| [reg query](reg-query.md) | 다음 계층의 하위 키와 레지스트리에 지정된 된 하위 키 아래에 있는 항목의 목록을 반환 합니다. |
| [reg restore](reg-restore.md) | 쓰기 저장 된 하위 키와 항목 레지스트리를 백업합니다. |
| [reg save](reg-save.md) | 지정된 된 파일에 지정 된 하위 키, 항목 및 레지스트리 값의 복사본을 저장합니다. |
| [reg unload](reg-unload.md) | 사용 하 여 로드 레지스트리의 섹션을 제거는 **reg 부하** 작업 합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
