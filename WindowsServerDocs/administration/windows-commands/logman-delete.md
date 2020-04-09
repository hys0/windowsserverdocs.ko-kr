---
title: logman 삭제
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8f3b2422-3dce-4fb4-adbb-8536b1d7da2b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e0ab38eab988770de4fbcef8af2c7be6a6137b16
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840756"
---
# <a name="logman-delete"></a>logman 삭제

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기존 데이터 수집기를 삭제 합니다.  

## <a name="syntax"></a>구문  
```  
logman delete <[-n] <name>> [options]  
```  
### <a name="parameters"></a>매개 변수  

|        매개 변수        |                                                                               설명                                                                               |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /?            |                                                                    도움말 상황에 맞는 표시 합니다.                                                                     |
|   -s <computer name>    |                                                          지정된 된 원격 컴퓨터에서 명령을 수행 합니다.                                                          |
|     -config <value>     |                                                         명령 옵션을 포함 하는 설정 파일을 지정 합니다.                                                         |
|       [-n] <name>       |                                                                   대상 데이터 수집기의 이름입니다.                                                                    |
|          -ets           |                                              이벤트 추적 세션 명령을 저장 하거나 예약 하지 않고 직접 보냅니다.                                               |
| -[-u < 사용자 [password] > | 사용자 계정으로 실행을 지정합니다. 암호에 대 한 \*를 입력 하면 암호를 묻는 메시지가 생성 됩니다. 암호 프롬프트에서 입력할 때 암호 표시 되지 않습니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와  
다음 명령은 데이터 수집기 perf_log을 삭제 합니다.  
```  
logman delete perf_log  
```  
## <a name="additional-references"></a>추가 참조  
[logman](logman.md)  
