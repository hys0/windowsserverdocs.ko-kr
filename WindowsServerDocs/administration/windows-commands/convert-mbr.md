---
title: convert mbr
description: Mbr 변환에 대 한 Windows 명령 항목은 MBR (마스터 부트 레코드) 파티션 스타일을 사용 하 여 GPT (GUID 파티션 테이블) 파티션 스타일로 빈 기본 디스크를 기본 디스크로 변환 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a635a4c0-af73-4330-b021-51d483424537
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eeaf79a380fb5f1074d2bbef004537804caa0d8d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847206"
---
# <a name="convert-mbr"></a>convert mbr

MBR (마스터 부트 레코드) 파티션 스타일을 사용 하 여 GPT (GUID 파티션 테이블) 파티션 스타일을 포함 하는 빈 기본 디스크를 기본 디스크로 변환 합니다.

> [!IMPORTANT]
> 디스크는 MBR 디스크로 변환 하려면 비어 있어야 합니다. 데이터를 백업 하 고 디스크를 변환 하기 전에 모든 파티션 또는 볼륨을 삭제 합니다.

이 명령을 사용 하는 방법에 대 한 지침은 [GUID 파티션 테이블 디스크를 마스터 부트 레코드 디스크로 변경](https://go.microsoft.com/fwlink/?LinkId=207050) (https://go.microsoft.com/fwlink/?LinkId=207050)을 참조 하세요.

## <a name="syntax"></a>구문

```
convert mbr [noerr]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|noerr|스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|

## <a name="remarks"></a>주의

-   이 작업을 수행 하려면 기본 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 기본 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

기본 디스크를 gpt 파티션에서에서 MBR 파티션 스타일으로 변환 하려면 다음을 입력 >:
```
convert mbr
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

