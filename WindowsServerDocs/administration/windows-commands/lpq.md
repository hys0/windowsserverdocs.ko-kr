---
title: lpq
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb6abcc4-310a-4fa4-927b-4084b62ca02e vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 79d9f19f70840c8e40d602ba7ce634d4a6dbb73b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866764"
---
# <a name="lpq"></a>lpq

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

라인 프린터 데몬 (LPD)를 실행 하는 컴퓨터에서 인쇄 큐의 상태를 표시 합니다.  
  
## <a name="syntax"></a>구문  
```  
lpq -S <ServerName> -P <printerName> [-l]  
```  
## <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|-S <ServerName>|컴퓨터 또는 장치를 표시 하려는 상태와 함께 LPD 인쇄 큐를 호스팅하는 공유 프린터 이름 또는 IP 주소) (으로 지정 합니다. 필수 사항입니다.|  
|-P <printerName>|표시 하려는 상태와 함께 인쇄 큐에 대 한 프린터 이름을 사용 하 여 지정 합니다. 필수 사항입니다.|  
|-l|인쇄 큐의 상태에 대 한 세부 정보가 표시 되도록 지정 합니다.|  
|/?|명령 프롬프트에 도움말을 표시합니다.|  
## <a name="remarks"></a>설명  
**-S** 및 **-P** 매개 변수는 대/소문자 구분 및 대문자로 입력 해야 합니다.  
## <a name="BKMK_examples"></a>예제  
이 예제에서 10.0.0.45 LPD 호스트 Laserprinter1 프린터 큐의 상태를 표시 하는 방법을 보여 줍니다.  
```  
lpq -S 10.0.0.45 -P Laserprinter1  
```  
#### <a name="additional-references"></a>추가 참조  
[명령줄 구문 키](command-line-syntax-key.md)  
[인쇄 명령 참조](print-command-reference.md)  
