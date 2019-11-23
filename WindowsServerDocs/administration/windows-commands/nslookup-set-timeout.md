---
title: nslookup set timeout
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07afdaf4-ffec-496f-a188-4e91cf1a28f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 32fcfcaeccb6599e9aaca21f9c085bb00857479c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372761"
---
# <a name="nslookup-set-timeout"></a>nslookup set timeout

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

조회 요청에 대 한 회신을 대기 하는 초기 시간 (초)을 변경 합니다.
## <a name="syntax"></a>구문
```
set timeout=<Number>
```
## <a name="parameters"></a>매개 변수

|    매개 변수    |                                           설명                                            |
|-----------------|--------------------------------------------------------------------------------------------------|
|    <Number>     | 회신을 기다릴 시간 (초) 수를 지정 합니다. 대기 시간 (초) 기본값은 5입니다. |
| {도움말 및 #124;?} |                      간단한 요약이 표시 되며 **nslookup** 하위 명령입니다.                       |

## <a name="remarks"></a>설명
- 요청에 대 한 회신 된 지정 된 시간 안에 수신 되지 않으면, 제한 시간을 두 배로 증가 하 고 요청 다시 전송 됩니다. 사용할 수는 **집합 재시도** 재시도 횟수를 제어 하는 명령입니다.
  ## <a name="BKMK_examples"></a>예와
  다음 예에서는 2 초에 대 한 응답의 제한 시간을 설정 합니다.
  ```
  set timeout=2
  ```
  ## <a name="additional-references"></a>추가 참조
  [명령줄 구문 키](command-line-syntax-key.md)
  [nslookup 설정 다시 시도](nslookup-set-retry.md)
