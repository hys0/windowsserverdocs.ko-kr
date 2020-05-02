---
title: 컨텍스트 설정
description: 섀도 복사본 만들기에 대 한 컨텍스트를 설정 하는 Set context에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fc16c7dd-e8f0-4c2a-8742-0bddb2848bfd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9494cb8a0a6b0e320240d74980049a4e49843ecd
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721929"
---
# <a name="set-contex"></a>설정 하면

섀도 복사본 만들기에 대 한 컨텍스트를 설정합니다. 매개 변수 없이 사용 하는 경우 **컨텍스트 설정** 명령 프롬프트에서 도움말을 표시 합니다.



## <a name="syntax"></a>구문

```
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|clientaccessible|섀도 복사본 클라이언트 버전의 Windows에서 사용할 수 있음을 지정 합니다.|
|지속적|프로그램 종료, 다시 설정 또는 다시 시작에서 섀도 복사본이 유지 되도록 지정 합니다.|
|volatile|삭제에는 섀도 복사 종료 또는 다시 설정 합니다.|
|nowriters|모든 기록기 제외를 지정 합니다.|

## <a name="remarks"></a>설명

-   *clientaccessible* 컨텍스트는 기본적으로 지속적으로 유지 합니다.

## <a name="examples"></a>예

섀도 복사본 DiskShadow를 종료할 때 삭제 되는 것을 방지 하려면 다음을 입력 합니다.
```
set context persistent
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)