---
title: ftp open_1
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 45de8b3c210fe0925ac3cc43c41d3e092d5dfe16
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438498"
---
# <a name="ftp-open1"></a>ftp: open_1

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 ftp 서버에 연결합니다.   
## <a name="syntax"></a>구문  
```  
open <computer> [<Port>]  
```  
### <a name="parameters"></a>매개 변수  

| 매개 변수  |                                           설명                                            |
|------------|--------------------------------------------------------------------------------------------------|
| <computer> |                연결 하려는 원격 컴퓨터를 지정 합니다.                 |
|  [<Port>]  | Ftp 서버에 연결 하는 데 TCP 포트 번호를 지정 합니다. 기본적으로 TCP 포트 21이 사용 됩니다. |

## <a name="remarks"></a>설명  
지정 하는 IP 주소 또는 컴퓨터 이름 (이 경우 DNS 서버 또는 호스트 파일을 사용할 수 있어야)을 사용할 수 **컴퓨터**합니다.  
## <a name="BKMK_Examples"></a>예제  
Ftp 서버에 연결 **형식인**합니다.  
```  
Open ftp.microsoft.com  
```  
Ftp 서버에 연결 **형식인** 755 TCP 포트에서 수신 하는 합니다.  
```  
open ftp.microsoft.com 755  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
