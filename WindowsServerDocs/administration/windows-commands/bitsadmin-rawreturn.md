---
title: bitsadmin rawreturn
description: '**Bitsadmin rawreturn** 에 대 한 Windows 명령 항목-구문 분석에 적합 한 데이터를 반환 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 86d769de460538acda696194348980de5752d6d8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380880"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

구문 분석에 적합 한 데이터를 반환 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /RawReturn
```

## <a name="remarks"></a>설명

출력에서 줄 바꿈 문자 및 서식 지정을 제거 합니다.

일반적으로이 명령을 **Create** 및 **Get\\** * 스위치와 함께 사용 하 여 값만 받습니다. 다른 스위치 전에이 스위치를 지정 해야 합니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업의 상태에 대 한 원시 데이터를 검색 *Mydownloadjob*합니다.
```
C:\>bitsadmin /RawReturn /GetState myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)