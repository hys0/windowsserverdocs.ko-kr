---
title: logman 삭제
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8f3b2422-3dce-4fb4-adbb-8536b1d7da2b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 00473b5178eca93e9644888fbaa4c4c96c0dd683
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842064"
---
# <a name="logman-delete"></a>logman 삭제

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기존 데이터 수집기를 삭제 합니다.  
  
## <a name="syntax"></a>구문  
```  
logman delete <[-n] <name>> [options]  
```  
## <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|/?|도움말 상황에 맞는 표시 합니다.|  
|-s <computer name>|지정된 된 원격 컴퓨터에서 명령을 수행 합니다.|  
|-config <value>|명령 옵션을 포함 하는 설정 파일을 지정 합니다.|  
|[-n] <name>|대상 데이터 수집기의 이름입니다.|  
|-ets|이벤트 추적 세션 명령을 저장 하거나 예약 하지 않고 직접 보냅니다.|  
|-[-u < 사용자 [password] >|사용자 계정으로 실행을 지정합니다. 입력 한 * 암호에 대 한 프롬프트를 생성 하는 암호에 대 한 합니다. 암호 프롬프트에서 입력할 때 암호 표시 되지 않습니다.|  
## <a name="BKMK_examples"></a>예제  
다음 명령은 데이터 수집기 perf_log을 삭제 합니다.  
```  
logman delete perf_log  
```  
#### <a name="additional-references"></a>추가 참조  
[logman](logman.md)  
