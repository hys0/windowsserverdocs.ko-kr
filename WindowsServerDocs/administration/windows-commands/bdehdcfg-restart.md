---
title: bdehdcfg restart
description: 드라이브 준비가 완료 된 후 컴퓨터를 다시 시작 해야 함을 bdehdcfg 알려주는 bdehdcfg restart 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 02d57eaef9b2f6e705a5bb30d7d52a09579d27c9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923465"
---
# <a name="bdehdcfg-restart"></a>bdehdcfg: 다시 시작

드라이브 준비가 완료 된 후 컴퓨터를 다시 시작 해야 함을 bdehdcfg 명령줄 도구에 알립니다. 다른 사용자가 컴퓨터에 로그온 하 여 **quiet** 명령이 지정 되지 않은 경우 컴퓨터를 다시 시작 해야 하는지 확인 하는 메시지가 표시 됩니다.

## <a name="syntax"></a>구문

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge} -restart
```

#### <a name="parameters"></a>매개 변수

이 명령에는 추가 매개 변수가 없습니다.

## <a name="examples"></a>예

**Restart** 명령을 사용 하려면 다음을 수행 합니다.

```
bdehdcfg -target default -restart
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
