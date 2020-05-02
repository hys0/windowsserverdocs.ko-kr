---
title: ftp open_1
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 15a27d2f7512da352a0f4ddf02fa2511ffce7c1d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725192"
---
# <a name="ftp-open_1"></a>ftp: open_1

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 ftp 서버에 연결 합니다.   
## <a name="syntax"></a>구문  
```  
open <computer> [<Port>]  
```  
#### <a name="parameters"></a>매개 변수  

| 매개 변수  |                                           설명                                            |
|------------|--------------------------------------------------------------------------------------------------|
| <computer> |                연결 하려는 원격 컴퓨터를 지정 합니다.                 |
|  [<Port>]  | Ftp 서버에 연결 하는 데 사용할 TCP 포트 번호를 지정 합니다. 기본적으로 TCP 포트 21이 사용 됩니다. |

## <a name="remarks"></a>설명  
**컴퓨터**를 지정 하려면 IP 주소 또는 컴퓨터 이름 (DNS 서버 또는 호스트 파일을 사용할 수 있어야 함)을 사용할 수 있습니다.  
## <a name="examples"></a>예  
**Ftp.microsoft.com**에서 ftp 서버에 연결 합니다.  
```  
Open ftp.microsoft.com  
```  
TCP 포트 755에서 수신 대기 하는 **ftp.microsoft.com** 에서 ftp 서버에 연결 합니다.  
```  
open ftp.microsoft.com 755  
```  
## <a name="additional-references"></a>추가 참조  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
