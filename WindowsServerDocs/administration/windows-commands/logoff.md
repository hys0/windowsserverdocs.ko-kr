---
title: 로그오프
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 939f09cc-de8c-436c-a05d-aca5f2a06371
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 88b3cbbbd52a965fd0a0de3c164e8dbc1f90d053
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437519"
---
# <a name="logoff"></a>로그오프

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에서 세션에서 사용자를 로그 오프 하 고 서버에서 세션을 삭제 합니다.
이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.

> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능을 참조 하세요 [어떤 새로운 Windows Server 2012의 원격 데스크톱 서비스](https://technet.microsoft.com/library/hh831527) 는 Windows Server TechNet 라이브러리에서.

## <a name="syntax"></a>구문
```
logoff [<SessionName> | <SessionID>] [/server:<ServerName>] [/v]
```
## <a name="parameters"></a>매개 변수

|      매개 변수       |                                                                             설명                                                                              |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <SessionName>     |                                                                  세션의 이름을 지정합니다.                                                                  |
|     <SessionID>      |                                                 서버에 세션을 식별 하는 숫자 ID를 지정 합니다.                                                 |
| /server:<ServerName> | 세션 로그 오프 하려는 사용자를 포함 하는 rd 세션 호스트 서버를 지정 합니다. 지정 하지 않으면 현재 활성화 되어 있는 서버에 사용 됩니다. |
|          /v          |                                                       수행 중인 작업에 대 한 정보를 표시 합니다.                                                        |
|          /?          |                                                                 명령 프롬프트에 도움말을 표시합니다.                                                                 |

## <a name="remarks"></a>설명
- 항상를 현재 로그온 세션에서 기록할 수 있습니다. 그러나 있어야 다른 세션에서 사용자를 로그 오프를 모든 권한이 있습니다.
- 경고 없이 세션에서 사용자를 로그 오프 사용자의 세션에서 데이터의 손실 될 수 있습니다. 사용 하 여 사용자에 게 메시지를 전송 해야는 **msg** 이 작업을 수행 하기 전에 경고를 표시 하는 명령입니다.
- 경우 <*SessionID*> 또는 <*SessionName*>를 지정 하지 않으면 **로그 오프** 현재 세션에서 사용자가 로그 오프 합니다. 지정 하는 경우 <*SessionName*>, 활성 이어야 합니다.
- 로그 오프 하면 사용자, 서버에서 모든 프로세스가 종료 되 고 세션이 삭제 됩니다.
- 콘솔 세션에서 사용자 오프 기록할 수 없습니다.
  ## <a name="BKMK_examples"></a>예제
- 현재 세션에서 사용자를 기록 하려면 다음을 입력 합니다.
  ```
  logoff
  ```
- 사용자를 로그 오프 한 세션에서 세션 사용 하 여 세션의 ID, 예를 들어 12를 입력 합니다.
  ```
  logoff 12
  ```
- 사용자를 로그 오프 한 세션에서 세션 및 서버 이름을 사용 하 여, 예를 들어 세션 TERM04 서버 1에서 입력 합니다.
  ```
  logoff TERM04 /server:Server1
  ```

#### <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)
-   [원격 데스크톱 서비스 &#40;터미널 서비스&#41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
