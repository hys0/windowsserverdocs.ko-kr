---
title: 'ksetup: setrealm'
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: acdbfaabe341c8efb19c6e9d183022375f679de7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841316"
---
# <a name="ksetupsetrealm"></a>ksetup: setrealm



Kerberos 영역의 이름을 설정합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /setrealm <DNSDomainName>
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<DNSDomainName >|DNS 도메인 이름을 간단한 도메인 이름 또는 정규화 된 도메인 이름 형식일 수 있습니다.|

## <a name="remarks"></a>주의

DNS 도메인 이름 매개 변수가 대문자로 입력 해야 합니다. 그렇지 않은 경우는 **ksetup** 명령을 계속 하려면 확인을 묻는 메시지가 표시 됩니다.

도메인 컨트롤러에서 Kerberos 영역을 설정 하는 것은 지원 되지 않습니다. 그렇게 하려고 하면 경고 및 명령 실패 합니다.

## <a name="examples"></a><a name=BKMK_Examples></a>예와

비-도메인 컨트롤러에서 CONTOSO Kerberos 영역에만 액세스를 제한 하는 특정 도메인 이름에이 컴퓨터에 대 한 영역을 설정 합니다.
```
ksetup /setrealm CONTOSO
```

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)
-   [Ksetup:removerealm](ksetup-removerealm.md)