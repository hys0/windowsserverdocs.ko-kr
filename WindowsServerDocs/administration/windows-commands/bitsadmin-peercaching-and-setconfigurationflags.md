---
title: bitsadmin peercaching and setconfigurationflags
description: Bitsadmin 피어 캐싱 및 setconfigurationflags 명령에 대 한 참조 항목 (컴퓨터에서 피어에 콘텐츠를 제공할 수 있는지 여부를 결정 하는 구성 플래그를 설정 하 고, 피어에서 콘텐츠를 다운로드할 수 있는지 여부를 결정 하는 구성 플래그 설정)
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ff0a2b49-66e3-4d40-824c-6a3816055d2e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3c3ce69ce7a372311ce0c30e9b3a391ea33f45ce
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717234"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>bitsadmin peercaching and setconfigurationflags

컴퓨터가 피어에 콘텐츠를 제공할 수 있는지 여부와 피어에서 콘텐츠를 다운로드할 수 있는지 여부를 결정 하는 구성 플래그를 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /peercaching /setconfigurationflags <job> <value>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| 값 | 이진 표현에서 비트에 대 한 다음 해석을 포함 하는 부호 없는 정수입니다.<ul><li>피어에서 작업 데이터를 다운로드할 수 있도록 하려면 최하위 비트를 설정 합니다.</li><li>작업의 데이터를 동료에 게 제공할 수 있도록 하려면 오른쪽에서 두 번째 비트를 설정 합니다.</li></ul>|

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에 대해 피어에서 다운로드할 작업 데이터를 지정 하려면 다음을 수행 합니다.

```
bitsadmin /peercaching /setconfigurationflags myDownloadJob 1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)

- [bitsadmin 피어 캐싱 명령](bitsadmin-peercaching.md)
