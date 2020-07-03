---
title: bitsadmin addfilewithranges
description: 지정 된 작업에 파일을 추가 하는 bitsadmin addfilewithranges 명령에 대 한 참조 문서입니다. BITS는 원격 파일에서 지정된 된 범위를 다운로드 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: df0ce0bf-dff1-4a48-a16f-fd2f4d5f7189
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5439cfb8330cda7c51150c720fe45faccca8e1ec
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927074"
---
# <a name="bitsadmin-addfilewithranges"></a>bitsadmin addfilewithranges

지정된 된 작업에 파일을 추가 합니다. BITS는 원격 파일에서 지정된 된 범위를 다운로드 합니다. 이 스위치는 다운로드 작업에 대해서만 유효 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /addfilewithranges <job> <remoteURL> <localname> <rangelist>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| remoteURL | 서버에 있는 파일의 URL입니다. |
| localname | 로컬 컴퓨터에 있는 파일의 이름입니다. 파일에 대 한 절대 경로를 포함 해야 합니다. |
| 범위 목록 | 쉼표로 구분 된 오프셋: 길이 쌍의 목록입니다. 길이 값에서 오프셋된 값을 구분 하려면 콜론을 사용 합니다. 예를 들어 값은 오프셋 `0:100,2000:100,5000:eof` 0에서 100 바이트를 전송 하도록 비트를, 오프셋 2000에서 100 바이트를 전송 하 고, 나머지 바이트는 오프셋 5000에서 파일 끝으로 전송 하도록 비트를 알려 줍니다. |

## <a name="remarks"></a>설명

- 토큰 **eof** 에 있는 오프셋 및 길이가 쌍 내에서 유효한 길이 값은 `<rangelist>`합니다. 지정된 된 파일의 끝까지 읽는 서비스에 지시 합니다.

- `addfilewithranges`길이가 0 인 범위가 동일한 오프셋을 사용 하 여 다른 범위와 함께 지정 된 경우 (예:) 오류 코드 0x8020002c를 사용 하 여 명령이 실패 합니다.

    `c:\bits>bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:0,100:5`

    **오류 메시지:** 0x8020002c에 파일을 추가할 수 없습니다. 바이트 범위 목록을 지원 되지 않는 몇 가지 겹치는 범위를 포함 합니다.

    **해결 방법:** 길이가 0 인 범위를 먼저 지정 하지 마십시오. 예를 들어 `bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:5,100:0`를 사용합니다.

## <a name="examples"></a>예

오프셋 0에서 100 바이트, 오프셋 2000에서 100 바이트, 오프셋 5000에서 파일 끝 까지의 나머지 바이트를 전송 하려면 다음을 수행 합니다.

```
bitsadmin /addfilewithranges http://downloadsrv/10mb.zip c:\10mb.zip 0:100,2000:100,5000:eof
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
