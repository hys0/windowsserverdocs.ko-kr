---
title: bitsadmin setreplyfilename
description: 서버 응답이 포함 된 파일의 경로를 지정 하는 bitsadmin setreplyfilename에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fd45174a7deac89cc943fb19d544e372c0198139
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849186"
---
# <a name="bitsadmin-setreplyfilename"></a>bitsadmin setreplyfilename

서버 응답을 포함 하는 파일의 경로를 지정 합니다.

**BITS 1.2 및 이전 버전**: 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetReplyFileName <Job> <Path>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|경로|서버 회신을 놓을 위치|

## <a name="remarks"></a>주의

업로드-회신 작업에 대해서만 유효 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 회신 filename pathfor 이라는 작업 *myDownloadJob*합니다.
```
C:\>bitsadmin /SetReplyFileName myDownloadJob c:\reply
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)