---
title: ksetup mapuser
description: Kerberos 주체의 이름을 계정에 매핑하는 ksetup mapuser 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 84113e6e-89ff-488a-9cd0-f14bbf23b543
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f387b8c3ff7cf7515a4f2ed9b8ea62d379332ec7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933694"
---
# <a name="ksetup-mapuser"></a>ksetup mapuser

Kerberos 보안 주체의 이름을 계정에 매핑합니다.

## <a name="syntax"></a>구문

```
ksetup /mapuser <principal> <account>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<principal>` | 모든 보안 주체 사용자의 정규화 된 도메인 이름을 지정 합니다. 예: mike@corp.CONTOSO.COM. 계정 매개 변수를 지정 하지 않으면 지정 된 보안 주체에 대 한 매핑이 삭제 됩니다. |
| `<account>` | 이 컴퓨터에 있는 계정 또는 보안 그룹 이름 (예: **게스트**, **도메인 사용자**또는 **관리자**)을 지정 합니다. 이 매개 변수를 생략 하면 지정 된 보안 주체에 대 한 매핑이 삭제 됩니다. |

#### <a name="remarks"></a>설명

- **도메인 게스트**등의 계정을 구체적으로 식별 하거나 와일드 카드 문자 (*)를 사용 하 여 모든 계정을 포함할 수 있습니다.

- 컴퓨터는 유효한 Kerberos 티켓이 있는 경우 지정 된 영역의 보안 주체를 인증 합니다.

- 외부 키 배포 센터 (KDC) 및 영역 구성이 변경 될 때마다 설정이 변경 된 컴퓨터를 다시 시작 해야 합니다.

### <a name="examples"></a>예

현재 매핑된 설정 및 기본 영역을 보려면 다음을 입력 합니다.

```
ksetup
```

Kerberos 영역 CONTOSO 내에서이 컴퓨터의 게스트 계정에 Mike Danseglio의 계정을 매핑하려면이 컴퓨터에 인증 하지 않고도 기본 제공 게스트 계정의 구성원에 대 한 모든 권한을 부여 합니다. 다음을 입력 합니다.

```
ksetup /mapuser mike@corp.CONTOSO.COM guest
```

CONTOSO의 자격 증명을 사용 하 여이 컴퓨터에 대 한 인증을 방지 하기 위해이 컴퓨터의 게스트 계정에 대 한 Mike Danseglio의 계정 매핑을 제거 하려면 다음을 입력 합니다.

```
ksetup /mapuser mike@corp.CONTOSO.COM
```

CONTOSO Kerberos 영역 내에서이 컴퓨터의 기존 계정에 Mike Danseglio의 계정을 매핑하려면 다음을 입력 합니다.

```
ksetup /mapuser mike@corp.CONTOSO.COM *
```

> [!NOTE]
> 이 컴퓨터에서 표준 사용자 및 게스트 계정만 활성 상태인 경우에는 Mike의 권한으로 설정 됩니다.

CONTOSO Kerberos 영역 내의 모든 계정을이 컴퓨터에서 이름이 같은 기존 계정에 매핑하려면 다음을 입력 합니다.

```
ksetup /mapuser * *
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)
