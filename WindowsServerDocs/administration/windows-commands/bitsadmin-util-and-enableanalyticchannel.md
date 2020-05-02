---
title: bitsadmin util and enableanalyticchannel
description: BITS 클라이언트 분석 채널을 사용 하거나 사용 하지 않도록 설정 하는 bitsadmin util 및 enableanalyticchannel 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0d7645aa-b91b-4ed7-b630-a1e1be6f6ae9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c1f5c8c924d1011928aca6ec1bcebd4d71abb015
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707767"
---
# <a name="bitsadmin-util-and-enableanalyticchannel"></a>bitsadmin util and enableanalyticchannel

BITS 클라이언트 분석 채널을 사용 하지 않도록 설정 하거나 사용 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /util /enableanalyticchannel TRUE|FALSE
```

| 매개 변수 | 설명 |
| --------- | ---------- |
| TRUE 또는 FALSE | **TRUE** 로 설정 하면 지정 된 파일에 대 한 콘텐츠 유효성 검사가 설정 되지만 **FALSE** 는 해제 됩니다. |

## <a name="examples"></a>예

BITS 클라이언트 분석 채널을 설정 하거나 해제 합니다.

```
bitsadmin /util / enableanalyticchannel TRUE
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin util 명령](bitsadmin-util.md)

- [bitsadmin 명령](bitsadmin.md)
