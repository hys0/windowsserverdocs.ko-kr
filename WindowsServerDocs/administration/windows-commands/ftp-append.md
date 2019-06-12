---
title: ftp 추가
description: 'Ftp에 대 한 Windows 명령을 항목 추가 '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9580d725120bb32a9b915d37cdbc173bfb17b859
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438847"
---
# <a name="ftp-append"></a>ftp: 추가

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 형식 설정을 사용 하 여 원격 컴퓨터의 파일에 로컬 파일을 추가 합니다.   
## <a name="syntax"></a>구문  
```  
append <LocalFile> [remoteFile]  
```  
### <a name="parameters"></a>매개 변수  

|  매개 변수   |                               설명                                |
|--------------|--------------------------------------------------------------------------|
| <LocalFile>  |                     추가할 로컬 파일을 지정 합니다.                     |
| [remoteFile] | 원격 컴퓨터에서 파일을 지정 <LocalFile> 추가 됩니다. |

## <a name="remarks"></a>설명  
하는 경우 *remoteFile* 생략 되 면 합니다 *LocalFile* 이름은 원격 파일 이름 대신 사용 됩니다.  
## <a name="BKMK_Examples"></a>예제  
원격 컴퓨터에서 file2.txt을 file1.txt를 추가 합니다.  
```  
append file1.txt file2.txt  
```  
원격 컴퓨터에서 file1.txt 라는 파일을 로컬 file1.txt를 추가 합니다.  
```  
append file1.txt  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
