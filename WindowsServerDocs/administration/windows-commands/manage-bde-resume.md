---
title: manage-bde resume
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ca3cd1ca-6f2c-4190-b68f-27816635facb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4559cfb429a4ad36feda94fcfcc1adc965562512
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820623"
---
# <a name="manage-bde-resume"></a>manage-bde: resume



일시 중지 된 후 BitLocker 암호화 또는 해독 다시 시작 합니다.

## <a name="syntax"></a>구문

```
manage-bde -resume [<Drive>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<드라이브>|드라이브 문자를 뒤에 콜론을 나타냅니다.|
|-computername|다른 컴퓨터에서 BitLocker 보호를 수정 하려면 bde.exe 사용될지를 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다.|
|\<Name>|BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.|
|-? 또는 /?|도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다.|
|-help 또는-h|명령 프롬프트에서 전체 도움말을 표시 합니다.|

## <a name="examples"></a>예

**-다시 시작** 명령을 사용 하 여 C 드라이브에서 BitLocker 암호화를 다시 시작 하는 방법을 설명 합니다.
```
manage-bde –resume C:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)