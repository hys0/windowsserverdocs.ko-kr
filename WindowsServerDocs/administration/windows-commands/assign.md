---
title: assign
description: 드라이브 문자 또는 탑재 지점을 포커스가 있는 볼륨에 할당 하는 assign 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 57912b73-622e-489b-b053-a369021ba8e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f17c22a0052ade6f16e7842813a04c95e76b57ab
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718983"
---
# <a name="assign"></a>assign

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포커스가 있는 볼륨 드라이브 문자 또는 탑재 지점을 지정합니다. 이 명령을 사용 하 여 이동식 드라이브에 연결 된 드라이브 문자를 변경할 수도 있습니다. 드라이브 문자 또는 탑재 지점을 지정 하지 않으면, 다음 사용 가능한 드라이브 문자가 할당 됩니다. 드라이브 문자 또는 탑재 지점을 사용 하 여에 이미 있으면 오류가 생성 됩니다.

이 작업을 수행 하려면 볼륨을 선택 해야 합니다. 사용 하 여는 **볼륨 선택** 볼륨을 선택 하 고 포커스를 이동 하는 명령입니다.

> [!IMPORTANT]
> 시스템 볼륨, 부팅 볼륨 또는 페이징 파일이 포함 된 볼륨에 드라이브 문자를 할당할 수 없습니다. 또한 OEM (원본 장비 제조업체) 파티션이나 기본 데이터 파티션이 아닌 gpt (GUID 파티션 테이블) 파티션에 드라이브 문자를 할당할 수 없습니다.

## <a name="syntax"></a>구문

```
assign [{letter=<d> | mount=<path>}] [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `letter=<d>` | 볼륨에 할당 하려는 드라이브 문자입니다. |
| `mount=<path>` | 볼륨에 할당 하려면 탑재 지점 경로입니다. 이 명령을 사용 하는 방법에 대 한 지침은 [탑재 지점 폴더 경로를 드라이브에 할당](https://docs.microsoft.com/windows-server/storage/disk-management/assign-a-mount-point-folder-path-to-a-drive)을 참조 하세요. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="examples"></a>예

E 포커스 볼륨에 할당 하려면 다음을 입력 합니다.

```
assign letter=e
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [볼륨 선택 명령](select-volume.md)