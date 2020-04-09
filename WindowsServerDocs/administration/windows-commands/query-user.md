---
title: 사용자 쿼리
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a670fb78-c055-464a-b61d-3a85632c52c5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6624c559bc85263da955f993ae7e4ad7e8b9ee2d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836806"
---
# <a name="query-user"></a>사용자 쿼리

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에서 사용자 세션에 대 한 정보를 표시 합니다.
이 명령을 사용 하는 방법에 대 한 예는 [예제](#BKMK_examples)를 참조 하세요.
> [!NOTE]
> 터미널 서비스는 Windows Server 2008 R2에서 원격 데스크톱 서비스로 이름이 변경되었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.
> ## <a name="syntax"></a>구문
> ```
> query user [<UserName> | <SessionName> | <SessionID>] [/server:<ServerName>]
> ```
> ### <a name="parameters"></a>매개 변수
> 
> |      매개 변수       |                                                     설명                                                     |
> |----------------------|---------------------------------------------------------------------------------------------------------------------|
> |      <UserName>      |                            쿼리 하려는 사용자의 로그온 이름을 지정 합니다.                             |
> |    <SessionName>     |                              쿼리 하려는 세션의 이름을 지정 합니다.                              |
> |     <SessionID>      |                               쿼리 하려는 세션의 ID를 지정 합니다.                               |
> | /server:<ServerName> | 쿼리할 rd 세션 호스트 서버를 지정 합니다. 그렇지 않으면 현재 rd 세션 호스트 서버가 사용 됩니다. |
> |          /?          |                                        명령 프롬프트에 도움말을 표시합니다.                                         |
> 
> ## <a name="remarks"></a>주의
> - 특정 사용자가 특정 rd 세션 호스트 서버에 로그온 했는지 여부를 확인 하려면이 명령을 사용할 수 있습니다. **쿼리 사용자** 는 다음 정보를 반환 합니다.
>   -   사용자의 이름
>   -   Rd 세션 호스트 서버의 세션 이름
>   -   세션 ID
>   -   (활성 또는 연결 끊기) 세션의 상태
>   -   유휴 시간 (세션에서 마지막 키 입력 이나 마우스 이동 이후 분 수)
>   -   사용자 로그온 날짜 및 시간
> - **쿼리 사용자**를 사용 하려면 모든 권한 또는 쿼리 정보 특별 한 액세스 권한이 있어야 합니다.
> - 사용자*이름*>, <*세션 이름*> 또는 <*SessionID*>를 < 지정 하지 않고 **쿼리 사용자** 를 사용 하는 경우 서버에 로그온 한 모든 사용자의 목록이 반환 됩니다. 또는 사용할 수도 있습니다 **세션 쿼리** 서버에서 모든 세션의 목록을 표시 합니다.
> - 때 **쿼리 사용자에 게** 정보를 반환, 보다 큼 (>) 기호는 현재 세션 앞에 표시 됩니다.
> - **/server** 매개 변수는 사용 하는 경우에 필요 **쿼리 사용자에 게** 원격 서버에서.
>   ## <a name="examples"></a><a name=BKMK_examples></a>예와
> - 시스템에 로그온 한 모든 사용자에 대 한 정보를 표시 하려면 다음을 입력 합니다.
>   ```
>   query user
>   ```
> - 서버 SERver1의 사용자 USER1에 대 한 정보를 표시 하려면 다음을 입력 합니다.
>   ```
>   query user USER1 /server:SERver1
>   ```
>   ## <a name="additional-references"></a>추가 참조
>   - 명령줄 [구문 키](command-line-syntax-key.md)
>   [쿼리](query.md)
>   [원격 데스크톱 서비스 (Terminal Services) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
