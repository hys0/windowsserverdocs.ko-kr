---
title: bitsadmin peercaching and getconfigurationflags
description: Bitsadmin 피어 캐싱 및 getconfigurationflags 명령에 대 한 참조 문서-컴퓨터가 피어에 콘텐츠를 제공 하는지 여부를 결정 하는 구성 플래그를 가져오며 피어에서 콘텐츠를 다운로드할 수 있는지 여부를 결정 하는 구성 플래그를 가져옵니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c6834e57ebccca94c6fdc7c6cff503e2d58378a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922990"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>bitsadmin peercaching and getconfigurationflags

컴퓨터가 피어에 콘텐츠를 제공 하는지 여부와 피어에서 콘텐츠를 다운로드할 수 있는지 여부를 결정 하는 구성 플래그를 가져옵니다.

## <a name="syntax"></a>구문

```
bitsadmin /peercaching /getconfigurationflags <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

명명 된 작업에 대 한 구성 플래그를 가져오려면 *Mydownloadjob*:

```
bitsadmin /peercaching /getconfigurationflags myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)

- [bitsadmin 피어 캐싱 명령](bitsadmin-peercaching.md)
