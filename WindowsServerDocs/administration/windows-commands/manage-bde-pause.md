---
title: 관리 bde 일시 중지
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: efda0e08-b9ff-4e71-83d8-bb666b3032bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 03b4cc18bbf2c9288b99956fcc6f8a38b538a84f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821644"
---
# <a name="manage-bde-pause"></a>관리 bde: 일시 중지



BitLocker 암호화를 일시 중지 하거나 암호 해독 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
manage-bde -pause <Volume> [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<볼륨 >|드라이브 문자 뒤에 콜론, 볼륨 GUID 경로 또는 탑재 된 볼륨입니다.|
|-computername|다른 컴퓨터에서 BitLocker 보호를 수정 하려면 bde.exe 사용될지를 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다.|
|\<이름 >|BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.|
|-? 또는 /?|도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다.|
|-help 또는-h|명령 프롬프트에서 전체 도움말을 표시 합니다.|

## <a name="BKMK_Examples"></a>예제

다음 예제를 사용 하 여 **-일시 중지** C 드라이브에서 BitLocker 암호화를 일시 중지 명령
```
manage-bde –pause C:
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)