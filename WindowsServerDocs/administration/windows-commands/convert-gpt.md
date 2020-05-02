---
title: convert gpt
description: Gpt 변환 명령에 대 한 참조 항목-MBR (마스터 부트 레코드) 파티션 스타일로 빈 기본 디스크를 GPT (GUID 파티션 테이블) 파티션 스타일을 사용 하는 기본 디스크로 변환 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b3b1b747-0a7a-4be2-8487-2c4be16ee190
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 25b28473716037235a70e05835e23790f93164a1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720774"
---
# <a name="convert-gpt"></a>convert gpt

MBR (마스터 부트 레코드) 파티션 스타일을 사용 하는 빈 기본 디스크를 GPT (GUID 파티션 테이블) 파티션 스타일을 사용 하는 기본 디스크로 변환 합니다. 이 작업을 수행 하려면 기본 MBR 디스크를 선택 해야 합니다. [디스크 선택 명령을](select-disk.md) 사용 하 여 기본 디스크를 선택 하 고 포커스를 이동 합니다.

> [!IMPORTANT]
> 디스크를 기본 디스크로 변환 하려면 비어 있어야 합니다. 데이터를 백업 하 고 디스크를 변환 하기 전에 모든 파티션 또는 볼륨을 삭제 합니다. GPT 변환할은 필요한 최소 디스크 크기는 128mb입니다.

> [!NOTE]
> 이 명령을 사용 하는 방법에 대 한 지침은 [마스터 부트 레코드 디스크를 GUID 파티션 테이블 디스크로 변경](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc725671(v=ws.11))을 참조 하세요.

## <a name="syntax"></a>구문

```
convert gpt [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="examples"></a>예

기본 디스크를 MBR 파티션 형식을에서 GPT 파티션 스타일으로 변환 하려면 다음을 입력 합니다.

```
convert gpt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [convert 명령](convert.md)
