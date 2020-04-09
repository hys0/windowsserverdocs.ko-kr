---
title: exit
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 23d1044b-f5c1-4180-ae6d-f553b48da4d9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 13cf7a7658394e59ce6cc7e66c3083cd3d359574
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844886"
---
# <a name="exit"></a>exit

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Cmd.exe 프로그램 (명령 인터프리터) 또는 현재 일괄 처리 스크립트를 종료합니다.  
이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.  
## <a name="syntax"></a>구문  
```  
exit [/b] [<exitCode>]  
```  
### <a name="parameters"></a>매개 변수  

| 매개 변수  |                                                                                         설명                                                                                          |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /b     |                                      Cmd.exe를 종료 하지 않고 현재 일괄 처리 스크립트를 종료 합니다. 배치 스크립트 외부에서 실행, Cmd.exe를 종료 합니다.                                      |
| `<exitCode>` | 번호를 지정합니다. 경우 **/b** 를 지정 하 고 ERRORLEVEL 환경 변수를 해당 숫자로 설정 됩니다. 종료 하는 경우 **Cmd.exe**, 프로세스 종료 코드를 해당 숫자로 설정 됩니다. |
|     /?     |                                                                             명령 프롬프트에 도움말을 표시합니다.                                                                             |

## <a name="examples"></a><a name=BKMK_examples></a>예와  
Cmd.exe 명령 인터프리터를 닫으려면 다음을 입력 합니다.  
```  
exit  
```  
## <a name="additional-references"></a>추가 참조  
-   - [명령줄 구문 키](command-line-syntax-key.md)  

