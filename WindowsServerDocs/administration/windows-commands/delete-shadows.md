---
title: 그림자를 삭제 합니다.
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b0d5414cb5b60face5245d7ea22d66c8629bfcb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873734"
---
# <a name="delete-shadows"></a>그림자를 삭제 합니다.



섀도 복사본을 삭제 합니다.

## <a name="syntax"></a>구문

```
delete shadows [all | volume <Volume> | oldest <Volume> | set <SetID> | id <ShadowID> | exposed {<Drive> | <MountPoint>}]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|모든|모든 섀도 복사본을 삭제합니다.|
|볼륨 \<볼륨 >|지정 된 볼륨의 모든 섀도 복사본을 삭제합니다.|
|가장 오래 된 \<볼륨 >|지정 된 볼륨의 가장 오래 된 섀도 복사본을 삭제합니다.|
|set \<SetID>|지정 된 ID의 섀도 복사본 집합에 대 한 섀도 복사본을 삭제 사용 하 여 별칭을 지정할 수는 **%** 별칭 현재 환경에 있는 경우 기호입니다.|
|id \<ShadowID>|지정 된 ID의 섀도 복사본을 삭제합니다. 사용 하 여 별칭을 지정할 수는 **%** 별칭 현재 환경에 있는 경우 기호입니다.|
|노출 {\<드라이브 > | <MountPoint>}|지정한 드라이브 문자 또는 탑재 지점에서 노출 하는 섀도 복사본을 삭제 합니다. C:\mountPoint 또는 p:와 같은 드라이브 문자 탑재 지점을 지정 합니다.|

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)