---
title: 클립
description: 명령 출력을 명령줄에서 Windows 클립보드로 리디렉션하는 clip의 windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 85322d85-3376-4806-845b-93ac77fe27bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0d997154a382cf39aa2b877d7a2b84f4ff34157d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847646"
---
# <a name="clip"></a>클립

명령줄의 명령 출력을 Windows 클립보드에 리디렉션합니다. 그런 다음이 텍스트 출력을 다른 프로그램에 붙여 넣을 수 있습니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
<Command> | clip
clip < <FileName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<명령 >|Windows 클립보드에 전송 하려는 출력의 명령을 지정 합니다.|
|\<파일 이름 >|Windows 클립보드로 보내려는 콘텐츠를 포함 하는 파일을 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의

**Clip** 명령을 사용 하 여 클립보드에서 텍스트를 받을 수 있는 모든 응용 프로그램에 직접 데이터를 복사할 수 있습니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

현재 디렉터리 목록을 Windows 클립보드에 복사 하려면 다음을 입력 합니다.
```
dir | clip
```
Generic. awk 라는 프로그램의 출력을 Windows 클립보드에 복사 하려면 다음을 입력 합니다.
```
awk -f generic.awk input.txt | clip
```
Readme.txt 라는 파일의 내용을 Windows 클립보드에 복사 하려면 다음을 입력 합니다.
```
clip < readme.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)