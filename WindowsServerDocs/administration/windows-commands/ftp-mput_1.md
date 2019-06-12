---
title: ftp mput_1
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: dd19a97246aa6155182cb055deceb4b5a5019f6c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438584"
---
# <a name="ftp-mput1"></a>ftp: mput_1

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

형식을 전송 하는 현재 파일을 사용 하 여 원격 컴퓨터에 로컬 파일을 복사 합니다.   
## <a name="syntax"></a>구문  
```  
mput <LocalFile>[ ]  
```  
### <a name="parameters"></a>매개 변수  

|  매개 변수  |                       설명                        |
|-------------|----------------------------------------------------------|
| <LocalFile> | 원격 컴퓨터로 복사 하려면 로컬 파일을 지정 합니다. |

## <a name="BKMK_Examples"></a>예제  
복사본 **Program1.exe** 하 고 **Program2.exe** 현재 파일 전송 유형을 사용 하 여 원격 컴퓨터에 있습니다.  
```  
mput Program1.exe Program2.exe  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: binary](ftp-binary.md)  
-   [명령줄 구문 키](command-line-syntax-key.md)  
