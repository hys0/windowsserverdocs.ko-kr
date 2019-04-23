---
title: nslookup set recurse
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1b7a93f-dfb0-4ccd-b230-e0953057fada
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ce2129a455ed5c8c2e4ef9540abb09102db2b5e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859344"
---
# <a name="nslookup-set-recurse"></a>nslookup set recurse



정보가 없는 경우 다른 서버를 쿼리 하는 도메인 이름 시스템 (DNS) 이름 서버를 알려 줍니다.

## <a name="syntax"></a>구문

```
set [no]recurse
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|**norecurse**|다른 서버에 쿼리 정보가 없는 경우에서 도메인 이름 시스템 (DNS) 이름 서버를 중지 합니다.|
|**recurse**|정보가 없는 경우 다른 서버를 쿼리 하는 도메인 이름 시스템 (DNS) 이름 서버를 알려 줍니다. 기본 구문은 **recurse**합니다.|
|{도움말 | ?}|간단한 요약이 표시 되며 **nslookup** 하위 명령입니다.|

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)