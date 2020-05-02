---
title: break
description: VSS에서 섀도 복사본 볼륨을 분리 하 고 일반 볼륨으로 액세스할 수 있게 하는 break 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: de2b6c95-1c2e-4a43-bec5-341a9014371b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7e8789ab68ecb98d190a79c3f1088aad05b83562
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707778"
---
# <a name="break"></a>break

VSS에서 섀도 복사본 볼륨을 분리 하 고 일반 볼륨으로 액세스할 수 있도록 합니다. 그런 다음 드라이브 문자 (할당 된 경우) 또는 볼륨 이름을 사용 하 여 볼륨에 액세스할 수 있습니다. 매개 변수 없이 사용 하는 경우 **나누기** 명령 프롬프트에서 도움말을 표시 합니다.

> [!NOTE]
> 이 명령은 가져온 후 하드웨어 섀도 복사본에만 해당 합니다.
>
> 표시 되는 섀도 복사본 처럼 표시 되는 볼륨은 기본적으로 읽기 전용입니다. 볼륨에 대 한 액세스 된 섀도 복사본 볼륨의 레코드가 없는 하드웨어 공급자에 게 직접 이루어집니다.

## <a name="syntax"></a>구문

```
break [writable] <setid>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 가능 | 볼륨에 대 한 읽기/쓰기 액세스를 사용 하도록 설정 합니다. |
| \<setid> | 섀도 복사본 집합의 ID를 지정 합니다. 하 여 환경 변수로 저장 되어 있는 섀도 복사본 ID의 별칭은 **메타 데이터를 로드** 명령에서 사용할 수는 *SetID* 매개 변수. |

## <a name="examples"></a>예

운영 체제에서 쓰기 가능한 볼륨으로 액세스할 수 있는 Alias1 별칭을 사용 하 여 섀도 복사본을 만들려면 다음을 수행 합니다.

```
break writable %Alias1%
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)