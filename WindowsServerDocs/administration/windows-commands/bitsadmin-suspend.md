---
title: bitsadmin suspend
description: 지정 된 작업을 일시 중단 하는 bitsadmin 일시 중단에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f9d42500-7bea-4aa8-a9f0-c22f6ed3e73b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0419f4cdf59d04539b8b4c6d47cec886197d412b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849056"
---
# <a name="bitsadmin-suspend"></a>bitsadmin suspend

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 작업을 일시 중단합니다.

## <a name="syntax"></a>구문

```
bitsadmin /Suspend <Job>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>주의

작업을 다시 시작 하려면 [bitsadmin resume](bitsadmin-resume.md) 스위치를 사용 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업을 일시 중단 *myDownloadJob*합니다.

```
C:\>bitsadmin /Suspend myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
