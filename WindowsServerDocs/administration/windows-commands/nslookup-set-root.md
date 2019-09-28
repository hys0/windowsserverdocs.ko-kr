---
title: nslookup set root
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08cf41ec9b6ac30699013112216a538dcf625fd5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372841"
---
# <a name="nslookup-set-root"></a>nslookup set root

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

쿼리에 사용 되는 루트 서버의 이름을 변경 합니다.
## <a name="syntax"></a>구문
```
set root=<RootServer>
```
## <a name="parameters"></a>매개 변수

|    매개 변수    |                                   설명                                    |
|-----------------|----------------------------------------------------------------------------------|
|  <RootServer>   | 루트 서버에 대 한 새 이름을 지정합니다. 기본값은 ns.nic.ddn.mil 합니다. |
| {도움말 및 #124;?} |              간단한 요약이 표시 되며 **nslookup** 하위 명령입니다.               |

## <a name="remarks"></a>설명
- **세트 루트** 영향을 줌 하위 명령에서 **루트** 하위 명령입니다.
  ## <a name="additional-references"></a>추가 참조
  [명령줄 구문 키](command-line-syntax-key.md)
  [nslookup root](nslookup-root.md)
