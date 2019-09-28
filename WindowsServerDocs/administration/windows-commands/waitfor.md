---
title: waitfor
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a48ef70d-4d28-4035-b6b0-7d7b46ac2157
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aecea0ad19ee42e61396eb8b8ccd579b9ce2057b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362605"
---
# <a name="waitfor"></a>waitfor



보내거나 시스템에 신호를 기다립니다. **Waitfor** 네트워크를 통해 컴퓨터를 동기화 하는 데 사용 됩니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
waitfor [/s <Computer> [/u [<Domain>\]<User> [/p [<Password>]]]] /si <SignalName>
waitfor [/t <Timeout>] <SignalName>
```

## <a name="parameters"></a>매개 변수

|       매개 변수       |                                                                                         설명                                                                                          |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s \<Computer >     | 이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다. 이 매개 변수는 모든 파일 및 명령에 지정 된 폴더에 적용 됩니다. |
| /u [\<Domain > \] @ no__t-2 |                              지정한 사용자 계정의 자격 증명을 사용 하 여 스크립트를 실행 합니다. 기본적으로 **waitfor** 현재 사용자의 자격 증명을 사용 합니다.                               |
|   /p [\<Password >]    |                                                    에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                     |
|          /si          |                                                                        네트워크를 통해 지정된 된 신호를 보냅니다.                                                                        |
|     /t \<Timeout >     |                                              신호를 기다릴 시간 (초) 수를 지정 합니다. 기본적으로 **waitfor** 무기한 대기 합니다.                                               |
|     @no__t 0SignalName >     |                                                신호를 지정 하는 **waitfor** 보내거나 될 때까지 대기 합니다. *SignalName* 는 대 소문자를 구분 하지 않습니다.                                                 |
|          /?           |                                                                             명령 프롬프트에 도움말을 표시합니다.                                                                             |

## <a name="remarks"></a>설명

-   신호 이름은 225 자의 초과할 수 없습니다. 사용할 수 있는 문자에는 a-z, A-Z, 0-9 및 확장 문자 집합 (128-255) ASCII 포함 됩니다.
-   사용 하지 않는 경우 **/s**, 신호는 도메인의 모든 시스템에 브로드캐스트 됩니다. 사용 하는 경우 **/s**, 신호는 지정된 된 시스템에만 전송 됩니다.
-   여러 인스턴스를 실행할 수 있습니다 **waitfor** 의 각 인스턴스는 단일 컴퓨터에서 **waitfor** 서로 다른 신호를 기다려야 합니다. 인스턴스 하나만 **waitfor** 주어진된 신호에 대 한 지정된 된 컴퓨터에서까지 대기할 수 있습니다.
-   사용 하 여 신호를 수동으로 활성화할 수는 **/si** 명령줄 옵션입니다.
-   **Waitfor** 에 Windows XP 및 Windows Server 2003 운영 체제를 실행 하는 서버에만 실행 되지만 Windows 운영 체제를 실행 하는 모든 컴퓨터에 신호를 보낼 수 있습니다.
-   만 컴퓨터 신호를 보내는 컴퓨터와 동일한 도메인에 있는 경우 신호를 받을 수 있습니다.
-   사용할 수 있습니다 **waitfor** 소프트웨어 빌드를 테스트할 수 있습니다. 예를 들어 컴파일 컴퓨터 신호를 실행 하는 여러 컴퓨터에 보낼 수 **waitfor** 는 컴파일 성공적으로 완료 된 후입니다. 에 신호를 받으면, 배치 파일은 포함 된 **waitfor** 즉시 소프트웨어를 설치 하거나 컴파일된 빌드에서 테스트 실행을 시작 하는 컴퓨터에 지시할 수 있습니다.

## <a name="BKMK_examples"></a>예와

"Espresso\build007" 신호가 수신 될 때까지 기다려야 다음을 입력 합니다.
```
waitfor espresso\build007
```
기본적으로 **waitfor** 신호를 기다립니다.

10 초 동안 시간이 초과 되기 전에 수신 되도록 "espresso\compile007" 신호를 기다려야 다음을 입력 합니다.
```
waitfor /t 10 espresso\build007
```
"Espresso\build007" 신호를 수동으로 활성화 하려면 다음을 입력 합니다.
```
waitfor /si espresso\build007
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)