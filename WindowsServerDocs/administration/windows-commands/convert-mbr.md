---
title: convert mbr
description: Mbr (마스터 부트 레코드) 파티션 스타일을 사용 하 여 GPT (GUID 파티션 테이블) 파티션 스타일을 포함 하는 빈 기본 디스크를 기본 디스크로 변환 하는 mbr 변환 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a635a4c0-af73-4330-b021-51d483424537
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 178384ff63267c6ca22069f49b980a316b7695aa
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720765"
---
# <a name="convert-mbr"></a>convert mbr

MBR (마스터 부트 레코드) 파티션 스타일을 사용 하 여 GPT (GUID 파티션 테이블) 파티션 스타일을 포함 하는 빈 기본 디스크를 기본 디스크로 변환 합니다. 이 작업을 수행 하려면 기본 디스크를 선택 해야 합니다. [디스크 선택 명령을](select-disk.md) 사용 하 여 기본 디스크를 선택 하 고 포커스를 이동 합니다.

> [!IMPORTANT]
> 디스크를 기본 디스크로 변환 하려면 비어 있어야 합니다. 데이터를 백업 하 고 디스크를 변환 하기 전에 모든 파티션 또는 볼륨을 삭제 합니다.

> [!NOTE]
> 이 명령을 사용 하는 방법에 대 한 지침은 [GUID 파티션 테이블 디스크를 마스터 부트 레코드 디스크로 변경](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc725797(v=ws.11))을 참조 하세요.

## <a name="syntax"></a>구문

```
convert mbr [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="examples"></a>예

기본 디스크를 gpt 파티션에서에서 MBR 파티션 스타일으로 변환 하려면 다음을 입력 >:

```
convert mbr
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [convert 명령](convert.md)
