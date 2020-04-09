---
title: bitsadmin 피어 캐싱 및 getconfigurationflags
description: '**Bitsadmin 피어 캐싱** 및 **getconfigurationflags**에 대 한 Windows 명령 항목으로, 컴퓨터에서 피어에 콘텐츠를 제공 하는지 여부를 결정 하는 구성 플래그를 가져옵니다 .이 항목에서 피어에서 콘텐츠를 다운로드할 수 있는지 확인 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: be8d6a719d63c8e9c6250320560b6ce21274c680
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850176"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>bitsadmin 피어 캐싱 및 getconfigurationflags

컴퓨터가 피어에 콘텐츠를 제공 하는지 여부와 피어에서 콘텐츠를 다운로드할 수 있는지 여부를 결정 하는 구성 플래그를 가져옵니다.

## <a name="syntax"></a>구문

```
bitsadmin /peercaching /getconfigurationflags <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 이름이 *Mydownloadjob*인 작업에 대 한 구성 플래그를 가져옵니다.

```
C:\> bitsadmin /peercaching /getconfigurationflags myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)