---
title: bitsadmin getreplyprogress
description: '**Bitsadmin getreplyprogress** 에 대 한 Windows 명령 항목-서버 회신의 크기와 진행률을 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f7cb0b4-ad95-44fd-a35d-0ddf5fc0b0d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c791fe98271b497e5ecf48338ab3bbb0cc50de98
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381244"
---
# <a name="bitsadmin-getreplyprogress"></a>bitsadmin getreplyprogress

크기와 서버 회신의 진행 상태를 검색합니다.

**BITS 1.2 및 이전 버전**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetReplyProgress <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

업로드-회신 작업에 대해서만 유효 합니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 검색 이라는 작업에 대 한 회신 진행률 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetReplyProgress myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)