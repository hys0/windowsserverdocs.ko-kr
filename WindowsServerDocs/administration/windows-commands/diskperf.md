---
title: diskperf
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f06916e8-069b-4ec8-a6eb-59f1d9f77111
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 829f0284d761e6a5134011fa1dff99646d55fc13
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377814"
---
# <a name="diskperf"></a>diskperf



Windows 2000에서는 실제 및 논리 디스크 성능 카운터가 기본적으로 사용 되지 않습니다.

**Diskperf** 는 windows XP, windows server 2003, windows server 2008, windows Vista, windows Server 2008 R2 및 windows 7에 포함 되어 있으므로를 실행 하는 컴퓨터에서 실제 또는 논리 디스크 성능 카운터를 원격으로 사용 하거나 사용 하지 않도록 설정할 수 있습니다. Windows 2000.

## <a name="syntax"></a>구문

```
diskperf [-Y[D|V] | -N[D|V]] [\\computername]
```

## <a name="options"></a>변수

|옵션|설명|
|------|-----------|
|-?|도움말 상황에 맞는 표시 합니다.|
|-y|컴퓨터를 다시 시작할 때 모든 디스크 성능 카운터를 시작 합니다.|
|-YD|컴퓨터를 다시 시작할 때 실제 드라이브에 대해 디스크 성능 카운터를 사용 하도록 설정 합니다.|
|-YV|컴퓨터를 다시 시작할 때 논리 드라이브 또는 저장소 볼륨에 대해 디스크 성능 카운터를 사용 하도록 설정 합니다.|
|-N|컴퓨터를 다시 시작할 때 모든 디스크 성능 카운터를 사용 하지 않도록 설정 합니다.|
|-ND|컴퓨터를 다시 시작할 때 실제 드라이브에 대해 디스크 성능 카운터를 사용 하지 않도록 설정 합니다.|
|-NV|컴퓨터를 다시 시작할 때 논리 드라이브 또는 저장소 볼륨에 대 한 디스크 성능 카운터를 사용 하지 않도록 설정 합니다.|
|\\ @ no__t *\<computername >*|디스크 성능 카운터를 사용 하거나 사용 하지 않도록 설정할 컴퓨터의 이름을 지정 합니다.|