---
title: tsdiscon
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13139674-7dee-4965-8cac-32f4928e8b9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2033cbc9b3d9127249656c3e0dcf95d872229797
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842544"
---
# <a name="tsdiscon"></a>tsdiscon

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에서 세션의 연결을 끊습니다.
이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.

> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능을 참조 하세요 [어떤 새로운 Windows Server 2012의 원격 데스크톱 서비스](https://technet.microsoft.com/library/hh831527) 는 Windows Server TechNet 라이브러리에서.

## <a name="syntax"></a>구문
```
tsdiscon [<SessionID> | <SessionName>] [/server:<ServerName>] [/v]
```

## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|\<SessionId>|연결을 끊을 세션의 ID를 지정 합니다.|
|\<SessionName>|연결을 끊을 세션의 이름을 지정 합니다.|
|/server:\<ServerName>|연결을 끊을 세션을 포함 하는 터미널 서버를 지정 합니다. 그렇지 않으면 현재 rd 세션 호스트 서버에서 사용 됩니다.|
|/v|수행 중인 작업에 대 한 정보를 표시 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   전체 제어 권한이 하거나 특별 한 액세스 권한을 다른 사용자 세션에서 연결을 분리 해야 합니다.
-   세션 ID 또는 세션 이름을 지정 하는 경우 **tsdiscon** 현재 세션의 연결을 끊습니다.
-   세션 연결을 끊을 때 실행 중이 던 모든 응용 프로그램 데이터의 손실 없이 해당 세션에 다시 연결 하면 자동 실행 됩니다. 사용 하 여 **세션 다시 설정** 연결이 끊긴된 세션의 실행 중인 응용 프로그램을 종료 하지만 되려면이 될 수 있음을 데이터 손실이 세션에서 인식 합니다.
-   합니다 **/server** 사용 하는 경우에 매개 변수는 필수 **tsdiscon** 원격 서버에서.
-   콘솔 세션 연결을 끊을 수 없습니다.

## <a name="BKMK_examples"></a>예제
-   현재 세션의 연결을 끊으려면 다음을 입력 합니다.
    ```
    tsdiscon
    ```
-   10 세션 연결을 끊으려면 다음을 입력 합니다.
    ```
    tsdiscon 10
    ```
-   Term04 세션 연결을 끊으려면 다음을 입력 합니다.
    ```
    tsdiscon TERM04
    ```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[원격 데스크톱 서비스 & #40; 터미널 서비스 및 #41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
