---
title: dfsrmig
description: Dfsrmig 명령에 대 한 참조 항목-FRS에서 DFS 복제로 SYSvol 복제를 마이그레이션하고, 마이그레이션 진행률에 대 한 정보를 제공 하 고, 마이그레이션을 지원 하기 위해 AD DS 개체를 수정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e1b6a464-6a93-4e66-9969-04f175226d8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a0329bd5829941595f9e1938f68eefb17036c132
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992716"
---
# <a name="dfsrmig"></a>dfsrmig

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

DFS 복제 서비스인 dfsrmig에 대 한 마이그레이션 도구는 DFS 복제 서비스와 함께 설치 됩니다. 이 도구는 FRS (파일 복제 서비스)에서 분산 파일 시스템 (DFS) 복제로 SYSvol 복제를 마이그레이션합니다. 또한 마이그레이션 진행률에 대 한 정보를 제공 하 고 마이그레이션을 지원 하기 위해 Active Directory Domain Services (AD DS) 개체를 수정 합니다.

## <a name="syntax"></a>구문

```
dfsrmig [/setglobalstate <state> | /getglobalstate | /getmigrationstate | /createglobalobjects |
/deleterontfrsmember [<read_only_domain_controller_name>] | /deleterodfsrmember [<read_only_domain_controller_name>] | /?]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| `/setglobalstate <state>` | *상태*에 지정 된 값에 해당 하는 도메인의 전역 마이그레이션 상태를 설정 합니다. 안정 된 상태에만 전역 마이그레이션 상태를 설정할 수 있습니다. *상태* 값은 다음과 같습니다.<ul><li>**0** -시작 상태</li><li>**1** -준비 상태</li><li>**2** -리디렉션된 상태</li><li>**3** -제거 됨 상태</li></ul> |
| /getglobalstate | PDC 에뮬레이터에서 실행할 때 AD DS 데이터베이스의 로컬 복사본에서 도메인에 대 한 현재 글로벌 마이그레이션 상태를 검색 합니다. 올바른 글로벌 마이그레이션 상태를 설정 하는 확인 하려면이 옵션을 사용 합니다.<p>**중요:** PDC 에뮬레이터 에서만이 명령을 실행 해야 합니다. |
| /getmigrationstate | 도메인의 모든 도메인 컨트롤러에 대 한 현재 로컬 마이그레이션 상태를 검색 하 고 이러한 로컬 상태가 현재 글로벌 마이그레이션 상태와 일치 하는지 여부를 확인 합니다. 모든 도메인 컨트롤러가 글로벌 마이그레이션 상태에 도달한 경우를 확인 하려면이 옵션을 사용 합니다. |
| /createglobalobjects | DFS 복제에서 사용 하는 AD DS의 전역 개체 및 설정을 만듭니다. 개체 및 설정을 수동으로 만드는 데이 옵션을 사용 해야 하는 유일한 경우는 다음과 같습니다.<ul><li>**새 읽기 전용 도메인 컨트롤러를 마이그레이션하는 동안 승격 됩니다**합니다. **준비** 된 상태로 전환 된 후에도 도메인에서 새 읽기 전용 도메인 컨트롤러의 수준을 올리는 경우 **제거** 된 상태로 마이그레이션하기 전에 새 도메인 컨트롤러에 해당 하는 개체가 만들어지지 않아 복제 및 마이그레이션이 실패 합니다.</li><li>**DFS 복제 서비스에 대 한 전역 설정이 누락 되었거나 삭제 되었습니다**. 도메인 컨트롤러에 대 한 이러한 설정이 누락 된 경우 **시작** 상태에서 **준비** 됨 상태로의 마이그레이션은 전환 **준비** 상태에서 정지 됩니다. **참고:** 때문에 읽기 전용 도메인 컨트롤러에 대 한 DFS 복제 서비스에 대 한 전역 AD DS 설정을 PDC 에뮬레이터에서 만들어지면 이러한 설정은 필요가 복제 된 읽기 전용 도메인 컨트롤러에 PDC 에뮬레이터에서 읽기 전용 도메인 컨트롤러에서 DFS 복제 서비스는 이러한 설정을 사용할 수 있습니다. Active Directory 복제 대기 시간으로 인해이 복제를 수행 하는 데 다소 시간이 걸릴 수 있습니다. |
| `/deleterontfrsmember [<read_only_domain_controller_name>]` | 지정 된 읽기 전용 도메인 컨트롤러에 해당 하는 FRS 복제에 대 한 전역 AD DS 설정을 삭제 하거나에 `<read_only_domain_controller_name>`값이 지정 되지 않은 경우 모든 읽기 전용 도메인 컨트롤러에 대 한 frs 복제에 대 한 전역 AD DS 설정을 삭제 합니다.<p>정상적인 마이그레이션 프로세스 중에는이 옵션을 사용할 필요가 없습니다. DFS 복제 서비스는 **리디렉션된** 상태에서 **제거** 상태로 마이그레이션하는 동안 자동으로 이러한 AD DS 설정을 삭제 하기 때문입니다. 읽기 전용 도메인 컨트롤러에서 자동 삭제가 실패 한 경우에만 AD DS 설정을 수동으로 삭제 하 고, **리디렉션된** 상태에서 **제거** 된 상태로 마이그레이션하는 동안 긴 ime에 대해 읽기 전용 도메인 컨트롤러를 정지 하려면이 옵션을 사용 합니다. |
| `/deleterodfsrmember [<read_only_domain_controller_name>]` | 지정 된 읽기 전용 도메인 컨트롤러에 해당 하는 DFS 복제에 대 한 전역 AD DS 설정을 삭제 하거나에 `<read_only_domain_controller_name>`값이 지정 되지 않은 경우 모든 읽기 전용 도메인 컨트롤러의 DFS 복제에 대 한 전역 AD DS 설정을 삭제 합니다.<p>이 옵션을 사용 하 여 읽기 전용 도메인 컨트롤러에서 자동 삭제가 실패 한 경우에만 AD DS 설정을 수동으로 삭제 하 고, 준비 된 상태에서 시작 상태로 마이그레이션하는 동안 오랜 시간 동안 읽기 전용 도메인 컨트롤러를 정지 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- PDC 에뮬레이터 `/setglobalstate <state>` 의 AD DS에서 전역 마이그레이션 상태를 설정 하려면 명령을 사용 하 여 마이그레이션 프로세스를 시작 하 고 제어 합니다. PDC 에뮬레이터를 사용할 수 없는 경우이 명령이 실패 합니다.

- **제거** 된 상태로의 마이그레이션은 취소할 수 없으며, 롤백할 수 없습니다. 따라서 SYSvol 복제에 대 한 DFS 복제를 사용 하도록 완전히 커밋된 경우에만 *상태* 에 대해 값 **3** 을 사용 합니다.

- 전역 마이그레이션 상태는 안정적인 마이그레이션 상태 여야 합니다.

- Active Directory 복제는 글로벌 상태를 도메인의 다른 도메인 컨트롤러에 복제 하지만 복제 대기 시간으로 인해 PDC 에뮬레이터 이외의 도메인 컨트롤러에서를 실행 `dfsrmig /getglobalstate` 하는 경우 불일치를 가져올 수 있습니다.

- 의 `dsfrmig /getmigrationstate` 출력은 현재 글로벌 상태로의 마이그레이션이 완료 되었는지 여부를 나타내며, 현재 글로벌 마이그레이션 상태에 아직 도달 하지 않은 모든 도메인 컨트롤러에 대 한 로컬 마이그레이션 상태를 나열 합니다. 도메인 컨트롤러에 대 한 로컬 마이그레이션 상태에는 현재 글로벌 마이그레이션 상태에 도달 하지 않은 도메인 컨트롤러에 대 한 전환 상태도 포함 될 수 있습니다.

- 읽기 전용 도메인 컨트롤러는 AD DS에서 설정을 삭제할 수 없습니다. PDC 에뮬레이터는이 작업을 수행 하 고 변경 내용은 active directory 복제에 대 한 적용 가능한 대기 시간 이후에 읽기 전용 도메인 컨트롤러에 복제 됩니다.

- **Dfsrmig** 명령은 Windows Server 도메인 기능 수준에서 실행 되는 도메인 컨트롤러 에서만 지원 됩니다. FRS에서 DFS 복제로의 SYSvol 마이그레이션은 해당 수준에서 작동 하는 도메인 컨트롤러 에서만 가능 하기 때문입니다.

- 실행할 수는 **dfsrmig** 만들거나 AD DS를 조작 하는 작업 하지만 모든 도메인 컨트롤러에서 명령을 개체 (읽기 전용 도메인 컨트롤러)에 없는 읽기 / 쓰기 가능 도메인 컨트롤러에만 허용 됩니다.

## <a name="examples"></a>예

전역 마이그레이션 상태를 준비 됨 (**1**)으로 설정 하 고 마이그레이션을 시작 하거나 준비 된 상태에서 롤백하려면 다음을 입력 합니다.

```
dfsrmig /setglobalstate 1
```

전역 마이그레이션 상태를 시작 (**0**)으로 설정 하 고 롤백을 시작 상태로 시작 하려면 다음을 입력 합니다.

```
dfsrmig /setglobalstate 0
```

전역 마이그레이션 상태를 표시 하려면 다음을 입력 합니다.

```
dfsrmig /getglobalstate
```

`dfsrmig /getglobalstate` 명령의 출력:

```
Current DFSR global state: Prepared
Succeeded.
```

모든 도메인 컨트롤러의 로컬 마이그레이션 상태가 전역 마이그레이션 상태와 일치 하는지 여부와 로컬 상태가 글로벌 상태와 일치 하지 않는 로컬 마이그레이션 상태가 있는지에 대 한 정보를 표시 하려면 다음을 입력 합니다.

```
dfsrmig /GetMigrationState
```

모든 도메인 컨트롤러 `dfsrmig /getmigrationstate` 의 로컬 마이그레이션 상태가 전역 마이그레이션 상태와 일치 하는 경우 명령의 출력:

```
All Domain Controllers have migrated successfully to Global state (Prepared).
Migration has reached a consistent state on all Domain Controllers.
Succeeded.
```

일부 도메인 컨트롤러 `dfsrmig /getmigrationstate` 의 로컬 마이그레이션 상태가 전역 마이그레이션 상태와 일치 하지 않을 때 명령의 출력입니다.

```
The following Domain Controllers are not in sync with Global state (Prepared):
Domain Controller (Local Migration State) DC type
=========
CONTOSO-DC2 (start) ReadOnly DC
CONTOSO-DC3 (Preparing) Writable DC
Migration has not yet reached a consistent state on all domain controllers
State information might be stale due to AD latency.
```

여기서 해당 설정이 만들어지지 않은 자동으로 마이그레이션하는 동안 도메인 컨트롤러에서 AD DS의 DFS 복제를 사용 하 여 전역 개체 및 설정을 만들거나 이러한 설정이 없는 경우 입력:

```
dfsrmig /createglobalobjects
```

이러한 설정이 마이그레이션 프로세스에 의해 자동으로 삭제 삭제 되지 않은 경우 contoso-d c 2 라는 읽기 전용 도메인 컨트롤러에 대 한 FRS 복제에 대 한 전역 AD DS 설정을 삭제 하려면 다음을 입력 합니다.

```
dfsrmig /deleterontfrsmember contoso-dc2
```

마이그레이션 프로세스에서 이러한 설정을 자동으로 삭제 되지 않은 경우 모든 읽기 전용 도메인 컨트롤러에 대 한 FRS 복제에 대 한 전역 AD DS 설정을 삭제 하려면 다음을 입력 합니다.

```
dfsrmig /deleterontfrsmember
```

마이그레이션 프로세스에서 이러한 설정을 자동으로 삭제 되지 않은 경우 contoso-d c 2 라는 읽기 전용 도메인 컨트롤러에 대 한 DFS 복제에 대 한 전역 AD DS 설정을 삭제 하려면 다음을 입력 합니다.

```
dfsrmig /deleterodfsrmember contoso-dc2
```

마이그레이션 프로세스에서 이러한 설정을 자동으로 삭제 되지 않은 경우 모든 읽기 전용 도메인 컨트롤러에 대 한 DFS 복제에 대 한 전역 AD DS 설정을 삭제 하려면 다음을 입력 합니다.

```
dfsrmig /deleterodfsrmember
```

명령 프롬프트에서 도움말을 표시 하려면 다음을 수행 합니다.

```
dfsrmig
```

```
dfsrmig /?
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](https://go.microsoft.com/fwlink/?LinkId=122056)

- [SYSvol 마이그레이션 시리즈: 2 부 dfsrmig: SYSvol 마이그레이션 도구](https://techcommunity.microsoft.com/t5/storage-at-microsoft/sysvol-migration-series-part-2-8211-dfsrmig-exe-the-sysvol/ba-p/423470)

- [Active Directory Domain Services](../../identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview.md)
