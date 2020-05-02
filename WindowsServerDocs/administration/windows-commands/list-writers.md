---
title: 작성기 나열
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1c30cbc4-f568-4fa7-b564-66c41d3ca82d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ef7fa0bd6e9857e22994178849e49afeb3305a2a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724482"
---
# <a name="list-writers"></a>작성기 나열



시스템에는 작성기를 나열 합니다. 매개 변수 없이 사용 하는 경우 **목록** 출력을 표시 **메타 데이터를 목록** 기본적으로 합니다.



## <a name="syntax"></a>구문

```
list writers [metadata | detailed | status]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|metadata|Id 및 기록기의 상태를 나열 하 고 구성 요소 세부 정보 및 제외 된 파일 등의 메타 데이터를 표시 합니다. 이것이 기본 매개 변수입니다.|
|자세한|와 동일한 정보를 나열 **메타 데이터**, 하지만 **자세한** 모든 구성 요소에 대 한 전체 파일 목록이 포함 됩니다.|
|상태|Id 및 등록 된 기록기의 상태를 나열합니다.|

## <a name="examples"></a>예

Id 및 기록기의 상태를 나열 하려면 다음을 입력 합니다.
```
list writers status
```
다음을 표시 하는 출력:
```
Listing writer status ...
* WRITER System Writer
        - Status: 5 (VSS_WS_WAITING_FOR_BACKUP_COMPLETE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {e8132975-6f93-4464-a53e-1050253ae220}
        - Instance ID: {7e631031-c695-4229-9da1-a7de057e64cb}
* WRITER Shadow Copy Optimization Writer
        - Status: 1 (VSS_WS_STABLE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f}
        - Instance ID: {9e362607-9794-4dd4-a7cd-b3d5de0aad20}
...
...
...
* WRITER Registry Writer
        - Status: 1 (VSS_WS_STABLE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {afbab4a2-367d-4d15-a586-71dbb18f8485}
        - Instance ID: {e87ba7e3-f8d8-42d8-b2ee-c76ae26b98e8}
8 writers listed. 
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)