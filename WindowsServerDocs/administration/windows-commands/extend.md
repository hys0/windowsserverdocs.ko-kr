---
title: extend
description: 포커스가 있는 볼륨 또는 파티션과 파일 시스템을 디스크의 사용 가능한 공간 (할당 되지 않은)으로 확장 하는 확장 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2414e21d-fc0b-40e8-9e33-3e072f8ad76b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fd10e2ad4d6d647f37e1ad113f1516104e66315f
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437198"
---
# <a name="extend"></a>extend

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포커스가 있는 볼륨 또는 파티션을 디스크의 사용 가능한 공간 (할당 되지 않은)으로 확장 합니다.

## <a name="syntax"></a>구문

```
extend [size=<n>] [disk=<n>] [noerr]
extend filesystem [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 크기 =`<n>` | 현재 볼륨 또는 파티션에 추가할 공간의 크기 (MB)를 지정 합니다. 크기를 지정 하는 경우 디스크에서 사용할 수 있는 연속 된 여유 공간을 모두 사용 됩니다. |
| 디스크 =`<n>` | 볼륨 또는 파티션이 확장 디스크를 지정 합니다. 없는 디스크를 지정 하는 경우 현재 디스크에 볼륨 또는 파티션이 확장 됩니다. |
| 파일 시스템 | 포커스가 있는 볼륨의 파일 시스템을 확장합니다. 디스크에 파일 시스템 볼륨으로 확장 되지 않은 경우에 사용할 수 있습니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

#### <a name="remarks"></a>설명

- 기본 디스크의 사용 가능한 공간이 볼륨 또는 포커스가 있는 파티션을 동일한 디스크에 있어야 합니다. 또한 포커스가 있는 볼륨 또는 파티션을 즉시 따라야 합니다. 즉, 다음 섹터 오프셋에서 시작 해야 합니다.

- 단순 또는 스팬 볼륨 동적 디스크에 볼륨은 동적 디스크의 여유 공간으로 확장할 수 있습니다. 이 명령을 사용 하 여, 스팬된 동적 볼륨으로 간단한 동적 볼륨을 변환할 수 있습니다. 미러된, RAID-5 및 스트라이프 볼륨을 확장할 수 없습니다.

- 이전에 파티션을 NTFS 파일 시스템으로 포맷, 파일 시스템은 더 큰 파티션에 자동으로 확장 하 고 데이터 손실을 발생 합니다.

- 이전에 파티션을 NTFS 이외의 파일 시스템으로 포맷, 파티션에 변경 되지 않고는 명령이 실패 합니다.

- 이전에 파티션의 파일 시스템으로 포맷 되지, 파티션은 여전히 확장할 수 있습니다.

- 파티션을 확장할 수는 연결 된 볼륨이 있어야 합니다.

## <a name="examples"></a>예

디스크 3, 500mb 하 여 볼륨 또는 포커스가 있는 파티션을 확장 하려면 다음을 입력 합니다.

```
extend size=500 disk=3
```

볼륨의 파일 시스템을 확장 된 후 확장 하려면 다음을 입력 합니다.

```
extend filesystem
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
