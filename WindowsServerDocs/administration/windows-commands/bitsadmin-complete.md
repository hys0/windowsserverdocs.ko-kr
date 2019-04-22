---
title: bitsadmin complete
description: Windows 명령 항목에 대 한 **bitsadmin 완료** -작업을 완료 합니다. 이 스위치를 사용 하기 전에 다운로드 한 파일을 사용할 수 없는 경우
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 561585da370f7e69aa3b83b3ddd7579bfc658a21
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817324"
---
# <a name="bitsadmin-complete"></a>bitsadmin complete

작업을 완료합니다. 이 스위치를 사용 하기 전에 다운로드 한 파일을 사용할 수 없는 경우 전송 된 상태로 이동 작업 후에이 스위치를 사용 합니다. 그렇지 않으면가 성공적으로 전송 된 파일만 사용할 수 있습니다.

## <a name="syntax"></a>구문

```
bitsadmin /complete <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제

작업의 상태를 전송 하는 경우 BITS가 작업의 모든 파일을 전송 했습니다. 그러나 파일이 사용할 수 없는 사용 하기 전에 **완료 /** 전환 합니다. 여러 작업을 사용 하는 경우 *myDownloadJob* 해당 이름으로 바꿔야 *myDownloadJob* 작업을 고유 하 게 식별 하는 작업의 GUID를 가진 합니다.
```
C:\>bitsadmin /complete myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)