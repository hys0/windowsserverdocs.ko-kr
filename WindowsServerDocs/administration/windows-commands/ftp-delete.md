---
title: ftp 삭제
description: Ftp 삭제에 대 한 Windows 명령을 항목
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c8af4beb83b789be1456d5556a0aa07749590fb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438719"
---
# <a name="ftp-delete"></a>ftp: 삭제

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 컴퓨터에서 파일을 삭제합니다.   
## <a name="syntax"></a>구문  
```  
delete <remoteFile>  
```  
### <a name="parameters"></a>매개 변수  

|  매개 변수   |          설명          |
|--------------|-------------------------------|
| <remoteFile> | 삭제할 파일을 지정 합니다. |

## <a name="BKMK_Examples"></a>예제  
원격 컴퓨터의 test.txt 파일을 삭제 합니다.  
```  
delete test.txt  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
