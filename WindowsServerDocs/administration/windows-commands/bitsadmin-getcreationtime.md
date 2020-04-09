---
title: bitsadmin getcreationtime
description: 지정 된 작업에 대 한 생성 시간을 검색 하는 **bitsadmin getcreationtime**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd8f718e53cc44dc5f4c6f5ff09c9a5c201e0564
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850746"
---
# <a name="bitsadmin-getcreationtime"></a>bitsadmin getcreationtime

지정 된 작업의 만든 시간을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getcreationtime <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 이름이 *Mydownloadjob*인 작업을 만든 시간을 검색 합니다.

```
C:\>bitsadmin /getcreationtime myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)