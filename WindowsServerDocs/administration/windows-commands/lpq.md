---
title: lpq
description: LPD 명령에 대 한 참조 문서는 LPD (Line printer Daemon)를 실행 하는 컴퓨터에서 인쇄 큐의 상태를 표시 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bb6abcc4-310a-4fa4-927b-4084b62ca02e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 373b1af5acbc43cbf52c45667c6feb571f1855a8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934555"
---
# <a name="lpq"></a>lpq

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

LPD (Line printer Daemon)를 실행 하는 컴퓨터에서 인쇄 큐의 상태를 표시 합니다.

## <a name="syntax"></a>구문

```
lpq -S <servername> -P <printername> [-l]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -S`<servername>` | 컴퓨터 또는 디바이스를 표시 하려는 상태와 함께 LPD 인쇄 큐를 호스팅하는 공유 프린터 이름 또는 IP 주소) (으로 지정 합니다. 이 매개 변수는 필수 이며 대문자 여야 합니다. |
| -P`<Printername>` | 표시 하려는 상태와 함께 인쇄 큐에 대 한 프린터 이름을 사용 하 여 지정 합니다. 이 매개 변수는 필수 이며 대문자 여야 합니다. |
| -l | 인쇄 큐의 상태에 대 한 세부 정보가 표시 되도록 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

*에서 10.0.0.45*의 LPD 호스트에서 *Laserprinter1* 프린터 큐의 상태를 표시 하려면 다음을 입력 합니다.

```
lpq -S 10.0.0.45 -P Laserprinter1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [인쇄 명령 참조](print-command-reference.md)
