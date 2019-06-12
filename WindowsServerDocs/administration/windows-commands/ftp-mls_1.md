---
title: ftp mls_1
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4738fd49-0e80-4bdf-a773-0f973db3a710 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a379ead9c56af096e121048a8c0f596f6879bb0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438544"
---
# <a name="ftp-mls1"></a>ftp: mls_1

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 디렉터리에서 파일 및 하위 디렉터리의 간단한 목록을 표시합니다.   
## <a name="syntax"></a>구문  
```  
mls <remoteFile>[ ] <LocalFile>  
```  
### <a name="parameters"></a>매개 변수  

|  매개 변수   |                       설명                       |
|--------------|---------------------------------------------------------|
| <remoteFile> | 목록을 확인 하려면 원하는 파일을 지정 합니다. |
| <LocalFile>  |  목록을 저장할 로컬 파일을 지정 합니다.  |

## <a name="remarks"></a>설명  
- 지정 *remoteFiles*  
  하이픈을 입력 ( **-** ) 원격 컴퓨터의 현재 작업 디렉터리를 사용 하도록 합니다.  
- 지정 *LocalFile*  
  하이픈을 입력 ( **-** ) 화면에 목록을 표시 합니다.  
  ## <a name="BKMK_Examples"></a>예제  
  파일 및 하위 디렉터리에 대 한 간단한 목록을 표시 **dir1** 하 고 **dir2**합니다.  
  ```  
  mls dir1 dir2 -  
  ```  
  파일 및 하위 디렉터리에 대 한 간단한 목록을 저장할 **dir1** 하 고 **dir2** 로컬 파일에 있는 **dirlist.txt**  
  ```  
  mls dir1 dir2 dirlist.txt   
  ```  
  ## <a name="additional-references"></a>추가 참조  
- [명령줄 구문 키](command-line-syntax-key.md)  
