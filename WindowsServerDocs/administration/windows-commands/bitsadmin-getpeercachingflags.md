---
title: bitsadmin getpeercachingflags
description: Bitsadmin getpeercachingflags 명령에 대 한 참조 문서-작업의 파일을 캐시 하 고 동료에 게 제공할 수 있는지 여부를 결정 하는 플래그를 검색 하 고 BITS에서 작업에 대 한 콘텐츠를 다운로드할 수 있는지 여부를 결정 하는 플래그를 검색 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3c3c9f28-4c04-4c49-a23a-dee5bbcc8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad270fb8003c518c43bae86b066fea5ebc31d008
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926861"
---
# <a name="bitsadmin-getpeercachingflags"></a>bitsadmin getpeercachingflags

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

작업의 파일을 캐시 하 고 동료에 게 제공 하 고 BITS 피어에서 작업에 대 한 콘텐츠를 다운로드 하는 경우를 결정 하는 플래그를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getpeercachingflags <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a>예

이름이 *Mydownloadjob*인 작업에 대 한 플래그를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /getpeercachingflags myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
