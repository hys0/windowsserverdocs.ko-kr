---
title: expose
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55cc7a292b81977a346f3f078a3b5623243ea46c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844806"
---
# <a name="expose"></a>expose



드라이브 문자, 공유 또는 탑재 지점으로 영구 섀도 복사본을 노출합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
expose <ShadowID> {<Drive:> | <Share> | <MountPoint>}
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|ShadowID|노출 하려는 섀도 복사본의 그림자 ID를 지정 합니다.|
|\<드라이브: >|드라이브 문자로 지정 된 섀도 복사본을 노출 합니다 (예: P:).|
|\<공유 >|공유에서 지정 된 섀도 복사본을 노출 합니다 (예: \\\\*MachineName*\)).|
|\<탑재 지점 >|탑재 지점에 지정 된 섀도 복사본을 노출 합니다 (예: C:\shadowcopy\)).|

## <a name="remarks"></a>주의

-   *ShadowID*대신 기존 별칭 또는 환경 변수를 사용할 수 있습니다. 사용 하 여 **추가** 매개 변수 없이 기존 별칭을 참조 하십시오.

## <a name="examples"></a><a name=BKMK_examples></a>예와

VSS_SHADOW_1 환경 변수와 연결 된 영구 섀도 복사본을 드라이브 X로 노출 하려면 다음을 입력 합니다.
```
expose %vss_shadow_1% x:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)