---
title: bitsadmin wrap
description: Windows 명령 항목에 대 한 **bitsadmin 래핑** -출력 다음 줄을 명령 창 맨 오른쪽 가장자리로 벗어난 텍스트의 줄을 래핑합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4834a8a17c72394b6ee8f051ec76919af9880124
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881674"
---
# <a name="bitsadmin-wrap"></a>bitsadmin wrap

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

명령 창에 맞게 출력을 래핑.

## <a name="syntax"></a>구문

```
bitsadmin /Wrap Job
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

전에 기타 스위치를 지정 합니다. 기본적으로 모든 스위치를 제외 합니다 [bitsadmin 모니터](bitsadmin-monitor.md) 전환, 출력을 래핑합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 정보를 검색 합니다. *myDownloadJob* 출력을 래핑합니다.

```
C:\>bitsadmin /Wrap /Info myDownloadJob /verbose
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
