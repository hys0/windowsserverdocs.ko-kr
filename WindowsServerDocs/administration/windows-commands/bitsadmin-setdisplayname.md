---
title: bitsadmin setdisplayname
description: 지정 된 작업의 표시 이름을 설정 하는 bitsadmin setdisplayname에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 601c5b406132e70fb7d4facb97329f7456002bb4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849546"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

지정된 된 작업의 표시 이름을 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetDisplayName <Job> <DisplayName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|DisplayName|지정된 된 작업의 표시 이름에 사용 되는 텍스트입니다.|

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 표시 이름을 설정 *myDownloadJob* 에 *myDownloadJob2*합니다.
```
C:\>bitsadmin /SetDisplayName myDownloadJob Download Music Job
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)