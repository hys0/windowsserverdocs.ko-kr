---
title: 숨깁니다
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58dc7d0f-52e9-4587-9487-d3b4c3e52640
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e10126739ef82b060e271e9b804a77658b5ec82
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392268"
---
# <a name="unexpose"></a>숨깁니다



**공개 명령을 사용** 하 여 노출 된 섀도 복사본을 노출 하지 않습니다. 노출 된 섀도 복사본은 섀도 ID, 드라이브 문자, 공유 또는 탑재 지점으로 지정할 수 있습니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
unexpose {<ShadowID> | <Drive:> | <Share> | <MountPoint>}
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|@no__t 0ShadowID >|지정 된 섀도 ID로 지정 된 섀도 복사본을 노출 하지 않습니다.|
|\<Drive: >|지정 된 드라이브 문자 (예: P 드라이브)와 연결 된 섀도 복사본을 노출 하지 않습니다.|
|\<Share >|지정 된 공유와 연결 된 섀도 복사본을 공개 하지 않습니다 (예: \\ @ no__t-1*MachineName*\)).|
|\<MountPoint|지정 된 탑재 지점과 연결 된 섀도 복사본을 공개 하지 않습니다 (예: C:\shadowcopy @ no__t-0).|

## <a name="remarks"></a>설명

-   *ShadowID*대신 기존 별칭 또는 환경 변수를 사용할 수 있습니다. 사용 하 여 **추가** 매개 변수 없이 기존 별칭을 참조 하십시오.

## <a name="BKMK_examples"></a>예와

숨깁니다 드라이브와 연결 된 섀도 복사본을 복사 하려면 다음을 입력 합니다.
```
unexpose P:
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)