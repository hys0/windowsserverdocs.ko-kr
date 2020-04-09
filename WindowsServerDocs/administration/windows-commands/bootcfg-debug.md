---
title: bootcfg debug
description: 지정 된 운영 체제 항목에 대 한 디버그 설정을 추가 하거나 변경 하는 bootcfg 디버그에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 28afa5fb-a236-46e2-b1a4-a3c43a49c437
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de225e1bd0f8406a0b28e5af28fd29bceb8e713c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848636"
---
# <a name="bootcfg-debug"></a>bootcfg debug

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

추가 하거나 지정된 된 운영 체제 항목에 대 한 디버그 설정을 변경 합니다.

## <a name="syntax"></a>구문
```
bootcfg /debug {ON | OFF | edit}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/port {COM1 | COM2 | COM3 | COM4}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <OSEntryLineNum>]
```
### <a name="parameters"></a>매개 변수

|                           매개 변수                           |                                                                                                                                                                                                                    설명                                                                                                                                                                                                                    |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                  {ON &#124; OFF&#124; 편집}                   | 디버깅에 사용할 값을 지정 합니다.<p>**ON** -지정 된 <OSEntryLineNum>에/debug 옵션을 추가 하 여 원격 디버깅 지원을 사용 하도록 설정 합니다.<p>**OFF** -지정 된 <OSEntryLineNum>에서/debug 옵션을 제거 하 여 원격 디버깅 지원을 사용 하지 않도록 설정 합니다.<p>**편집** -지정 된 <OSEntryLineNum>에 대 한/debug 옵션과 연결 된 값을 변경 하 여 포트 및 전송 속도 설정을 변경할 수 있습니다. |
|                         /s <computer>                         |                                                                                                                                                                이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                                                                                                                                                 |
|                      /u <Domain>\\<User>                      |                                                                                                                       <User> 또는 <Domain>\\<User>에 지정 된 사용자의 계정 권한으로 명령을 실행 합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한.                                                                                                                        |
|                         /p <Password>                         |                                                                                                                                                                               에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                                                                                                                                               |
|       /port {COM1 &#124; COM2 &#124; COM3 &#124; COM4}        |                                                                                                                                                                디버깅에 사용할 COM 포트를 지정 합니다. 디버깅을 사용 하지 않도록 설정 하는 경우에는 **/port** 매개 변수를 사용 하지 마십시오.                                                                                                                                                                |
| /baud {9600&#124; 19200&#124; 38400&#124; 57600&#124; 115200} |                                                                                                                                                               디버깅에 사용할 전송 속도를 지정 합니다. 디버깅을 사용 하지 않도록 설정 하는 경우 **/baud** 매개 변수를 사용 하지 마세요.                                                                                                                                                                |
|                     /id <OSEntryLineNum>                      |                                                                                                               디버깅 옵션이 추가 된 Boot.ini 파일의 [운영 체제] 섹션에 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다.                                                                                                                |
|                              /?                               |                                                                                                                                                                                                       명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                                                        |

##### <a name="remarks"></a>주의
- 1394 포트 디버깅이 필요한 경우 [bootcfg dbg1394](bootcfg-dbg1394.md)를 사용 합니다.
  ## <a name="examples"></a><a name=BKMK_examples></a>예와
  다음 예에서는 **bootcfg/debug**명령을 사용 하는 방법을 보여 줍니다.
  ```
  bootcfg /debug on /port com1 /id 2 
  bootcfg /debug edit /port com2 /baud 19200 /id 2 
  bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /debug off /id 2
  ```
  ## <a name="additional-references"></a>추가 참조
  - [명령줄 구문 키](command-line-syntax-key.md)
