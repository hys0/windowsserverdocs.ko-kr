---
title: 복구
description: '* * * *에 대 한 참조 문서'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9f84f661-f3cd-48c8-bf08-87819cf626fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e9afb6c418558078496871b71bfaff706753b0a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936758"
---
# <a name="repair"></a>복구

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

\-실패 한 디스크 영역을 지정 된 동적 디스크로 바꿔 포커스가 있는 RAID 5 볼륨을 복구 합니다.



## <a name="syntax"></a>구문

```
repair disk=<n> [align=<n>] [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수  |                                                                                             설명                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 디스크로\=<n>  |                                                                 실패 한 디스크 영역을 대체 하는 동적 디스크를 지정 합니다.                                                                 |
| 않아\=<n> |          모든 볼륨 또는 파티션 범위에 있는 가장 가까운 맞춤 경계선을 맞춥니다. *n* 은 \( \) 디스크의 시작부터 가장 가까운 맞춤 경계로 표시 되는 kb 수입니다.           |
|   noerr    | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="remarks"></a>설명

-   지정 된 동적 디스크는 RAID에 실패 한 디스크 영역의 전체 크기 보다 크거나 여유 공간이 있어야 합니다.\-5 볼륨입니다.

-   raid에서 볼륨\-5 배열을이 작업이 성공 하기 위해 선택 해야 합니다. 사용 하 여는 **볼륨 선택** 볼륨을 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="examples"></a>예
동적 디스크 4로 바꾸어 포커스가 있는 볼륨을 바꾸려면를 입력 합니다.

```
repair disk=4
```

## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)




