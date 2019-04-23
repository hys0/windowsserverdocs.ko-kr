---
title: ftp ls_1
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c45e26f6578510837f190ae20e3140e619dc59cb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841764"
---
# <a name="ftp-ls1"></a>ftp: ls_1

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

파일 및 원격 컴퓨터에서 하위 디렉터리의 간단한 목록을 표시합니다.   
## <a name="syntax"></a>구문  
```  
ls [<remotedirectory>] [<LocalFile>]  
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|[<remotedirectory>]|목록이 표시 하려는 디렉터리를 지정 합니다. 디렉터리가 없는 지정 된 경우 원격 컴퓨터의 현재 작업 디렉터리 사용 됩니다.|  
|[<LocalFile>]|목록을 저장할 로컬 파일을 지정 합니다. 로컬 파일을 지정 하지 않으면 결과 화면에 표시 됩니다.|  
## <a name="BKMK_Examples"></a>예제  
파일 및 원격 컴퓨터에서 하위 디렉터리의 간단한 목록을 표시 합니다.  
```  
ls  
```  
약식된 디렉터리 나열 **dir1** 라는 로컬 파일에 저장 하 고 원격 컴퓨터의 **dirlist.txt**  
```  
ls dir1 dirlist.txt   
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
