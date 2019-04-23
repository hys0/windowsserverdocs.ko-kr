---
title: Vdisk를 병합 합니다.
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5865bb08-89a3-406c-8328-0ef8868d03e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 159e307912cb06bc3ea5e452f735e786c0cf9965
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847014"
---
# <a name="merge-vdisk"></a>Vdisk를 병합 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

차이점 보관용 가상 하드 디스크 (VHD) VHD 해당 부모와 함께 병합합니다. 부모 VHD 차이점 보관용 VHD에서 수정 내용을 적용 하도록 수정 됩니다.
> [!NOTE]
> 이 명령은 Windows 7과 Windows Server 2008 r 2에 적용 됩니다.
## <a name="syntax"></a>구문
```
merge vdisk depth=<n>
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|depth=<n>|병합 부모 VHD 파일의 수를 나타냅니다. 예를 들어 **깊이 = 1** 차이점 보관용 체인의 한 수준으로 차이점 보관용 VHD를 병합할 나타냅니다.|
## <a name="remarks"></a>설명
-   VHD는 선택 하 고이 작업이 성공 하기 위해 분리 해야 합니다. 사용 하 여는 **vdisk 선택** VHD를 선택 하 고 포커스를 이동 하는 명령입니다.
-   이 매개 변수에서 부모 VHD를 수정합니다. 결과적으로, 부모에 종속 되어 있는 기타 차이점 보관용 Vhd를 더 이상 유효 하지 않습니다.
## <a name="BKMK_Examples"></a>예제
VHD 부모를 사용 하 여 차이점 보관용 VHD를 병합 하려면 다음을 입력 합니다.
```
merge vdisk depth=1
```
## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)
-   [vdisk를 연결 합니다.](attach-vdisk.md)
-   [vdisk를 압축 합니다.](compact-vdisk.md)

-   [세부 vdisk](detail-vdisk.md)
-   [Vdisk를 분리 합니다.](detach-vdisk.md)
-   [vdisk를 확장 합니다.](expand-vdisk.md)
-   [vdisk를 선택 합니다.](select-vdisk.md)
-   [list_1](list_1.md)
