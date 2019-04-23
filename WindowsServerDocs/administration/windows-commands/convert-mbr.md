---
title: convert mbr
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a635a4c0-af73-4330-b021-51d483424537
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da8d62567863bc38a5aa0b35a8f3fe4ee24cc888
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834614"
---
# <a name="convert-mbr"></a>convert mbr



GUID 파티션 테이블 (GPT) 파티션 스타일을 사용 하 여 빈 기본 디스크 마스터 부트 레코드 (MBR) 파티션 스타일을 사용 하 여 기본 디스크 변환 합니다.

> [!IMPORTANT]
> 디스크는 MBR 디스크로 변환 하려면 비어 있어야 합니다. 데이터를 백업 하 고 디스크를 변환 하기 전에 모든 파티션 또는 볼륨을 삭제 합니다.

이 명령을 사용 하는 방법에 대 한 지침은 [마스터 부트 레코드 디스크로 GUID 파티션 테이블 변경](https://go.microsoft.com/fwlink/?LinkId=207050) (https://go.microsoft.com/fwlink/?LinkId=207050)합니다.

## <a name="syntax"></a>구문

```
convert mbr [noerr]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|noerr|만 스크립팅 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|

## <a name="remarks"></a>설명

-   이 작업을 수행 하려면 기본 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 기본 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="BKMK_examples"></a>예제

기본 디스크를 gpt 파티션에서에서 MBR 파티션 스타일으로 변환 하려면 다음을 입력 >:
```
convert mbr
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

