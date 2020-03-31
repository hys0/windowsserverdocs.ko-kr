---
title: manage-bde 변환
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69463db9-7e03-47ff-b233-a95d5055725f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0fc273bc84e0bc25a7409941af6dca02b6042640
ms.sourcegitcommit: 479ad84a0d6c7c7b8308122b8bac8308cb36fe9b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80391701"
---
# <a name="manage-bde-changekey"></a>manage-bde: 변환



운영 체제 드라이브에 대 한 시작 키를 수정합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
manage-bde -changekey [<Drive>] [<PathToExternalKeyDirectory>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<드라이브 >|드라이브 문자를 뒤에 콜론을 나타냅니다.|
|\<PathToExternalKeyDirectory >|드라이브를 잠금 해제를 사용할 수 있는 외부 시작 키 파일을 저장할 디렉터리 위치를 나타냅니다.|
|-computername|다른 컴퓨터에서 BitLocker 보호를 수정 하려면 bde.exe 사용될지를 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다.|
|\<이름 >|BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.|
|-? 또는 /?|도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다.|
|-help 또는-h|명령 프롬프트에서 전체 도움말을 표시 합니다.|

## <a name="examples"></a><a name="BKMK_Examples"></a>예와

다음 예제를 사용 하 여 **-변환** C 드라이브에서 BitLocker 암호화를 사용 하 여 E 드라이브에 시작 키를 새로 만드는 명령을
```
manage-bde -changekey C: E:\
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)
