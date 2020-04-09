---
title: bitsadmin setnotifycmdline
description: Bitsadmin setnotifycmdline에 대 한 Windows 명령 항목-작업에서 데이터 전송을 완료할 때 또는 작업이 상태로 전환 될 때 실행 되는 명령줄 명령을 설정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 415ae6ef-8549-48b2-9693-2368a6e24075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 761a7003e44e8dc15cb2dd2f1ce5a1a23be53286
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849336"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

작업에서 데이터 전송을 완료할 때 또는 작업이 상태로 전환 될 때 실행 되는 명령줄 명령을 설정 합니다.

**BITS 1.2 및 이전 버전**: 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetNotifyCmdLine <Job> <ProgramName> [ProgramParameters]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|ProgramName|작업이 완료 될 때 실행할 명령의 이름입니다.|
|ProgramParameters|매개 변수를 전달 하려는 *ProgramName*합니다.|

## <a name="remarks"></a>주의

NULL을 지정할 수 있습니다 *ProgramName* 및 *ProgramParameters*합니다. 경우 *ProgramName* 이 NULL 이면 *ProgramParameters* NULL 이어야 합니다.

> [!IMPORTANT]
> 경우 *ProgramParameters* 가 NULL이 아니면 첫 번째 매개 변수는 *ProgramParameters* 일치 해야 *ProgramName*합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 작업 라는 메모장을 실행 하는 서비스에서 사용 되는 명령줄 명령 *myDownloadJob* 완료 합니다.
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe NULL
```
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe notepad c:\eula.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)