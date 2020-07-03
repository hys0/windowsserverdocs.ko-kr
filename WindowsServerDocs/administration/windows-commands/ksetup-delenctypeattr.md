---
title: ksetup delenctypeattr
description: 도메인에 대 한 암호화 유형 특성을 제거 하는 ksetup delenctypeattr에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc25ef3-e271-4229-a712-72c507df55aa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5aabbb99f40d8d22189d6abccc188161b7ee2f5c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925487"
---
# <a name="ksetup-delenctypeattr"></a>ksetup delenctypeattr

도메인에 대 한 암호화 유형 특성을 제거 합니다. 성공 또는 실패 완료 시 상태 메시지가 표시 됩니다.

**Klist** 명령을 실행 하 고 출력을 확인 하 여 Kerberos TGT (티켓 허용 티켓) 및 세션 키의 암호화 유형을 볼 수 있습니다. 명령을 실행 하 여 도메인을 연결 하 고 사용 하도록 설정할 수 있습니다 `ksetup /domain <domainname>` .

## <a name="syntax"></a>구문

```
ksetup /delenctypeattr <domainname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ----------| ----------- |
| `<domainname>` | 연결을 설정 하려는 도메인 이름입니다. 정규화 된 도메인 이름 또는 corp.contoso.com 또는 contoso와 같은 간단한 형식의 이름을 사용할 수 있습니다. |

### <a name="examples"></a>예

이 컴퓨터에 설정 된 현재 암호화 유형을 확인 하려면 다음을 입력 합니다.

```
klist
```

도메인을 mit.contoso.com로 설정 하려면 다음을 입력 합니다.

```
ksetup /domain mit.contoso.com
```

도메인에 대 한 암호화 유형 특성을 확인 하려면 다음을 입력 합니다.

```
ksetup /getenctypeattr mit.contoso.com
```

Mit.contoso.com 도메인에 대 한 암호화 유형 설정 특성을 제거 하려면 다음을 입력 합니다.

```
ksetup /delenctypeattr mit.contoso.com
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [klist 명령](klist.md)

- [ksetup 명령](ksetup.md)

- [ksetup 도메인 명령](ksetup-domain.md)

- [ksetup addenctypeattr 명령](ksetup-addenctypeattr.md)

- [ksetup setenctypeattr 명령](ksetup-setenctypeattr.md)
