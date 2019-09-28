---
title: bitsadmin wrap
description: '**Bitsadmin 줄 바꿈** 에 대 한 Windows 명령 항목-명령 창의 가장 오른쪽 가장자리를 벗어나 확장 되는 출력 텍스트 줄을 다음 줄로 줄 바꿈 합니다.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 5609fb6f38716795a545e0c7fe3939f893a8c8d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380682"
---
# <a name="bitsadmin-wrap"></a>bitsadmin wrap

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

출력을 명령 창에 맞게 래핑합니다.

## <a name="syntax"></a>구문

```
bitsadmin /Wrap Job
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

다른 스위치 앞에를 지정 합니다. 기본적으로 [bitsadmin 모니터](bitsadmin-monitor.md) 스위치를 제외한 모든 스위치는 출력을 래핑합니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 이름이 *Mydownloadjob* 인 작업에 대 한 정보를 검색 하 고 출력을 래핑합니다.

```
C:\>bitsadmin /Wrap /Info myDownloadJob /verbose
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
