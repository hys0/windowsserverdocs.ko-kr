---
title: ftp 가져오기
description: Ftp get에 대 한 Windows 명령 항목
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4cc74b56fa849a25ed2f4e4a37d339b1da87c24f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376395"
---
# <a name="ftp-get"></a>ftp: get

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 파일을 로컬 컴퓨터에 복사 합니다.   
## <a name="syntax"></a>구문  
```  
get <remoteFile> [<LocalFile>]  
```  
### <a name="parameters"></a>매개 변수  

|   매개 변수   |                                                              설명                                                               |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------|
| <remoteFile>  |                                                   복사할 원격 파일을 지정 합니다.                                                   |
| [<LocalFile>] | 로컬 컴퓨터에서 사용할 파일의 이름을 지정 합니다. *Localfile* 을 지정 하지 않으면 파일에 *remotefile* 이름이 지정 됩니다. |

## <a name="remarks"></a>설명  
**Get** 명령은 **recv** 명령과 동일 합니다.  
## <a name="BKMK_Examples"></a>예와  
현재 파일 전송 형식을 사용 하 여 로컬 컴퓨터에 **test.txt** 를 복사 합니다.  
```  
get test.txt  
```  
현재 파일 전송 형식을 사용 하 여 **테스트 .txt** 를 로컬 컴퓨터에 **test1** 로 복사 합니다.  
```  
Get test.txt test1.txt  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: 이진](ftp-binary.md)  
-   [명령줄 구문 키](command-line-syntax-key.md)  
