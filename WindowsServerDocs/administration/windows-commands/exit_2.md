---
title: exit
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23d1044b-f5c1-4180-ae6d-f553b48da4d9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e599f84389b23e527e3718a620d5fdfefe24edb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439465"
---
# <a name="exit"></a>exit

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Cmd.exe 프로그램 (명령 인터프리터) 또는 현재 일괄 처리 스크립트를 종료합니다.  
이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.  
## <a name="syntax"></a>구문  
```  
exit [/b] [<exitCode>]  
```  
## <a name="parameters"></a>매개 변수  

| 매개 변수  |                                                                                         설명                                                                                          |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /b     |                                      Cmd.exe를 종료 하지 않고 현재 일괄 처리 스크립트를 종료 합니다. 배치 스크립트 외부에서 실행, Cmd.exe를 종료 합니다.                                      |
| <exitCode> | 번호를 지정합니다. 경우 **/b** 를 지정 하 고 ERRORLEVEL 환경 변수를 해당 숫자로 설정 됩니다. 종료 하는 경우 **Cmd.exe**, 프로세스 종료 코드를 해당 숫자로 설정 됩니다. |
|     /?     |                                                                             명령 프롬프트에 도움말을 표시합니다.                                                                             |

## <a name="BKMK_examples"></a>예제  
Cmd.exe 명령 인터프리터를 닫으려면 다음을 입력 합니다.  
```  
exit  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  

