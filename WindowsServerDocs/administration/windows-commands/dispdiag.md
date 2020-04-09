---
title: dispdiag
description: 표시 정보를 파일에 기록 하는 dispdiag에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 498294aa6678cc4904880128bca55d7900c91db5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845386"
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
|-지연 \<초 >|지정 된 시간 *(초)* 으로 데이터 컬렉션을 지연 시킵니다.|
|-out \<FilePath >|수집 된 데이터를 저장할 경로와 파일 이름을 지정 합니다. 이 매개 변수는 마지막 매개 변수 여야 합니다.|
|-?|사용 가능한 명령 매개 변수를 표시 하 고 사용 하기 위한 도움말을 제공 합니다.|