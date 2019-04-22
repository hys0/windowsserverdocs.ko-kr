---
title: bitsadmin create
description: Windows 명령 항목에 대 한 **bitsadmin 만들기** -지정 된 표시 이름을 사용 하 여 전송 작업을 만듭니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a8c53af-900b-4c24-9265-5b8b08213fac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d6ce5a4fdc21d879bf0a265e3c4185d83311464a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817194"
---
# <a name="bitsadmin-create"></a>bitsadmin create

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 표시 이름과 함께 전송 작업을 만듭니다. 로컬 파일에는 서버에서 데이터를 전송 하는 작업을 다운로드 합니다. 서버에 로컬 파일에서 작업 전송 데이터를 업로드 합니다. 업로드-회신 작업 서버에 로컬 파일에서 데이터를 전송 하 고 서버에서 회신 파일을 수신 합니다.

사용 된 [bitsadmin resume](bitsadmin-resume.md) 전송 큐에서 작업을 활성화 하는 스위치입니다.

## <a name="syntax"></a>구문

```
bitsadmin /create [type] DisplayName
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|type|-   **/ 다운로드** 로컬 파일에는 서버에서 데이터를 전송 합니다.<br />-   **/ 업로드** 서버로 로컬 파일에서 데이터를 전송 합니다.<br />-   **/ 업로드-회신** 서버로 로컬 파일에서 데이터를 전송 하 고 서버에서 회신 파일을 받습니다.<br />-이 매개 변수의 기본값은 **다운로드/** 명령줄에 지정 되지 않은 경우.|
|DisplayName|새로 만든된 작업에 할당 된 표시 이름입니다.|

**1.2 및 이전 비트**: /Upload 형식과 /Upload-Reply 제공 되지 않습니다.

## <a name="BKMK_examples"></a>예제

이라는 다운로드 작업을 만들고 *myDownloadJob*합니다.

```
C:\>bitsadmin /create myDownloadJob
```

## <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
