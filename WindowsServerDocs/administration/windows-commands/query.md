---
title: query
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 675c5128-f3cf-4e8f-8a3f-b29ab2a8b6de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8d89ae8c7c526bce396b2583abc1728456f7bcc3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836826"
---
# <a name="query"></a>query

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

프로세스, 세션 및 원격 데스크톱 세션 호스트 (RD 세션 호스트) 서버에 대 한 정보를 표시합니다.

> [!NOTE]
> 터미널 서비스는 Windows Server 2008 R2에서 원격 데스크톱 서비스로 이름이 변경되었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.

## <a name="syntax"></a>구문
```
query process
query session
query termserver
query user
```

### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[쿼리 프로세스](query-process.md)|Rd 세션 호스트 서버에서 실행 중인 프로세스에 대 한 정보를 표시 합니다.|
|[세션 쿼리](query-session.md)|Rd 세션 호스트 서버에서 세션에 대 한 정보를 표시 합니다.|
|[termserver 쿼리](query-termserver.md)|네트워크에 있는 모든 rd 세션 호스트 서버 목록을 표시 합니다.|
|[사용자 쿼리](query-user.md)|Rd 세션 호스트 서버에서 사용자 세션에 대 한 정보를 표시 합니다.|

## <a name="additional-references"></a>추가 참조
- 명령줄 [구문 키](command-line-syntax-key.md)
[원격 데스크톱 서비스 (Terminal Services) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
