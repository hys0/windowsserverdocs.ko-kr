---
title: manage-bde KeyPackage
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c631ef10-2a2f-4541-8578-292f2d4e9e80
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3a53edd060cb8c7a7a52e86130b2136893a42150
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840106"
---
# <a name="manage-bde-keypackage"></a>manage-bde: KeyPackage



드라이브에 대 한 키 패키지를 생성합니다. 키 패키지를 손상 된 드라이브를 복구 하려면 복구 도구와 함께에서 사용할 수 있습니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
manage-bde -KeyPackage [<Drive>] [-ID <KeyProtectoryID>] [-path <PathToExternalKeyDirectory>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<드라이브 >|드라이브 문자를 뒤에 콜론을 나타냅니다.|
|-ID|이 ID 값으로 지정 된 식별자와 키 보호기를 사용 하 여 키 패키지를 만듭니다.|
|-경로|만든 키 패키지를 저장 하는 위치입니다.|
|-computername|다른 컴퓨터에서 BitLocker 보호를 수정 하려면 bde.exe 사용될지를 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다.|
|\<이름 >|BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.|
|-? 또는 /?|도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다.|
|-help 또는-h|명령 프롬프트에서 전체 도움말을 표시 합니다.|

## <a name="examples"></a><a name=BKMK_Examples></a>예와

다음 예제를 사용 하는 **-KeyPackage** GUID로 식별 되는 키 보호기 기반으로 C 드라이브에 대 한 키 패키지를 만들고 F:\Folder에 키 패키지를 저장 하는 명령입니다.
```
manage-bde -KeyPackage C: -id {84E151C1...7A62067A512} -path f:\Folder
```

> [!TIP]
> 사용 하 여 **관리 bde – 보호기 – 가져오기** 함께 패키지를 만드는 키에 대 한 ID 값으로 사용 하 여 사용할 수 있는 Guid의 목록을 가져오려면 원하는 드라이브 문자입니다.

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)