---
title: bitsadmin setvalidationstate
description: Windows 명령 항목에 대 한 **bitsadmin setvalidationstate** -작업 내에서 지정된 된 파일의 콘텐츠 유효성 검사 상태를 설정 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 647389aaac06d1eb109052548c1b24f7579bde2f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851244"
---
# <a name="bitsadmin-setvalidationstate"></a>bitsadmin setvalidationstate



작업 내에서 지정된 된 파일의 콘텐츠 유효성 검사 상태를 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetValidationState <Job> <file index> <true|false> 
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|파일 인덱스|0부터 시작|
|True|False|TRUE로 설정 된 파일의 내용을 올바른지, 그렇지 않으면 FALSE로 설정|

## <a name="BKMK_examples"></a>예제

2 파일의 콘텐츠 유효성 검사 상태 라는 작업에 대해 TRUE로 설정 하는 다음 예제에서는 *myJob*합니다.
```
C:\>bitsadmin /SetValidationState myJob 2 TRUE 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)