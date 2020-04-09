---
title: ktmutil
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 53bc56df-f0e5-443b-ab20-bbf8b11d4a9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e65312ea4bb3169b90c2550b8b945919b86587f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841196"
---
# <a name="ktmutil"></a>ktmutil



커널 트랜잭션 관리자 유틸리티를 시작합니다. 매개 변수 없이 사용 하는 경우 **ktmutil** 사용할 수 있는 하위 표시 됩니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
ktmutil list tms 
ktmutil list transactions [{TmGuid}]
ktmutil resolve complete {TmGuid} {RmGuid} {EnGuid}
ktmutil resolve commit {TxGuid}
ktmutil resolve rollback {TxGuid}
ktmutil force commit {??Guid}
ktmutil force rollback {??Guid}
ktmutil forget
```

### <a name="parameters"></a>매개 변수

## <a name="remarks"></a>주의

## <a name="examples"></a><a name=BKMK_examples></a>예와

커밋 GUID 311a9209-03f4-11dc-918f-00188b8f707b 포함 하는 Indoubt 트랜잭션을 강제 하려면 다음을 입력 합니다.
```
ktmutil force commit {311a9209-03f4-11dc-918f-00188b8f707b}
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)