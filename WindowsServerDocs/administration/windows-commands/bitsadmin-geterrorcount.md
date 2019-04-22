---
title: bitsadmin geterrorcount
description: Windows 명령 항목에 대 한 **bitsadmin geterrorcount** -지정된 된 된 작업에 일시적인 오류를 생성 하는 횟수를 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91045372931efec0e3189132a275eeacab584de4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818374"
---
# <a name="bitsadmin-geterrorcount"></a>bitsadmin geterrorcount



지정된 된 된 작업에 일시적인 오류를 생성 하는 횟수를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetErrorCount <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 오류 개수 정보를 검색 합니다. *myDownloadJob*합니다.
```
C:\>bitsadmin /GetErrorCount myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)