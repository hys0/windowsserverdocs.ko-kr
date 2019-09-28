---
title: serverweroptin
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a7d5791e059d31e416f848f6e8df648c8f9bd27d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371022"
---
# <a name="serverweroptin"></a>serverweroptin

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

오류 보고를 사용할 수 있습니다.
## <a name="syntax"></a>구문
```
serverweroptin [/query] [/detailed] [/summary]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/ 쿼리|현재 설정을 확인 합니다.|
|자세한 /|자세한 보고서를 자동으로 보냅니다.|
|요약 /|요약 보고서를 자동으로 보냅니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|
## <a name="BKMK_Examples"></a>예와
현재 설정의 확인 하려면 다음을 입력 합니다.
```
serverweroptin /query
```
자세한 보고서를 자동으로 보내려면 다음을 입력 합니다.
```
serverweroptin /detailed
```
요약 보고서를 자동으로 전송 하려면 다음을 입력합니다
```
serverweroptin /summary
```
## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)

