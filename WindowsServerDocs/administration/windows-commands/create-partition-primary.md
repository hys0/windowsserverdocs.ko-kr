---
title: create partition primary
description: 기본 디스크에 포커스가 있는 주 파티션을 만드는 create partition primary 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6d652d8e-3935-4a91-8ced-b17c0e7937be
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9014b69528d4a67ba2c9c11b8ec53cf3a0f569f6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929623"
---
# <a name="create-partition-primary"></a>create partition primary

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포커스가 있는 기본 디스크에 주 파티션을 만듭니다. 파티션이 만들어지면 포커스는 자동으로 새 파티션으로 이동 합니다.

> [!IMPORTANT]
> 이 작업을 수행 하려면 기본 디스크를 선택 해야 합니다. [디스크 선택](select-disk.md) 명령을 사용 하 여 기본 디스크를 선택 하 고 포커스를 이동 해야 합니다.

## <a name="syntax"></a>구문

```
create partition primary [size=<n>] [offset=<n>] [id={ <byte> | <guid> }] [align=<n>] [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 크기 =`<n>` | 파티션의 크기 (mb)를 지정 합니다. 크기를 지정 하는 경우 파티션이 될 때까지 할당 되지 않은 현재 지역에서 공간을 계속 합니다. |
| offset =`<n>` | 파티션이 생성 되는 오프셋 (KB)입니다. 없는 오프셋을 지정 하는 경우 파티션을 저장 하는 데 충분히 큰 가장 큰 디스크 범위의 시작 부분에 시작 됩니다. |
| align =`<n>` | 모든 파티션 범위에 있는 가장 가까운 맞춤 경계선을 맞춥니다. 일반적으로 성능 향상을 위해 하드웨어 RAID 논리 단위 번호 (LUN) 배열과 함께 사용. `<n>`디스크의 시작부터 가장 가까운 맞춤 경계로 해당 하는 킬로바이트 (KB)의 수입니다. |
| id = { `<byte>  | <guid>` } | 파티션 형식을 지정합니다. 이 매개 변수는 OEM (주문자 상표 제조업) 사용을 위한 것입니다. 이 매개 변수는 모든 파티션 형식 바이트 또는 GUID를 지정할 수 있습니다. DiskPart는 16 진수 형식의 바이트 인지 아니면 GUID 인지 확인 하는 것을 제외 하 고는 파티션 형식 유효성을 검사 하지 않습니다. **주의:** 이 매개 변수를 사용 하 여 파티션 만들기 실패 하거나 시작 하지 못할 컴퓨터 발생할 수 있습니다. Gpt 디스크를 사용 하는 OEM 또는 IT 전문가가 아닌 경우이 매개 변수를 사용 하 여 gpt 디스크에 파티션을 만들지 마십시오. 대신 항상 [create partition efi](create-partition-efi.md) 명령을 사용 하 여 efi 시스템 파티션을 만들고, 파티션 [msr 만들기](create-partition-msr.md) 명령을 사용 하 여 Microsoft 예약 파티션을 만들고, [파티션 기본 만들기](create-partition-primary.md)명령을 사용 하 여 `id={ <byte>  | <guid>` gpt 디스크에 주 파티션을 만듭니다.<p>**MBR (마스터 부트 레코드) 디스크의**경우 파티션에 대 한 16 진수 형식의 파티션 유형 바이트를 지정 해야 합니다. 이 매개 변수를 지정 하지 않으면 명령은 `0x06` 파일 시스템이 설치 되지 않도록 지정 하는 형식의 파티션을 만듭니다. 다음은 이러한 템플릿의 예입니다.<ul><li>**LDM 데이터 파티션:** 0x42</li><li>**복구 파티션:** 0x27</li><li>**인식 된 OEM 파티션:** 12, 0X84, 0Xde, 0XFE, 0xde</li></ul><p>**Gpt (GUID 파티션 테이블) 디스크의**경우 만들려는 파티션에 대 한 파티션 유형 GUID를 지정할 수 있습니다. 인식 된 Guid는 다음과 같습니다.<ul><li>**EFI 시스템 파티션:** c12a7328-f81f-11d2-ba4b-00a0c93ec93b</li><li>**Microsoft Reserved partition:** e3c9e316-0b5c-4db8-817d-f92df00215ae</li><li>**기본 데이터 파티션:** ebd0a0a2-b9e5-4433-87c0-68b6b72699c7</li><li>**LDM 메타 데이터 파티션 (동적 디스크):** 5808c8aa-7e8f-42e0-85d2-e1e90434cfb3</li><li>**LDM 데이터 파티션 (동적 디스크):** af9b60a0-1431-4f62-bc68-3311714a69ad</li><li>**복구 파티션:** de94bba4-06d1-4d40-a16a-bfd50179d6ac<p>Gpt 디스크에 대해이 매개 변수를 지정 하지 않으면 명령은 기본 데이터 파티션을 만듭니다.</li></ul> |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 디스크 크기는 오류 코드를 수행 합니다. |

## <a name="examples"></a>예

1000 메가바이트 주 파티션 크기에서를 만들려면 다음을 입력 합니다.

```
create partition primary size=1000
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [assign 명령](assign.md)

- [create 명령](create.md)

- [select disk](select-disk.md)
