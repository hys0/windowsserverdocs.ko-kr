---
title: bdehdcfg 다시 시작
description: '**Bdehdcfg 다시 시작**에 대 한 Windows 명령 항목으로, 드라이브 준비가 완료 된 후 컴퓨터를 다시 시작 해야 함을 bdehdcfg에 알려 줍니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ae6f8d31c09feddf8f994c28d34e4e1b08cc322
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851036"
---
# <a name="bdehdcfg-restart"></a>bdehdcfg: 다시 시작

컴퓨터 다시 시작 해야 드라이브 준비 되어도 Bdehdcfg 명령줄 도구에 알립니다. 이 명령을 사용할 수 있는 방법을의 예제를 참조 하십시오. [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -restart
```

#### <a name="parameters"></a>매개 변수

이 명령은 추가 매개 변수를 사용 합니다.

## <a name="remarks"></a>주의

다른 사용자가 컴퓨터에 로그온 하는 경우와 **quiet** 명령을 지정 하지 않으면, 컴퓨터를 다시 시작 해야 있는지 확인 하는 메시지가 표시 됩니다.

## <a name="examples"></a><a name="BKMK_Examples"></a>예와

다음 예제를 사용 하는 **다시 시작** 명령입니다.

```
bdehdcfg -target default -restart
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [Bdehdcfg](bdehdcfg.md)