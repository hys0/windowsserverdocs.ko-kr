---
title: subst
description: 드라이브 문자를 사용 하 여 경로 연결 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3e69234c-2312-4343-868b-afc1017c622a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 858195de89ca8661cf47c25b6cf9b519cc4efbf8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858074"
---
# <a name="subst"></a>subst



드라이브 문자를 경로 연결합니다. 매개 변수 없이 사용 하는 경우 **subst** 적용 가상 드라이브의 이름을 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
subst [<Drive1>: [<Drive2>:]<Path>] 
subst <Drive1>: /d
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<Drive1>:|경로 할당할 가상 드라이브를 지정 합니다.|
|[\<Drive2>:]\<Path>|실제 드라이브와 가상 드라이브에 할당 하 고 원하는 경로 지정 합니다.|
|/d|대체 된 가상 드라이브를 삭제합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   다음 명령은 작동 하지 않습니다 하 고에 지정 된 드라이브에서 사용할 수 없습니다는 **subst** 명령:

    **chkdsk**

    **diskcomp**

    **diskcopy**

    **format**

    **label**

    **recover**
-   *Drive1* 매개 변수로 지정 된 범위 내에 있어야 합니다.는 **lastdrive** 명령입니다. 그렇지 않으면 **subst** 다음과 같은 오류 메시지가 표시 됩니다.

    `Invalid parameter - drive1:`

## <a name="BKMK_examples"></a>예제

B:\User\Betty\Forms 경로 대 한 가상 드라이브 Z를 만들려면 다음을 입력 합니다.
```
subst z: b:\user\betty\forms 
```
전체 경로 입력 하는 대신 다음과 같이 뒤에 콜론 가상 드라이브의 문자를 입력 하 여이 디렉터리를 도달할 수 있습니다.
```
z: 
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)