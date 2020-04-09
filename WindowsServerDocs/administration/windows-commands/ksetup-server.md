---
title: 'ksetup: 서버'
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7889e1a03d3c0eec1958bf1d6356c67e9371a80f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841446"
---
# <a name="ksetupserver"></a>ksetup: 서버



사용 하 여 변경 내용이 적용 되도록 Windows 운영 체제를 실행 하는 컴퓨터에 대 한 이름을 지정할 수 있습니다 **ksetup** 대상 컴퓨터를 업데이트 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /server <ServerName>
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<ServerName >|있는 구성은 효과적으로 IPops897.corp.contoso.com 같은 수의 전체 컴퓨터 이름입니다.</br>불완전 한 정규화 된 도메인 컴퓨터 이름이 지정 된 경우 명령이 실패 합니다.|

## <a name="remarks"></a>주의

대상된 서버 이름을; 제거할 수 없으므로 만 기본값 로컬 컴퓨터 이름으로 다시 변경할 수 있습니다.

레지스트리에 저장 된 대상 서버 이름 **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\LSA\Kerberos**합니다. 사용 하 여 보고 되지 않습니다 **ksetup**합니다.

## <a name="examples"></a><a name=BKMK_Examples></a>예와

확인 프로그램 **ksetup** 구성을 Contoso 도메인에 연결 되어 있는 IPops897 컴퓨터에 적용 합니다.
```
ksetup /server IPops897.corp.contoso.com
```

## <a name="additional-references"></a>추가 참조

-   [Ksetup](ksetup.md)
-   - [명령줄 구문 키](command-line-syntax-key.md)