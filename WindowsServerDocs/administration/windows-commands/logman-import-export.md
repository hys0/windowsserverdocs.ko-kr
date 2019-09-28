---
title: logman 가져오기 | 내보내기
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 309274b5288bd1c17259e01cf563ae8685a2094e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374465"
---
# <a name="logman-import--export"></a>logman 가져오기 | 내보내기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

XML 파일에서 데이터 수집기 집합을 가져오거나 데이터 수집기 집합을 XML 파일로 내보냅니다.  

## <a name="syntax"></a>구문  
```  
logman import <[-n] <name>> <-xml <name>> [options]  
logman export <[-n] <name>> <-xml <name>> [options]  
```  
## <a name="parameters"></a>매개 변수  

|        매개 변수        |                                                                        설명                                                                        |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
|           -?            |                                                             도움말 상황에 맞는 표시 합니다.                                                              |
|   -s <computer name>    |                                                   지정된 된 원격 컴퓨터에서 명령을 수행 합니다.                                                   |
|     -config <value>     |                                                  명령 옵션을 포함 하는 설정 파일을 지정 합니다.                                                  |
|       [-n] <name>       |                                                                대상 개체의 이름입니다.                                                                 |
|       -xml <name>       |                                                         가져오거나 내보낼 XML 파일의 이름입니다.                                                         |
|          -ets           |                                       이벤트 추적 세션 명령을 저장 하거나 예약 하지 않고 직접 보냅니다.                                        |
| -[-u < 사용자 [password] > | 사용자 계정으로 실행입니다. 암호에 대해 \*을 입력 하면 암호를 묻는 메시지가 생성 됩니다. 암호 프롬프트에서 입력할 때 암호 표시 되지 않습니다. |
|           -y            |                                                      메시지를 표시 하지 않고 모든 질문에 예로 답변 합니다.                                                       |

## <a name="BKMK_examples"></a>예와  
다음 명령은 데이터 수집기 집합 이라는 perf_log으로 컴퓨터 _ 1에서 XML 파일 c:\windows\perf_log.xml를 가져옵니다.  
```  
logman import perf_log -s server_1 -xml "c:\windows\perf_log.xml"  
```  
#### <a name="additional-references"></a>추가 참조  
[logman](logman.md)  
