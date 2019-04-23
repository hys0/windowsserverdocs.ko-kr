---
title: clip
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85322d85-3376-4806-845b-93ac77fe27bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b10876e115c1f0dcac3448948003852449012087
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862394"
---
# <a name="clip"></a>clip



Windows 클립보드에 명령줄에서 명령 출력을 리디렉션합니다. 다른 프로그램에이 텍스트 출력을 붙여넣을 수 있습니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
<Command> | clip
clip < <FileName>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<명령 >|Windows 클립보드에 보내려는 출력이 명령을 지정 합니다.|
|\<FileName>|Windows 클립보드에 전송 하려는 내용이 파일을 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

사용할 수는 **클립** 클립보드에서 텍스트를 받을 수 있는 모든 응용 프로그램에 직접 데이터를 복사 하는 명령입니다.

## <a name="BKMK_examples"></a>예제

Windows 클립보드에 나열 되는 현재 디렉터리에 복사 하려면 다음을 입력 합니다.
```
dir | clip
```
Windows 클립보드로 Generic.awk 프로그램의 출력을 복사 하려면 다음을 입력 합니다.
```
awk -f generic.awk input.txt | clip
```
Windows 클립보드에 Readme.txt 파일의 내용을 복사 하려면 다음을 입력 합니다.
```
clip < readme.txt
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)