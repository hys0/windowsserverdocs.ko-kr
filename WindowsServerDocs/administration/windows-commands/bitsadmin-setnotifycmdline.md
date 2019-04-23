---
title: bitsadmin setnotifycmdline
description: 에 대 한 Windows 명령을 항목 * * *-bitsadmin setnotifycmdlineSets 데이터 전송 작업이 끝나면 또는 작업 상태가 될 때 실행될지는 명령줄 명령입니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 415ae6ef-8549-48b2-9693-2368a6e24075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1cea4e99cbaaf3881c6f436bdb932090ad6b006
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859074"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

데이터 전송 작업이 끝나면 또는 작업 상태가 될 때 실행할 명령줄 명령을 설정 합니다.

**1.2 및 이전 비트**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetNotifyCmdLine <Job> <ProgramName> [ProgramParameters]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|ProgramName|작업이 완료 될 때 실행할 명령의 이름입니다.|
|ProgramParameters|매개 변수를 전달 하려는 *ProgramName*합니다.|

## <a name="remarks"></a>설명

NULL을 지정할 수 있습니다 *ProgramName* 및 *ProgramParameters*합니다. 경우 *ProgramName* 이 NULL 이면 *ProgramParameters* NULL 이어야 합니다.

> [!IMPORTANT]
> 경우 *ProgramParameters* 가 NULL이 아니면 첫 번째 매개 변수는 *ProgramParameters* 일치 해야 *ProgramName*합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 작업 라는 메모장을 실행 하는 서비스에서 사용 되는 명령줄 명령 *myDownloadJob* 완료 합니다.
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe NULL
```
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe "notepad c:\eula.txt"
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)