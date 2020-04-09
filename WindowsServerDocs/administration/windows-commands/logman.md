---
title: logman
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 574a5203-5b3b-4759-a678-f26d00dde447
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bb6654cce0e23ac08a2fa6334d6144b08c8b65f3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840406"
---
# <a name="logman"></a>logman

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**logman** 는 이벤트 추적 세션 및 성능 로그를 만들고 관리 하며 명령줄에서 성능 모니터의 많은 기능을 지원 합니다.
## <a name="syntax"></a>구문
```
logman [create | query | start | stop | delete| update | import | export | /?] [options]
```
## <a name="actions"></a>작업
|작업|설명|
|-----|--------|
|[logman create](logman-create.md)|카운터, 추적, 구성 데이터 수집기 또는 API를 만듭니다.|
|[logman query](logman-query.md)|데이터 수집기 속성을 쿼리 합니다.|
|[logman start &#124; stop](logman-start-stop.md)|데이터 수집을 시작 하거나 중지 합니다.|
|[logman delete](logman-delete.md)|기존 데이터 수집기를 삭제 합니다.|
|[logman update](logman-update.md)|기존 데이터 수집기의 속성을 업데이트 합니다.|
|[logman import &#124; export](logman-import-export.md)|XML 파일에서 데이터 수집기 집합을 가져오거나 데이터 수집기 집합을 XML 파일로 내보냅니다.|
