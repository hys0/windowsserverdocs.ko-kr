---
title: dispdiag
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9c96c70aac1b3329e050fa8b02743e61fed44d15
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831464"
---
# <a name="dispdiag"></a>dispdiag



로그 파일에 정보를 표시합니다.

## <a name="syntax"></a>구문

```
dispdiag [-testacpi] [-d] [-delay <Seconds>] [-out <FilePath>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-testacpi|바로 가기 키 진단 테스트를 실행합니다. 테스트 중 모든 키에 대 한 코드 및 스캔 코드 누른 키 이름을 표시 합니다.|
|-d|테스트 결과 사용 하 여 덤프 파일을 생성합니다.|
|-지연 \<시간 (초) >|지정 된 시간에 사용 하 여 데이터의 컬렉션을 지연 *초*합니다.|
|-out \<FilePath>|경로 및 수집 된 데이터를 저장할 파일 이름을 지정 합니다. 마지막 매개 변수 이어야 합니다.|
|-?|사용 가능한 명령 매개 변수를 표시 하 고 사용 하기 위한 도움말을 제공 합니다.|