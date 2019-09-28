---
title: bitsadmin setreplyfilename
description: '**Bitsadmin setreplyfilename** 에 대 한 Windows 명령 항목-서버 응답이 포함 된 파일의 경로를 지정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a490b5bc565549d096b6f43f42758f77570fcb26
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380418"
---
# <a name="bitsadmin-setreplyfilename"></a>bitsadmin setreplyfilename

서버 응답을 포함 하는 파일의 경로 지정 합니다.

**BITS 1.2 및 이전 버전**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetReplyFileName <Job> <Path>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|경로|서버 회신을 놓을 위치|

## <a name="remarks"></a>설명

업로드-회신 작업에 대해서만 유효 합니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 회신 filename pathfor 이라는 작업 *myDownloadJob*합니다.
```
C:\>bitsadmin /SetReplyFileName myDownloadJob c:\reply
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)