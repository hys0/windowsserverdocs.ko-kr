---
title: ftp open_1
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c5da1c73362c0396300f712b2e45b906d1652604
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376193"
---
# <a name="ftp-open_1"></a>ftp: open_1

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 ftp 서버에 연결 합니다.   
## <a name="syntax"></a>구문  
```  
open <computer> [<Port>]  
```  
### <a name="parameters"></a>매개 변수  

| 매개 변수  |                                           설명                                            |
|------------|--------------------------------------------------------------------------------------------------|
| <computer> |                연결 하려는 원격 컴퓨터를 지정 합니다.                 |
|  [<Port>]  | Ftp 서버에 연결 하는 데 사용할 TCP 포트 번호를 지정 합니다. 기본적으로 TCP 포트 21이 사용 됩니다. |

## <a name="remarks"></a>설명  
**컴퓨터**를 지정 하려면 IP 주소 또는 컴퓨터 이름 (DNS 서버 또는 호스트 파일을 사용할 수 있어야 함)을 사용할 수 있습니다.  
## <a name="BKMK_Examples"></a>예와  
**Ftp.microsoft.com**에서 ftp 서버에 연결 합니다.  
```  
Open ftp.microsoft.com  
```  
TCP 포트 755에서 수신 대기 하는 **ftp.microsoft.com** 에서 ftp 서버에 연결 합니다.  
```  
open ftp.microsoft.com 755  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
