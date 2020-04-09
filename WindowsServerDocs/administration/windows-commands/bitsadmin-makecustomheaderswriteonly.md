---
title: bitsadmin makecustomheaderswriteonly
description: 작업의 사용자 지정 HTTP 헤더 쓰기 전용을 만드는 **bitsadmin makecustomheaderswriteonly**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 9183b1b5de51020c5c6d2efad2c0a788d158a183
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850246"
---
# <a name="bitsadmin-makecustomheaderswriteonly"></a>bitsadmin makecustomheaderswriteonly

작업의 사용자 지정 HTTP 헤더를 쓰기 전용으로 설정 합니다.

> [!Important]
> 이 작업은 실행 취소할 수 없습니다.

## <a name="syntax"></a>구문

```
bitsadmin /makecustomheaderswriteonly <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 *Mydownloadjob*이라는 작업에 대 한 사용자 지정 HTTP 헤더 쓰기 전용을 만듭니다.

```
C:\>bitsadmin /makecustomheaderswriteonly myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)