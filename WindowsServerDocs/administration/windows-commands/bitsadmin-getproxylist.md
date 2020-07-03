---
title: bitsadmin getproxylist-지정 된 작업에 대 한 프록시 목록을 검색 합니다.
description: 지정 된 작업에 대 한 프록시 목록을 검색 하는 bitsadmin getproxylist 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60c66db909b9b62d33ffda09e3b696362b6a65a0
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926815"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

지정 된 작업에 사용할 쉼표로 구분 된 프록시 서버 목록을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getproxylist <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

이름이 *Mydownloadjob*인 작업에 대 한 프록시 목록을 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getproxylist myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
