---
title: convert
description: 디스크를 디스크 유형 간에 변환 하는 변환 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ae151297-af21-4701-bd69-21d775518e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f93f2b16838a6f54af3f28b7e0883808a6cd013a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928906"
---
# <a name="convert"></a>convert

다른 하나의 디스크 종류에서 디스크를 변환합니다.

## <a name="syntax"></a>구문

```
convert basic
convert dynamic
convert gpt
convert mbr
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| [기본 변환 명령](convert-basic.md) | 빈 동적 디스크를 기본 디스크로 변환합니다. |
| [동적 명령 변환](convert-dynamic.md) | 기본 디스크를 동적 디스크로 변환합니다. |
| [gpt 변환 명령](convert-gpt.md) | MBR (마스터 부트 레코드) 파티션 스타일을 사용 하는 빈 기본 디스크를 GPT (GUID 파티션 테이블) 파티션 스타일을 사용 하는 기본 디스크로 변환 합니다. |
| [mbr 명령 변환](convert-mbr.md) | MBR (마스터 부트 레코드) 파티션 스타일을 사용 하 여 GPT (GUID 파티션 테이블) 파티션 스타일을 포함 하는 빈 기본 디스크를 기본 디스크로 변환 합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
