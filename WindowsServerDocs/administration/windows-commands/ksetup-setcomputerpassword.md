---
title: 'ksetup: setcomputerpassword'
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1d3742476385eb770c9cb5c798c1f6ab27c74f8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374936"
---
# <a name="ksetupsetcomputerpassword"></a>ksetup: setcomputerpassword



로컬 컴퓨터에 대 한 암호를 설정합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /setcomputerpassword <Password>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<Password >|제공 된 암호를 사용 하 여 로컬 컴퓨터에서 컴퓨터 계정을 설정 합니다.</br>암호는 관리자 권한이 있는 계정을 사용 하 여 설정할 수만 있습니다. 암호는 1에서 156 영숫자 또는 특수 문자를 수 있습니다.|

## <a name="remarks"></a>설명

이 명령은 컴퓨터 계정에만 적용 됩니다.

암호 변경 내용 적용 하려면 컴퓨터를 다시 시작 해야 합니다.

컴퓨터 계정 암호는 표시 되지 않습니다 레지스트리에 출력으로는 **ksetup** 명령입니다.

## <a name="BKMK_Examples"></a>예와

$897 IPop에 IPops897에서 로컬 컴퓨터에서 컴퓨터 계정 암호를 변경!.
```
ksetup /setcomputerpassword IPop$897!
```

#### <a name="additional-references"></a>추가 참조

-   [Ksetup](ksetup.md)
-   [명령줄 구문 키](command-line-syntax-key.md)