---
title: bitsadmin setnotifyflags
description: Windows 명령 항목에 대 한 **bitsadmin setnotifyflags** -이벤트가 지정된 된 된 작업에 대 한 알림 플래그를 설정 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc817e03e0f1916ea392830d14985a7a1377d69a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868794"
---
# <a name="bitsadmin-setnotifyflags"></a>bitsadmin setnotifyflags

이벤트가 지정된 된 작업에 대 한 알림 플래그를 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetNotifyFlags <Job> <NotifyFlags>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|NotifyFlags|주의 참조 하십시오.|

## <a name="remarks"></a>설명

합니다 **NotifyFlags** 매개 변수는 다음과 같은 알림 플래그 중 하나 이상을 포함할 수 있습니다.

|---|---| | 1 | 작업의 모든 파일 전송 된 경우 이벤트를 생성 합니다. | | 2 | 오류가 발생 하면 이벤트를 생성 합니다. | | 4 | 알림을 사용 하지 않도록 설정 합니다. |

## <a name="BKMK_examples"></a>예제

다음 예제에서는 전송에 대 한 알림 플래그를 설정 및 오류 이벤트 라는 작업에 대 한 작업 *myDownloadJob*합니다.
```
C:\>bitsadmin /SetNotifyFlags myDownloadJob 3
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)