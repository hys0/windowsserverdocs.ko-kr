---
title: vdisk를 확장 합니다.
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ae547b4-3813-4b86-bacd-bc273c028a2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cf8fd0b05ca5baeeee4fadd670adb3169130d04e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837404"
---
# <a name="expand-vdisk"></a>vdisk를 확장 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

가상 하드 디스크 (VHD)를 지정 하는 크기로 확장 합니다.
> [!NOTE]
> 이 명령은 Windows 7과 Windows Server 2008 r 2에 적용 됩니다.
## <a name="syntax"></a>구문
```
expand vdisk maximum=<n>
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|최대 =<n>|메가바이트 (MB) 단위로 VHD에 대 한 새 크기를 지정합니다.|
## <a name="remarks"></a>설명
-   VHD는 선택 하 고이 작업이 성공 하기 위해 분리 해야 합니다. 사용 하는 **vdisk를 선택** 볼륨을 선택 하 고 포커스를 이동 하는 명령입니다.
## <a name="BKMK_Examples"></a>예제
선택한 VHD를 20GB로 확장 하려면 다음을 입력 합니다.
```
expand vdisk maximum=20000
```
## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)
-   [vdisk를 연결 합니다.](attach-vdisk.md)
-   [vdisk를 압축 합니다.](compact-vdisk.md)

-   [Vdisk를 분리 합니다.](detach-vdisk.md)
-   [세부 vdisk](detail-vdisk.md)
-   [Vdisk를 병합 합니다.](merge-vdisk.md)
-   [vdisk를 선택 합니다.](select-vdisk.md)
-   [list_1](list_1.md)
