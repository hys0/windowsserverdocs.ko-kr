---
title: 볼륨 추가
description: '**볼륨 추가**에 대 한 Windows 명령 항목. 섀도 복사본 집합에 볼륨을 추가 합니다. 섀도 복사본 집합은 섀도 복사 될 볼륨의 집합입니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b7d4d35d-8bda-46d2-8df5-eb598cecaaba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 806ab273dbb63eb7341520f56a07691fe3fac214
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851356"
---
# <a name="add-volume"></a>볼륨 추가

볼륨의 섀도 복사본을 설정 하려면 되 섀도 복사 되는 볼륨의 집합에 추가 합니다. 이 명령은 섀도 복사본을 만들 필요 합니다. 매개 변수 없이 사용 하는 경우 **볼륨 추가** 명령 프롬프트에서 도움말을 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
add volume <Volume> [provider <ProviderID>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
| `<Volume>` | 섀도 복사 설정에 추가할 볼륨을 지정 합니다. 하나 이상의 볼륨 섀도 복사본 만들기 필요 합니다.|
| `[provider \<ProviderID>]` | 섀도 복사본 만들기를 사용 하 여 등록 된 공급자의 공급자 ID를 지정 합니다. 경우 **공급자** 를 지정 하지 않으면 기본 공급자가 사용 됩니다.|

## <a name="remarks"></a>주의

-   볼륨에는 한 번에 하나씩 추가 됩니다.

-   볼륨 추가 될 때마다 VSS에 해당 볼륨의 섀도 복사본 만들기를 지원 하는지 확인 하십시오 확인 됩니다. 그러나이 기본 검사 수에서 무효화 될,의 나중에 사용 된 **컨텍스트 설정** 명령입니다.

-   섀도 복사본을 만들 때 다음 스크립트에 대 한 별칭을 사용할 수 있도록 환경 변수 별칭을 섀도 ID에 연결 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

에 현재 등록 된 공급자 목록을 볼 수는 `DISKSHADOW>` 프롬프트에 입력 합니다.

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

섀도 복사본 집합 C 드라이브 추가 라는 별칭 system1 파티션이나 하를 지정 하려면 다음을 입력 합니다.

```
add volume c: alias System1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)