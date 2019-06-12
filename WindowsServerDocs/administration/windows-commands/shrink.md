---
title: 축소
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec87cc7c-9846-465e-a10d-4ee10db4f4e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 09cc9ce7beebc04a0a45cd93c2b0da25c5a1a49e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441258"
---
# <a name="shrink"></a>축소

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diskpart 축소 명령을 지정한 양만큼 선택한 볼륨의 크기를 줄입니다. 이 명령은 볼륨의 끝에 사용 되지 않은 공간에서 사용할 수 있는 사용 가능한 디스크 공간을 만듭니다.

## <a name="syntax"></a>구문
```
shrink [desired=<n>] [minimum=<n>] [nowait] [noerr]
shrink querymax [noerr]
```
## <a name="parameters"></a>매개 변수

|  매개 변수  |                                                                                             설명                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| desired=<n> |                                                     원하는 양의 공간 (mb) 볼륨의 크기를 줄이기 위해 하 여 지정 합니다.                                                     |
| minimum=<n> |                                                           해당 볼륨의 크기를 줄이기 위해 mb에서 공간의 최소 크기를 지정 합니다.                                                           |
|  응용   |                       Mb 볼륨을 줄일 수 있는 공간의 최대 크기를 반환 합니다. 응용 프로그램은 현재 볼륨에 액세스 하는 경우이 값이 변경 될 수 있습니다.                        |
|   nowait    |                                                       축소 하는 진행 중인 동안에 즉시 반환 하는 명령을 강제로 수행 합니다.                                                        |
|    noerr    | 만 스크립팅 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="remarks"></a>설명
- 파일 시스템에 없는 경우 또는 NTFS 파일 시스템을 사용 하 여 서식이 지정 하는 경우에 볼륨의 크기를 줄일 수 있습니다.
- 이 명령은 기본 볼륨 단순 또는 스팬 동적 볼륨에 사용 됩니다.
- 원하는 크기를 지정 하지 않은 경우 볼륨이 줄어듭니다 최소한으로 지정 하는 경우.
- 최소 크기를 지정 하지 않은 경우 볼륨이 줄어듭니다 원하는 양으로 지정 하는 경우.
- 볼륨에 따라 줄어듭니다 최소한 아니고 원하는 크기를 지정 하는 경우 최대한 많이 있습니다.
- 최소 크기를 지정 하 고 사용 가능한 빈 공간이 충분 하지 않습니다, 경우 명령이 실패 합니다.
- 이 작업을 수행 하려면 볼륨을 선택 해야 합니다. 사용 하 여는 **볼륨 선택** 볼륨을 선택 하 고 포커스를 이동 하는 명령입니다.
- 이 명령은 원래 장비 제조업체 (OEM) 파티션, 확장 가능 펌웨어 인터페이스 (EFI) 시스템 파티션 또는 복구 파티션을에서 작동 하지 않습니다.
  ## <a name="BKMK_examples"></a>예제
  250와 500 메가바이트 간의 가장 큰 가능한 양만큼 선택한 볼륨의 크기를 줄이려면 다음을 입력 합니다.
  ```
  shrink desired=500 minimum=250
  ```
  볼륨을 줄일 수 있습니다 (mb)의 최대 수를 표시 하려면 다음을 입력 합니다.
  ```
  shrink querymax
  ```

[Resize-Partition](https://technet.microsoft.com/library/hh848680.aspx)
