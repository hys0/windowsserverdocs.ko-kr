---
title: bitsadmin getnotifycmdline
description: Windows 명령 항목에 대 한 **bitsadmin getnotifycmdline** -데이터 전송 작업이 끝나면 실행 되는 명령줄 명령을 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3ca7b2e67c0b5672733a25465fba89d1bd69d07a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817294"
---
# <a name="bitsadmin-getnotifycmdline"></a>bitsadmin getnotifycmdline

데이터 전송 작업이 완료 될 때 실행할 명령줄 명령을 검색 합니다.

**1.2 및 이전 비트**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetNotifyCmdLine <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 작업 라는 서비스를 사용한 명령줄 명령을 검색 *myDownloadJob* 완료 합니다.
```
C:\>bitsadmin /GetNotifyCmdLine myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)