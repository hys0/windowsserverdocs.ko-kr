---
title: 세션 쿼리
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abc0ace8-0b74-4b6e-a937-a78bb4b61a1f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bde9a246f2c46eaa466f2863c2cfc3c28a3a04eb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384913"
---
# <a name="query-session"></a>세션 쿼리

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에서 세션에 대 한 정보를 표시 합니다.
목록에는 활성 세션에 대 한 뿐만 아니라 서버에서 실행 하는 다른 세션에 대 한 정보가 포함 됩니다.
이 명령을 사용 하는 방법에 대 한 예는 [예제](#BKMK_examples)를 참조 하세요.
> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.
> ## <a name="syntax"></a>구문
> ```
> query session [<SessionName> | <UserName> | <SessionID>] [/server:<ServerName>] [/mode] [/flow] [/connect] [/counter]
> ```
> ## <a name="parameters"></a>매개 변수
> 
> |      매개 변수       |                                                      설명                                                      |
> |----------------------|-----------------------------------------------------------------------------------------------------------------------|
> |    <SessionName>     |                               쿼리 하려는 세션의 이름을 지정 합니다.                               |
> |      <UserName>      |                           쿼리 하려는 세션이 사용자의 이름을 지정 합니다.                            |
> |     <SessionID>      |                                쿼리 하려는 세션의 ID를 지정 합니다.                                |
> | /server:<ServerName> |                  쿼리할 rd 세션 호스트 서버를 식별 합니다. 기본값은 현재 서버.                   |
> |        /mode         |                                            현재 줄 설정을 표시합니다.                                            |
> |        /flow         |                                        현재 흐름 제어 설정을 표시합니다.                                        |
> |       연결 /       |                                          현재의 연결 설정을 표시 합니다.                                           |
> |       카운터 /       | 현재 카운터 정보를 표시, 만들어진 세션의 총 수를 포함 하 여 연결이 해제 및 다시 연결 합니다. |
> |          /?          |                                         명령 프롬프트에 도움말을 표시합니다.                                          |
> 
> ## <a name="remarks"></a>설명
> - 항상 사용자는 사용자가 현재 로그온 세션을 쿼리할 수 있습니다. 다른 세션을 쿼리하려면 사용자에 게 쿼리 정보 특별 한 액세스 권한이 있어야 합니다.
> - < 세션*이름*>, <*사용자 이름*> 또는 <*SessionID*>를 사용 하 여 세션을 지정 하지 않으면 **쿼리 세션** 은 시스템의 모든 활성 세션에 대 한 정보를 표시 합니다.
> - 때 **세션 쿼리** 정보를 반환, 보다 큼 (>) 기호는 현재 세션 앞에 표시 됩니다. 다음은 예제 출력 **세션 쿼리**:
>   ```
>   C:\>query session
>    SESSIONNAME    USERNAME       ID STATE  TYPE   DEVICE
>   console        Administrator1  0 active wdcon
>    rdp-tcp#1      User1           1 active wdtshare
>    rdp-tcp                        2 listen wdtshare
>                                   4 idle
>                                   5 idle
>   ```
>   보다 큼 (>) 기호는 현재 세션을 나타냅니다. 세션 이름에는 세션에 할당 된 이름을 지정 합니다. 사용자 이름에는 세션에 연결 하는 사용자의 사용자 이름을 나타냅니다. 상태는 세션의 현재 상태에 대 한 정보를 제공합니다. 형식은 세션 유형을 나타냅니다. 존재 하지 않는 콘솔 이나 네트워크에 연결 된 세션에 대 한, 장치에는 세션에 할당 된 장치 이름입니다. 세션 정보 다음 주석 세션 프로필에서 시작 됩니다. DISABLED로 구성 된 초기 상태는 모든 세션에 표시 되지 않는 **세션 쿼리** 설정 될 때까지 나열 합니다.
>   ## <a name="BKMK_examples"></a>예와
> - SERver2 서버에서 모든 활성 세션에 대 한 정보를 표시 하려면 다음을 입력 합니다.
>   ```
>   query session /server:SERver2
>   ```
> - 활성 세션 modeM02에 대 한 정보를 표시 하려면 다음을 입력 합니다.
>   ```
>   query session modeM02
>   ```
>   #### <a name="additional-references"></a>추가 참조
>   [명령줄 구문 키](command-line-syntax-key.md)
>   [쿼리](query.md)
>   [원격 데스크톱 서비스 &#40;터미널&#41; 서비스 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
