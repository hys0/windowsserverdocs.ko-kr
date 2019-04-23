---
title: 목록 작성기
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1c30cbc4-f568-4fa7-b564-66c41d3ca82d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6fbab6644d46dbb352a5d5a51abefb293f3ffe6f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866744"
---
# <a name="list-writers"></a>목록 작성기



시스템에는 작성기를 나열 합니다. 매개 변수 없이 사용 하는 경우 **목록** 출력을 표시 **메타 데이터를 목록** 기본적으로 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
list writers [metadata | detailed | status]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|메타데이터|Id 및 기록기의 상태를 나열 하 고 구성 요소 세부 정보 및 제외 된 파일 등의 메타 데이터를 표시 합니다. 이것이 기본 매개 변수입니다.|
|자세한|와 동일한 정보를 나열 **메타 데이터**, 하지만 **자세한** 모든 구성 요소에 대 한 전체 파일 목록이 포함 됩니다.|
|상태|Id 및 등록 된 기록기의 상태를 나열합니다.|

## <a name="BKMK_examples"></a>예제

Id 및 기록기의 상태를 나열 하려면 다음을 입력 합니다.
```
list writers status
```
다음을 표시 하는 출력:
```
Listing writer status ...
* WRITER "System Writer"
        - Status: 5 (VSS_WS_WAITING_FOR_BACKUP_COMPLETE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {e8132975-6f93-4464-a53e-1050253ae220}
        - Instance ID: {7e631031-c695-4229-9da1-a7de057e64cb}
* WRITER "Shadow Copy Optimization Writer"
        - Status: 1 (VSS_WS_STABLE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f}
        - Instance ID: {9e362607-9794-4dd4-a7cd-b3d5de0aad20}
...
...
...
* WRITER "Registry Writer"
        - Status: 1 (VSS_WS_STABLE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {afbab4a2-367d-4d15-a586-71dbb18f8485}
        - Instance ID: {e87ba7e3-f8d8-42d8-b2ee-c76ae26b98e8}
8 writers listed. 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)