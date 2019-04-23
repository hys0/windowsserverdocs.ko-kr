---
title: bitsadmin getnotifyinterface
description: Windows 명령 항목에 대 한 **bitsadmin getnotifyinterface** -다른 프로그램에 지정된 된 된 작업에 대 한 COM 콜백 인터페이스를 등록 하는 경우 결정 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8316721a20cc477f9e8e15fc57b5d1c861da3ff4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868044"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

다른 프로그램이 지정된 된 된 작업에 대 한 COM 콜백 인터페이스 (알림 인터페이스)를 등록에 있는지 여부를 결정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetNotifyInterface <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

등록 또는 미등록 표시합니다.

> [!NOTE]
> 콜백 인터페이스를 등록 하는 프로그램을 확인 하는 것이 불가능 합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 검색 이라는 작업에 대 한 알림 인터페이스 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetNotifyInterface myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)