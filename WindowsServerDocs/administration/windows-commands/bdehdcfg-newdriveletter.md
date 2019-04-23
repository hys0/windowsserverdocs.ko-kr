---
title: bdehdcfg newdriveletter
description: Bdehdcfg newdriveletter-에 대 한 Windows 명령을 항목 시스템 드라이브로 사용할 드라이브의 부분에 새 드라이브 문자를 할당 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd40942dfb724d46c0fa9a43c4646e1db09d2a76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887144"
---
# <a name="bdehdcfg-newdriveletter"></a>Bdehdcfg: newdriveletter



시스템 드라이브로 사용할 드라이브의 부분에 새 드라이브 문자를 할당 합니다. 이 명령을 사용할 수 있는 방법을의 예제를 참조 하십시오. [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -newdriveletter <DriveLetter>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<DriveLetter>|지정 된 대상 드라이브에 할당할 드라이브 문자를 정의 합니다.|

## <a name="remarks"></a>설명

모범 사례로, 시스템 드라이브는 드라이브 문자를 할당 하지 않으면 것이 좋습니다.

## <a name="BKMK_Examples"></a>예제

다음 예제에서는 드라이브 문자가 P. 할당 되 고 기본 드라이브를 보여 줍니다.
```
bdehdcfg -target default -newdriveletter P:
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)