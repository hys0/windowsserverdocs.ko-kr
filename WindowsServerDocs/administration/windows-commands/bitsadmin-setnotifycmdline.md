---
title: bitsadmin setnotifycmdline
description: '**Bitsadmin setnotifycmdline**에 대 한 Windows 명령 항목-작업에서 데이터 전송을 완료할 때 실행 되거나 작업이 상태로 전환 될 때 실행 되는 명령줄 명령을 설정 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 415ae6ef-8549-48b2-9693-2368a6e24075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b268b68cbd355a7fe7f993d678a98f6fcb99f0ab
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122894"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

작업에서 데이터 전송을 완료 하거나 작업이 지정 된 상태로 전환 될 때 실행 되는 명령줄 명령을 설정 합니다.

> [!NOTE]
> 이 명령은 BITS 1.2 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /setnotifycmdline <job> <program_name> [program_parameters]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| program_name | 작업이 완료 될 때 실행할 명령의 이름입니다. 이 값을 NULL로 설정할 수 있지만 그렇지 않은 경우에는 *PROGRAM_PARAMETERS* null로도 설정 해야 합니다. |
| program_parameters | *Program_name*에 전달할 매개 변수입니다. 이 값은 NULL로 설정할 수 있습니다. *PROGRAM_PARAMETERS* NULL로 설정 되지 않은 경우 *program_parameters* 의 첫 번째 매개 변수가 *program_name*와 일치 해야 합니다. |

## <a name="examples"></a>예

다음 예제에서는 *Mydownloadjob* 이라는 작업이 완료 된 후 notepad.exe를 실행 하는 서비스에서 사용 하는 명령줄 명령을 설정 합니다.

```
C:\>bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe NULL
```

```
C:\>bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe notepad c:\eula.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)