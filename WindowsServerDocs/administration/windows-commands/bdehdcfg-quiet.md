---
title: bdehdcfg quiet
description: Bdehdcfg quiet 명령에 대 한 참조 문서로, bdehdcfg에 모든 작업 및 오류를 표시 하지 않도록 지시 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7f75b702-890b-4ff9-805c-edf5cadd8822
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b6a62314109d1c299187d87fba23b8e59669d66
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923455"
---
# <a name="bdehdcfg-quiet"></a>bdehdcfg: quiet

모든 작업 및 오류가 명령줄 인터페이스에 표시 되지 않도록 bdehdcfg 명령줄 도구에 알립니다. 드라이브 준비 중에 표시 되는 모든 예/아니요 (Y/N) 프롬프트는 "예" 대답을 가정 합니다. 드라이브 준비 중에 발생 한 오류를 보려면 아래에서 시스템 이벤트 로그를 검토는 **Windows BitLocker DrivePreparationTool Microsoft** 이벤트 공급자.

## <a name="syntax"></a>구문

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge} -quiet
```

#### <a name="parameters"></a>매개 변수

이 명령에는 추가 매개 변수가 없습니다.

## <a name="examples"></a>예

**자동** 명령을 사용 하려면 다음을 수행 합니다.

```
bdehdcfg -target default -quiet
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
