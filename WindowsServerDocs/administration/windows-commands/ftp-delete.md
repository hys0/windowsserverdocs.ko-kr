---
title: ftp 삭제
description: Ftp 삭제에 대 한 Windows 명령 항목
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4683e63700a22d8ac8016fb118475a341221e7f6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843566"
---
# <a name="ftp-delete"></a>ftp: 삭제

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 컴퓨터에서 파일을 삭제 합니다.   
## <a name="syntax"></a>구문  
```  
delete <remoteFile>  
```  
#### <a name="parameters"></a>매개 변수  

|  매개 변수   |          설명          |
|--------------|-------------------------------|
| <remoteFile> | 삭제할 파일을 지정 합니다. |

## <a name="examples"></a><a name=BKMK_Examples></a>예와  
원격 컴퓨터에서 test.txt 파일을 삭제 합니다.  
```  
delete test.txt  
```  
## <a name="additional-references"></a>추가 참조  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
