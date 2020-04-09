---
title: msg
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9501cf3e-568e-4982-9987-8daecc6c17ff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91a85cd5d043b6c613f88e199670f55f6e0e72a7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839146"
---
# <a name="msg"></a>msg

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에서 사용자에 게 메시지를 보냅니다.
이 명령을 사용 하는 방법에 대 한 예는 [예제](#BKMK_examples)를 참조 하세요.
> [!NOTE]
> 터미널 서비스는 Windows Server 2008 R2에서 원격 데스크톱 서비스로 이름이 변경되었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.

## <a name="syntax"></a>구문
```
msg {<UserName> | <SessionName> | <SessionID>| @<FileName> | *} [/server:<ServerName>] [/time:<Seconds>] [/v] [/w] [<Message>]
```

### <a name="parameters"></a>매개 변수

|      매개 변수       |                                                                                                                               설명                                                                                                                               |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <UserName>      |                                                                                                  메시지를 수신 하려는 사용자의 이름을 지정 합니다.                                                                                                   |
|    <SessionName>     |                                                                                                 메시지를 수신 하려는 세션의 이름을 지정 합니다.                                                                                                 |
|     <SessionID>      |                                                                                            메시지를 수신 하려는 사용자의 세션이의 숫자 ID를 지정 합니다.                                                                                            |
|     @<FileName>      |                                                                         사용자 이름, 세션 이름 및 메시지를 수신 하려면 세션 Id의 목록을 포함 하는 파일을 식별 합니다.                                                                         |
|          \*          |                                                                                                           시스템에서 모든 사용자 이름에 메시지를 보냅니다.                                                                                                            |
| /server:<ServerName> |                                              메시지를 수신 하려는 세션 또는 사용자의 rd 세션 호스트 서버를 지정 합니다. 지정 하지 않으면 **/server** 를 현재 로그온 서버를 사용 합니다.                                              |
|   /시간:<Seconds>    | 사용자가 보낸 메시지는 사용자의 화면에 표시 되는 시간을 지정 합니다. 시간 제한에 도달 하면 메시지가 사라집니다. 사용자가 메시지를 보고 하 고 클릭 될 때까지 사용자의 화면에 메시지가 남아 시간 제한이 설정 된 경우 **확인**합니다. |
|          /v          |                                                                                                         수행 중인 작업에 대 한 정보를 표시 합니다.                                                                                                         |
|          /w          |         메시지가 수신 된 사용자의 승인을 기다립니다. 이 매개 변수를 사용 하 여 **/시간:** <*초*> 경우를 방지 하려면 지연 시간이 길어질 수는 사용자가 즉시 응답 하지 않습니다. 이 매개 변수를 사용 하 여 **/v** 에 도움이 됩니다.          |
|      <Message>       |                  보낼 메시지의 텍스트를 지정 합니다. 메시지를 지정 하는 경우 메시지를 입력 하 라는 메시지가 됩니다. 파일에 포함 된 메시지를 보내려면 작음 (<) 기호 뒤에 파일 이름을 입력 합니다.                  |
|          /?          |                                                                                                                  명령 프롬프트에 도움말을 표시합니다.                                                                                                                   |

## <a name="remarks"></a>주의
-   사용자 또는 세션을 지정 하지 않으면 **msg** 는 오류 메시지를 표시 합니다. 세션을 지정할 때 활성 이어야 합니다.
-   사용자는 메시지를 보내려면 메시지 특별 한 액세스 권한이 있어야 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와
-   현재 오후 1 시에 대 한 모든 세션에 대 한 모든 세션에 대 한 소개를 알려 주는 메시지를 보내려면 다음을 입력 합니다.
    ```
    msg User1 Let's meet at 1PM today
    ```
-   ModeM02 세션에 동일한 메시지를 보내려면 다음을 입력 합니다.
    ```
    msg modem02 Let's meet at 1PM today
    ```
-   12 번 세션에서 메시지를 보내려면 다음을 입력 합니다.
    ```
    msg 12 Let's meet at 1PM today
    ```
-   USERlist 파일에 포함 된 모든 세션에 메시지를 보내려면 다음을 입력 합니다.
    ```
    msg @userlist Let's meet at 1PM today
    ```
-   로그온 되어 있는 모든 사용자에 게는 메시지를 보내려면 다음을 입력 합니다.
    ```
    msg * Let's meet at 1PM today
    ```
-   승인 제한 시간 (예: 10 초)으로 모든 사용자에 게는 메시지를 보내려면 다음을 입력 합니다.
    ```
    msg * /time:10 Let's meet at 1PM today
    ```

## <a name="additional-references"></a>추가 참조
-  - [명령줄 구문 키](command-line-syntax-key.md)
-  [원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
