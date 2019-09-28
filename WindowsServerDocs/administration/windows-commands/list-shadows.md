---
title: 섀도 목록 표시
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe568423-00ae-4ede-a1e7-07977cb50ad1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2640c04aef34cd6433efe529ac08c0294ba1c3b9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374763"
---
# <a name="list-shadows"></a>섀도 목록 표시



시스템에 있는 영구 및 기존 비영구 섀도 복사본을 나열 합니다.

## <a name="syntax"></a>구문

```
list shadows {all | set <SetID> | id <ShadowID>}
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|모두|모든 섀도 복사본을 나열합니다.|
|\<SetID > 설정|섀도 복사본에 지정 된 섀도 복사본 세트 ID에 속하는 나열|
|id \<ShadowID >|지정 된 섀도 복사본 ID 가진 모든 섀도 복사본을 나열합니다.|

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)