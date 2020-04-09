---
title: bitsadmin addfilewithranges
description: 지정 된 작업에 파일을 추가 하는 **bitsadmin addfilewithranges**에 대 한 Windows 명령 항목입니다. BITS는 원격 파일에서 지정된 된 범위를 다운로드 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: df0ce0bf-dff1-4a48-a16f-fd2f4d5f7189
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60b448550473691bbbaf573f99f00609e14e0f42
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850956"
---
# <a name="bitsadmin-addfilewithranges"></a>bitsadmin addfilewithranges

지정된 된 작업에 파일을 추가 합니다. BITS는 원격 파일에서 지정된 된 범위를 다운로드 합니다. 이 스위치는 다운로드 작업에 대해서만 유효 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /AddFileWithRanges <Job> <RemoteURL> <LocalName> <RangeList>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업 | 작업의 표시 이름 또는 GUID입니다. |
| RemoteURL | 서버에 있는 파일의 URL입니다. |
| LocalName | 로컬 컴퓨터에 있는 파일의 이름입니다. 파일에 대 한 절대 경로를 포함 해야 합니다. |
| RangeList | 쉼표로 구분 된 오프셋: 길이 쌍의 목록입니다. 길이 값에서 오프셋된 값을 구분 하려면 콜론을 사용 합니다. 예를 들어 `0:100,2000:100,5000:eof` 값은 오프셋 0에서 100 바이트, 오프셋 2000의 100 바이트, 오프셋 5000에서 파일 끝 까지의 나머지 바이트를 전송 하도록 비트를 지시 합니다. |

## <a name="remarks"></a>주의

- 토큰 **eof** 는 *\<범위 목록 >* 의 오프셋 및 길이 쌍 내에서 유효한 길이 값입니다. 지정된 된 파일의 끝까지 읽는 서비스에 지시 합니다.

- 길이가 0 인 범위가 동일한 오프셋을 사용 하는 다른 범위와 함께 지정 된 경우 AddFileWithRanges는 실패 합니다 (예: 0x8020002c).

    `C:\bits>bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:0,100:5`

    **오류 메시지:** 0x8020002c에 파일을 추가할 수 없습니다. 바이트 범위 목록을 지원 되지 않는 몇 가지 겹치는 범위를 포함 합니다.

    **해결 방법:** 길이가 0 인 범위를 먼저 지정 하지 마십시오. 예를 들어 다음을 사용 합니다. 

    `bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:5,100:0.`

## <a name="examples"></a>예

다음 예제에서는 0, 100 바이트에서에서 오프셋 오프셋된 2000에서에서 100 바이트를 전송 하는 비트 하 고에서 남아 있는 바이트 오프셋 5000 파일의 끝에 키를 누릅니다.

```
C:\>bitsadmin /addfilewithranges http://downloadsrv/10mb.zip c:\10mb.zip 0:100,2000:100,5000:eof
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)