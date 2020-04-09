---
title: 숨깁니다
description: 숨깁니다에 대 한 Windows 명령 항목으로, 노출 명령을 사용 하 여 노출 된 섀도 복사본을 노출 하지 않습니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 58dc7d0f-52e9-4587-9487-d3b4c3e52640
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f2f8bbdb3b810ffbf9332608a016fc3b3e188e9f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832356"
---
# <a name="unexpose"></a>숨깁니다

**공개 명령을 사용** 하 여 노출 된 섀도 복사본을 노출 하지 않습니다. 노출 된 섀도 복사본은 섀도 ID, 드라이브 문자, 공유 또는 탑재 지점으로 지정할 수 있습니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
unexpose {<ShadowID> | <Drive:> | <Share> | <MountPoint>}
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<ShadowID >|지정 된 섀도 ID로 지정 된 섀도 복사본을 노출 하지 않습니다.|
|\<드라이브: >|지정 된 드라이브 문자 (예: P 드라이브)와 연결 된 섀도 복사본을 노출 하지 않습니다.|
|\<공유 >|지정 된 공유와 연결 된 섀도 복사본을 공개 하지 않습니다 (예: \\\\*MachineName*\)).|
|\<탑재 지점 >|지정 된 탑재 지점과 연결 된 섀도 복사본을 노출 합니다 (예: C:\shadowcopy\)).|

## <a name="remarks"></a>주의

-   *ShadowID*대신 기존 별칭 또는 환경 변수를 사용할 수 있습니다. 사용 하 여 **추가** 매개 변수 없이 기존 별칭을 참조 하십시오.

## <a name="examples"></a><a name=BKMK_examples></a>예와

숨깁니다 드라이브와 연결 된 섀도 복사본을 복사 하려면 다음을 입력 합니다.
```
unexpose P:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)