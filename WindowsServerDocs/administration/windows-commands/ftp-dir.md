---
title: ftp 디렉터리
description: Ftp 디렉터리에 대 한 Windows 명령을 항목
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 78ac8ac5e9fc4894f55401bb234aa98de981adf7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835254"
---
# <a name="ftp-dir"></a>ftp: dir

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 컴퓨터 디렉터리의 파일과 하위 디렉터리의 목록을 표시합니다.   
## <a name="syntax"></a>구문  
```  
dir [<remotedirectory>] [<LocalFile>]  
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|[<remotedirectory>]|목록이 표시 하려는 디렉터리를 지정 합니다. 디렉터리가 없는 지정 된 경우 원격 컴퓨터의 현재 작업 디렉터리 사용 됩니다.|  
|[<LocalFile>]|로컬 파일을 저장할 디렉터리 목록을 지정 합니다. 로컬 파일을 지정 하지 않으면 결과 화면에 표시 됩니다.|  
## <a name="BKMK_Examples"></a>예제  
디렉터리에 대 한 목록을 표시할 **dir1** 원격 컴퓨터.  
```  
dir dir1  
```  
로컬 파일에 있는 원격 컴퓨터의 현재 디렉터리의 목록을 저장할 **dirlist.txt**합니다.  
```  
dir . dirlist.txt  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
