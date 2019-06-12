---
title: 텔넷 송신
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c217abc-1182-466e-914c-1ff16755021b vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 36dc7f861e88cf991af57dda2f150107c6870f0f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441046"
---
# <a name="telnet-send"></a>텔넷: 보내기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

텔넷 서버에 텔넷 명령을 보냅니다.   
## <a name="syntax"></a>구문  
```  
sen[d] {ao | ayt | brk | esc | ip | synch | <string>} [?]  
```  
### <a name="parameters"></a>매개 변수  

| 매개 변수 |                     설명                      |
|-----------|------------------------------------------------------|
|    ao     |       텔넷 명령을 중단 출력을 보냅니다.        |
|    ayt    |       있습니다에 하는 텔넷 명령을 보냅니다.       |
|    brk    |            텔넷 명령을 brk를 보냅니다.            |
|    esc 키    |      현재 텔넷 이스케이프 문자를 보냅니다.      |
|    ip     |     프로세스를 중단 텔넷 명령을 보냅니다.     |
|   동기화   |           텔넷 명령을 동기화를 보냅니다.           |
| <string>  | 텔넷 서버에 입력 문자열을 보냅니다. |
|     ?     |     이 명령을 사용 하 여 관련 된 도움말을 표시 합니다.      |

## <a name="BKMK_Examples"></a>예제  
Send는 텔넷 서버 수 있습니다.  
```  
sen ayt  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
