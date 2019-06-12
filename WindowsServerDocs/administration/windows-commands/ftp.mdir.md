---
title: ftp mdir
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90eec45b-558b-4b8d-bbe4-b56d98e1ca70 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4ec445c3e367a46dc40d10a37c0b3b8e53a10e3
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438334"
---
# <a name="ftp-mdir"></a>ftp: mdir

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 디렉터리에서 파일 및 하위 디렉터리의 디렉터리 목록을 표시합니다.   
## <a name="syntax"></a>구문  
```  
mdir <remoteFile>[ ] <LocalFile>  
```  
### <a name="parameters"></a>매개 변수  

|  매개 변수   |                               설명                                |
|--------------|--------------------------------------------------------------------------|
| <remoteFile> |   목록이 표시 하려는 디렉터리 또는 파일을 지정 합니다.   |
| <LocalFile>  | 목록을 저장할 로컬 파일을 지정 합니다. 이 매개 변수는 필수적 요소입니다. |

## <a name="remarks"></a>설명  
- 사용할 수 있습니다 **mdir** 여러 파일을 지정 합니다.  
- 지정 *remoteFile*  
  하이픈을 입력 ( **-** ) 원격 컴퓨터의 현재 작업 디렉터리를 사용 하도록 합니다.  
- 지정 된 *LocalFile*  
  하이픈을 입력 ( **-** ) 화면에 목록을 표시 합니다.  
  ## <a name="BKMK_Examples"></a>예제  
  디렉터리 목록을 표시할 **dir1** 하 고 **dir2** 화면에서  
  ```  
  mdir dir1 dir2 -  
  ```  
  결합 된 디렉터리 목록을 저장할 **dir1** 하 고 **dir2** 라는 로컬 파일에서 **dirlist.txt**  
  ```  
  mdir dir1 dir2 dirlist.txt  
  ```  
  ## <a name="additional-references"></a>추가 참조  
- [명령줄 구문 키](command-line-syntax-key.md)  
