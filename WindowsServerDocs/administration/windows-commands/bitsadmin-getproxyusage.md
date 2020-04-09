---
title: bitsadmin getproxyusage
description: 지정 된 작업에 대 한 프록시 사용 설정을 검색 하는 **bitsadmin getproxyusage**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 01c9bb9a1d413fa847482f652e18eed30ad76109
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850516"
---
# <a name="bitsadmin-getproxyusage"></a>bitsadmin getproxyusage

지정된 된 작업에 대 한 프록시 사용 설정을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getproxyusage <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="remarks"></a>주의

프록시 사용 값은 다음과 같습니다.

- **사전 구성** -소유자의 Internet Explorer 기본값을 사용 합니다.

- **No_Proxy** -프록시 서버를 사용 하지 않습니다.

- **Override** -명시적 프록시 목록을 사용 합니다.

- 자동 **검색-프록시 설정을 자동으로 검색** 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 프록시 사용을 검색 *myDownloadJob*합니다.

```
C:\>bitsadmin /getproxyusage myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)