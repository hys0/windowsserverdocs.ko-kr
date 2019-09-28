---
title: ftp 디렉터리
description: Ftp 디렉터리에 대 한 Windows 명령 항목
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c47971c52135d79ce62f935bfed981f6eefcecaa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376437"
---
# <a name="ftp-dir"></a>ftp: dir

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 컴퓨터의 디렉터리 파일 및 하위 디렉터리 목록을 표시 합니다.   
## <a name="syntax"></a>구문  
```  
dir [<remotedirectory>] [<LocalFile>]  
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|[<remotedirectory>]|목록을 보려는 디렉터리를 지정 합니다. 디렉터리가 지정 되지 않은 경우 원격 컴퓨터의 현재 작업 디렉터리를 사용 합니다.|  
|[<LocalFile>]|디렉터리 목록을 저장할 로컬 파일을 지정 합니다. 로컬 파일을 지정 하지 않으면 결과가 화면에 표시 됩니다.|  
## <a name="BKMK_Examples"></a>예와  
원격 컴퓨터에 **dir1** 에 대 한 디렉터리 목록을 표시 합니다.  
```  
dir dir1  
```  
원격 컴퓨터에 있는 현재 디렉터리의 목록을 로컬 파일의 파일 **목록 .txt**에 저장 합니다.  
```  
dir . dirlist.txt  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
