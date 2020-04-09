---
title: ftp remotehelp_1
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3c4a4ffec01fce5cde8b2aa9dd1fa0704f3a85ff
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843056"
---
# <a name="ftp-remotehelp_1"></a>ftp: remotehelp_1

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 명령에 대 한 도움말을 표시 합니다.   
## <a name="syntax"></a>구문  
```  
remotehelp [<Command>]  
```  
#### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|[<Command>]|도움말을 원하는 명령의 이름을 지정 합니다. 경우 *명령* 를 지정 하지 않으면 **ftp** 모든 원격 명령 목록이 표시 됩니다.|  
## <a name="remarks"></a>주의  
사용 하 여 원격 명령을 실행 하면 **견적** 또는 **리터럴**합니다.  
## <a name="examples"></a><a name=BKMK_Examples></a>예와  
원격 명령 목록을 표시 합니다.  
```  
remotehelp  
```  
에 대 한 구문을 표시는 **솜씨** 원격 명령입니다.  
```  
remotehelp feat  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: 따옴표](ftp-quote.md)  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
