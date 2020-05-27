---
title: manage-bde setidentifier
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7092d18f-4ac9-4c73-a20f-1246ca60e75e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f3e0b553c324099ed3f80c158a5f14d9a31e4d54
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820613"
---
# <a name="manage-bde-setidentifier"></a>manage-bde: setidentifier



드라이브 식별자 필드에 지정 된 값을 드라이브에 설정 된 **조직에 대 한 고유 식별자를 제공** 그룹 정책 설정.

## <a name="syntax"></a>구문

```
manage-bde –setidentifier <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]
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

**-Setidentifier** 명령을 사용 하 여 C의 BitLocker 드라이브 식별자 필드를 설정 하는 방법을 보여 줍니다.
```
manage-bde –setidentifier C:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)
-   [BitLocker와 함께 데이터 복구 에이전트를 사용합니다.](https://technet.microsoft.com/library/dd875560(WS.10).aspx)