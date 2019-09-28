---
title: Vssadmin list 그림자
description: Vssadmin list shadows 명령에 대 한 설명입니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 49bee3deac463b68fda94097bb183bcbf1c89810
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362586"
---
# <a name="vssadmin-list-shadows"></a>Vssadmin list 그림자

>적용 대상: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, windows server 2012, windows server 2008 R2, Windows Server 2008

지정 된 볼륨의 모든 기존 섀도 복사본을 나열 합니다. 이 명령을 매개 변수 없이 사용 하면 컴퓨터의 모든 볼륨 섀도 복사본이 **섀도 복사본 집합**에 따라 결정 된 순서 대로 표시 됩니다.

## <a name="syntax"></a>구문

```PowerShell
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---|---|
|/for = \<ForVolumeSpec >|섀도 복사본이 나열 될 볼륨을 지정 합니다.|
|/shadow = \<ShadowID >|ShadowID에 지정 된 섀도 복사본을 나열 합니다. 섀도 복사본 ID를 가져오려면 **vssadmin list shadows** 명령을 사용 합니다. 섀도 복사본 ID를 입력할 때 다음 형식을 사용 합니다. 여기서 각 *X* 는 16 진수 문자를 나타냅니다.<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX-XXXX-XXXX|

## <a name="additional-references"></a>추가 참조

* [명령줄 구문 키](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [List](vssadmin.md)