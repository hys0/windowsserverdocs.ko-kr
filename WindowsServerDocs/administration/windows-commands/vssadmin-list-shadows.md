---
title: List shadows
description: Vssadmin 목록에 대 한 설명을 명령 섀도 처리합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 07da36da1473563c3236a4fafc3ceae06259981a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861154"
---
# <a name="vssadmin-list-shadows"></a>List shadows

>적용 대상: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

지정된 된 볼륨의 모든 기존 섀도 복사본을 나열합니다. 매개 변수 없이이 명령을 사용 하는 경우 표시 순서에 따라 컴퓨터의 모든 볼륨 섀도 복사본 **섀도 복사본 집합**합니다.

## <a name="syntax"></a>구문

```PowerShell
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---|---|
|/for=\<ForVolumeSpec>|볼륨 섀도 복사본에 대 한 나열 됩니다 지정 합니다.|
|/shadow=\<ShadowID>|ShadowID로 지정 된 섀도 복사본을 나열 합니다. 섀도 복사본 ID을 사용 합니다 **list shadows** 명령입니다. 다음 형식으로 사용 하는 섀도 복사본 ID를 입력 하는 경우 여기서 각 *X* 16 진수 문자를 나타냅니다.<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|

## <a name="additional-references"></a>추가 참조

* [명령줄 구문 키](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)