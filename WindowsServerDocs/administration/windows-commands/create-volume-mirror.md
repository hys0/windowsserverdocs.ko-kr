---
title: 볼륨 미러 만들기
description: 지정 된 두 동적 디스크를 사용 하 여 볼륨 미러를 만드는 볼륨 미러 만들기 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 48776917-783a-47ff-8da4-1cab77cea34b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: be6e4496876636351b6e0853626a9ff9bb421f18
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993254"
---
# <a name="create-volume-mirror"></a>볼륨 미러 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 동적 디스크가 두 개를 사용 하 여 미러를 볼륨을 만듭니다. 볼륨을 만든 후 포커스는 자동으로 새 볼륨으로 이동 합니다.

## <a name="syntax"></a>구문

```
create volume mirror [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| 크기 =`<n>` | 볼륨이 각 디스크에서 차지할 디스크 공간의 크기 (mb)를 지정 합니다. 크기를 지정 하는 경우 새 볼륨 남은 공간 가장 작은 디스크 및 각 후속 디스크에 같은 크기의 공간을 차지 합니다. |
| disk =`<n>`,`<n>`[`,<n>,...`] | 미러 볼륨이 만들어집니다 동적 디스크를 지정 합니다. 미러 볼륨을 만들려면 두 가지 동적 디스크가 필요 합니다. 지정 된 크기와 같은 공간 크기는 **크기** 매개 변수는 각 디스크에 할당 됩니다. |
| align =`<n>` | 모든 볼륨 범위에 있는 가장 가까운 맞춤 경계선을 맞춥니다. 이 매개 변수는 일반적으로 성능을 향상 시키기 위해 하드웨어 RAID LUN (논리 단위 번호) 배열과 함께 사용 됩니다. `<n>`디스크의 시작부터 가장 가까운 맞춤 경계로 해당 하는 킬로바이트 (KB)의 수입니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 오류 지점이 수행 합니다. |

## <a name="examples"></a>예

1과 2를 디스크에 크기가 1000 메가바이트 미러 볼륨을 만들려면 다음을 입력 합니다.

```
create volume mirror size=1000 disk=1,2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [create 명령](create.md)
