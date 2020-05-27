---
title: list
description: 디스크 목록, 디스크의 파티션, 디스크의 볼륨 또는 Vhd (가상 하드 디스크)를 표시 하는 목록 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 69b105a1-9710-4a06-8102-38cc9e475ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 422460fc405326b5802ff1f00827f690d6599b1b
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820203"
---
# <a name="list"></a>list

디스크의 디스크, 디스크의 파티션, 디스크의 볼륨 또는 Vhd (가상 하드 디스크)의 목록을 표시 합니다.

## <a name="syntax"></a>구문

```
list { disk | partition | volume | vdisk }
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| disk | 디스크 및 해당 디스크에 대 한 정보 (예: 크기, 사용 가능한 공간 크기, 디스크가 기본 또는 동적 디스크 인지 여부, 디스크에서 MBR (마스터 부트 레코드) 또는 GPT (GUID 파티션 테이블) 파티션 스타일)를 사용 하는지 여부에 대 한 정보를 표시 합니다. |
| partition | 현재 디스크의 파티션 테이블에 나열 된 파티션을 표시 합니다. |
| 볼륨 | 모든 디스크에 기본 및 동적 볼륨 목록을 표시합니다. |
| vdisk | 연결 및/또는 선택 된 Vhd의 목록을 표시 합니다. 이 명령은 현재 선택 되어; 경우 분리 된 Vhd를 나열 그러나, VHD가 연결 될 때까지 알 수 없는 디스크 유형 설정 됩니다. 별표 (*)로 표시 된 VHD에 포커스가 있습니다. |

#### <a name="remarks"></a>설명

- 동적 디스크에 파티션을 나열할 때 파티션은 디스크의 동적 볼륨에 해당 하지 않을 수 있습니다. 이러한 불일치는 동적 디스크에 시스템 볼륨이 나 부팅 볼륨 (디스크에 있는 경우)에 대 한 파티션 테이블의 항목이 포함 되어 있기 때문에 발생 합니다. 또한 동적 볼륨에 사용할 공간을 예약 하기 위해 디스크의 나머지 부분을 차지 하는 파티션을 포함 합니다.

- 별표 (*)로 표시 된 개체에 포커스가 있습니다.

- 디스크가 없는 경우 디스크를 나열할 때 디스크 번호 앞에 M이 붙습니다. 예를 들어 첫 번째 누락 된 디스크의 번호는 *M0*입니다.

### <a name="examples"></a>예

```
list disk
list partition
list volume
list vdisk
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
