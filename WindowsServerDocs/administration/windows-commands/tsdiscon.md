---
title: tsdiscon
description: Tsdiscon에 대 한 Windows 명령 항목으로, 원격 데스크톱 세션 호스트 서버에서 세션의 연결을 끊습니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 13139674-7dee-4965-8cac-32f4928e8b9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b008fa920290043b64e7421e91a545123634f1e7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832516"
---
# <a name="tsdiscon"></a>tsdiscon

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 서버에서 세션의 연결을 끊습니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

> [!NOTE]
> 터미널 서비스는 Windows Server 2008 R2에서 원격 데스크톱 서비스로 이름이 변경되었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.

## <a name="syntax"></a>구문
```
tsdiscon [<SessionID> | <SessionName>] [/server:<ServerName>] [/v]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|\<SessionId >|연결을 끊을 세션의 ID를 지정 합니다.|
|\<세션 이름 >|연결을 끊을 세션의 이름을 지정 합니다.|
|/server:\<ServerName >|연결을 끊을 세션이 포함 된 터미널 서버를 지정 합니다. 그렇지 않으면 현재 rd 세션 호스트 서버가 사용 됩니다.|
|/v|수행 중인 작업에 대 한 정보를 표시 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의
-   세션에서 다른 사용자의 연결을 끊으려면 모든 권한 또는 특별 한 액세스 연결 끊기 권한이 있어야 합니다.
-   세션 ID 또는 세션 이름을 지정 하지 않으면 **tsdiscon** 는 현재 세션의 연결을 끊습니다.
-   세션의 연결을 끊을 때 실행 중이 던 모든 응용 프로그램은 데이터 손실 없이 해당 세션에 다시 연결할 때 자동으로 실행 됩니다. 세션 **다시 설정** 을 사용 하 여 연결 되지 않은 세션의 실행 중인 응용 프로그램을 종료 하지만이로 인해 세션에서 데이터가 손실 될 수 있습니다.
-   **/Server** 매개 변수는 원격 서버에서 **tsdiscon** 를 사용 하는 경우에만 필요 합니다.
-   콘솔 세션의 연결을 끊을 수 없습니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와
- 현재 세션의 연결을 끊으려면 다음을 입력 합니다.
  ```
  tsdiscon
  ```
- 세션 10의 연결을 끊으려면 다음을 입력 합니다.
  ```
  tsdiscon 10
  ```
- TERM04 라는 세션의 연결을 끊으려면 다음을 입력 합니다.
  ```
  tsdiscon TERM04
  ```
  ## <a name="additional-references"></a>추가 참조
  - 명령줄 [구문 키](command-line-syntax-key.md)
  [원격 데스크톱 서비스 (Terminal Services) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
