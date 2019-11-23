---
title: shadow
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f81d9717-6883-4e14-9508-4b2a87e48ea7 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cb2fad4b0a553e736755f2dc56e5d88297a1fef5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383964"
---
# <a name="shadow"></a>shadow

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에서 다른 사용자의 활성 세션을 원격으로 제어할 수 있습니다.
이 명령을 사용 하는 방법에 대 한 예는 [예제](#BKMK_examples)를 참조 하세요.

## <a name="syntax"></a>구문
```
shadow {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]
```

### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|\<세션 이름 >|원격으로 제어 하려는 세션의 이름을 지정 합니다.|
|\<SessionID >|원격으로 제어 하려는 세션의 ID를 지정 합니다. 사용 하 여 **쿼리 사용자에 게** 세션 및 세션 Id의 목록을 표시 합니다.|
|/server:\<ServerName >|원격으로 제어 하려는 세션이 포함 된 rd 세션 호스트 서버를 지정 합니다. 기본적으로 현재 rd 세션 Host4 서버가 사용 됩니다.|
|/v|수행 중인 작업에 대 한 정보를 표시 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   볼 수도 있고 적극적으로 세션을 제어할 수도 있습니다. 사용자의 세션을 적극적으로 제어 하려는 경우 키보드 및 마우스 동작을 세션에 입력할 수 있습니다.
-   항상 사용자 자신의 세션을 원격으로 제어할 수 있습니다 (현재 세션 제외). 그러나 다른 세션을 원격으로 제어 하려면 모든 권한 또는 원격 제어 특별 액세스 권한이 있어야 합니다.
-   또한 원격 데스크톱 서비스 관리자를 사용 하 여 원격 제어를 시작할 수 있습니다.
-   모니터링을 시작 하기 전에 서버를 세션이 원격으로 제어 하려고 합니다.이 경고 비활성화 되어 있지 않으면 사용자에 게 경고 합니다. 세션은 사용자의 응답을 대기 하는 동안 몇 초 동안 중지 된 것 나타날 수 있습니다. 사용자 및 세션에 대 한 원격 제어를 구성 하려면 원격 데스크톱 서비스 구성 도구나 로컬 사용자 및 그룹 및 active directory 사용자 및 컴퓨터에 대 한 원격 데스크톱 서비스 확장을 사용 합니다.
-   세션은 원격 제어 또는 작업이 실패 하는 세션에 사용 되는 비디오 해상도 지원할 수 있어야 합니다.
-   콘솔 세션은 둘 다 원격으로 제어할 수 다른 세션도 수 원격 제어 될 다른 세션에서.
-   원격 제어 (숨김)를 종료 하려는 경우에는 CTRL +\* (숫자 키패드의 \*만 사용)를 누릅니다.

## <a name="BKMK_examples"></a>예와
-   그림자 세션 93에 다음을 입력 합니다.
    ```
    shadow 93
    ```
-   ACCTG01 세션을, 다음을 입력 합니다.
    ```
    shadow ACCTG01
    ```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[원격 데스크톱 서비스 & #40; 터미널 서비스 및 #41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
