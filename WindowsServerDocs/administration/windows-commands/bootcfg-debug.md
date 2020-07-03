---
title: bootcfg debug
description: 지정 된 운영 체제 항목에 대 한 디버그 설정을 추가 하거나 변경 하는 bootcfg debug 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 28afa5fb-a236-46e2-b1a4-a3c43a49c437
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da4179d85d4e84918e75fb4c8490e229230412eb
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926324"
---
# <a name="bootcfg-debug"></a>bootcfg debug

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

추가 하거나 지정된 된 운영 체제 항목에 대 한 디버그 설정을 변경 합니다.

>[!NOTE]
> 1394 포트를 디버깅 하려는 경우에는 대신 [bootcfg dbg1394](bootcfg-dbg1394.md) 명령을 사용 합니다.

## <a name="syntax"></a>구문

```
bootcfg /debug {on | off | edit}[/s <computer> [/u <domain>\<user> /p <password>]] [/port {COM1 | COM2 | COM3 | COM4}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <osentrylinenum>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{on | off | edit}` | 다음을 포함 하 여 포트 디버깅의 값을 지정 합니다.<ul><li>**sign-on.** 지정 된에/debug 옵션을 추가 하 여 원격 디버깅을 지원할 수 있도록 합니다 `<osentrylinenum>` .</li><li>**해제.** 지정 된에서/debug 옵션을 제거 하 여 원격 디버깅 지원을 사용 하지 않도록 설정 <osentrylinenum> 합니다.</li><li>**편집할.** 지정 된에 대 한/debug 옵션과 연결 된 값을 변경 하 여 포트 및 전송 속도 설정을 변경할 수 있습니다 <osentrylinenum> .</li></ul> |
| `/s <computer>` | 원격 컴퓨터의 이름 또는 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않음). 기본값은 로컬 컴퓨터입니다. |
| `/u <domain>\<user>`  | 또는로 지정 된 사용자의 계정 권한으로 명령을 실행 합니다 `<user>` `<domain>\<user>` . 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
| `/p <password>` | 에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. |
| `/port {COM1 | COM2 | COM3 | COM4}` |  디버깅에 사용할 COM 포트를 지정 합니다. 디버깅을 사용 하지 않도록 설정한 경우이 매개 변수를 사용 하지 마세요. |
| `/baud {9600 | 19200 | 38400 | 57600 | 115200}` | 디버깅에 사용할 전송 속도를 지정 합니다. 디버깅을 사용 하지 않도록 설정한 경우이 매개 변수를 사용 하지 마세요. |
| `/id <osentrylinenum>` | 운영 체제 로드 옵션 추가 되는 Boot.ini 파일의 [운영 체제] 섹션에 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

**Bootcfg/debug** 명령을 사용 하려면 다음을 수행 합니다.

```
bootcfg /debug on /port com1 /id 2
bootcfg /debug edit /port com2 /baud 19200 /id 2
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /debug off /id 2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bootcfg 명령](bootcfg.md)
