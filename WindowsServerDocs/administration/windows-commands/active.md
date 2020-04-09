---
title: 활성
description: '**활성**에 대 한 Windows 명령 항목 (기본 디스크에서)은 포커스가 있는 파티션을 활성으로 표시 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f25da2e-87fc-4392-a7ee-f38d09b7873c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 42f2e0d367344355e8f9a570f37cfbdc5dfc4590
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851376"
---
# <a name="active"></a>활성

기본 디스크에 활성으로 포커스가 있는 파티션을 표시합니다.

> [!CAUTION]
> DiskPart는 파티션을 운영 체제 시작 파일이 포함 될 수 인지만 확인 합니다. 파티션의 내용을 확인 하지 않습니다. 파티션을 활성으로 잘못 표시 하는 경우 운영 체제 시작 파일을 포함 하지 않는 컴퓨터 시작할 수 없습니다.

## <a name="syntax"></a>구문

```
active
```- 

## Remarks

-   This informs the basic input/output system (BIOS) or Extensible Firmware Interface (EFI) that the partition or volume is a valid system partition or system volume.

-   Only partitions can be marked as active.

-   A partition must be selected for this operation to succeed. Use the **select partition** command to select a partition and shift the focus to it.

## <a name=BKMK_examples></a>Examples

To mark the partition with focus as the active partition, type:

```
활성
```
## Additional References

- [Command-Line Syntax Key](command-line-syntax-key.md)