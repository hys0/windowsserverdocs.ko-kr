---
title: 원격 데스크톱 서비스 (터미널 서비스) 명령 참조
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2f371848-5c48-470c-908c-afbc95d3a805
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8ff9cad993b220c2ef58f19d0064691407beacf9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887524"
---
# <a name="remote-desktop-services-terminal-services-command-reference"></a>원격 데스크톱 서비스 (터미널 서비스) 명령 참조

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음은 명령줄 도구를 원격 데스크톱 서비스의 목록이 있습니다.
> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능을 참조 하세요 [어떤 새로운 Windows Server 2012의 원격 데스크톱 서비스](https://technet.microsoft.com/library/hh831527) 는 Windows Server TechNet 라이브러리에서.
|Command|설명|
|------|--------|
|[change](change.md)|로그온, COM 포트 매핑 및 설치 모드에 대 한 원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버 설정을 변경합니다.|
|[로그온 변경](change-logon.md)|또는 rd 세션 호스트 서버의 클라이언트 세션에서 로그온을 사용 하지 않도록 설정 하거나 현재 로그온 상태를 표시 합니다.|
|[포트 변경](change-port.md)|나열 하거나 MS-DOS 응용 프로그램과 호환 되도록 COM 포트 매핑을 변경 합니다.|
|[change user](change-user.md)|rd 세션 호스트 서버에 대 한 설치 모드를 변경 합니다.|
|[chglogon](chglogon.md)|또는 rd 세션 호스트 서버의 클라이언트 세션에서 로그온을 사용 하지 않도록 설정 하거나 현재 로그온 상태를 표시 합니다.|
|[chgport](chgport.md)|나열 하거나 MS-DOS 응용 프로그램과 호환 되도록 COM 포트 매핑을 변경 합니다.|
|[chgusr](chgusr.md)|rd 세션 호스트 서버에 대 한 설치 모드를 변경 합니다.|
|[flattemp](flattemp.md)|하나의 임시 폴더를 사용 하지 않도록 설정 하거나 사용 합니다.|
|[logoff](logoff.md)|Rd 세션 호스트 서버에서 세션에서 사용자를 로그 오프 하 고 서버에서 세션을 삭제 합니다.|
|[msg](msg.md)|Rd 세션 호스트 서버에서 사용자에 게 메시지를 보냅니다.|
|[mstsc](mstsc.md)|rd 세션 호스트 서버 또는 다른 원격 컴퓨터에 대 한 연결을 만듭니다.|
|[qappsrv](qappsrv.md)|네트워크에서 모든 rd 세션 호스트 서버 목록을 표시 합니다.|
|[qprocess](qprocess.md)|Rd 세션 호스트 서버에서 실행 중인 프로세스에 대 한 정보를 표시 합니다.|
|[query](query.md)|프로세스, 세션 및 rd 세션 호스트 서버에 대 한 정보를 표시합니다.|
|[쿼리 프로세스](query-process.md)|Rd 세션 호스트 서버에서 실행 중인 프로세스에 대 한 정보를 표시 합니다.|
|[쿼리 세션](query-session.md)|Rd 세션 호스트 서버에서 세션에 대 한 정보를 표시합니다.|
|[쿼리 termserver](query-termserver.md)|네트워크에서 모든 rd 세션 호스트 서버 목록을 표시 합니다.|
|[쿼리 사용자에 게](query-user.md)|Rd 세션 호스트 서버에서 사용자 세션에 대 한 정보를 표시합니다.|
|[quser](quser.md)|Rd 세션 호스트 서버에서 사용자 세션에 대 한 정보를 표시합니다.|
|[qwinsta](qwinsta.md)|Rd 세션 호스트 서버에서 세션에 대 한 정보를 표시합니다.|
|[rdpsign](rdpsign.md)|디지털 방식으로 원격 데스크톱 프로토콜 (.rdp) 파일에 서명할 수 있습니다.|
|[세션 다시 설정](reset-session.md)|Rd 세션 호스트 서버에서 세션 다시 설정 (삭제) 할 수 있습니다.|
|[rwinsta](rwinsta.md)|Rd 세션 호스트 서버에서 세션 다시 설정 (삭제) 할 수 있습니다.|
|[shadow](shadow.md)|Rd 세션 호스트 서버에서 다른 사용자의 활성 세션을 원격으로 제어할 수 있습니다.|
|[tscon](tscon.md)|Rd 세션 호스트 서버에서 다른 세션에 연결합니다.|
|[tsdiscon](tsdiscon.md)|Rd 세션 호스트 서버에서 세션의 연결을 끊습니다.|
|[tskill](tskill.md)|Rd 세션 호스트 서버에서 세션에서 실행 하는 프로세스를 종료 합니다.|
|[tsprof](tsprof.md)|한 사용자에서 다른 원격 데스크톱 서비스 사용자 구성 정보를 복사합니다.|
