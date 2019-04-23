---
title: diskperf
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a99f18b56c9295e902a3c89e2e89b36c9c1b6c89
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852584"
---
# <a name="diskperf"></a>diskperf



Windows 2000에서는 실제 / 논리 디스크 성능 카운터는 기본적으로 사용할 수 없습니다.

**Diskperf** 원격으로 사용 하도록 설정 하거나 실행 하는 컴퓨터의 실제 또는 논리 디스크 성능 카운터를 사용 하지 않도록 설정 하는 데 사용 될 수 있도록 Windows XP, Windows Server 2003, Windows Server 2008, Windows Vista, Windows Server 2008 R2 및 Windows 7에 포함 됩니다 Windows 2000입니다.

## <a name="syntax"></a>구문

```
diskperf [-Y[D|V] | -N[D|V]] [\\computername]
```

## <a name="options"></a>변수

|옵션|설명|
|------|-----------|
|-?|도움말 상황에 맞는 표시 합니다.|
|-y|컴퓨터를 다시 시작할 때 모든 디스크 성능 카운터를 시작 합니다.|
|-YD|컴퓨터 다시 시작 될 때 물리적 드라이브에 대 한 디스크 성능 카운터를 사용 합니다.|
|-YV|컴퓨터가 다시 시작 하는 경우 논리 드라이브 또는 저장소 볼륨의 디스크 성능 카운터를 사용 하도록 설정 합니다.|
|-N|컴퓨터를 다시 시작할 때 모든 디스크 성능 카운터를 사용 하지 않도록 설정 합니다.|
|-ND|컴퓨터 다시 시작 될 때 물리적 드라이브에 대 한 디스크 성능 카운터를 사용 하지 않도록 설정 합니다.|
|-NV|컴퓨터가 다시 시작 하는 경우 논리 드라이브 또는 저장소 볼륨의 디스크 성능 카운터를 사용 하지 않도록 설정 합니다.|
|\\\\*\<computername>*|디스크 성능 카운터를 사용 하지 않도록 설정 하거나 사용 하려는 컴퓨터의 이름을 지정 합니다.|