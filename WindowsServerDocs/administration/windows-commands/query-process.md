---
title: 쿼리 프로세스
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 36ce3ffc-0092-4eb1-a374-28e6616ca946
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e15a41fc931d2cf04d60759a63e3b80392265175
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840724"
---
# <a name="query-process"></a>쿼리 프로세스

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에서 실행 중인 프로세스에 대 한 정보를 표시 합니다.
이 명령을 사용 하 여 특정 사용자를 실행 하는 프로그램을 찾으려면 및 또한 어떤 사용자가 특정 프로그램을 실행 합니다.
이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.
> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능을 참조 하세요 [어떤 새로운 Windows Server 2012의 원격 데스크톱 서비스](https://technet.microsoft.com/library/hh831527) 는 Windows Server TechNet 라이브러리에서.
## <a name="syntax"></a>구문
```
query process [* | <ProcessID> | <UserName> | <SessionName> | /id:<nn> | <ProgramName>] [/server:<ServerName>]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|*|모든 세션에 대 한 프로세스를 나열합니다.|
|<ProcessID>|쿼리 하려는 프로세스를 식별 하는 숫자 ID를 지정 합니다.|
|<UserName>|표시 하려는 프로세스의 사용자 이름을 지정 합니다.|
|<SessionName>|표시 하려는 프로세스의 세션의 이름을 지정 합니다.|
|/id:<nn>|표시 하려는 프로세스의 세션의 ID를 지정 합니다.|
|<ProgramName>|쿼리 하려는 프로세스의 프로그램의 이름을 지정 합니다. .Exe 확장명은 필수입니다.|
|/server:<ServerName>|표시 하려는 프로세스의 rd 세션 호스트 서버를 지정 합니다. 지정 하지 않으면 서버에 현재 로그온이 사용 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|
## <a name="remarks"></a>설명
-   관리자 권한을 갖기 때문에 모든 **쿼리 프로세스** 함수입니다.
-   지정 하지 않으면 경우는 <*사용자 이름*>, <*SessionName*>, **/id:**<*nn*>, <*ProgramName*>, 또는 **\*** 매개 변수 **쿼리 프로세스** 현재 사용자에 속하는 프로세스만 표시 됩니다.
-   세션을 지정 된 경우 활성 세션을 식별 해야 합니다.
-   **쿼리 프로세스** 다음 정보를 반환 합니다.
    -   프로세스를 소유 하는 사용자
    -   프로세스를 소유 하는 세션
    -   세션의 ID
    -   프로세스의 이름
    -   프로세스의 ID
-   때 **쿼리 프로세스** 현재 세션에 속해 있는 각 프로세스의 정보를 반환, 보다 큼 (>) 기호가 표시 됩니다.
## <a name="BKMK_examples"></a>예제
-   모든 세션에서 사용 중인 프로세스에 대 한 정보를 표시 하려면 다음을 입력 합니다.
    ```
    query process *
    ```
-   세션 ID가 2에서 사용 중인 프로세스에 대 한 정보를 표시 하려면 다음을 입력 합니다.
    ```
    query process /ID:2
    ```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[쿼리의](query.md)
[Remote Desktop Services &#40;터미널&#41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
