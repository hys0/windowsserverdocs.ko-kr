---
title: ftp mdelete_1
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f578a50207439f9bfb21c2607f0aa60a20fad292
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725034"
---
# <a name="ftp-mdelete_1"></a>ftp: mdelete_1

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 컴퓨터에서 파일을 삭제 합니다.   
## <a name="syntax"></a>구문  
```  
mdelete <remoteFile>[ ]  
```  
#### <a name="parameters"></a>매개 변수  

|  매개 변수   |             설명              |
|--------------|--------------------------------------|
| <remoteFile> | 삭제할 원격 파일을 지정 합니다. |

## <a name="examples"></a>예  
원격 파일을 삭제 합니다 **. .exe** 및 **b. .exe**.  
```  
mdelete a.exe b.exe  
```  
## <a name="additional-references"></a>추가 참조  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
