---
title: 'ksetup: setcomputerpassword'
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e65ea6e935d9fde9c23842755c36e418928dec7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841376"
---
# <a name="ksetupsetcomputerpassword"></a>ksetup: setcomputerpassword



로컬 컴퓨터에 대 한 암호를 설정합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /setcomputerpassword <Password>
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|암호 \<>|제공 된 암호를 사용 하 여 로컬 컴퓨터에서 컴퓨터 계정을 설정 합니다.</br>암호는 관리자 권한이 있는 계정을 사용 하 여 설정할 수만 있습니다. 암호는 1에서 156 영숫자 또는 특수 문자를 수 있습니다.|

## <a name="remarks"></a>주의

이 명령은 컴퓨터 계정에만 적용 됩니다.

암호 변경 내용 적용 하려면 컴퓨터를 다시 시작 해야 합니다.

컴퓨터 계정 암호는 표시 되지 않습니다 레지스트리에 출력으로는 **ksetup** 명령입니다.

## <a name="examples"></a><a name=BKMK_Examples></a>예와

$897 IPop에 IPops897에서 로컬 컴퓨터에서 컴퓨터 계정 암호를 변경!.
```
ksetup /setcomputerpassword IPop$897!
```

## <a name="additional-references"></a>추가 참조

-   [Ksetup](ksetup.md)
-   - [명령줄 구문 키](command-line-syntax-key.md)