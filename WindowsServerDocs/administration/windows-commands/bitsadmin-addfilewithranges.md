---
title: bitsadmin addfilewithranges
description: Windows 명령 항목에 대 한 **bitsadmin 0 인** -지정된 된 된 작업에 파일을 추가 합니다. BITS는 원격 파일에서 지정된 된 범위를 다운로드 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df0ce0bf-dff1-4a48-a16f-fd2f4d5f7189
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5e1e4f8af9117928f9ab044d29e65f57aa5a119
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811273"
---
# <a name="bitsadmin-addfilewithranges"></a>bitsadmin addfilewithranges

지정된 된 작업에 파일을 추가 합니다. BITS는 원격 파일에서 지정된 된 범위를 다운로드 합니다. 이 스위치는 다운로드 작업에 대해서만 유효 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /AddFileWithRanges <Job> <RemoteURL> <LocalName> <RangeList>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|RemoteURL|*RemoteURL* 서버에서 파일의 URL입니다.|
|LocalName|*LocalName* 로컬 컴퓨터에 있는 파일의 이름입니다. *LocalName* 파일에 절대 경로 포함 해야 합니다.|
|RangeList|*RangeList* 오프셋: 길이가 쌍의는 쉼표로 구분 된 목록입니다. 길이 값에서 오프셋된 값을 구분 하려면 콜론을 사용 합니다. 예를 들어 값 `0:100,2000:100,5000:eof` 오프셋 0, 100 바이트 오프셋 2000에서에서 100 바이트를 전송 하는 비트를 지시 하 고에서 남아 있는 바이트 오프셋 5000 파일의 끝에 있습니다.|

## <a name="more-information"></a>추가 정보

-   토큰 **eof** 에 있는 오프셋 및 길이가 쌍 내에서 유효한 길이 값은  *\<RangeList >* 합니다. 지정된 된 파일의 끝까지 읽는 서비스에 지시 합니다.
-   길이가 0 인 범위와 같은 동일한 오프셋을 사용 하 여 다른 범위와 함께 지정 된 경우 0 인 오류 코드 0x8020002c 못합니다 note: C:\bits > bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:0, 100:5

    오류 메시지: 0x8020002c 작업에 파일을 추가할 수 없습니다. 바이트 범위 목록을 지원 되지 않는 몇 가지 겹치는 범위를 포함 합니다.

    해결 방법: 먼저 빈 범위를 지정 하지 마십시오. 예를 들어: bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:5, 100:0 합니다.

## <a name="examples"></a>예

다음 예제에서는 0, 100 바이트에서에서 오프셋 오프셋된 2000에서에서 100 바이트를 전송 하는 비트 하 고에서 남아 있는 바이트 오프셋 5000 파일의 끝에 키를 누릅니다.

```
C:\>bitsadmin /addfilewithranges http://downloadsrv/10mb.zip c:\10mb.zip "0:100,2000:100,5000:eof"
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)