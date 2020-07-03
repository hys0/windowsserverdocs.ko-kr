---
title: add volume
description: 섀도 복사본 집합에 볼륨을 추가 하는 볼륨 추가 명령에 대 한 참조 문서입니다. 섀도 복사본 집합은 섀도 복사 될 볼륨의 집합입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b7d4d35d-8bda-46d2-8df5-eb598cecaaba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3cd80a60fd3215a2234d4eb5be8a62da91e2cba4
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924085"
---
# <a name="add-volume"></a>add volume

볼륨의 섀도 복사본을 설정 하려면 되 섀도 복사 되는 볼륨의 집합에 추가 합니다. 섀도 복사본을 만들 때 다음 스크립트에 대 한 별칭을 사용할 수 있도록 환경 변수 별칭을 섀도 ID에 연결 합니다.

볼륨에는 한 번에 하나씩 추가 됩니다. 볼륨이 추가 될 때마다 VSS에서 해당 볼륨에 대 한 섀도 복사본 만들기를 지원 하는지 확인 합니다. 이 검사는 나중에 **set context** 명령을 사용 하 여 무효화 될 수 있습니다.

이 명령은 섀도 복사본을 만들 필요 합니다. 매개 변수 없이 사용 하는 경우 **볼륨 추가** 명령 프롬프트에서 도움말을 표시 합니다.

## <a name="syntax"></a>구문

```
add volume <volume> [provider <providerid>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<volume>` | 섀도 복사 설정에 추가할 볼륨을 지정 합니다. 하나 이상의 볼륨 섀도 복사본 만들기 필요 합니다. |
| `[provider \<providerid>]` | 섀도 복사본을 만드는 데 사용할 등록 된 공급자의 공급자 ID를 지정 합니다. 경우 **공급자** 를 지정 하지 않으면 기본 공급자가 사용 됩니다. |

## <a name="examples"></a>예

에 현재 등록 된 공급자 목록을 볼 수는 `diskshadow>` 프롬프트에 입력 합니다.

```
list providers
```

다음과 같은 출력에는 기본적으로 사용 되는 단일 공급자를 표시 합니다.

```
* ProviderID: {b5946137-7b9f-4925-af80-51abd60b20d5}
        Type: [1] VSS_PROV_SYSTEM
        Name: Microsoft Software Shadow Copy provider 1.0
        Version: 1.0.0.7
        CLSID: {65ee1dba-8ff4-4a58-ac1c-3470ee2f376a}
1 provider registered.
```

드라이브 C:를 섀도 복사본 집합에 추가 하 고 *System1*라는 별칭을 할당 하려면 다음을 입력 합니다.

```
add volume c: alias System1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [컨텍스트 명령 설정](set-context.md)
