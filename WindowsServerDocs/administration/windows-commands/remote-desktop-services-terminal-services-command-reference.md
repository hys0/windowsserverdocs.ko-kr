---
title: 원격 데스크톱 서비스 (터미널 서비스) 명령 참조
description: '* * * *에 대 한 참조 문서'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2f371848-5c48-470c-908c-afbc95d3a805
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55466409517b63c52f88a7acec3a8f4aba7d258d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933475"
---
# <a name="remote-desktop-services-terminal-services-command-reference"></a>원격 데스크톱 서비스 (터미널 서비스) 명령 참조

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음은 명령줄 도구를 원격 데스크톱 서비스의 목록이 있습니다.
> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.
>
> |                 명령                 |                                                      설명                                                       |
> |-----------------------------------------|------------------------------------------------------------------------------------------------------------------------|
> |           [change](change.md)           | 로그온, COM 포트 매핑 및 설치 모드에 대 한 원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버 설정을 변경 합니다. |
> |     [change logon](change-logon.md)     |    Rd 세션 호스트 서버의 클라이언트 세션에서 로그온을 사용 하거나 사용 하지 않도록 설정 하거나 현재 로그온 상태를 표시 합니다.     |
> |      [change port](change-port.md)      |                   MS-DOS 응용 프로그램과 호환 되도록 COM 포트 매핑을 나열 하거나 변경 합니다.                    |
> |      [change user](change-user.md)      |                                rd 세션 호스트 서버에 대 한 설치 모드를 변경 합니다.                                |
> |         [chglogon](chglogon.md)         |    Rd 세션 호스트 서버의 클라이언트 세션에서 로그온을 사용 하거나 사용 하지 않도록 설정 하거나 현재 로그온 상태를 표시 합니다.     |
> |          [chgport](chgport.md)          |                   MS-DOS 응용 프로그램과 호환 되도록 COM 포트 매핑을 나열 하거나 변경 합니다.                    |
> |           [chgusr](chgusr.md)           |                                rd 세션 호스트 서버에 대 한 설치 모드를 변경 합니다.                                |
> |         [flattemp](flattemp.md)         |                                      하나의 임시 폴더를 사용 하지 않도록 설정 하거나 사용 합니다.                                       |
> |           [logoff](logoff.md)           |          Rd 세션 호스트 서버의 세션에서 사용자를 로그 오프 하 고 서버에서 세션을 삭제 합니다.          |
> |              [msg](msg.md)              |                                Rd 세션 호스트 서버에서 사용자에 게 메시지를 보냅니다.                                 |
> |            [mstsc](mstsc.md)            |                       rd 세션 호스트 서버 또는 다른 원격 컴퓨터에 대 한 연결을 만듭니다.                        |
> |          [qappsrv](qappsrv.md)          |                             네트워크에 있는 모든 rd 세션 호스트 서버 목록을 표시 합니다.                             |
> |         [qprocess](qprocess.md)         |                  Rd 세션 호스트 서버에서 실행 중인 프로세스에 대 한 정보를 표시 합니다.                   |
> |            [쿼리](query.md)            |                      프로세스, 세션 및 rd 세션 호스트 서버에 대 한 정보를 표시 합니다.                      |
> |    [query process](query-process.md)    |                  Rd 세션 호스트 서버에서 실행 중인 프로세스에 대 한 정보를 표시 합니다.                   |
> |    [query session](query-session.md)    |                           Rd 세션 호스트 서버에서 세션에 대 한 정보를 표시 합니다.                            |
> | [query termserver](query-termserver.md) |                             네트워크에 있는 모든 rd 세션 호스트 서버 목록을 표시 합니다.                             |
> |       [query user](query-user.md)       |                         Rd 세션 호스트 서버에서 사용자 세션에 대 한 정보를 표시 합니다.                         |
> |            [quser](quser.md)            |                         Rd 세션 호스트 서버에서 사용자 세션에 대 한 정보를 표시 합니다.                         |
> |          [qwinsta](qwinsta.md)          |                           Rd 세션 호스트 서버에서 세션에 대 한 정보를 표시 합니다.                            |
> |          [rdpsign](rdpsign.md)          |                          디지털 방식으로 원격 데스크톱 프로토콜 (.rdp) 파일에 서명할 수 있습니다.                          |
> |    [reset session](reset-session.md)    |                         Rd 세션 호스트 서버에서 세션을 다시 설정 (삭제) 할 수 있습니다.                          |
> |          [rwinsta](rwinsta.md)          |                         Rd 세션 호스트 서버에서 세션을 다시 설정 (삭제) 할 수 있습니다.                          |
> |           [shadow](shadow.md)           |            Rd 세션 호스트 서버에서 다른 사용자의 활성 세션을 원격으로 제어할 수 있습니다.             |
> |            [tscon](tscon.md)            |                               Rd 세션 호스트 서버에서 다른 세션에 연결 합니다.                                |
> |         [tsdiscon](tsdiscon.md)         |                                 Rd 세션 호스트 서버에서 세션의 연결을 끊습니다.                                  |
> |           [tskill](tskill.md)           |                           Rd 세션 호스트 서버의 세션에서 실행 중인 프로세스를 종료 합니다.                            |
> |           [tsprof](tsprof.md)           |              한 사용자에서 다른 원격 데스크톱 서비스 사용자 구성 정보를 복사합니다.               |
