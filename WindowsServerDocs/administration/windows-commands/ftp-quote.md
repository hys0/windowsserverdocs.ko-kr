---
title: ftp 견적
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4500a1d3-c091-42c7-a909-f61df7f2e993 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1bf13704150d602fbfa4e3b1a3fb1774d3bf7363
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843036"
---
# <a name="ftp-quote"></a>ftp: 따옴표

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

축 자 인수를 원격 ftp 서버에 보냅니다. 단일 ftp 회신 코드가 반환 됩니다.   
## <a name="syntax"></a>구문  
```  
quote <Argument>[ ]  
```  
#### <a name="parameters"></a>매개 변수  

| 매개 변수  |                    설명                    |
|------------|---------------------------------------------------|
| <Argument> | Ftp 서버에 보낼 인수를 지정 합니다. |

## <a name="remarks"></a>주의  
**견적** 명령은 동일 합니다는 **리터럴** 명령입니다.  
## <a name="examples"></a><a name=BKMK_Examples></a>예와  
**Quit** 명령을 원격 ftp 서버에 보냅니다.  
```  
quote quit  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: literal_1](ftp-literal_1.md)  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
