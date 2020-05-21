---
title: fsutil objectid
description: 파일, 디렉터리 및 링크와 같은 다른 개체를 추적 하는 개체 식별자를 관리 하는 fsutil objectid 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 693ab895-9d0c-47c1-9f52-df5cd287842a
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: cdaa3fb0a8a439e568e4b181890db49923e109e7
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435810"
---
# <a name="fsutil-objectid"></a>fsutil objectid

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

DLT (분산 링크 추적) 클라이언트 서비스 및 FRS (파일 복제 서비스)에서 사용 하는 내부 개체인 Oid (개체 식별자)를 관리 하 여 파일, 디렉터리 및 링크와 같은 다른 개체를 추적 합니다. 개체 식별자 대부분 프로그램에서 표시 되지 않으며 수정 해서는 안 됩니다.

> [!WARNING]
> 개체 식별자를 삭제, 설정 또는 수정 하지 마십시오. 삭제 하거나 개체 식별자를 설정 및 데이터의 전체 볼륨까지 파일 일부 데이터가 손실 될 수 있습니다. 또한 DLT (분산 링크 추적) 클라이언트 서비스 및 FRS (파일 복제 서비스)에서 부정적인 동작이 발생할 수 있습니다.

## <a name="syntax"></a>구문

```
fsutil objectid [create] <filename>
fsutil objectid [delete] <filename>
fsutil objectid [query] <filename>
fsutil objectid [set] <objectID> <birthvolumeID> <birthobjectID> <domainID> <filename>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| create | 지정된 된 파일에 아직 없는 경우 하나는 개체 식별자를 만듭니다. 이 하위 명령에 해당 하는 파일에는 개체 식별자에 이미 있는 경우는 **쿼리** 하위 명령입니다. |
| delete | 개체 식별자를 삭제합니다. |
| Query | 개체 식별자를 쿼리 합니다. |
| set | 개체 식별자를 설정합니다. |
| `<objectID>` | 볼륨 내에서 고유 하 게 보장 되는 파일 관련 16 바이트 16 진수 식별자를 설정 합니다. 개체 식별자는 DLT (분산 링크 추적) 클라이언트 서비스 및 파일을 식별 하는 FRS (파일 복제 서비스)에 사용 됩니다. |
| `<birthvolumeID>` | 볼륨에 파일이 있던 개체 식별자를 처음 얻었을 때를 나타냅니다. 이 값은 DLT 클라이언트 서비스에서 사용 되는 16 바이트 16 진수 식별자입니다. |
| `<birthobjectID>` | 파일의 원래 개체 식별자를 나타냅니다 (파일이 이동 될 때 *ObjectID* 는 변경 될 수 있음). 이 값은 DLT 클라이언트 서비스에서 사용 되는 16 바이트 16 진수 식별자입니다. |
| `<domainID>` | 16 바이트 16 진수 도메인 식별자입니다. 이 값은 현재 사용 되지 않으며 모두 0으로 설정 해야 합니다. |
| `<filename>` | 파일 이름 및 확장명을 포함 하는 파일의 전체 경로를 지정 합니다 (예: *C:\documents\filename.txt*). |

#### <a name="remarks"></a>설명

- 개체 식별자가 있는 모든 파일에는 역시 출생 볼륨 식별자, 생년월일 개체 id를 및 도메인 식별자입니다. 파일을 이동 하는 경우 개체 식별자 변경할 수 있지만 출생 볼륨 및 생년월일 개체 식별자 동일 하 게 유지 합니다. 이 동작을 통해 Windows 운영 체제는 항상 이동 되었는지에 관계 없이 파일을 검색 합니다.

### <a name="examples"></a>예

개체 식별자를 만들려면 다음을 입력 합니다.

`fsutil objectid create c:\temp\sample.txt`

개체 식별자를 삭제 하려면 다음을 입력 합니다.

`fsutil objectid delete c:\temp\sample.txt`

개체 식별자를 쿼리하려면 다음을 입력 합니다.

`fsutil objectid query c:\temp\sample.txt`

개체 식별자를 설정 하려면 다음을 입력 합니다.

`fsutil objectid set 40dff02fc9b4d4118f120090273fa9fc f86ad6865fe8d21183910008c709d19e 40dff02fc9b4d4118f120090273fa9fc 00000000000000000000000000000000 c:\temp\sample.txt`

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [fsutil](fsutil.md)
