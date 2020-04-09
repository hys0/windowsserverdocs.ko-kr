---
title: bdehdcfg newdriveletter
description: '**Bdehdcfg newdriveletter**에 대 한 Windows 명령 항목으로, 시스템 드라이브로 사용 되는 드라이브 부분에 새 드라이브 문자를 할당 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a8757e7d0684912525817708fbe34953b049582
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851056"
---
# <a name="bdehdcfg-newdriveletter"></a>bdehdcfg: newdriveletter

시스템 드라이브로 사용할 드라이브의 부분에 새 드라이브 문자를 할당 합니다. 이 명령을 사용할 수 있는 방법을의 예제를 참조 하십시오. [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -newdriveletter <DriveLetter>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------| ----------- |
|`<DriveLetter>`|지정 된 대상 드라이브에 할당할 드라이브 문자를 정의 합니다.|

## <a name="remarks"></a>주의

모범 사례로, 시스템 드라이브는 드라이브 문자를 할당 하지 않으면 것이 좋습니다.

## <a name="examples"></a><a name="BKMK_Examples"></a>예와

다음 예제에서는 드라이브 문자가 P. 할당 되 고 기본 드라이브를 보여 줍니다.

```
bdehdcfg -target default -newdriveletter P:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [Bdehdcfg](bdehdcfg.md)