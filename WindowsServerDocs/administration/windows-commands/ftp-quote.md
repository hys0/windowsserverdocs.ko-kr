---
title: ftp 견적
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4500a1d3-c091-42c7-a909-f61df7f2e993 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f468bfc384673818dc53be303f82cd4803cb2eb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438495"
---
# <a name="ftp-quote"></a>ftp: 견적

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 ftp 서버에 정확 하 게 인수를 보냅니다. 단일 ftp 응답 코드가 반환 됩니다.   
## <a name="syntax"></a>구문  
```  
quote <Argument>[ ]  
```  
### <a name="parameters"></a>매개 변수  

| 매개 변수  |                    설명                    |
|------------|---------------------------------------------------|
| <Argument> | Ftp 서버로 보낼 인수를 지정 합니다. |

## <a name="remarks"></a>설명  
**견적** 명령은 동일 합니다는 **리터럴** 명령입니다.  
## <a name="BKMK_Examples"></a>예제  
송신을 **종료** 원격 ftp 서버에 명령 합니다.  
```  
quote quit  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: literal_1](ftp-literal_1.md)  
-   [명령줄 구문 키](command-line-syntax-key.md)  
