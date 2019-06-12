---
title: ftp mdelete_1
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7b342f9d728e91085d5edf2f8e1ece00b48bec8d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438323"
---
# <a name="ftp-mdelete1"></a>ftp: mdelete_1

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 컴퓨터에서 파일을 삭제합니다.   
## <a name="syntax"></a>구문  
```  
mdelete <remoteFile>[ ]  
```  
### <a name="parameters"></a>매개 변수  

|  매개 변수   |             설명              |
|--------------|--------------------------------------|
| <remoteFile> | 삭제할 원격 파일을 지정 합니다. |

## <a name="BKMK_Examples"></a>예제  
원격 파일을 삭제할 **a.exe** 하 고 **b.exe**합니다.  
```  
mdelete a.exe b.exe  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
