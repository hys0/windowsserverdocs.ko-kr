---
title: bitsadmin getproxyusage
description: '**Bitsadmin getproxyusage** 에 대 한 Windows 명령 항목-지정 된 작업에 대 한 프록시 사용 설정을 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ea9a22f4fb35af3436d02d9f23b62ce0888a26b0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381295"
---
# <a name="bitsadmin-getproxyusage"></a>bitsadmin getproxyusage



지정된 된 작업에 대 한 프록시 사용 설정을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetProxyUsage <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

가능한 값은 다음과 같습니다.
-   미리-소유자의 Internet Explorer 기본값을 사용 합니다.
-   NO_PROXY-프록시 서버를 사용 하지 마십시오.
-   재정의-명시적 프록시 목록을 사용 합니다.
-   자동 검색-프록시 설정 자동 검색 합니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 프록시 사용을 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetProxyUsage myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)