---
title: bitsadmin rawreturn
description: 구문 분석에 적합 한 데이터를 반환 하는 bitsadmin rawreturn 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: af465bb9f51ab6f43980c43bf2be1f5158429a82
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717089"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

구문 분석에 적합 한 데이터를 반환 합니다. 일반적으로이 명령을 **/create** 및 **/get*** 스위치와 함께 사용 하 여 값만 수신 합니다. 다른 스위치 전에이 스위치를 지정 해야 합니다.

> [!NOTE]
> 이 명령은 줄 바꿈 문자를 제거 하 고 출력에서 서식을 지정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /rawreturn
```

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업의 상태에 대 한 원시 데이터를 검색 하려면 다음을 수행 합니다.

```
bitsadmin /rawreturn /getstate myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
