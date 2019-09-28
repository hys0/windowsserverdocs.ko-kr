---
title: expose
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 819484364e8375c4d58e4d022681eedeaa7084ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377281"
---
# <a name="expose"></a>expose



드라이브 문자, 공유 또는 탑재 지점으로 영구 섀도 복사본을 노출합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
expose <ShadowID> {<Drive:> | <Share> | <MountPoint>}
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|ShadowID|노출 하려는 섀도 복사본의 그림자 ID를 지정 합니다.|
|\<Drive: >|드라이브 문자로 지정 된 섀도 복사본을 노출 합니다 (예: P:).|
|\<Share >|공유에 지정 된 섀도 복사본을 노출 합니다 (예: \\ @ no__t-1*MachineName*\)).|
|\<MountPoint|탑재 지점에 지정 된 섀도 복사본을 노출 합니다 (예: C:\shadowcopy @ no__t-0).|

## <a name="remarks"></a>설명

-   *ShadowID*대신 기존 별칭 또는 환경 변수를 사용할 수 있습니다. 사용 하 여 **추가** 매개 변수 없이 기존 별칭을 참조 하십시오.

## <a name="BKMK_examples"></a>예와

VSS_SHADOW_1 환경 변수와 연결 된 영구 섀도 복사본을 드라이브 X로 노출 하려면 다음을 입력 합니다.
```
expose %vss_shadow_1% x:
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)