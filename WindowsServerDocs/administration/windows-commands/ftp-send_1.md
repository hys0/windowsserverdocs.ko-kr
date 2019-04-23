---
title: ftp send_1
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3dca11f0d534eb875a71fa2c39cdd4dc674ad788
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862124"
---
# <a name="ftp-send1"></a>ftp: send_1

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 컴퓨터에 로컬 파일을 복사 합니다.   
## <a name="syntax"></a>구문  
```  
send <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|<LocalFile>|복사할 로컬 파일을 지정 합니다.|  
|<remoteFile>|원격 컴퓨터에서 사용 하 여 이름을 지정 합니다.|  
## <a name="remarks"></a>설명  
-   **보낼** 명령은 동일 합니다는 **배치** 명령입니다.  
-   하는 경우 *remoteFile* 지정 하지 않으면 파일 제공할지는 *LocalFile* 이름입니다.  
## <a name="BKMK_Examples"></a>예제  
로컬 파일을 복사 **test.txt** 하 고 이름을 **test1.txt** 원격 컴퓨터.  
```  
send test.txt test1.txt  
```  
로컬 파일을 복사 **program.exe** 원격 컴퓨터에 있습니다.  
```  
send program.exe  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
