---
title: convert
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae151297-af21-4701-bd69-21d775518e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d78f7adbc26acf9787ad39019e1450542a6acda2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379032"
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

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[기본 변환](convert-basic.md)|빈 동적 디스크를 기본 디스크로 변환합니다.|
|[동적 변환](convert-dynamic.md)|기본 디스크를 동적 디스크로 변환합니다.|
|[Gpt 변환](convert-gpt.md)|MBR (마스터 부트 레코드) 파티션 스타일을 사용 하는 빈 기본 디스크를 GPT (GUID 파티션 테이블) 파티션 스타일을 사용 하는 기본 디스크로 변환 합니다.|
|[Mbr 변환](convert-mbr.md)|MBR (마스터 부트 레코드) 파티션 스타일을 사용 하 여 GPT (GUID 파티션 테이블) 파티션 스타일을 포함 하는 빈 기본 디스크를 기본 디스크로 변환 합니다.|

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

