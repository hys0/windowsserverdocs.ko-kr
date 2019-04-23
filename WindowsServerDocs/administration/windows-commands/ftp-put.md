---
title: ftp 입력
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95cc1e3f-523d-4374-98b8-16e6c276b2ca vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3307ba71e7b3c8b4113f9ed29ab06660dafa5f6f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868744"
---
# <a name="ftp-put"></a>ftp: 배치

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 컴퓨터에 로컬 파일을 복사 합니다.   
## <a name="syntax"></a>구문  
```  
put <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|<LocalFile>|복사할 로컬 파일을 지정 합니다.|  
|[<remoteFile>]|원격 컴퓨터에서 사용 하 여 이름을 지정 합니다.|  
## <a name="remarks"></a>설명  
-   **배치** 명령은 동일 합니다는 **보낼** 명령입니다.  
-   하는 경우 *remoteFile* 지정 하지 않으면 파일 제공할지는 *LocalFile* 이름입니다.  
## <a name="BKMK_Examples"></a>예제  
로컬 파일을 복사 **test.txt** 하 고 이름을 **test1.txt** 원격 컴퓨터.  
```  
put test.txt test1.txt  
```  
로컬 파일을 복사 **program.exe** 원격 컴퓨터에 있습니다.  
```  
put program.exe  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: binary](ftp-binary.md)  
-   [명령줄 구문 키](command-line-syntax-key.md)  
