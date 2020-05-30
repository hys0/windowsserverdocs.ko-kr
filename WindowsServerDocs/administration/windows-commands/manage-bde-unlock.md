---
title: manage-bde 잠금 해제
description: 복구 암호나 복구 키를 사용 하 여 BitLocker로 보호 된 드라이브의 잠금을 해제 하는 manage-bde unlock 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7852bf7d-9102-40be-adcb-71e8f4dfde72
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 67d4c0ec78870af45f0b98f2ab04d85b19e92af9
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222151"
---
# <a name="manage-bde-unlock"></a>manage-bde 잠금 해제

복구 암호 또는 복구 키를 사용 하 여 BitLocker 보호 드라이브를 잠금 해제 합니다.

## <a name="syntax"></a>구문

```
manage-bde -unlock {-recoverypassword <password>|-recoverykey <pathtoexternalkeyfile>} <drive> [-certificate {-cf pathtocertificatefile | -ct certificatethumbprint} {-pin}] [-password] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -recoverypassword | 드라이브 잠금을 해제 하는 데 복구 암호를 사용 하도록 지정 합니다. 사용할 수도 있습니다 **-rp** 이 명령의 축약된 버전으로 합니다. |
| `<password>` | 드라이브를 잠금 해제를 사용할 수 있는 복구 암호를 나타냅니다. |
| -recoverykey | 외부 복구 키 파일의 드라이브 잠금을 해제 하는 것을 지정 합니다. 사용할 수도 있습니다 **-날짜별** 이 명령의 축약된 버전으로 합니다. |
| `<pathtoexternalkeyfile>` | 드라이브를 잠금 해제를 사용할 수 있는 외부 복구 키 파일을 나타냅니다. |
| `<drive>` | 드라이브 문자를 뒤에 콜론을 나타냅니다. |
| -인증서 | 볼륨의 잠금을 해제 하기 위한 BitLocker 인증서에 대 한 로컬 사용자 인증서는 로컬 사용자 인증서 저장소에 있습니다. 사용할 수도 있습니다 **-cert** 이 명령의 축약된 버전으로 합니다. |
| -cf`<pathtocertificatefile>` | 인증서 파일의 경로입니다. |
| -ct`<certificatethumbprint>` | PIN을 선택적으로 포함할 수 있는 인증서 지문 (-핀). |
| -암호 | 볼륨의 잠금을 해제 하려면 암호에 대 한 프롬프트를 표시 합니다. 사용할 수도 있습니다 **-pw** 이 명령의 축약된 버전으로 합니다. |
| -computername | 다른 컴퓨터에서 BitLocker 보호를 수정 하는 데 manage-bde.exe를 사용 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다. |
| `<name>` | BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다. |
| -? 또는 /? | 도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다. |
| -help 또는-h | 명령 프롬프트에서 전체 도움말을 표시 합니다. |

### <a name="examples"></a>예

다른 드라이브의 백업 폴더에 저장 된 복구 키 파일을 사용 하 여 드라이브 E의 잠금을 해제 하려면 다음을 입력 합니다.

```
manage-bde –unlock E: -recoverykey F:\Backupkeys\recoverykey.bek
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [manage-bde 명령](manage-bde.md)
