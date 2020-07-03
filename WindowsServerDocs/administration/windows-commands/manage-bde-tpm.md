---
title: manage-bde tpm 관리
description: 컴퓨터의 TPM (신뢰할 수 있는 플랫폼 모듈)을 구성 하는 manage-bde tpm 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bed203c5de5351162f4c465e43631a4869f0e9a1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922195"
---
# <a name="manage-bde-tpm"></a>manage-bde tpm 관리

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

컴퓨터의 신뢰할 수 있는 플랫폼 모듈 (TPM)를 구성합니다.

## <a name="syntax"></a>구문

```
manage-bde -tpm [-turnon] [-takeownership <ownerpassword>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -켬 | 사용 하 고 TPM 소유자 암호를 설정 해야 TPM을 활성화 합니다. 사용할 수도 있습니다 **-t** 이 명령의 축약된 버전으로 합니다. |
| -takeownership | 소유자 암호를 설정 하 여 TPM의 소유권을 갖습니다. 사용할 수도 있습니다 **-o** 이 명령의 축약된 버전으로 합니다. |
| `<ownerpassword>` | TPM에 대해 지정 하는 소유자 암호를 나타냅니다. |
| -computername | 다른 컴퓨터에서 BitLocker 보호를 수정 하는 데 manage-bde.exe를 사용 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다. |
| `<name>` | BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다. |
| -? 또는 /? | 도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다. |
| -help 또는-h | 명령 프롬프트에서 전체 도움말을 표시 합니다. |

### <a name="examples"></a>예

TPM을 켜려면 다음을 입력 합니다.

```
manage-bde  tpm -turnon
```

TPM의 소유권을 가져오고 소유자 암호를로 설정 하려면 *0wnerP@ss* 다음을 입력 합니다.

```
manage-bde  tpm  takeownership 0wnerP@ss
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [Windows PowerShell 용 TPM 관리 cmdlet](https://docs.microsoft.com/powershell/module/trustedplatformmodule/)

- [manage-bde 명령](manage-bde.md)
