---
title: vdisk를 압축 합니다.
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40ca0820-67de-4160-b62a-e9bf63fe2790
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ba04bdc8c469ef80853b6092b8745defa1f3f19e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877304"
---
# <a name="compact-vdisk"></a>vdisk를 압축 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

동적 확장 가상 하드 디스크 (VHD) 파일의 실제 크기를 줄입니다. 이 매개 변수 파일을 추가할 수 있지만 이러한 자동으로 줄이지 않는 크기에 파일을 삭제 하면 Vhd 크기 증가 동적으로 확장 되므로 유용 합니다.
> [!NOTE]
> 이 명령은 Windows 7과 Windows Server 2008 r 2에 적용 됩니다.
## <a name="syntax"></a>구문
```
compact vdisk
```
## <a name="remarks"></a>설명
-   이 작업이 성공 하기 위해 동적 확장 VHD는 선택 해야 합니다. 사용 하 여는 **vdisk 선택** VHD를 선택 하 고 포커스를 이동 하는 명령입니다.
-   동적 확장 Vhd 분리 되거나 읽기 전용으로 연결 되는 압축할 수 있습니다.
## <a name="BKMK_Examples"></a>예제
동적 확장 VHD를 압축 하려면 다음을 입력 합니다.
```
compact vdisk
```
## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)
-   [vdisk를 연결 합니다.](attach-vdisk.md)

-   [세부 vdisk](detail-vdisk.md)
-   [Vdisk를 분리 합니다.](detach-vdisk.md)
-   [vdisk를 확장 합니다.](expand-vdisk.md)
-   [Vdisk를 병합 합니다.](merge-vdisk.md)
-   [vdisk를 선택 합니다.](select-vdisk.md)
-   [list_1](list_1.md)
