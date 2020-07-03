---
title: msg
description: 원격 데스크톱 세션 호스트 서버에서 사용자에 게 메시지를 보내는 msg 명령에 대 한 참조 문서
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9501cf3e-568e-4982-9987-8daecc6c17ff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6eff557b1fb7eb2c5f67b2902762786bbfc839c1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934970"
---
# <a name="msg"></a>msg

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 서버에서 사용자에 게 메시지를 보냅니다.

> [!NOTE]
> 메시지를 보내려면 메시지에 특별 한 액세스 권한이 있어야 합니다.

## <a name="syntax"></a>구문

```
msg {<username> | <sessionname> | <sessionID>| @<filename> | *} [/server:<servername>] [/time:<seconds>] [/v] [/w] [<message>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<username>` | 메시지를 수신 하려는 사용자의 이름을 지정 합니다. 사용자 또는 세션을 지정 하지 않으면이 명령은 오류 메시지를 표시 합니다. 세션을 지정할 때 활성 이어야 합니다. |
| `<sessionname>` | 메시지를 수신 하려는 세션의 이름을 지정 합니다. 사용자 또는 세션을 지정 하지 않으면이 명령은 오류 메시지를 표시 합니다. 세션을 지정할 때 활성 이어야 합니다. |
| `<sessionID>` | 메시지를 수신 하려는 사용자의 세션이의 숫자 ID를 지정 합니다. |
| `@<filename>` | 사용자 이름, 세션 이름 및 메시지를 수신 하려면 세션 Id의 목록을 포함 하는 파일을 식별 합니다. |
| * | 시스템에서 모든 사용자 이름에 메시지를 보냅니다. |
| /server:`<servername>` | 메시지를 수신 하려는 세션 또는 사용자의 원격 데스크톱 세션 호스트 서버를 지정 합니다. 지정 하지 않으면 **/server** 를 현재 로그온 서버를 사용 합니다. |
| /시간`<seconds>` | 사용자가 보낸 메시지는 사용자의 화면에 표시 되는 시간을 지정 합니다. 시간 제한에 도달 하면 메시지가 사라집니다. 사용자가 메시지를 보고 하 고 클릭 될 때까지 사용자의 화면에 메시지가 남아 시간 제한이 설정 된 경우 **확인**합니다. |
| /v | 수행 중인 작업에 대 한 정보를 표시 합니다. |
| /w | 메시지가 수신 된 사용자의 승인을 기다립니다. 사용자가 즉시 응답 하지 않는 경우이 매개 변수를 사용 `/time:<*seconds*>` 하 여 긴 지연 시간을 방지할 수 있습니다. 이 매개 변수를 사용 하 여 **/v** 에 도움이 됩니다. |
| `<message>` | 보낼 메시지의 텍스트를 지정 합니다. 메시지를 지정 하는 경우 메시지를 입력 하 라는 메시지가 됩니다. 파일에 포함 된 메시지를 보내려면 작음 (<) 기호 뒤에 파일 이름을 입력 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

메시지를 보내려면 *User1*의 모든 세션에 대 한 *오후 1 시를 살펴보겠습니다* . 다음을 입력 합니다.

```
msg User1 Let's meet at 1PM today
```

*ModeM02*세션에 동일한 메시지를 보내려면 다음을 입력 합니다.

```
msg modem02 Let's meet at 1PM today
```

*Userlist*파일에 포함 된 모든 세션에 메시지를 보내려면 다음을 입력 합니다.

```
msg @userlist Let's meet at 1PM today
```

로그온 되어 있는 모든 사용자에 게는 메시지를 보내려면 다음을 입력 합니다.

```
msg * Let's meet at 1PM today
```

승인 제한 시간 (예: 10 초)으로 모든 사용자에 게는 메시지를 보내려면 다음을 입력 합니다.

```
msg * /time:10 Let's meet at 1PM today
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
