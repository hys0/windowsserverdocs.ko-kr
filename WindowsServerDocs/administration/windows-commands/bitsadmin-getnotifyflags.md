---
title: bitsadmin getnotifyflags
description: Windows 명령 항목에 대 한 **bitsadmin getnotifyflags** -지정된 된 된 작업에 대 한 알림 플래그를 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 690e94805c5e61d96603e4ade102fb3a4bda409e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889284"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags



지정된 된 된 작업에 대 한 알림 플래그를 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetNotifyFlags <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

작업은 다음과 같은 알림 플래그 중 하나 이상을 포함할 수 있습니다.

|---|---| | 0x001 | 작업의 모든 파일 전송 된 경우 이벤트를 생성 합니다. | | 0x002 | 오류가 발생 하면 이벤트를 생성 합니다. | | 0x004 | 알림을 사용 하지 않도록 설정 합니다. | | 0x008 | 작업 수정 되거나 전송이 진행 하는 경우 이벤트를 생성 합니다. |

## <a name="BKMK_examples"></a>예제

다음 예제에서는 검색 이라는 작업에 대 한 알림 플래그 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetNotifyFlags myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)