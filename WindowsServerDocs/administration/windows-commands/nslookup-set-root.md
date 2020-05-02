---
title: nslookup set root
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d913669fd4fede06c9983756df1bbf626ca430ac
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723575"
---
# <a name="nslookup-set-root"></a>nslookup set root

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

쿼리에 사용 되는 루트 서버 이름을 변경 합니다.
## <a name="syntax"></a>구문
```
set root=<RootServer>
```
### <a name="parameters"></a>매개 변수

|    매개 변수    |                                   설명                                    |
|-----------------|----------------------------------------------------------------------------------|
|  <RootServer>   | 루트 서버에 대 한 새 이름을 지정합니다. 기본값은 ns.nic.ddn.mil 합니다. |
| {도움말 및 #124;?} |              간단한 요약이 표시 되며 **nslookup** 하위 명령입니다.               |

## <a name="remarks"></a>설명
- **세트 루트** 영향을 줌 하위 명령에서 **루트** 하위 명령입니다.
  ## <a name="additional-references"></a>추가 참조
  - [명령줄 구문 키](command-line-syntax-key.md)
  [nslookup 루트](nslookup-root.md)
