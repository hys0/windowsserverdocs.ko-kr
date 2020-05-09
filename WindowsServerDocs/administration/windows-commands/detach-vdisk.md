---
title: 분리 vdisk
description: 선택 된 가상 하드 디스크 (VHD)가 호스트 컴퓨터의 로컬 하드 디스크 드라이브로 나타나지 않도록 하는 detach vdisk 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5f01dcb8-9237-4564-ad94-8a8dd0fd0cca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 427b27630341589f3ff6dd422667e1247f5b64ec
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993079"
---
# <a name="detach-vdisk"></a>분리 vdisk

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

선택한 VHD (가상 하드 디스크)가 호스트 컴퓨터의 로컬 하드 디스크 드라이브로 나타나지 않도록 합니다. VHD를 분리 하는 경우에 다른 위치에 복사할 수 있습니다. 시작 하기 전에이 작업을 수행 하려면 VHD를 선택 해야 합니다. 사용 하 여는 [vdisk 선택](select-vdisk.md) VHD를 선택 하 고 포커스를 이동 하는 명령입니다.


## <a name="syntax"></a>구문

```
detach vdisk [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="examples"></a>예

선택한 VHD를 분리 하려면 다음을 입력 합니다.

```
detach vdisk
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [vdisk 명령 연결](attach-vdisk.md)

- [compact vdisk 명령](compact-vdisk.md)

- [detail vdisk 명령](detail-vdisk.md)

- [확장 vdisk 명령](expand-vdisk.md)

- [Merge vdisk 명령](merge-vdisk.md)

- [vdisk 명령 선택](select-vdisk.md)

- [list 명령](list.md)
