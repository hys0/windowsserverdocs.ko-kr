---
title: bdehdcfg driveinfo
description: '에 대 한 Windows 명령을 항목 * * bdehdcfg: driveinfo * *-드라이브 문자, 총 크기, 최대 여유 공간, 및 파티션 특성을 표시 합니다.'
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2d065e7-eced-4509-a1a0-ee2521a7f02e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4aa041c27b1797e7d00476212887a7dc6dbc1880
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889064"
---
# <a name="bdehdcfg-driveinfo"></a>bdehdcfg: driveinfo

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

드라이브 문자, 총 크기, 최대 여유 공간, 및 파티션 특성을 표시합니다. 유효한 파티션으로 나열 됩니다. 4 개의 주 또는 확장 된 파티션이 이미 존재 하는 경우에 할당 되지 않은 공간 나열 되지 않습니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.
## <a name="syntax"></a>구문
```
bdehdcfg -driveinfo <DriveLetter>
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|<DriveLetter>|드라이브 문자 뒤에 콜론으로 지정 합니다.|
## <a name="remarks"></a>설명
이 명령은 정보 제공 용 이므로 이며은 드라이브를 수정 하지 않습니다.
## <a name="BKMK_Examples"></a>예제
다음 예제에서는 C 드라이브에 대 한 드라이브 정보를 표시 합니다.
```
bdehdcfg  driveinfo C:
```
## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)
-   [bdehdcfg](bdehdcfg.md)
