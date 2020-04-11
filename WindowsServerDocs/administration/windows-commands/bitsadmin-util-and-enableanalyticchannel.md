---
title: bitsadmin util 및 enableanalyticchannel
description: BITS 클라이언트 분석 채널을 사용 하거나 사용 하지 않도록 설정 하는 **bitsadmin util 및 enableanalyticchannel**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0d7645aa-b91b-4ed7-b630-a1e1be6f6ae9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8ff1f835415979036fdc0f8aa637fe693e57d46
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122680"
---
# <a name="bitsadmin-util-and-enableanalyticchannel"></a>bitsadmin util 및 enableanalyticchannel

BITS 클라이언트 분석 채널을 사용 하지 않도록 설정 하거나 사용 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /util /enableanalyticchannel TRUE|FALSE
```

| 매개 변수 | 설명 |
| --------- | ---------- |
| TRUE 또는 FALSE | **TRUE** 로 설정 하면 지정 된 파일에 대 한 콘텐츠 유효성 검사가 설정 되지만 **FALSE** 는 해제 됩니다. |

## <a name="examples"></a>예

다음 예에서는 BITS 클라이언트 분석 채널입니다.

```
C:\>bitsadmin /util / enableanalyticchannel TRUE
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)