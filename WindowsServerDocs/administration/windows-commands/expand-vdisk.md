---
title: vdisk 확장
description: VHD (가상 하드 디스크)를 지정 된 크기로 확장 하는 expand vdisk 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ae547b4-3813-4b86-bacd-bc273c028a2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 48973178f35f792b52fa81e5ed59449ca5db2559
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436188"
---
# <a name="expand-vdisk"></a>vdisk 확장

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

VHD (가상 하드 디스크)를 지정 된 크기로 확장 합니다.

VHD는 선택 하 고이 작업이 성공 하기 위해 분리 해야 합니다. [Select vdisk 명령을](select-vdisk.md) 사용 하 여 볼륨을 선택 하 고 포커스를 이동 합니다.

## <a name="syntax"></a>구문

```
expand vdisk maximum=<n>
```

### <a name="parameters"></a>매개 변수

 | 매개 변수 | 설명 |
 |---------- | ----------- |
 | 최대값 =`<n>` | 메가바이트 (MB) 단위로 VHD에 대 한 새 크기를 지정합니다. |

### <a name="examples"></a>예

선택한 VHD를 20GB로 확장 하려면 다음을 입력 합니다.

```
expand vdisk maximum=20000
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [vdisk 명령 선택](select-vdisk.md)

- [vdisk 명령 연결](attach-vdisk.md)

- [compact vdisk 명령](compact-vdisk.md)

- [vdisk 명령 분리](detach-vdisk.md)

- [detail vdisk 명령](detail-vdisk.md)

- [merge vdisk 명령](merge-vdisk.md)

- [list 명령](list.md)
