---
title: ftp 추가
description: Ftp 추가에 대 한 참조 항목
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b53228473b8ea16a0955c244d60fae77cf4f7d7f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725400"
---
# <a name="ftp-append"></a>ftp: 추가

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 형식 설정을 사용 하 여 원격 컴퓨터의 파일에 로컬 파일을 추가 합니다.   
## <a name="syntax"></a>구문  
```  
append <LocalFile> [remoteFile]  
```  
#### <a name="parameters"></a>매개 변수  

|  매개 변수   |                               설명                                |
|--------------|--------------------------------------------------------------------------|
| <LocalFile>  |                     추가할 로컬 파일을 지정 합니다.                     |
| RemoteFile | 원격 컴퓨터에서 파일을 지정 <LocalFile> 추가 됩니다. |

## <a name="remarks"></a>설명  
*Remotefile* 을 생략 하면 원격 파일 이름 대신 *localfile* 이름이 사용 됩니다.  
## <a name="examples"></a>예  
원격 컴퓨터의 file2에 file1을 추가 합니다.  
```  
append file1.txt file2.txt  
```  
원격 컴퓨터의 파일 이름에 로컬 파일 이름 .txt를 추가 합니다.  
```  
append file1.txt  
```  
## <a name="additional-references"></a>추가 참조  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
