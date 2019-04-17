---
title: Vssadmin 삭제 그림자
description: Vssadmin 삭제 그림자 명령에 대 한 설명입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 71119174c7fc5929eb4e1982183ba0aed7eb1735
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082448"
---
# <a name="vssadmin-delete-shadows"></a>Vssadmin 삭제 그림자

>적용 대상: 10 Windows, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

지정된 된 볼륨 섀도 복사본을 삭제합니다.

## <a name="syntax"></a>구문

```PowerShell
vssadmin delete shadows /for=<ForVolumeSpec> [/oldest | /all | /shadow=<ShadowID>] [/quiet]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---|---|
|/ =에 대 한 \ < ForVolumeSpec >|어떤 볼륨 섀도 복사본을 삭제할 수를 지정 합니다.|
|가장 오래 된 /|가장 오래 된 섀도 복사본을 삭제합니다.|
|모든 /|지정된 된 볼륨 섀도 복사본을 모두 삭제합니다.|
|그림자 / = \ < ShadowID >|ShadowID에서 지정한 섀도 복사본을 삭제 합니다. 섀도 복사본 ID **vssadmin 목록 그림자** 명령을 사용 하십시오. 섀도 복사본 ID를 입력 하는 경우는 다음과 같은 형식을 사용 여기서 각각의 *X* 16 진수 문자를 나타냅니다.<br><br>XXXXXXXX-이며-이며-이며-XXXXXXXXXXXX|
|자동 /|명령을 실행 하는 동안 메시지를 표시 되지 않습니다를 지정 합니다.|

## <a name="remarks"></a>설명

클라이언트에서 액세스할 수 있는 형식에만 섀도 복사본을 삭제할 수 있습니다.

## <a name="examples"></a>예

C 볼륨의 가장 오래 된 섀도 복사본을 삭제 하려면 다음이 명령을 입력 합니다.

```PowerShell
vssadmin delete shadows /for=c: /oldest
```

## <a name="additional-references"></a>추가 참조 자료

* [명령줄 구문 키](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)
* [Vssadmin 목록 그림자](vssadmin-list-shadows.md)