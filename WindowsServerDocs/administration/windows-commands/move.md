---
title: move
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fde290a8-d385-450f-8987-ee837fed667d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: efd0cd0716c564a9570647820056ab9c38e41274
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839376"
---
# <a name="move"></a>move



한 디렉터리에서 하나 이상의 파일을 다른 디렉터리로 이동합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
move [{/y | /-y}] [<Source>] [<Target>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/y|기존 대상 파일을 덮어쓸 것인지를 확인 하는 메시지를 표시 하지 않습니다.|
|/ y|기존 대상 파일을 덮어쓸 것인지 확인 메시지를 표시 하도록 합니다.|
|\<원본 >|이동할 파일 또는 파일의 이름과 경로 지정 합니다. 디렉터리를 이름을 바꾸거나 이동 하려는 경우 *소스* 현재 디렉터리 경로 및 이름 이어야 합니다.|
|\<대상 >|경로 파일을 이동 하는 이름을 지정 합니다. 디렉터리를 이름을 바꾸거나 이동 하려는 경우 *대상* 원하는 디렉터리 경로 및 이름 이어야 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의

-   **/y** 는 /z에서 명령줄 옵션을 미리 설정할 수 있습니다. 이를 재정의할 수 있습니다 **/y** 명령줄에 있습니다. 기본값은 하지 않는 한 파일을 덮어쓰기 전에 확인 하는 **복사** 일괄 처리 스크립트 내에서 명령을 실행 합니다.
-   지원 되지 않는 암호화 EFS (파일 시스템) 오류가 발생 하는 볼륨에 암호화 된 파일을 이동 합니다. 먼저 파일을 암호 해독을 지 원하는 EFS 볼륨으로 파일을 이동 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

\Second_Q\Reports 디렉터리로 \Data 디렉터리에서 확장명이.xls 인 모든 파일을 이동, 다음을 입력 합니다.
```
move \data\*.xls \second_q\reports\ 
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)