---
title: ksetup changepassword
description: Ksetup changepassword 명령에 대 한 참조 문서-kpasswd (키 배포 센터) 암호를 사용 하 여 로그온 한 사용자의 암호를 변경 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 283078e7-a88f-4875-90e6-f8605e6b7ea7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e49a9c0a796357c89efd3c86373c77468670176c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925507"
---
# <a name="ksetup-changepassword"></a>ksetup changepassword

키 배포 센터 (KDC) 암호 (kpasswd) 값을 사용 하 여 로그온 한 사용자의 암호를 변경 합니다. 명령의 출력은 성공 또는 실패 상태를 알려 줍니다.

명령을 실행 하 고 출력을 확인 하 여 **kpasswd** 가 설정 되어 있는지 여부를 확인할 수 있습니다 `ksetup /dumpstate` .


## <a name="syntax"></a>구문

```
ksetup /changepassword <oldpassword> <newpassword>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<oldpassword>` | 로그온 한 사용자의 기존 암호를 지정 합니다. |
| `<newpassword>` | 로그온 한 사용자의 새 암호를 지정 합니다. 이 암호는이 컴퓨터에 설정 된 모든 암호 요구 사항을 충족 해야 합니다. |

#### <a name="remarks"></a>설명

- 현재 도메인에서 사용자 계정을 찾을 수 없는 경우 사용자 계정이 있는 도메인 이름을 입력 하 라는 메시지가 표시 됩니다.

- 다음 로그온 할 때 암호 변경을 강제로 적용 하려면이 명령을 사용 하 여 별표 (*)를 사용할 수 있으므로 사용자에 게 새 암호를 입력 하 라는 메시지가 표시 됩니다.

-

### <a name="examples"></a>예

이 도메인의 컴퓨터에 현재 로그온 되어 있는 사용자의 암호를 변경 하려면 다음을 입력 합니다.

```
ksetup /changepassword Pas$w0rd Pa$$w0rd
```

Contoso 도메인에 현재 로그온 되어 있는 사용자의 암호를 변경 하려면 다음을 입력 합니다.

```
ksetup /domain CONTOSO /changepassword Pas$w0rd Pa$$w0rd
```

현재 로그온 한 사용자가 다음에 로그온 할 때 암호를 변경 하도록 하려면 다음을 입력 합니다.

```
ksetup /changepassword Pas$w0rd *
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)

- [ksetup ffstate 명령](ksetup-dumpstate.md)

- [ksetup addkpasswd 명령](ksetup-addkpasswd.md)

- [ksetup delkpasswd 명령](ksetup-delkpasswd.md)

- [ksetup ffstate 명령](ksetup-dumpstate.md)
