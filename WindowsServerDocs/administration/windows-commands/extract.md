---
title: 추출
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 20dab03e-f6e1-4eb8-b8a1-fd6f1d97ee83
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 967f08e271019cc33970419179c9ddbf902b1882
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377265"
---
# <a name="extract"></a>추출



## <a name="syntax"></a>구문

```
EXTRACT [/Y] [/A] [/D | /E] [/L dir] cabinet [filename ...]
EXTRACT [/Y] source [newname]
EXTRACT [/Y] /C source destination
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|캐비닛|파일 두 개 이상의 파일이 포함 되어 있습니다.|
|파일 이름|캐비닛에서 추출 하는 파일의 이름입니다. 여러 파일 이름 (공백으로 구분) 및 와일드 카드를 사용할 수 있습니다.|
|원본|압축된 파일 (하나의 파일 캐비닛)입니다.|
|새 이름|추출 된 파일에 새 파일 이름입니다. 을 제공 하지 않으면 원래 이름이 사용 됩니다.|
|/ A|모든 캐비닛을 처리 합니다. 언급 한 첫 번째 캐비닛에 시작 해 서 캐비닛 체인을 따릅니다.|
|/C|대상 (DMF 디스크에서 복사)을 소스 파일을 복사 합니다.|
|/D|캐비닛 디렉터리 (압축 해제를 방지 하려면 파일 이름으로 사용)을 표시 합니다.|
|/E|Extract (대신를 사용 *합니다.* 파일을 추출 하려면 모든).|
|/L dir|(기본값은 현재 디렉터리)는 압축 푼된 파일을 배치할 위치입니다.|
|/Y|기존 파일 덮어쓰기 전에 표시 되지 않습니다.|

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)