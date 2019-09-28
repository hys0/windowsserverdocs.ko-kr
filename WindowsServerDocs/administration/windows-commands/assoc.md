---
title: assoc
description: '**Assoc** 의 Windows 명령 항목-파일 이름 확장명 연결을 표시 하거나 수정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 237bedda-b24c-4fec-a39c-9b7eacf96417
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e4a6fd700cbe66897a24f01f66387e76e07b568b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382673"
---
# <a name="assoc"></a>assoc



표시 하거나 파일 이름 확장명 연결을 수정 합니다. 매개 변수 없이 사용 하는 경우 **assoc** 모든는 현재 파일 이름 확장명 연결의 목록이 표시 됩니다.

> [!NOTE]
> 이 명령은 CMD 내 에서만 지원 됩니다. EXE 및를 PowerShell에서 사용할 수 없습니다.
>

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
assoc [<.ext>[=[<FileType>]]]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|<.ext >|파일 이름 확장명을 지정합니다.|
|\<FileType >|지정 된 파일 이름 확장명에 연결할 파일 유형을 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   파일 이름 확장명에 대 한 파일 형식 연결을 제거 하려면 스페이스바를 눌러 등호 뒤 공백을 추가 합니다.
-   현재 파일 형식에 정의 된 열려 있는 명령 문자열을 보려면 사용 하 여는 **ftype** 명령입니다.
-   출력을 리디렉션할 **assoc** 사용 하 여 텍스트 파일에는 **>** 리디렉션 연산자입니다.

## <a name="BKMK_examples"></a>예와

파일 이름 확장명이.txt 인에 대 한 현재 파일 형식 연결을 보려면 다음을 입력 합니다.
```
assoc .txt
```
파일 이름 확장명이.bak에 대 한 파일 형식 연결을 제거 하려면 다음을 입력 합니다.
```
assoc .bak= 
```

> [!NOTE]
> 등호 뒤에 공백을 추가 해야 합니다.

출력을 보려면 **assoc** 형식 한 번에 한 화면:
```
assoc | more
```
출력으로 보내려면 **assoc** 파일 assoc.txt를 입력 합니다.
```
assoc>assoc.txt
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
