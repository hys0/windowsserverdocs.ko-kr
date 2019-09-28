---
title: manage-bde autounlock
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 063528bf-d235-4b44-887a-52a7d983e01a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e6927c964a3f35c70fc3b9467cc2d16bbd973b17
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374145"
---
# <a name="manage-bde-autounlock"></a>manage-bde: autounlock



BitLocker로 보호 된 데이터 드라이브 자동 잠금 해제를 관리 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
manage-bde -autounlock [{-enable|-disable|-clearallkeys}] <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]

```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-사용 하도록 설정|데이터 드라이브 자동 잠금 해제 수 있습니다.|
|-사용 하지 않도록 설정|데이터 드라이브 자동 잠금 해제 하는 사용 하지 않도록 설정 합니다.|
|-clearallkeys|운영 체제 드라이브에 저장 된 모든 외부 키를 제거합니다.|
|\<Drive >|드라이브 문자를 뒤에 콜론을 나타냅니다.|
|-computername|다른 컴퓨터에서 BitLocker 보호를 수정 하려면 bde.exe 사용될지를 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다.|
|\<이름 >|BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.|
|-? 또는 /?|도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다.|
|-help 또는-h|명령 프롬프트에서 전체 도움말을 표시 합니다.|

## <a name="BKMK_Examples"></a>예와

다음 예제를 사용 하는 **-자동 잠금 해제** 데이터 드라이브 E에 대 한 자동 잠금 해제를 사용 하도록 설정 하는 명령
```
manage-bde –autounlock -enable E:
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)