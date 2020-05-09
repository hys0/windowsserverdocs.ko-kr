---
title: 논리적 파티션 만들기
description: 파티션 작성 논리 명령에 대 한 참조 항목으로, 기존 확장 파티션에 논리 파티션을 만듭니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f59b79a-d690-4d0e-ad38-40df5a0ce38e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 99b8c837fe5da295087f9b146bf429d91ebc8693
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993273"
---
# <a name="create-partition-logical"></a>논리적 파티션 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기존 확장 파티션에 논리 파티션을 만듭니다. 파티션이 만들어지면 포커스는 자동으로 새 파티션으로 이동 합니다.

>[!IMPORTANT]
> MBR (마스터 부트 레코드) 디스크 에서만이 명령을 사용할 수 있습니다. [디스크 선택](select-disk.md) 명령을 사용 하 여 기본 MBR 디스크를 선택 하 고 포커스를 이동 해야 합니다.
>
> 논리 드라이브를 만들려면 먼저 [확장 파티션을](create-partition-extended.md) 만들어야 합니다.

## <a name="syntax"></a>구문

```
create partition logical [size=<n>] [offset=<n>] [align=<n>] [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| 크기 =`<n>` | 논리 파티션의 크기 (mb)를 지정 합니다 .이 크기는 확장 된 파티션 보다 작아야 합니다. 크기를 지정 하는 경우 파티션을 확장 파티션의 가능한 공간이 없을 때까지 계속 합니다. |
| offset =`<n>` | 파티션이 생성 되는 오프셋 (KB)을 지정 합니다. 오프셋 반올림을 완전히 사용 되는 모든 실린더 크기를 채웁니다. 오프셋이, 파티션은 저장 하는 데 충분히 큰 첫 번째 디스크에에서 배치 됩니다. 파티션은 **size =`<n>`** 로 지정 된 수의 바이트 이상입니다. 논리 파티션에 대 한 크기를 지정 하면 확장된 파티션의 보다 작아야 합니다. |
| align =`<n>` | 모든 볼륨 또는 파티션 범위에 있는 가장 가까운 맞춤 경계선을 맞춥니다. 일반적으로 성능 향상을 위해 하드웨어 RAID 논리 단위 번호 (LUN) 배열과 함께 사용. `<n>`디스크의 시작부터 가장 가까운 맞춤 경계로 해당 하는 킬로바이트 (KB)의 수입니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

#### <a name="remarks"></a>설명

- **Size** 및 **offset** 매개 변수가 지정 되지 않은 경우 논리 파티션은 확장 파티션에서 사용 가능한 가장 큰 디스크 범위에 생성 됩니다.

## <a name="examples"></a>예

선택된 된 디스크의 확장 파티션의 크기를 메가바이트 1000 논리적 파티션을 만들려면 다음을 입력 합니다.

```
create partition logical size=1000
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [create 명령](create.md)

- [select disk](select-disk.md)
