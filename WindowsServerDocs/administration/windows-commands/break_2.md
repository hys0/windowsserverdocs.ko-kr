---
title: break
description: Windows 명령 항목에 대 한 **break_2** -VSS에서 섀도 복사본 볼륨을 분리 하 고 일반 볼륨으로 액세스할 수 있도록 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de2b6c95-1c2e-4a43-bec5-341a9014371b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 49516539ae603e2c93b3fc395c77786be790d663
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886334"
---
# <a name="break"></a>break



VSS에서 섀도 복사본 볼륨을 분리 하 고 일반 볼륨으로 액세스할 수 있도록 합니다. 볼륨은 드라이브 문자 (할당) 하는 경우 또는 볼륨 이름을 사용 하 여 액세스할 수 있습니다. 매개 변수 없이 사용 하는 경우 **나누기** 명령 프롬프트에서 도움말을 표시 합니다.

> [!NOTE]
> 이 명령은 가져온 후 하드웨어 섀도 복사본에만 해당 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
break [writable] <SetID>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[쓰기]|사용 하도록 설정 읽기/쓰기 볼륨에 액세스 합니다.|
|\<SetID>|섀도 복사본 집합의 ID를 지정 합니다.|

## <a name="remarks"></a>설명

-   섀도 복사본에서 발생 한 것 처럼 노출 된 볼륨은 기본적으로 읽기 전용입니다.
-   하 여 환경 변수로 저장 되어 있는 섀도 복사본 ID의 별칭은 **메타 데이터를 로드** 명령에서 사용할 수는 *SetID* 매개 변수.

## <a name="BKMK_examples"></a>예제

그림자 Alias1 운영 체제에서 쓰기 가능한 볼륨으로 액세스할 수 있는 별칭 이름으로 복사 하려면 다음을 입력 합니다.
```
break writable %Alias1%
```

> [!NOTE]
> 볼륨에 대 한 액세스 된 섀도 복사본 볼륨의 레코드가 없는 하드웨어 공급자에 게 직접 이루어집니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)