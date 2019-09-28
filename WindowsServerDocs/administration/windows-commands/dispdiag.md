---
title: dispdiag
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b640883a207648d2ef6c9a7d6e5366cd0bb384c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377760"
---
# <a name="dispdiag"></a>dispdiag



표시 정보를 파일에 기록 합니다.

## <a name="syntax"></a>구문

```
dispdiag [-testacpi] [-d] [-delay <Seconds>] [-out <FilePath>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-testacpi|핫키 진단 테스트를 실행 합니다. 테스트 하는 동안 누른 키의 키 이름, 코드 및 검사 코드를 표시 합니다.|
|-d|테스트 결과를 사용 하 여 덤프 파일을 생성 합니다.|
|-delay \<Seconds >|지정 된 시간 *(초)* 으로 데이터 컬렉션을 지연 시킵니다.|
|-out \<Filefile>|수집 된 데이터를 저장할 경로와 파일 이름을 지정 합니다. 이 매개 변수는 마지막 매개 변수 여야 합니다.|
|-?|사용 가능한 명령 매개 변수를 표시 하 고 사용 하기 위한 도움말을 제공 합니다.|