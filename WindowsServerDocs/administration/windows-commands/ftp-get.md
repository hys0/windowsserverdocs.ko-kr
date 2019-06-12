---
title: ftp 가져오기
description: Ftp에 대 한 Windows 명령을 항목 가져오기
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 28961ccf0ae04b52586728f9c68a9b2ca3e69b1d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438771"
---
# <a name="ftp-get"></a>ftp: 가져오기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 유형을 사용 하 여 로컬 컴퓨터에 원격 파일을 복사 합니다.   
## <a name="syntax"></a>구문  
```  
get <remoteFile> [<LocalFile>]  
```  
### <a name="parameters"></a>매개 변수  

|   매개 변수   |                                                              설명                                                               |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------|
| <remoteFile>  |                                                   원격 파일 복사를 지정 합니다.                                                   |
| [<LocalFile>] | 로컬 컴퓨터에서 사용 하 여 파일의 이름을 지정 합니다. 하는 경우 *LocalFile* 지정 하지 않으면 파일 제공할지는 *remoteFile* 이름입니다. |

## <a name="remarks"></a>설명  
**가져옵니다** 명령은 동일 합니다 **recv** 명령입니다.  
## <a name="BKMK_Examples"></a>예제  
복사본 **test.txt** 현재 파일 전송 유형을 사용 하 여 로컬 컴퓨터에 있습니다.  
```  
get test.txt  
```  
복사본 **test.txt** 으로 로컬 컴퓨터로 **test1.txt** 현재 파일을 사용 하 여 전송 형식입니다.  
```  
Get test.txt test1.txt  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: binary](ftp-binary.md)  
-   [명령줄 구문 키](command-line-syntax-key.md)  
