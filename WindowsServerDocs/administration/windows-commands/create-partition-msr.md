---
title: create partition msr
description: Gpt (GUID 파티션 테이블) 디스크에 MSR (Microsoft 예약) 파티션을 만드는 create partition msr에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 04fba033-23cb-4521-bd5d-db96131f2e73
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2714c47c467fda9c6ca3451331ab9bc7991d4591
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929646"
---
# <a name="create-partition-msr"></a>create partition msr

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Gpt (GUID 파티션 테이블) 디스크에 Microsoft 예약 (MSR) 파티션을 만듭니다. Microsoft Reserved partition은 모든 gpt 디스크에 필요 합니다. 이 파티션의 크기는 gpt 디스크의 전체 크기에 따라 달라 집니다. Microsoft 예약 파티션을 만들려면 gpt 디스크의 크기가 32 이상 이어야 합니다.

> [!IMPORTANT]
> 이 명령을 사용할 때는 매우 주의 해야 합니다. Gpt 디스크에는 특정 파티션 레이아웃이 필요 하므로 Microsoft 예약 파티션을 만들면 디스크를 읽을 수 없게 될 수 있습니다.
>
> 이 작업을 수행 하려면 기본 gpt 디스크를 선택 해야 합니다. 기본 gpt 디스크를 선택 하 고 포커스를 이동 하려면 [디스크 선택](select-disk.md) 명령을 사용 해야 합니다.

## <a name="syntax"></a>구문

```
create partition msr [size=<n>] [offset=<n>] [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 크기 =`<n>` | 파티션의 크기 (mb)입니다. 파티션을 사용 하는 바이트에서 길이가에 지정한 수 만큼 `<n>`합니다. 크기를 지정 하는 경우에 현재 지역에서 사용 가능한 공간이 더 이상 없는 파티션을 계속 합니다. |
| offset =`<n>` | 파티션이 생성 되는 오프셋 (KB)을 지정 합니다. 오프셋 반올림을 완전히 사용 되는 모든 섹터 크기를 채웁니다. 오프셋이, 파티션은 저장 하는 데 충분히 큰 첫 번째 디스크에에서 배치 됩니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

#### <a name="remarks"></a>설명

- Windows 운영 체제를 부팅 하는 데 사용 되는 gpt 디스크에서 EFI (Extensible 펌웨어 인터페이스) 시스템 파티션은 디스크의 첫 번째 파티션과 Microsoft Reserved partition입니다. 데이터 저장소에만 사용 되는 gpt 디스크는 EFI 시스템 파티션을 포함 하지 않습니다 .이 경우 Microsoft Reserved partition은 첫 번째 파티션입니다.

- Windows에서 Microsoft 예약 파티션을 탑재 하지 않습니다. 에 데이터를 저장할 수 없습니다 하 고 삭제할 수는 없습니다.

## <a name="examples"></a>예

1000 메가바이트 Microsoft 예약 파티션 크기에서를 만들려면 다음을 입력 합니다.

```
create partition msr size=1000
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [create 명령](create.md)

- [select disk](select-disk.md)
