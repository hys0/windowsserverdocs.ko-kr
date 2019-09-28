---
title: Vssadmin delete 그림자
description: Vssadmin delete 그림자 명령에 대 한 설명입니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9779da98ecb43245fe206390d9b70471f15d706e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362611"
---
# <a name="vssadmin-delete-shadows"></a>Vssadmin delete 그림자

>적용 대상: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, windows server 2012, windows server 2008 R2, Windows Server 2008

지정 된 볼륨의 섀도 복사본을 삭제 합니다.

## <a name="syntax"></a>구문

```PowerShell
vssadmin delete shadows /for=<ForVolumeSpec> [/oldest | /all | /shadow=<ShadowID>] [/quiet]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---|---|
|/for = \<ForVolumeSpec >|삭제할 볼륨의 섀도 복사본을 지정 합니다.|
|/oldest|가장 오래 된 섀도 복사본만 삭제 합니다.|
|/all|지정 된 볼륨의 섀도 복사본을 모두 삭제 합니다.|
|/shadow = \<ShadowID >|ShadowID에 지정 된 섀도 복사본을 삭제 합니다. 섀도 복사본 ID를 가져오려면 **vssadmin list shadows** 명령을 사용 합니다. 섀도 복사본 ID를 입력할 때 다음 형식을 사용 합니다. 여기서 각 *X* 는 16 진수 문자를 나타냅니다.<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX-XXXX-XXXX|
|/quiet|명령이 실행 되는 동안 메시지를 표시 하지 않도록 지정 합니다.|

## <a name="remarks"></a>설명

클라이언트 액세스 가능 유형을 사용 하 여 섀도 복사본을 삭제할 수 있습니다.

## <a name="examples"></a>예

볼륨 C의 가장 오래 된 섀도 복사본을 삭제 하려면 다음 명령을 입력 합니다.

```PowerShell
vssadmin delete shadows /for=c: /oldest
```

## <a name="additional-references"></a>추가 참조

* [명령줄 구문 키](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [List](vssadmin.md)
* [Vssadmin list 그림자](vssadmin-list-shadows.md)