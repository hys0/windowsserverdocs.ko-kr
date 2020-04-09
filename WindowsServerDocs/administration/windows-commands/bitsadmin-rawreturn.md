---
title: bitsadmin rawreturn
description: '**Bitsadmin rawreturn**에 대 한 Windows 명령 항목으로, 구문 분석에 적합 한 데이터를 반환 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e8cd84b6082b1fda8061ee7b324dd66991d3b206
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849886"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

구문 분석에 적합 한 데이터를 반환 합니다. 일반적으로이 명령을 **/create** 및 **/get*** 스위치와 함께 사용 하 여 값만 수신 합니다. 다른 스위치 전에이 스위치를 지정 해야 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /rawreturn
```

## <a name="remarks"></a>주의

- 출력에서 줄 바꿈 문자 및 서식 지정을 제거 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업의 상태에 대 한 원시 데이터를 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /rawreturn /getstate myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)