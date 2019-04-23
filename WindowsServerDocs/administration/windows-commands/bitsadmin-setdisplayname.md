---
title: bitsadmin setdisplayname
description: Windows 명령 항목에 대 한 **bitsadmin setdisplayname** -지정된 된 된 작업의 표시 이름을 가져오거나 설정 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d50cd2785e42b554cee340abc97fe4e4b53adcfc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843674"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname



지정된 된 작업의 표시 이름을 설정합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetDisplayName <Job> <DisplayName>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|DisplayName|지정된 된 작업의 표시 이름에 사용 되는 텍스트입니다.|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 표시 이름을 설정 *myDownloadJob* 에 *myDownloadJob2*합니다.
```
C:\>bitsadmin /SetDisplayName myDownloadJob "Download Music Job"
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)