---
title: 숨깁니다
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58dc7d0f-52e9-4587-9487-d3b4c3e52640
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fe9cb5dfd8ae6c71fdc72ddc1e8421229f98f5d0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837474"
---
# <a name="unexpose"></a>숨깁니다



사용 하 여 노출 된 섀도 복사본 unexposes 합니다 **노출** 명령입니다. 섀도 ID, 드라이브 문자, 공유 또는 탑재 지점에서 노출 된 섀도 복사본을 지정할 수 있습니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
unexpose {<ShadowID> | <Drive:> | <Share> | <MountPoint>}
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<ShadowID>|지정된 된 섀도 ID로 지정 된 섀도 복사본 unexposes|
|\<드라이브: >|지정한 드라이브 문자 (예를 들어 드라이브 P)를 사용 하 여 연결 된 섀도 복사본을 unexposes입니다.|
|\<Share>|지정 된 공유와 연결 된 섀도 복사본 unexposes (예를 들어 \\ \\ *MachineName*\)합니다.|
|\<MountPoint>|지정한 탑재 지점과 연결 된 섀도 복사본 unexposes (예를 들어 C:\shadowcopy\)합니다.|

## <a name="remarks"></a>설명

-   기존 별칭 또는 환경 변수 대신 사용할 수 있습니다 *ShadowID*합니다. 사용 하 여 **추가** 매개 변수 없이 기존 별칭을 참조 하십시오.

## <a name="BKMK_examples"></a>예제

P 드라이브와 연결 된 섀도 복사본을 숨깁니다, 다음을 입력 합니다.
```
unexpose P:
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)