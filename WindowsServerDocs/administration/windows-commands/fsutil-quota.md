---
title: fsutil quota
description: 네트워크 기반 저장소를 보다 정확 하 게 제어할 수 있도록 NTFS 볼륨의 디스크 할당량을 관리 하는 fsutil quota 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 21225c11-7c72-4ea2-96bd-e63d4beb3be5
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: f757f822a903f6b5c6d221e17f87cf1e73d1555f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925229"
---
# <a name="fsutil-quota"></a>fsutil quota

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

네트워크 기반 저장소를 보다 정확 하 게 제어할 수 있도록 NTFS 볼륨의 디스크 할당량을 관리 합니다.

## <a name="syntax"></a>구문

```
fsutil quota [disable] <volumepath>
fsutil quota [enforce] <volumepath>
fsutil quota [modify] <volumepath> <threshold> <limit> <username>
fsutil quota [query] <volumepath>
fsutil quota [track] <volumepath>
fsutil quota [violations]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| disable | 할당량 추적 및 지정된 된 볼륨에 적용 하는 사용 하지 않도록 설정 합니다. |
| 강제 적용 | 지정된 된 볼륨에 대 한 할당량 사용량을 적용합니다. |
| 수정 | 기존 디스크 할당량을 수정 하거나 새 할당량을 만듭니다. |
| Query | 기존 디스크 할당량 나열 합니다. |
| track | 디스크에서 지정 된 볼륨에서 사용을 추적 합니다. |
| 위반 | 시스템 및 애플리케이션 로그를 검색 하 고 할당량 위반이 검색 되었습니다 또는 사용자 할당량 임계값 또는 할당량 제한에 도달한 있는지를 나타내는 메시지가 표시 됩니다. |
| `<volumepath>` | 필수 요소. 드라이브 이름 뒤에 콜론 또는 GUID (형식)를 지정 합니다 `volume{GUID}` . |
| `<threshold>`  | 경고가 발생 하는 제한 (바이트)을 설정 합니다. 이 매개 변수는 명령에 필요 `fsutil quota modify` 합니다. |
| `<limit>` | 허용 되는 최대 디스크 사용량 (바이트)을 설정 합니다. 이 매개 변수는 명령에 필요 `fsutil quota modify` 합니다. |
| `<username>` | 도메인 또는 사용자 이름을 지정합니다. 이 매개 변수는 명령에 필요 `fsutil quota modify` 합니다. |

#### <a name="remarks"></a>설명

- 디스크 할당량은 볼륨 단위로 구현 되며, 하드 및 소프트 저장소 제한을 사용자 단위로 구현할 수 있도록 합니다.

- 새 사용자를 추가할 때마다 할당량 제한을 설정 하는 데 **fsutil quota** 를 사용 하는 write 스크립트를 사용 하거나, 할당량 한도를 자동으로 추적 하 고, 보고서로 컴파일한 후 자동으로 시스템 관리자에 게 전자 메일로 보낼 수 있습니다.

### <a name="examples"></a>예

GUID, {928842df-5a01-11de-a85c-806e6f6e6963}를 사용 하 여 지정 된 디스크 볼륨에 대 한 기존 디스크 할당량을 나열 하려면 다음을 입력 합니다.

```
fsutil quota query volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

드라이브 문자를 지정 된 디스크 볼륨에 대 한 기존 디스크 할당량을 나열 하려면 **c:**, 유형:

```
fsutil quota query C:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [fsutil](fsutil.md)
