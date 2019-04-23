---
title: 메타 데이터를 로드 합니다.
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c535487-668b-44fc-babb-ff59cf7d190e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b52b5040fc8c834b04cad83ca4b0cfab103fdc43
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871334"
---
# <a name="load-metadata"></a>메타 데이터를 로드 합니다.



변환할 수 있는 섀도 복사본을 가져오기 전에 메타 데이터.cab 파일을 로드 하거나 복원 하는 경우 기록기 메타 데이터를 로드 합니다. 매개 변수 없이 사용 하는 경우 **메타 데이터를 로드** 명령 프롬프트에서 도움말을 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
load metadata [<Drive>:][<Path>]<MetaData.cab>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[\<Drive>:][<Path>]|메타 데이터 파일의 위치를 지정합니다.|
|MetaData.cab|로드할 메타 데이터.cab 파일을 지정 합니다.|

## <a name="remarks"></a>설명

-   사용할 수는 **가져올** 전송 가능한 섀도 복사본을 가져오려면 명령에 지정 된 메타 데이터에 따라 **메타 데이터를 로드**합니다.
-   이 명령은 필요 하기 전에 **복원을 시작** 선택한 작성자 및 복원에 대 한 구성 요소를 로드 하는 명령입니다.

## <a name="BKMK_examples"></a>예제

기본 위치에서 metafile.cab 라는 메타 데이터 파일을 로드 하려면 다음을 입력 합니다.
```
load metadata metafile.cab
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)