---
title: tskill
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08986e6a-6900-4ece-85a1-8f73b14db1b3 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 59958481a7c832aca7bc25d7d4d3ebbf4e8ef80c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835044"
---
# <a name="tskill"></a>tskill

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에서 세션에서 실행 하는 프로세스를 종료 합니다.
이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.

> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능을 참조 하세요 [어떤 새로운 Windows Server 2012의 원격 데스크톱 서비스](https://technet.microsoft.com/library/hh831527) 는 Windows Server TechNet 라이브러리에서.

## <a name="syntax"></a>구문
```
tskill {<ProcessID> | <ProcessName>} [/server:<ServerName>] [/id:<SessionID> | /a] [/v]
```

## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|\<ProcessID>|종료 하려는 프로세스의 ID를 지정 합니다.|
|\<ProcessName>|종료 하는 프로세스의 이름을 지정 합니다. 이 매개 변수는 와일드 카드 문자를 포함할 수 있습니다.|
|/server:\<ServerName>|종료 하는 프로세스를 포함 하는 터미널 서버를 지정 합니다. 하는 경우 **/server** 지정 하지 않으면 현재 RD 세션 호스트 서버를 사용 합니다.|
|/id:\<SessionID>|지정된 된 세션에서 실행 중인 프로세스를 종료 합니다.|
|/ a|모든 세션에서 실행 중인 프로세스를 종료 합니다.|
|/v|수행 중인 작업에 대 한 정보를 표시 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   사용할 수 있습니다 **tskill** 관리자가 아닌 사용자에 속하는 프로세스만 종료 합니다. 관리자 권한을 갖기 때문에 모든 **tskill** 함수 및 다른 사용자 세션에서 실행 중인 프로세스를 종료할 수 있습니다.
-   세션에서 실행 되는 모든 프로세스를 종료 하는 경우 세션이 종료 됩니다.
-   사용 하는 경우는 *ProcessName* 및 **/server: * * * ServerName* 매개 변수를 하나 지정 해야 합니다 **/id: * * * SessionID* 또는 **/a** 매개 변수입니다.

## <a name="BKMK_examples"></a>예제
-   6543 프로세스를 종료 하려면 다음을 입력 합니다.
    ```
    tskill 6543
    ```
-   탐색기"프로세스" 5 세션에서 실행을 종료 하려면 다음을 입력 합니다.
    ```
    tskill explorer /id:5
    ```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[원격 데스크톱 서비스 & #40; 터미널 서비스 및 #41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
