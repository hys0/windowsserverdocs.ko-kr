---
title: Vssadmin 목록 그림자
description: Vssadmin 목록에 대 한 설명이 숨기는 명령입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 07da36da1473563c3236a4fafc3ceae06259981a
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082539"
---
# <a name="vssadmin-list-shadows"></a>Vssadmin 목록 그림자

>적용 대상: 10 Windows, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

지정 된 볼륨의 모든 기존 섀도 복사본을 나열합니다. 매개 변수 없이이 명령을 사용 하면 모든 볼륨 섀도 복사본 **섀도 복사본을 설정**하 여 지정 하는 순서에 해당 컴퓨터에 표시 됩니다.

## <a name="syntax"></a>구문

```PowerShell
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---|---|
|/ =에 대 한 \ < ForVolumeSpec >|어떤 볼륨 섀도 복사본에 대 한 나열을 지정 합니다.|
|그림자 / = \ < ShadowID >|ShadowID에서 지정한 섀도 복사본을 나열 합니다. 섀도 복사본 ID **vssadmin 목록 그림자** 명령을 사용 하십시오. 섀도 복사본 ID를 입력 하는 경우는 다음과 같은 형식으로을 사용 여기서 각각의 *X* 16 진수 문자를 나타냅니다.<br><br>XXXXXXXX-이며-이며-이며-XXXXXXXXXXXX|

## <a name="additional-references"></a>추가 참조 자료

* [명령줄 구문 키](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)