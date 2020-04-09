---
title: bitsadmin geterror
description: 지정 된 작업에 대 한 자세한 오류 정보를 검색 하는 **bitsadmin geterror**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c65b072bb190e3e516b917c310942146bb3f3d2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850706"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror

지정 된 작업에 대 한 자세한 오류 정보를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /geterror <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 오류 정보를 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /geterror myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)