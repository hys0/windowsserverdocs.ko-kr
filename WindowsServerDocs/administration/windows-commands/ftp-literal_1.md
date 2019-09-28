---
title: ftp literal_1
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fb81aa2d-07fa-4e79-bf44-1fb5526fdf14 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 393dea27e8567a72a5bd25c927282ade93e317c9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376266"
---
# <a name="ftp-literal_1"></a>ftp: literal_1

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012는 축 자 인수를 원격 ftp 서버에 보냅니다. 단일 ftp 회신 코드가 반환 됩니다.   

## <a name="syntax"></a>구문  
```  
literal <Argument> [ ]  
```  
### <a name="parameters"></a>매개 변수  

| 매개 변수  |                    설명                    |
|------------|---------------------------------------------------|
| <Argument> | Ftp 서버에 보낼 인수를 지정 합니다. |

## <a name="remarks"></a>설명  
**리터럴** 명령은 **quote** 명령과 동일 합니다.  
## <a name="BKMK_Examples"></a>예와  
**Quit** 명령을 원격 ftp 서버에 보냅니다.  
```  
literal quit  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: 따옴표](ftp-quote.md)  
-   [명령줄 구문 키](command-line-syntax-key.md)  
