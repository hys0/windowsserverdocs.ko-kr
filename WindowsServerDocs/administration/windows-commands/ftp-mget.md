---
title: ftp mget
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 72b45f84622fcd6abf7a743f606fb514def584cd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843356"
---
# <a name="ftp-mget"></a>ftp: mget

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 파일을 로컬 컴퓨터에 복사 합니다.   
## <a name="syntax"></a>구문  
```  
mget <remoteFile>[ ]  
```  
#### <a name="parameters"></a>매개 변수  

|  매개 변수   |                        설명                        |
|--------------|-----------------------------------------------------------|
| <remoteFile> | 로컬 컴퓨터에 복사할 원격 파일을 지정 합니다. |

## <a name="examples"></a><a name=BKMK_Examples></a>예와  
현재 파일 전송 형식을 사용 하 여 원격 파일을 로컬 **컴퓨터에 복사** 합니다 **.**  
```  
mget a.exe b.exe  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: 이진](ftp-binary.md)  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
