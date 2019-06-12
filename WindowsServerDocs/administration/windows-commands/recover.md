---
title: 복구
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf9be2e3-90c8-4773-a201-dc503b91948e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d6b9b5544394bfc69a2dc9f7be26ed8355a3f690
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441963"
---
# <a name="recover"></a>복구



잘못 된 이거나 결함이 있는 디스크에서 읽을 수 있는 정보를 복구합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
recover [<Drive>:][<Path>]<FileName>
```

## <a name="parameters"></a>매개 변수

|           매개 변수           |                                          설명                                          |
|-------------------------------|-----------------------------------------------------------------------------------------------|
| [\<Drive>:][<Path>]<FileName> | 복구 하려는 파일의 이름과 위치를 지정 합니다. *FileName* 가 필요 합니다. |
|              /?               |                             명령 프롬프트에 도움말을 표시합니다.                              |

## <a name="remarks"></a>설명

-   **복구** 명령 파일을 섹터 단위로 읽고 좋은 섹터에서 데이터를 복구 합니다. 불량 섹터의 데이터가 손실 됩니다.
-   불량 섹터에서 보고 **chkdsk** 작업에 대 한 디스크를 준비할 때 "불량"으로 표시 되었습니다. 위험 하지, 및 **복구** 에 영향을 주지 않습니다.
-   불량 섹터의 모든 데이터가 손실 되는 파일을 복구 하는 경우 한 번에 하나의 파일을 복구할 해야 있습니다.
-   와일드 카드 문자를 사용할 수 없습니다 ( **&#42;** 하 고 **?** ) 사용 하 여는 **복구할** 명령입니다. 파일 (및 현재 디렉터리에 없는 경우 파일의 위치)를 지정 해야 합니다.

## <a name="BKMK_examples"></a>예제

D 드라이브 \Fiction 디렉터리에 Story.txt 파일을 복구 하려면 다음을 입력 합니다.
```
recover d:\fiction\story.txt 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)