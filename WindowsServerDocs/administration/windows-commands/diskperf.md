---
title: diskperf
description: Windows 2000를 실행 하는 컴퓨터에서 실제 또는 논리 디스크 성능 카운터를 원격으로 사용 하거나 사용 하지 않도록 설정 하는 데 사용할 수 있는 diskperf에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f06916e8-069b-4ec8-a6eb-59f1d9f77111
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1b07471c051d57d0279e4fd8b38afdc4acdc4069
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845466"
---
# <a name="diskperf"></a>diskperf

Windows 2000에서는 실제 및 논리 디스크 성능 카운터가 기본적으로 사용 되지 않습니다.

**Diskperf** 는 windows XP, windows server 2003, windows server 2008, windows Vista, windows Server 2008 R2 및 windows 7에 포함 되어 있으므로 windows 2000을 실행 하는 컴퓨터에서 실제 또는 논리 디스크 성능 카운터를 원격으로 사용 하거나 사용 하지 않도록 설정할 수 있습니다.

## <a name="syntax"></a>구문

```
diskperf [-Y[D|V] | -N[D|V]] [\\computername]
```

## <a name="options"></a>옵션

|옵션|설명|
|------|-----------|
|-?|도움말 상황에 맞는 표시 합니다.|
|-Y|컴퓨터를 다시 시작할 때 모든 디스크 성능 카운터를 시작 합니다.|
|-YD|컴퓨터를 다시 시작할 때 실제 드라이브에 대해 디스크 성능 카운터를 사용 하도록 설정 합니다.|
|-YV|컴퓨터를 다시 시작할 때 논리 드라이브 또는 저장소 볼륨에 대해 디스크 성능 카운터를 사용 하도록 설정 합니다.|
|-N|컴퓨터를 다시 시작할 때 모든 디스크 성능 카운터를 사용 하지 않도록 설정 합니다.|
|-ND|컴퓨터를 다시 시작할 때 실제 드라이브에 대해 디스크 성능 카운터를 사용 하지 않도록 설정 합니다.|
|-NV|컴퓨터를 다시 시작할 때 논리 드라이브 또는 저장소 볼륨에 대 한 디스크 성능 카운터를 사용 하지 않도록 설정 합니다.|
|\\\\ *\<computername >*|디스크 성능 카운터를 사용 하거나 사용 하지 않도록 설정할 컴퓨터의 이름을 지정 합니다.|