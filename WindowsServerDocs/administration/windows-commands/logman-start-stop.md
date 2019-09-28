---
title: logman 시작 | 중지
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a40006a1-876e-474b-aaf1-f365c730deea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 395d325b31ee596e1394e7ed796a444f159d15fc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374413"
---
# <a name="logman-start--stop"></a>logman 시작 | 중지

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

데이터 수집기를 시작 하 고 시작 시간을 수동으로 설정 하거나 데이터 수집기 집합을 중지 하 고 종료 시간을 수동으로 설정 합니다.  

## <a name="syntax"></a>구문  
```  
logman start <[-n] <name>> [options]  
logman stop <[-n] <name>> [options]  
```  
## <a name="parameters"></a>매개 변수  

|     매개 변수      |                                 설명                                  |
|--------------------|------------------------------------------------------------------------------|
|         -?         |                       도움말 상황에 맞는 표시 합니다.                       |
| -s <computer name> |            지정된 된 원격 컴퓨터에서 명령을 수행 합니다.             |
|  -config <value>   |           명령 옵션을 포함 하는 설정 파일을 지정 합니다.            |
|    [-n] <name>     |                          대상 개체의 이름입니다.                          |
|        -ets        | 이벤트 추적 세션 명령을 저장 하거나 예약 하지 않고 직접 보냅니다. |
|        -으로         |               요청한 작업을 비동기적으로 수행 합니다.                |

## <a name="BKMK_examples"></a>예와  
다음 명령은 원격 컴퓨터 _ 1에 데이터 수집기 perf_log를 시작 합니다.  
```  
logman start perf_log -s server_1  
```  
#### <a name="additional-references"></a>추가 참조  
[logman](logman.md)  
