---
title: create volume stripe
description: 두 개 이상의 지정 된 동적 디스크를 사용 하 여 스트라이프 볼륨을 만드는 볼륨 스트라이프 만들기 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 20dce735-5f7c-4f83-a580-d087e2913a00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8cb20a7741d49201b88345374ba1c435e81a77f6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929524"
---
# <a name="create-volume-stripe"></a>create volume stripe

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

두 개 이상의 지정 된 동적 디스크를 사용 하 여 스트라이프 볼륨을 만듭니다. 볼륨을 만든 후 포커스는 자동으로 새 볼륨으로 이동 합니다.

## <a name="syntax"></a>구문

```
create volume stripe [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- |  -----------|
| 크기 =`<n>` | 볼륨이 각 디스크에서 차지 하는 디스크 공간의 크기 (mb)입니다. 크기를 지정 하는 경우 새 볼륨 남은 공간 가장 작은 디스크 및 각 후속 디스크에 같은 크기의 공간을 차지 합니다. |
| 디스크 =`<n>,<n>[,<n>,...]` | 동적 디스크는 스트라이프 볼륨 생성 됩니다. 스트라이프 볼륨을 만들려면 두 개 이상의 동적 디스크가 필요 합니다. 에 해당 하는 공간의 크기는 `size=<n>` 각 디스크에 할당 됩니다. |
| align =`<n>` | 모든 볼륨 범위에 있는 가장 가까운 맞춤 경계선을 맞춥니다. 일반적으로 성능 향상을 위해 하드웨어 RAID 논리 단위 번호 (LUN) 배열과 함께 사용. `<n>`디스크의 시작부터 가장 가까운 맞춤 경계로 해당 하는 킬로바이트 (KB)의 수입니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="examples"></a>예

1과 2를 디스크에 크기가 1000 메가바이트 스트라이프 볼륨을 만들려면 다음을 입력 합니다.

```
create volume stripe size=1000 disk=1,2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [create 명령](create.md)
