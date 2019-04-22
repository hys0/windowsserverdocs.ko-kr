---
title: 관리 bde 다시 시작
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca3cd1ca-6f2c-4190-b68f-27816635facb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8b4f655cf6e37df7397c45f1214fa8799776a758
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823134"
---
# <a name="manage-bde-resume"></a>관리 bde: 다시 시작



일시 중지 된 후 BitLocker 암호화 또는 해독 다시 시작 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
manage-bde -resume [<Drive>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<Drive>|드라이브 문자를 뒤에 콜론을 나타냅니다.|
|-computername|다른 컴퓨터에서 BitLocker 보호를 수정 하려면 bde.exe 사용될지를 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다.|
|\<이름 >|BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.|
|-? 또는 /?|도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다.|
|-help 또는-h|명령 프롬프트에서 전체 도움말을 표시 합니다.|

## <a name="BKMK_Examples"></a>예제

다음 예제를 사용 하는 **-다시 시작** C 드라이브에서 BitLocker 암호화를 다시 시작 하는 명령
```
manage-bde –resume C:
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)