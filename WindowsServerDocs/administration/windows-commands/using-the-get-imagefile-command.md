---
title: get-비 표시
description: Windows 이미지 (.wim) 파일에 포함 된 이미지에 대 한 정보를 검색 하는 get 파일 항목에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e1e296fb-20cf-4a60-9db4-4cbac7d4dab5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 127b5282b74020f002c7ccc55663fc2571584582
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932225"
---
# <a name="get-imagefile"></a>get-비 표시

Windows 이미지 (.wim) 파일에 포함 된 이미지에 대 한 정보를 검색 합니다.

## <a name="syntax"></a>구문

```
WDSUTIL [Options] /Get-ImageFile /ImageFile:<wim file path> [/Detailed]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/Dt:\<WIM file path>|.Wim 파일의 전체 경로 파일 이름을 지정합니다.|
|[/ 자세한]|각 이미지에서 모든 이미지 메타 데이터를 반환합니다. 이 옵션을 사용 하지 않는 경우 기본 동작은 반환할 이미지 이름, 설명 및 파일 이름입니다.|

## <a name="examples"></a>예

이미지에 대 한 정보를 보려면 다음을 입력 합니다.
```
WDSUTIL /Get-ImageFile /ImageFile:C:\temp\install.wim
```
자세한 정보를 보려면 다음을 입력 합니다.
```
WDSUTIL /Verbose /Get-ImageFile /ImageFile:\\Server\Share\My Folder \install.wim /Detailed
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)