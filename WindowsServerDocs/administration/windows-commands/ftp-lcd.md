---
title: ftp lcd
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 60a25808-6abb-408b-8373-0bbdcd0994b4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 646cbfe3feadb63388694218758dae165ffb49c4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725259"
---
# <a name="ftp-lcd"></a>ftp: lcd

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

로컬 컴퓨터의 작업 디렉터리를 변경 합니다. 기본적으로 작업 디렉터리는 **ftp** 가 시작 된 디렉터리입니다.   
## <a name="syntax"></a>구문  
```  
lcd [<directory>]  
```  
#### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|[<directory>]|변경할 로컬 컴퓨터의 디렉터리를 지정 합니다. *디렉터리* 를 지정 하지 않으면 현재 작업 디렉터리가 기본 디렉터리로 변경 됩니다.|  
## <a name="examples"></a>예  
로컬 컴퓨터의 작업 디렉터리를 **C:\dir1** 로 변경 합니다.  
```  
lcd C:\dir1  
```  
## <a name="additional-references"></a>추가 참조  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
