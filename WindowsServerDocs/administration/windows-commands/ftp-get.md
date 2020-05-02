---
title: ftp 가져오기
description: Ftp get에 대 한 참조 항목
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 37423f81fd72e79cebcdf169160ad3e8033b69b2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725292"
---
# <a name="ftp-get"></a>ftp: get

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 파일을 로컬 컴퓨터에 복사 합니다.   
## <a name="syntax"></a>구문  
```  
get <remoteFile> [<LocalFile>]  
```  
#### <a name="parameters"></a>매개 변수  

|   매개 변수   |                                                              설명                                                               |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------|
| <remoteFile>  |                                                   복사할 원격 파일을 지정 합니다.                                                   |
| [<LocalFile>] | 로컬 컴퓨터에서 사용할 파일의 이름을 지정 합니다. *Localfile* 을 지정 하지 않으면 파일에 *remotefile* 이름이 지정 됩니다. |

## <a name="remarks"></a>설명  
**Get** 명령은 **recv** 명령과 동일 합니다.  
## <a name="examples"></a>예  
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
-   - [명령줄 구문 키](command-line-syntax-key.md)  
