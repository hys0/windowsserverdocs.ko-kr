---
title: wmic
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76397c72-d06f-4cea-88cf-c7603315a983
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c68866fbe0c8f5b16dae77e2121331f06cdc726
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885844"
---
# <a name="wmic"></a>wmic



대화형 명령 셸에서 WMI 정보를 표시합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
command </parameter>
```

## <a name="sub-commands"></a>하위 명령

다음 하위 명령을 항상 사용할 수 있습니다.

|하위 명령|설명|
|-----------|-----------|
|class|클래스는 WMI 스키마에 직접 액세스 하는 WMIC의 기본 별칭 모드에서 나와 있습니다.|
|path|WMI 스키마에 있는 인스턴스를 직접 액세스 하는 WMIC의 기본 별칭 모드에서 나와 있습니다.|
|컨텍스트|모든 전역 스위치의 현재 값을 표시합니다.|
|[종료 \| 종료]|종료는 WMIC 명령 셸.|

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|</parameter>|\<간결한 설명, 시작 동사. >|
|</param2>|\<다른 간결한 설명, 시작 동사. >|


## <a name="BKMK_examples"></a>예제

모든 전역 스위치의 현재 값을 표시 하려면 다음을 입력 합니다.
```
wmic context
```
출력이 다음이 표시 됩니다.
```
NAMESPACE    : root\cimv2
ROLE         : root\cli
NODE(S)      : BOBENTERPRISE
IMPLEVEL     : IMPERSONATE
[AUTHORITY   : N/A]
AUTHLEVEL    : PKTPRIVACY
LOCALE       : ms_409
PRIVILEGES   : ENABLE
TRACE        : OFF
RECORD       : N/A
INTERACTIVE  : OFF
FAILFAST     : OFF
OUTPUT       : STDOUT
APPEND       : STDOUT
USER         : N/A
AGGREGATE    : ON
```
언어를 변경 하려면 ID 사용 하는 명령줄을 사용 하 여 영어 (로캘 ID 409)을 유형:
```
wmic /locale:ms_409
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)