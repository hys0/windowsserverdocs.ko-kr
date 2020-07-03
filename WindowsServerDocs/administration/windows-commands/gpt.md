---
title: gpt
description: Gpt 명령에 대 한 참조 문서로, 포커스가 있는 파티션에 gpt 특성을 할당 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1d6f9029-807f-4420-a336-36669b5361bc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 40d3536f5a6be0bf520095e3ba61f75b7a2addc7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924619"
---
# <a name="gpt"></a>gpt

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기본 GUID 파티션 테이블 (gpt) 디스크에서이 명령은 포커스가 있는 파티션에 gpt 특성을 할당 합니다. Gpt 파티션 특성은 파티션 사용에 대 한 추가 정보를 제공 합니다. 일부 특성은 GUID 파티션 형식에 따라 다릅니다.

이 작업을 수행 하려면 기본 gpt 파티션을 선택 해야 합니다. [파티션 선택 명령을](select-partition.md) 사용 하 여 기본 gpt 파티션을 선택 하 고 포커스를 이동 합니다.

> [!CAUTION]
> Gpt 특성을 변경 하면 기본 데이터 볼륨에 드라이브 문자가 할당 되지 않거나 파일 시스템이 탑재 되지 않을 수 있습니다. OEM (원본 장비 제조업체) 또는 gpt 디스크에 익숙한 IT 전문가가 아니면 gpt 특성을 변경 하지 않는 것이 좋습니다.

## <a name="syntax"></a>구문

```
gpt attributes=<n>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 특성 =`<n>` | 포커스가 있는 파티션을에 적용할 특성에 대 한 값을 지정 합니다. Gpt 특성 필드는 두 개의 하위 필드를 포함 하는 64 비트 필드입니다. 하위 필드는 모든 파티션 Id에 공통적으로 적용 하는 동안 파티션 ID의 경우에만 더 높은 필드 해석 됩니다. 사용 가능한 값은 다음과 같습니다.<ul><li>**0x0000000000000001** -컴퓨터가 제대로 작동 하는 데 필요한 파티션을 지정 합니다.</li><li>**0x8000000000000000** -디스크를 다른 컴퓨터로 이동 하거나 컴퓨터에서 처음으로 디스크를 볼 때 파티션이 드라이브 문자를 수신 하지 않도록 지정 합니다.</li><li>**0x4000000000000000** -탑재 관리자에서 검색 되지 않도록 파티션의 볼륨을 숨깁니다.</li><li>**0x2000000000000000** -파티션이 다른 파티션의 섀도 복사본 임을 지정 합니다.</li><li>**0x1000000000000000** -파티션을 읽기 전용으로 지정 합니다. 이 특성을 쓰지 볼륨을 방지 합니다.</li></ul><p>이러한 특성에 대 한 자세한 내용은 [Create_PARTITION_PARAMETERS 구조체](https://docs.microsoft.com/windows/win32/api/vds/ns-vds-create_partition_parameters)에서 특성 섹션을 참조 하세요. |

#### <a name="remarks"></a>설명

- EFI 시스템 파티션에 운영 체제를 시작 하는 데 필요한 바이너리만 포함 되어 있습니다. 따라서 쉽게 OEM 바이너리 또는 이진 파일에 대 한 다른 파티션에 위치 하는 운영 체제입니다.

### <a name="examples"></a>예

컴퓨터에서 포커스가 있는 파티션에 드라이브 문자를 자동으로 할당 하지 않도록 하려면 gpt 디스크를 이동 하는 동안 다음을 입력 합니다.

```
gpt attributes=0x8000000000000000
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [파티션 선택 명령](select-partition.md)

- [create_PARTITION_PARAMETERS 구조체](https://docs.microsoft.com/windows/win32/api/vds/ns-vds-create_partition_parameters)
