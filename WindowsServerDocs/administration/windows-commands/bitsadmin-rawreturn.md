---
title: bitsadmin rawreturn
description: Windows 명령 항목에 대 한 **bitsadmin rawreturn** -구문 분석에 적합 한 데이터를 반환 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 80eef106452a45ac4f071446ec8d427b757c443d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817024"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

구문 분석에 적합 한 데이터를 반환합니다.

## <a name="syntax"></a>구문

```
bitsadmin /RawReturn
```

## <a name="remarks"></a>설명

줄무늬 줄 바꿈 문자 및 출력에서 서식 지정 합니다.

일반적으로이 명령은 함께에서 사용 합니다 **만들기** 및 **가져오기\***  스위치 값만 받을 수 있습니다. 다른 전환 하기 전에이 스위치를 지정 해야 합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업의 상태에 대 한 원시 데이터를 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /RawReturn /GetState myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)