---
title: ftp mput_1
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 980f15e7-7cf1-4813-9946-a8cc4edfb198 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6308f7b47d58bc25d964944f96fbc83a26350962
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376210"
---
# <a name="ftp-mput_1"></a>ftp: mput_1

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 컴퓨터에 로컬 파일을 복사 합니다.   
## <a name="syntax"></a>구문  
```  
mput <LocalFile>[ ]  
```  
### <a name="parameters"></a>매개 변수  

|  매개 변수  |                       설명                        |
|-------------|----------------------------------------------------------|
| <LocalFile> | 원격 컴퓨터에 복사할 로컬 파일을 지정 합니다. |

## <a name="BKMK_Examples"></a>예와  
현재 파일 전송 형식을 사용 하 여 **Program1** 및 **program2.c** 을 원격 컴퓨터에 복사 합니다.  
```  
mput Program1.exe Program2.exe  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: 이진](ftp-binary.md)  
-   [명령줄 구문 키](command-line-syntax-key.md)  
