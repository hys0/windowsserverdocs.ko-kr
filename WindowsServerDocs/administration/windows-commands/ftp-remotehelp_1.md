---
title: ftp remotehelp_1
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd64af157f7ce05330cdafe6e4db6787fa765859
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889594"
---
# <a name="ftp-remotehelp1"></a>ftp: remotehelp_1

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 명령에 대 한 도움말을 표시 합니다.   
## <a name="syntax"></a>구문  
```  
remotehelp [<Command>]  
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|[<Command>]|도움말을 원하는 명령의 이름을 지정 합니다. 경우 *명령* 를 지정 하지 않으면 **ftp** 모든 원격 명령 목록이 표시 됩니다.|  
## <a name="remarks"></a>설명  
사용 하 여 원격 명령을 실행 하면 **견적** 또는 **리터럴**합니다.  
## <a name="BKMK_Examples"></a>예제  
원격 명령 목록을 표시 합니다.  
```  
remotehelp  
```  
에 대 한 구문을 표시는 **솜씨** 원격 명령입니다.  
```  
remotehelp feat  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: quote](ftp-quote.md)  
-   [명령줄 구문 키](command-line-syntax-key.md)  
