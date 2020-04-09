---
title: bitsadmin util 및 repairservice
description: Bitsadmin util 및 repairservice에 대 한 Windows 명령 항목으로, 다양 한 버전의 BITS 서비스에서 알려진 문제를 해결 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aaaa6edab22031dc53d266984bb669634e3bb362
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848896"
---
# <a name="bitsadmin-util-and-repairservice"></a>bitsadmin util 및 repairservice

BITS를 시작 하지 못하는 경우이 스위치를 사용 하 여 다양 한 비트 버전의 알려진 문제를 해결할 수 있습니다.

**Bitsadmin 1.5 및 이전 버전:**  지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /Util /RepairService [/Force]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|Force|선택적-삭제 한 서비스를 다시 만듭니다.|

## <a name="remarks"></a>주의

이 스위치는 잘못 된 서비스 구성 및 Windows 서비스 (예: LANManworkstation)에 대 한 종속성 및 네트워크 디렉터리와 관련 된 오류를 해결 합니다. 이 스위치는 해결 된 문제가 있는지 여부를 나타내는 출력을 생성 합니다.

> [!NOTE]
> BITS가 서비스를 다시 만드는 경우 지역화 된 시스템에서 서비스 설명 문자열을 영어로 설정할 수 있습니다.

> [!IMPORTANT]
> 이 명령은 Windows Vista에서 지원 되지 않습니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 비트 서비스 구성을 수정합니다.
```
C:\>bitsadmin /Util /RepairService
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)