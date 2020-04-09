---
title: bitsadmin geterrorcount
description: 지정 된 작업에서 일시적인 오류가 발생 한 횟수를 검색 하는 bitsadmin geterrorcount에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1711781dd416311e45874b7c611f3f8f42a06854
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850696"
---
# <a name="bitsadmin-geterrorcount"></a>bitsadmin geterrorcount

지정 된 작업에서 일시적인 오류가 발생 한 횟수를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /geterrorcount <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 오류 개수 정보를 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /geterrorcount myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)