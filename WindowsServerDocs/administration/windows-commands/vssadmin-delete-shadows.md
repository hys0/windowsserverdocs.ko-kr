---
title: Vssadmin 삭제 그림자
description: Vssadmin 삭제 그림자 명령의 설명입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 71119174c7fc5929eb4e1982183ba0aed7eb1735
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847094"
---
# <a name="vssadmin-delete-shadows"></a>Vssadmin 삭제 그림자

>적용 대상: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

지정된 된 볼륨의 섀도 복사본을 삭제합니다.

## <a name="syntax"></a>구문

```PowerShell
vssadmin delete shadows /for=<ForVolumeSpec> [/oldest | /all | /shadow=<ShadowID>] [/quiet]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---|---|
|/for=\<ForVolumeSpec>|볼륨의 섀도 복사본 삭제 되도록 지정 합니다.|
|/oldest|가장 오래 된 섀도 복사본을 삭제합니다.|
|/all|모든 지정 된 볼륨의 섀도 복사본을 삭제합니다.|
|/shadow=\<ShadowID>|ShadowID로 지정 된 섀도 복사본을 삭제 합니다. 섀도 복사본 ID을 사용 합니다 **list shadows** 명령입니다. 섀도 복사본 ID를 입력 하면 다음 형식을 사용 하 여 여기서 각 *X* 16 진수 문자를 나타냅니다.<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|
|/quiet|명령을 실행 하는 동안 메시지를 표시 되지 않습니다 지정 합니다.|

## <a name="remarks"></a>설명

섀도 복사본 클라이언트에서 액세스할 수 있는 형식을 사용 하 여 삭제할 수 있습니다.

## <a name="examples"></a>예

볼륨 C의 가장 오래 된 섀도 복사본을 삭제 하려면 다음이 명령을 입력 합니다.

```PowerShell
vssadmin delete shadows /for=c: /oldest
```

## <a name="additional-references"></a>추가 참조

* [명령줄 구문 키](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)
* [List shadows](vssadmin-list-shadows.md)