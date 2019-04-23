---
title: logman 가져오기 | 내보내기
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c258daba-fb93-47c0-a53b-2fe83ed2c743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 67621b109c379cc2758b4036460b6bb82df3e3d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848304"
---
# <a name="logman-import--export"></a>logman 가져오기 | 내보내기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

데이터 수집기 집합 XML 파일에서 가져오거나 내보낼 데이터 수집기 집합을 XML 파일로.  
  
## <a name="syntax"></a>구문  
```  
logman import <[-n] <name>> <-xml <name>> [options]  
logman export <[-n] <name>> <-xml <name>> [options]  
```  
## <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|-?|도움말 상황에 맞는 표시 합니다.|  
|-s <computer name>|지정된 된 원격 컴퓨터에서 명령을 수행 합니다.|  
|-config <value>|명령 옵션을 포함 하는 설정 파일을 지정 합니다.|  
|[-n] <name>|대상 개체의 이름입니다.|  
|-xml <name>|가져오거나 내보낼 XML 파일의 이름입니다.|  
|-ets|이벤트 추적 세션 명령을 저장 하거나 예약 하지 않고 직접 보냅니다.|  
|-[-u < 사용자 [password] >|사용자 계정으로 실행입니다. 입력 한 * 암호에 대 한 프롬프트를 생성 하는 암호에 대 한 합니다. 암호 프롬프트에서 입력할 때 암호 표시 되지 않습니다.|  
|-y|메시지를 표시 하지 않고 모든 질문에 예로 답변 합니다.|  
## <a name="BKMK_examples"></a>예제  
다음 명령은 데이터 수집기 집합 이라는 perf_log으로 컴퓨터 _ 1에서 XML 파일 c:\windows\perf_log.xml를 가져옵니다.  
```  
logman import perf_log -s server_1 -xml "c:\windows\perf_log.xml"  
```  
#### <a name="additional-references"></a>추가 참조  
[logman](logman.md)  
