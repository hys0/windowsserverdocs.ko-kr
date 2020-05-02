---
title: compact vdisk
description: 동적 확장 VHD (가상 하드 디스크) 파일의 실제 크기를 줄이는 compact vdisk 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 40ca0820-67de-4160-b62a-e9bf63fe2790
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4ae5c653645c9f6f3ef97501a59932682c24be3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82711146"
---
# <a name="compact-vdisk"></a>compact vdisk

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

동적 확장 VHD (가상 하드 디스크) 파일의 실제 크기를 줄입니다. 이 매개 변수는 파일을 추가할 때 동적으로 확장 되는 Vhd 크기가 증가 하기 때문에 유용 하지만 파일을 삭제할 때 크기를 자동으로 줄이지 않습니다.

## <a name="syntax"></a>구문

```
compact vdisk
```

### <a name="remarks"></a>설명

- 이 작업이 성공 하려면 동적 확장 VHD를 선택 해야 합니다. [Select vdisk 명령을](select-vdisk.md) 사용 하 여 VHD를 선택 하 고 포커스를 이동 합니다.

- 분리 되거나 읽기 전용으로 연결 된 경우에만 압축을 동적으로 확장할 수 있습니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [vdisk 명령 연결](attach-vdisk.md)

- [detail vdisk 명령](detail-vdisk.md)

- [Vdisk 명령 분리](detach-vdisk.md)

- [확장 vdisk 명령](expand-vdisk.md)

- [Merge vdisk 명령](merge-vdisk.md)

- [vdisk 명령 선택](select-vdisk.md)

- [list 명령](list.md)
