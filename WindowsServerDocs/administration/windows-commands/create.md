---
title: create
description: 디스크에 파티션 또는 섀도 파티션, 하나 이상의 디스크에 볼륨 또는 VHD (가상 하드 디스크)를 만드는 create 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b45acde1-8f4f-4ec3-b905-d8188f884af8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b5b31f43e58b9e2eddb18f624c1054c9d028f4c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929535"
---
# <a name="create"></a>create

디스크, 하나 이상의 디스크에 있는 볼륨 또는 VHD (가상 하드 디스크)에 파티션 또는 그림자를 만듭니다. 이 명령을 사용 하 여 섀도 디스크에서 볼륨을 만드는 경우 섀도 복사본 집합에 하나 이상의 볼륨이 이미 있어야 합니다.

## <a name="syntax"></a>구문

```
create partition
create volume
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| [create partition primary 명령](create-partition-primary.md) | 포커스가 있는 기본 디스크에 주 파티션을 만듭니다. |
| [create partition efi 명령](create-partition-efi.md) | Itanium 기반 컴퓨터의 gpt (GUID 파티션 테이블) 디스크에 EFI (확장 가능 펌웨어 인터페이스) 시스템 파티션을 만듭니다. |
| [파티션 만들기 확장 명령](create-partition-extended.md) | 포커스가 있는 디스크에는 확장 된 파티션을 만듭니다. |
| [create partition logical 명령](create-partition-logical.md) | 기존 확장 파티션의 논리 파티션을 만듭니다. |
| [create partition msr 명령](create-partition-msr.md) | Gpt (GUID 파티션 테이블) 디스크에 Microsoft 예약 (MSR) 파티션을 만듭니다. |
| [단순 볼륨 만들기 명령](create-volume-simple.md) | 지정된 된 동적 디스크의 단순 볼륨을 만듭니다. |
| [볼륨 미러 만들기 명령](create-volume-mirror.md) | 지정 된 동적 디스크가 두 개를 사용 하 여 미러를 볼륨을 만듭니다. |
| [볼륨 raid 명령 만들기](create-volume-raid.md) | 지정 된 동적 디스크를 세 개 이상 사용 하 여 RAID-5 볼륨을 만듭니다. |
| [볼륨 스트라이프 만들기 명령](create-volume-stripe.md) | 두 개 이상의 지정 된 동적 디스크를 사용 하 여 스트라이프 볼륨을 만듭니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
