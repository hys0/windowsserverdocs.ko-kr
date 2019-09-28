---
title: 별칭 추가
description: '**별칭 추가** 에 대 한 Windows 명령 항목-별칭 환경에 별칭을 추가 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5fe12f5d-11e9-4f3d-b7f9-40b26c8685e5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f2834376e497f54eadf1d9077e74f9c398202c5a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382821"
---
# <a name="add-alias"></a>별칭 추가



별칭 환경에 별칭을 추가합니다. 매개 변수 없이 사용 하는 경우 **별칭 추가** 명령 프롬프트에서 도움말을 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
add alias <AliasName> <AliasValue>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|@no__t 0AliasName >|별칭의 이름을 지정합니다.|
|@no__t 0AliasValue >|별칭 값을 지정합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   별칭 메타 데이터 파일에 저장 되 고으로 로드 되는 **메타 데이터를 로드** 명령입니다.

## <a name="BKMK_examples"></a>예와

해당 별칭을 포함 하 여 모든 그림자를 나열 하려면 다음을 입력 합니다.
```
list shadows all
```
다음 발췌에서는 기본 별칭 VSS_SHADOW_x가 할당 된 섀도 복사본을 보여 줍니다.
```
* Shadow Copy ID = {ff47165a-1946-4a0c-b7f4-80f46a309278}
%VSS_SHADOW_1%
```
이 섀도 복사본에 system1 파티션이나 라는 이름의 새 별칭을 할당 하려면 다음을 입력 합니다.
```
add alias System1 %VSS_SHADOW_1%
```
또는 섀도 복사본 ID를 사용 하 여 별칭을 할당할 수 있습니다.
```
add alias System1 {ff47165a-1946-4a0c-b7f4-80f46a309278}
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)