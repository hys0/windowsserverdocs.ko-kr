---
title: tscon
description: 원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에서 다른 세션에 연결 되는 tscon에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 315a9793-cd10-4987-bb68-89a9d13f7fce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5679af2a53e28b91712a373e8d3c5d63850efbe1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934213"
---
# <a name="tscon"></a>tscon

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 서버의 다른 세션에 연결 합니다.



> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.

## <a name="syntax"></a>구문
```
tscon {<SessionID> | <SessionName>} [/dest:<SessionName>] [/password:<pw> | /password:*] [/v]
```
### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|\<SessionID>|연결 하려는 세션의 ID를 지정 합니다. Optional **/dest:** < *세션 이름*> 매개 변수를 사용 하는 경우 연결 하려는 세션의 ID입니다.|
|\<SessionName>|연결 하려는 세션의 이름을 지정 합니다.|
|/dest\<SessionName>|현재 세션의 이름을 지정 합니다. 이 세션은 새 세션에 연결할 때 연결을 끊습니다.|
|/password\<pw>|연결 하려는 세션을 소유 하는 사용자의 암호를 지정 합니다. 이 암호는 연결 하는 사용자가 세션을 소유 하지 않은 경우에 필요 합니다.|
|/password: *|연결 하려는 세션을 소유 하는 사용자의 암호를 묻는 메시지를 표시 합니다.|
|/v|수행 중인 작업에 대 한 정보를 표시 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   다른 세션에 연결 하려면 모든 권한 또는 연결 액세스 권한이 있어야 합니다.
-   **/Dv:** 세션 < *이름*> 매개 변수를 사용 하면 다른 사용자의 세션을 다른 세션에 연결할 수 있습니다.
-   <*password*> 매개 변수에 암호를 지정 하지 않고 대상 세션이 현재 사용자에 게 속해 있지 않으면 **tscon** 가 실패 합니다.
-   콘솔 세션에는 연결할 수 없습니다.

## <a name="examples"></a>예
- 현재 rd 세션 호스트 서버에서 세션 12에 연결 하 고 현재 세션의 연결을 끊으려면 다음을 입력 합니다.
  ```
  tscon 12
  ```
- 현재 rd 세션 호스트 서버에서 mypass 암호를 사용 하 여 세션 23에 연결 하 고 현재 세션의 연결을 끊으려면 다음을 입력 합니다.
  ```
  tscon 23 /password:mypass
  ```
- TERM03 라는 세션을 TERM05 세션에 연결한 다음 세션 TERM05 연결을 끊으려면 (연결 된 경우) 다음을 입력 합니다.
  ```
  tscon TERM03 /v /dest:TERM05
  ```
  ## <a name="additional-references"></a>추가 참조
  - [명령줄 구문 키](command-line-syntax-key.md) 
   [원격 데스크톱 서비스 (터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
