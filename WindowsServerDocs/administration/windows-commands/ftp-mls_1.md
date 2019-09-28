---
title: ftp mls_1
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: a84a0f8f3121ea19876744e9ef04bebf5f9fcb08
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376263"
---
# <a name="ftp-mls_1"></a>ftp: mls_1

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 디렉터리에서 파일 및 하위 디렉터리의 축약 된 목록을 표시 합니다.   
## <a name="syntax"></a>구문  
```  
mls <remoteFile>[ ] <LocalFile>  
```  
### <a name="parameters"></a>매개 변수  

|  매개 변수   |                       설명                       |
|--------------|---------------------------------------------------------|
| <remoteFile> | 목록을 보려는 파일을 지정 합니다. |
| <LocalFile>  |  목록을 저장할 로컬 파일을 지정 합니다.  |

## <a name="remarks"></a>설명  
- *Remotefiles* 지정  
  원격 컴퓨터에서 현재 작업 디렉터리를 사용 하려면 하이픈 ( **-** )을 입력 합니다.  
- *Localfile* 지정  
  화면에 목록을 표시 하려면 하이픈 ( **-** )을 입력 합니다.  
  ## <a name="BKMK_Examples"></a>예와  
  **Dir1** 및 **dir2**에 대 한 파일 및 하위 디렉터리의 축약 된 목록을 표시 합니다.  
  ```  
  mls dir1 dir2 -  
  ```  
  **Dir1** 및 **dir2** 에 대 한 간략 한 파일 및 하위 디렉터리 목록을 로컬 파일 파일 목록에 저장 **합니다.**  
  ```  
  mls dir1 dir2 dirlist.txt   
  ```  
  ## <a name="additional-references"></a>추가 참조  
- [명령줄 구문 키](command-line-syntax-key.md)  
