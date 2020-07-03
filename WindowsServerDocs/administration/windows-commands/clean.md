---
title: clean
description: 포커스가 있는 디스크에서 모든 파티션 또는 볼륨 형식을 제거 하는 Diskpart 정리 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a30e1f765959ed60efa662301f95defc21d6587
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929901"
---
# <a name="clean"></a>clean

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포커스가 있는 디스크에서 모든 파티션 또는 볼륨 형식을 제거 합니다.

>[!NOTE]
> 이 명령의 PowerShell 버전은 [clear-disk 명령을](https://docs.microsoft.com/powershell/module/storage/clear-disk)참조 하세요.

## <a name="syntax"></a>구문

```
clean [all]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 모두 | 각 섹터 디스크에서 디스크에 포함 된 모든 데이터를 완전히 삭제를 0으로 설정 되어 있는지를 지정 합니다. |

#### <a name="remarks"></a>설명

- MBR (마스터 부트 레코드) 디스크에는 MBR 분할 정보 및 숨겨진 섹터 정보만 덮어쓰여집니다.

- Gpt (GUID 파티션 테이블) 디스크에서 보호 MBR을 비롯 한 gpt 분할 정보를 덮어씁니다. 숨겨진된 섹터 정보가 없는 합니다.

- 이 작업을 수행 하려면 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="examples"></a>예

선택된 된 디스크에서 모든 서식을 제거 하려면 다음을 입력 합니다.

```
clean
```

## <a name="additional-references"></a>추가 참조

- [clear-disk 명령](https://docs.microsoft.com/powershell/module/storage/clear-disk)

- [명령줄 구문 키](command-line-syntax-key.md)
