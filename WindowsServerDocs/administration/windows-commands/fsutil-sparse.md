---
title: fsutil sparse
description: 스파스 파일을 관리 하는 fsutil sparse 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 77545920-2d13-4f35-a4d1-14dbec8340dc
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: e68ac844bb7aa7e22a9df0ddb0c982b3701231d7
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435718"
---
# <a name="fsutil-sparse"></a>fsutil sparse

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

스파스 파일을 관리 합니다. 스파스 파일은 하나 이상의 영역에 할당 되지 않은 데이터를 포함 하는 파일입니다.

프로그램은 이러한 할당 되지 않은 영역에 0 값을 가진 바이트를 포함 하 고 있으며, 이러한 0을 나타내는 디스크 공간이 없다는 것을 볼 수 있습니다. 스파스 파일을 읽을 때 할당 된 데이터는 저장 시에 반환 되 고 할당 되지 않은 데이터가 반환 기본적으로 c2 보안 요구 사항에 따라 0으로. 할당을 취소할 수에서 아무 곳 이나 파일에서 데이터를 허용 하는 스파스 파일을 지원 합니다.

## <a name="syntax"></a>구문

```
fsutil sparse [queryflag] <filename>
fsutil sparse [queryrange] <filename>
fsutil sparse [setflag] <filename>
fsutil sparse [setrange] <filename> <beginningoffset> <length>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| queryflag | 스파스를 쿼리 합니다. |
| queryrange | 파일을 검색 하 고 0이 아닌 데이터를 포함할 수 있는 범위를 검색 합니다. |
| setflag | 스파스로 표시 된 파일을 표시합니다. |
| setrange | 파일의 지정된 된 범위를 0으로 채웁니다. |
| `<filename>` | 파일 이름 및 확장명을 포함 하는 파일의 전체 경로를 지정 합니다 (예: *C:\documents\filename.txt*). |
| `<beginningoffset>` | 스파스로 표시할 파일 내의 오프셋을 지정 합니다. |
| `<length>` | 스파스로 표시할 파일의 영역 길이 (바이트)를 지정 합니다. |

#### <a name="remarks"></a>설명

- 모든 의미 있는 데이터 또는 0이 아닌 데이터는 할당 되지만 의미 없는 모든 데이터 (0으로 구성 된 데이터의 많은 문자열)는 할당 되지 않습니다.

- 스파스 파일에서 큰 범위의 0 디스크 할당이 필요 하지 않을 수 있습니다. 0이 아닌 데이터에 대 한 공간은 파일이 기록 될 때 필요에 따라 할당 됩니다.

- 만 스파스 또는 압축 된 파일 수는 0으로 설정 운영 체제에 알려진 범위.

- 파일이 스파스 또는 압축 된 경우 NTFS는 파일 내에서 디스크 공간 할당을 취소할 수 있습니다. 이 바이트 범위 파일 크기를 확장 하지 않고 0으로 설정 합니다.

### <a name="examples"></a>예

*C:\temp* 디렉터리에서 *.sample* 이라는 파일에 스파스를 표시 하려면 다음을 입력 합니다.

```
fsutil sparse setflag c:\temp\sample.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [fsutil](fsutil.md)
