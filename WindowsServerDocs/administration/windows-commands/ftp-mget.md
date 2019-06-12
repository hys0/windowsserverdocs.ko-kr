---
title: ftp mget
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e43bf8b6e7067a31b3ec51336b0b43845ab88f63
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438607"
---
# <a name="ftp-mget"></a>ftp: mget

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일을 사용 하 여 로컬 컴퓨터에 원격 파일 복사 전송 형식입니다.   
## <a name="syntax"></a>구문  
```  
mget <remoteFile>[ ]  
```  
### <a name="parameters"></a>매개 변수  

|  매개 변수   |                        설명                        |
|--------------|-----------------------------------------------------------|
| <remoteFile> | 로컬 컴퓨터에 복사 하려면 원격 파일을 지정 합니다. |

## <a name="BKMK_Examples"></a>예제  
원격 파일 복사 **a.exe** 하 고 **b.exe** 현재 파일 전송 유형을 사용 하 여 로컬 컴퓨터에 있습니다.  
```  
mget a.exe b.exe  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: binary](ftp-binary.md)  
-   [명령줄 구문 키](command-line-syntax-key.md)  
