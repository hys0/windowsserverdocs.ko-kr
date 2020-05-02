---
title: dispdiag
description: 표시 정보를 파일에 기록 하는 dispdiag에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f9f44e261b9c46157fb3e6bb7f9105af2480a60b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719405"
---
# <a name="dispdiag"></a>dispdiag

표시 정보를 파일에 기록 합니다.

## <a name="syntax"></a>구문

```
dispdiag [-testacpi] [-d] [-delay <Seconds>] [-out <FilePath>]
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-testacpi|핫키 진단 테스트를 실행 합니다. 테스트 하는 동안 누른 키의 키 이름, 코드 및 검사 코드를 표시 합니다.|
|-d|테스트 결과를 사용 하 여 덤프 파일을 생성 합니다.|
|-지연 \<초>|지정 된 시간 *(초)* 으로 데이터 컬렉션을 지연 시킵니다.|
|-out \<FilePath>|수집 된 데이터를 저장할 경로와 파일 이름을 지정 합니다. 이 매개 변수는 마지막 매개 변수 여야 합니다.|
|-?|사용 가능한 명령 매개 변수를 표시 하 고 사용 하기 위한 도움말을 제공 합니다.|