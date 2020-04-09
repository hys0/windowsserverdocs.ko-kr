---
title: serverceipoptin
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3d7d7fa7-0689-4797-b802-36fe260d21a0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c0625694053a2d673cd86e12d6f6d54662a6c81d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834682"
---
# <a name="serverceipoptin"></a>serverceipoptin

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ceip (사용자 환경 개선 프로그램)에 참여할 수 있습니다.
## <a name="syntax"></a>구문
```
serverceipoptin [/query] [/enable] [/disable]
```
#### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/ 쿼리|현재 설정을 확인 합니다.|
|같습니다.|참여를 활성화 합니다.|
|/disable|참여를 비활성화합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|
## <a name="examples"></a><a name=BKMK_Examples></a>예와
현재 설정의 확인 하려면 다음을 입력 합니다.
```
serverceipoptin /query
```
참여를 활성화 하려면 다음을 입력 합니다.
```
serverceipoptin /enable
```
참여를 비활성화 하려면 다음을 입력 합니다.
```
serverceipoptin /disable
```
## <a name="additional-references"></a>추가 참조
-   - [명령줄 구문 키](command-line-syntax-key.md)

