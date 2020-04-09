---
title: break
description: VSS에서 섀도 복사본 볼륨을 분리 하 고 일반 볼륨으로 액세스할 수 있게 하는 break_2에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: de2b6c95-1c2e-4a43-bec5-341a9014371b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6683c44c84f4baae5f016f7df62d5bd6591cff70
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848256"
---
# <a name="break"></a>break

VSS에서 섀도 복사본 볼륨을 분리 하 고 일반 볼륨으로 액세스할 수 있도록 합니다. 그런 다음 드라이브 문자 (할당 된 경우) 또는 볼륨 이름을 사용 하 여 볼륨에 액세스할 수 있습니다. 매개 변수 없이 사용 하는 경우 **나누기** 명령 프롬프트에서 도움말을 표시 합니다.

> [!NOTE]
> 이 명령은 가져온 후 하드웨어 섀도 복사본에만 해당 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
break [writable] <SetID>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|가능|볼륨에 대 한 읽기/쓰기 액세스를 사용 하도록 설정 합니다.|
|\<SetID >|섀도 복사본 집합의 ID를 지정 합니다.|

## <a name="remarks"></a>주의

-   표시 되는 섀도 복사본 처럼 표시 되는 볼륨은 기본적으로 읽기 전용입니다.
-   하 여 환경 변수로 저장 되어 있는 섀도 복사본 ID의 별칭은 **메타 데이터를 로드** 명령에서 사용할 수는 *SetID* 매개 변수.

## <a name="examples"></a><a name=BKMK_examples></a>예와

그림자 Alias1 운영 체제에서 쓰기 가능한 볼륨으로 액세스할 수 있는 별칭 이름으로 복사 하려면 다음을 입력 합니다.
```
break writable %Alias1%
```

> [!NOTE]
> 볼륨에 대 한 액세스 된 섀도 복사본 볼륨의 레코드가 없는 하드웨어 공급자에 게 직접 이루어집니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)