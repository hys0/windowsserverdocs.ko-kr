---
title: compact vdisk
description: Windows 명령 항목 forcompact vdisk는 동적 확장 VHD (가상 하드 디스크) 파일의 실제 크기를 줄입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 40ca0820-67de-4160-b62a-e9bf63fe2790
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9691be21c188fbc2c3b2e782acde127270decf56
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847426"
---
# <a name="compact-vdisk"></a>compact vdisk

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

동적 확장 VHD (가상 하드 디스크) 파일의 실제 크기를 줄입니다. 이 매개 변수는 파일을 추가할 때 동적으로 확장 되는 Vhd 크기가 증가 하기 때문에 유용 하지만 파일을 삭제할 때 크기를 자동으로 줄이지 않습니다.

> [!NOTE]
> 이 명령은 Windows 7과 Windows Server 2008 r 2에 적용 됩니다.

## <a name="syntax"></a>구문
```
compact vdisk
```

## <a name="remarks"></a>주의

- 이 작업이 성공 하려면 동적 확장 VHD를 선택 해야 합니다. 사용 하 여는 **vdisk 선택** VHD를 선택 하 고 포커스를 이동 하는 명령입니다.

- 분리 되거나 읽기 전용으로 연결 된 Vhd만 동적으로 확장할 수 있습니다.

## <a name="examples"></a><a name=BKMK_Examples></a>예와
동적 확장 VHD를 압축 하려면 다음을 입력 합니다.
```
compact vdisk
```

## <a name="additional-references"></a>추가 참조
- - [명령줄 구문 키](command-line-syntax-key.md)
- [연결 vdisk](attach-vdisk.md)
- [세부 정보 vdisk](detail-vdisk.md)
- [분리 vdisk](detach-vdisk.md)
- [vdisk 확장](expand-vdisk.md)
- [Merge vdisk](merge-vdisk.md)
- [vdisk 선택](select-vdisk.md)
- [list_1](list_1.md)
