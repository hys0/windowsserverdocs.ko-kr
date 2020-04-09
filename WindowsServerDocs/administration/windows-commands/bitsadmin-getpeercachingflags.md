---
title: bitsadmin getpeercachingflags
description: '**Bitsadmin getpeercachingflags**에 대 한 Windows 명령 항목-작업의 파일을 캐시 하 고 동료에 게 제공할 수 있는지 여부를 결정 하는 플래그를 검색 하 고 BITS에서 작업의 콘텐츠를 다운로드할 수 있는지 여부를 결정 하는 플래그를 검색 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3c3c9f28-4c04-4c49-a23a-dee5bbcc8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cdf9683d1a65400286b4604bd9420a5ab863d4af
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850556"
---
# <a name="bitsadmin-getpeercachingflags"></a>bitsadmin getpeercachingflags

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

작업의 파일을 캐시 하 고 동료에 게 제공 하 고 BITS 피어에서 작업에 대 한 콘텐츠를 다운로드 하는 경우를 결정 하는 플래그를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getpeercachingflags <job> 
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 플래그를 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /getpeercachingflags myJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)