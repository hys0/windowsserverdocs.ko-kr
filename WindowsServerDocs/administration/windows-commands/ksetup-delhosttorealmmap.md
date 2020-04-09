---
title: 'ksetup: delhosttorealmmap'
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3faee482-a96c-4614-86fd-aaa446643ec4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 85e9f6b4a9f1c9050ed843f3837a2bd87aaf6eae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841736"
---
# <a name="ksetupdelhosttorealmmap"></a>ksetup: delhosttorealmmap



명시 된 호스트와 영역 간의 SPN (서비스 사용자 이름) 매핑을 제거 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /delhosttorealmmap <HostName> <RealmName>
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<호스트 이름 >|호스트 이름은 컴퓨터 이름이 며 컴퓨터의 정규화 된 도메인 이름으로 지정할 수 있습니다.|
|\<RealmName >|영역 이름은 CORP. 같은 대문자는 DNS 이름으로 명시 CONTOSO.COM입니다.|

## <a name="remarks"></a>주의

영역에 대 한 호스트 (또는 영역에 대 한 여러 호스트) 매핑이 있는 경우이 명령은 해당 매핑을 제거 합니다.

매핑은 **HKEY_LOCAL_MACHINE \system\currentcontolset\lsa\kerberos\hosttorealm**의 레지스트리에 기록 됩니다. 이 명령을 사용한 후 레지스트리에서 매핑을 확인 해야 합니다.

## <a name="examples"></a><a name=BKMK_Examples></a>예와

영역 CONTOSO의 구성을 변경 하 여 호스트 컴퓨터 IPops897의 매핑을 영역으로 삭제 합니다.
```
ksetup /delhosttorealmmap IPops897 CONTOSO
```
이 명령을 실행 한 후 레지스트리에서 매핑을 확인할 수 있습니다.

## <a name="additional-references"></a>추가 참조

-   [Ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   - [명령줄 구문 키](command-line-syntax-key.md)