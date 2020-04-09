---
title: ftp literal_1
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fb81aa2d-07fa-4e79-bf44-1fb5526fdf14 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f502bb56c94734870962f56cfb85dcc17ddc3f93
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843396"
---
# <a name="ftp-literal_1"></a>ftp: literal_1

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012는 축 자 인수를 원격 ftp 서버에 보냅니다. 단일 ftp 회신 코드가 반환 됩니다.   

## <a name="syntax"></a>구문  
```  
literal <Argument> [ ]  
```  
#### <a name="parameters"></a>매개 변수  

| 매개 변수  |                    설명                    |
|------------|---------------------------------------------------|
| <Argument> | Ftp 서버에 보낼 인수를 지정 합니다. |

## <a name="remarks"></a>주의  
**리터럴** 명령은 **quote** 명령과 동일 합니다.  
## <a name="examples"></a><a name=BKMK_Examples></a>예와  
**Quit** 명령을 원격 ftp 서버에 보냅니다.  
```  
literal quit  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: 따옴표](ftp-quote.md)  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
