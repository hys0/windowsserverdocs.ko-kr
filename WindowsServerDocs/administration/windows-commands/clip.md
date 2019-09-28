---
title: clip
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 82186869782c47f41930d46b4c33a710e6addedf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379353"
---
# <a name="clip"></a>clip



명령줄에서 Windows 클립보드로 명령 출력을 리디렉션합니다. 그런 다음이 텍스트 출력을 다른 프로그램에 붙여 넣을 수 있습니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
<Command> | clip
clip < <FileName>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<Command >|Windows 클립보드에 전송 하려는 출력의 명령을 지정 합니다.|
|\<파일 이름 >|Windows 클립보드로 보내려는 콘텐츠를 포함 하는 파일을 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

**Clip** 명령을 사용 하 여 클립보드에서 텍스트를 받을 수 있는 모든 응용 프로그램에 직접 데이터를 복사할 수 있습니다.

## <a name="BKMK_examples"></a>예와

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

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)