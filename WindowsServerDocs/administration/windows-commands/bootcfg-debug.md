---
title: bootcfg debug
description: Windows 명령 항목에 대 한 **bootcfg 디버그** -추가 하거나 지정된 된 운영 체제 항목에 대 한 디버그 설정을 변경 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28afa5fb-a236-46e2-b1a4-a3c43a49c437
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44a1145384a62d30f055cb48fd7ed6adccd2c69b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434826"
---
# <a name="bootcfg-debug"></a>bootcfg debug

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

추가 하거나 지정된 된 운영 체제 항목에 대 한 디버그 설정을 변경 합니다.

## <a name="syntax"></a>구문
```
bootcfg /debug {ON | OFF | edit}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/port {COM1 | COM2 | COM3 | COM4}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>매개 변수

|                           매개 변수                           |                                                                                                                                                                                                                    설명                                                                                                                                                                                                                    |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                  {ON &#124; OFF&#124; 편집}                   | 디버깅에 대 한 값을 지정합니다.<br /><br />**ON** -지정 된 /debug 옵션을 추가 하 여 원격 디버깅 지원을 통해 <OSEntryLineNum>합니다.<br /><br />**OFF** -지정 된 위치에서 /debug 옵션을 제거 하 여 원격 디버깅 지원을 해제 <OSEntryLineNum>합니다.<br /><br />**편집할** -지정 된 /debug 옵션을 사용 하 여 관련 된 값을 변경 하 여 포트 및 전송 변경 속도 설정 허용 <OSEntryLineNum>합니다. |
|                         /s <computer>                         |                                                                                                                                                                이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                                                                                                                                                 |
|                      /u <Domain>\\<User>                      |                                                                                                                       지정한 사용자의 계정 권한으로 명령을 실행 <User> 나 <Domain> \\ <User>합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한.                                                                                                                        |
|                         /p <Password>                         |                                                                                                                                                                               에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                                                                                                                                               |
|       포트 / {COM1 &#124; COM2 &#124; COM3 &#124; COM4}        |                                                                                                                                                                디버깅에 사용할 COM 포트를 지정 합니다. 사용 하지 않는 합니다 **/포트** 디버깅 하는 경우 매개 변수에 사용할 수 없게 됩니다.                                                                                                                                                                |
| /baud {9600&#124; 19200&#124; 38400&#124; 57600&#124; 115200} |                                                                                                                                                               디버깅에 사용할 전송 속도 지정 합니다. 사용 하지 않는 합니다 **/baud** 디버깅 하는 경우 매개 변수에 사용할 수 없게 됩니다.                                                                                                                                                                |
|                     /id <OSEntryLineNum>                      |                                                                                                               디버깅 옵션 추가 되는 Boot.ini 파일의 [운영 체제] 섹션에서 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다.                                                                                                                |
|                              /?                               |                                                                                                                                                                                                       명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                                                        |

##### <a name="remarks"></a>설명
- 1394 포트 디버깅가 필요한 경우 사용 하 여 [bootcfg dbg1394](bootcfg-dbg1394.md)합니다.
  ## <a name="BKMK_examples"></a>예제
  다음 예제에서는 사용 하는 방법을 표시 합니다 **bootcfg /debug**명령:
  ```
  bootcfg /debug on /port com1 /id 2 
  bootcfg /debug edit /port com2 /baud 19200 /id 2 
  bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /debug off /id 2
  ```
  #### <a name="additional-references"></a>추가 참조
  [명령줄 구문 키](command-line-syntax-key.md)
