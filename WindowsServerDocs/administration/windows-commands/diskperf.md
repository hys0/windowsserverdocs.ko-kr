---
title: diskperf
description: Windows를 실행 하는 컴퓨터에서 실제 또는 논리 디스크 성능 카운터를 원격으로 사용 하거나 사용 하지 않도록 설정 하는 데 사용할 수 있는 diskperf 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f06916e8-069b-4ec8-a6eb-59f1d9f77111
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 092518f414d6e27436c46ffd6f9f15b6e6c0407e
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992434"
---
# <a name="diskperf"></a>diskperf

**Diskperf** 명령은 Windows를 실행 하는 컴퓨터에서 원격으로 실제 또는 논리 디스크 성능 카운터를 사용 하거나 사용 하지 않도록 설정 합니다.

## <a name="syntax"></a>구문

```
diskperf [-y[d|v] | -n[d|v]] [\\computername]
```

## <a name="options"></a>옵션

| 옵션 | Description |
| ------ | ----------- |
| -y | 컴퓨터를 다시 시작할 때 모든 디스크 성능 카운터를 시작 합니다. |
| -yd | 컴퓨터를 다시 시작할 때 실제 드라이브에 대해 디스크 성능 카운터를 사용 하도록 설정 합니다. |
| -yv | 컴퓨터를 다시 시작할 때 논리 드라이브 또는 저장소 볼륨에 대 한 디스크 성능 카운터를 사용 하도록 설정 합니다. |
| -n | 컴퓨터를 다시 시작할 때 모든 디스크 성능 카운터를 사용 하지 않도록 설정 합니다. |
| -nd | 컴퓨터를 다시 시작할 때 실제 드라이브에 대해 디스크 성능 카운터를 사용 하지 않도록 설정 합니다. |
| -nv | 컴퓨터를 다시 시작할 때 논리 드라이브 또는 저장소 볼륨에 대 한 디스크 성능 카운터를 사용 하지 않도록 설정 합니다. |
| `\\<computername>` | 디스크 성능 카운터를 사용 하거나 사용 하지 않도록 설정할 컴퓨터의 이름을 지정 합니다. |
| -? | 도움말 상황에 맞는 표시 합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
