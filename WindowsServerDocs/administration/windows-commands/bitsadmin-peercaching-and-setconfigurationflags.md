---
title: bitsadmin 피어 캐싱 및 setconfigurationflags
description: '**Bitsadmin 피어 캐싱** 및 **setconfigurationflags**에 대 한 Windows 명령 항목은 컴퓨터에서 피어에 콘텐츠를 제공할 수 있는지 여부를 결정 하는 구성 플래그를 설정 하 고 피어에서 콘텐츠를 다운로드할 수 있는지 여부를 결정 하는 구성 플래그'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ff0a2b49-66e3-4d40-824c-6a3816055d2e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ebaa09da2d4594d2762e67dc5884dd15cf4d1da8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850136"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>bitsadmin 피어 캐싱 및 setconfigurationflags

컴퓨터가 피어에 콘텐츠를 제공할 수 있는지 여부와 피어에서 콘텐츠를 다운로드할 수 있는지 여부를 결정 하는 구성 플래그를 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /peercaching /setconfigurationflags <job> <value>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| 값 | 이진 표현에서 비트에 대 한 다음 해석을 포함 하는 부호 없는 정수입니다.<ul><li> 피어에서 작업 데이터를 다운로드할 수 있도록 하려면 최하위 비트를 설정 합니다.</li><li>작업의 데이터를 동료에 게 제공할 수 있도록 하려면 오른쪽에서 두 번째 비트를 설정 합니다.</li></ul>|

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예에서는 *Mydownloadjob*이라는 작업에 대해 피어에서 다운로드할 작업 데이터를 지정 합니다.

```
C:\> bitsadmin /peercaching /setconfigurationflags myDownloadJob 1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)