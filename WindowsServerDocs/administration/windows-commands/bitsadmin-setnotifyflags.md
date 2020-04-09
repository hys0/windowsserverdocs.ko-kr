---
title: bitsadmin setnotifyflags
description: Bitsadmin setnotifyflags에 대 한 Windows 명령 항목으로, 지정 된 작업에 대 한 이벤트 알림 플래그를 설정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fd3001fa4ae7f51cab92556f4f2f498511cca5ae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849286"
---
# <a name="bitsadmin-setnotifyflags"></a>bitsadmin setnotifyflags

이벤트가 지정된 된 작업에 대 한 알림 플래그를 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetNotifyFlags <Job> <NotifyFlags>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|NotifyFlags|주의 참조 하십시오.|

## <a name="remarks"></a>주의

**NotifyFlags** 매개 변수는 다음 알림 플래그 중 하나 이상을 포함할 수 있습니다.

|-----|-----| | 1 | 작업의 모든 파일이 전송 되 면 이벤트를 생성 합니다. | | 2 | 오류가 발생 하면 이벤트를 생성 합니다. | | 4 | 알림을 사용 하지 않도록 설정 합니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 전송에 대 한 알림 플래그를 설정 및 오류 이벤트 라는 작업에 대 한 작업 *myDownloadJob*합니다.
```
C:\>bitsadmin /SetNotifyFlags myDownloadJob 3
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)