---
title: dfsrmig
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e1b6a464-6a93-4e66-9969-04f175226d8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da05aec5ca5a5634585c5f5406181c5c90ee3a30
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856944"
---
# <a name="dfsrmig"></a>dfsrmig

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

`dfsrmig` 명령 분산 파일 시스템 (DFS) 복제에 SYSvol 복제에서 복제 서비스 FRS (파일)을 마이그레이션합니다 마이그레이션 진행률에 대 한 정보를 제공 하 고 active directory Domain Services (AD DS) 개체를 수정 마이그레이션을 지원 합니다.
이 명령을 사용 하는 방법의 예 참조는 [예제](#BKMK_examples) 이 문서 뒷부분의 섹션입니다.
## <a name="syntax"></a>구문
```
dfsrmig [/SetGlobalState <state> | /GetGlobalState | /GetMigrationState | /createGlobalObjects | 
/deleteRoNtfrsMember [<read_only_domain_controller_name>] | /deleteRoDfsrMember [<read_only_domain_controller_name>] | /?]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/SetGlobalState <state>|도메인에 대 한 원하는 전역 마이그레이션 상태를 지정 된 값에 해당 하는 상태로 설정 *상태*합니다.<br /><br />마이그레이션 또는 롤백 프로세스를 진행 하려면 유효한 상태를 순환 하려면이 명령을 사용 합니다. 이 옵션을 사용 하면 시작 하 고 AD DS에 PDC 에뮬레이터에서 전역 마이그레이션 상태를 설정 하 여 마이그레이션 프로세스를 제어할 수 있습니다. PDC 에뮬레이터를 사용할 수 없는 경우이 명령은 실패 합니다.<br /><br /> 안정 된 상태에만 전역 마이그레이션 상태를 설정할 수 있습니다. 유효한 값은 *상태*, 따라서 **0** 시작 상태에 대 한 **1** 준비 상태에 대 한 **2** Redirected 상태에 대 한 및 **3** 제거 상태에 대 한 합니다.<br /><br />값을 사용 하므로, 해당 상태에서 롤백 수 없는 마이그레이션 제거 상태로 되돌릴 수 없는 **3** 에 대 한 *상태* 만 하는 경우 완벽 하 게 committd SYSvol에 대 한 DFS 복제를 사용 하 여 복제 합니다.|
|/ GetGlobalState|PDC 에뮬레이터에서 실행할 때 AD DS 데이터베이스의 로컬 복사본에서 도메인에 대 한 현재 글로벌 마이그레이션 상태를 검색 합니다.<br /><br />올바른 글로벌 마이그레이션 상태를 설정 하는 확인 하려면이 옵션을 사용 합니다. 안정적인 마이그레이션 상태 전역 마이그레이션 상태를 따라서 될 수 있습니다 결과 하는 **dfsrmig** 명령을 사용 하 여 보고서는 **/GetGlobalState** 옵션으로 설정할 수 상태에 해당는 **/SetGlobalState** 옵션입니다.<br /><br />실행 해야는 **dfsrmig** 명령과 **/GetGlobalState** PDC 에뮬레이터 에서만 옵션입니다. active directory 복제는 도메인에서 다른 도메인 컨트롤러에 전역 상태를 복제 하지만 실행 하는 경우 복제 대기 시간 불일치를 야기 수는 **dfsrmig** 명령과 **/GetGlobalState**  이외의 PDC 에뮬레이터 도메인 컨트롤러에 대 한 옵션입니다. PDC 에뮬레이터 아닌 다른 도메인 컨트롤러의 로컬 마이그레이션 상태를 확인 하려면 사용 된 **/GetMigrationState** 옵션을 사용 합니다.|
|/ GetMigrationState|도메인의 모든 도메인 컨트롤러에 대 한 현재 로컬 마이그레이션 상태를 검색 하 고 로컬 상태는 현재 글로벌 마이그레이션 상태와 일치 하는지 여부를 결정 합니다.<br /><br />모든 도메인 컨트롤러가 글로벌 마이그레이션 상태에 도달한 경우를 확인 하려면이 옵션을 사용 합니다. 출력은 **dsfrmig** 명령을 사용 하는 경우는 **/GetMigrationState** 옵션 나타냅니다 여부 현재 전역 상태에 대 한 마이그레이션 완료 되며 현재 글로벌 마이그레이션 상태에 도달 하지 하는 모든 도메인 컨트롤러에 대 한 로컬 마이그레이션 상태를 나열 합니다. 도메인 컨트롤러에 대 한 로컬 마이그레이션 상태는 현재 글로벌 마이그레이션 상태에 도달 하지 하는 도메인 컨트롤러에 대 한 전환 상태를 포함할 수 있습니다.|
|/createGlobalObjects|DFS 복제를 사용 하는 AD DS에 전역 개체 및 설정을 만듭니다.<br /><br />만들기 때문에 DFS 복제 서비스를 자동으로 이러한 AD DS 개체 및 설정을 start 상태에서 준비 된 상태를 마이그레이션하는 동안 일반적인 마이그레이션 과정에서이 옵션을 사용할 필요가 없습니다. 이 옵션을 사용 하 여 수동으로 다음과 같은 상황에서 이러한 개체 및 설정을 만들려면:<br /><br />-   **새 읽기 전용 도메인 컨트롤러를 마이그레이션하는 동안 승격 됩니다**합니다. DFS 복제 서비스는은 start 상태에서 준비 된 상태를 마이그레이션하는 동안 AD DS 개체 및 DFS 복제에 대 한 설정을 자동으로 만듭니다. 에 해당 하는 개체는 다음이 전환 후 하지만 제거 상태로 마이그레이션 전에 도메인에 새 읽기 전용 도메인 컨트롤러 승격 됩니다 새로 활성화 된 읽기 전용 도메인 컨트롤러는 AD DS에 복제 및 마이그레이션 일으키는 실패 생성 되지 않습니다.<br />-이 경우에 실행할 수 있습니다 합니다 **dfsrmig** 명령 제품을 **/createGlobalObjects** 수동으로 없는 하는 모든 읽기 전용 도메인 컨트롤러에서 개체를 만드는 옵션을 합니다. 이 명령을 실행 개체 및 DFS 복제 서비스에 대 한 설정을 이미 있는 도메인 컨트롤러는 영향을 주지 않습니다.<br />-   **DFS 복제 서비스에 대 한 전역 설정을 누락 되거나 삭제 된**합니다. 이러한 설정은 특정 도메인 컨트롤러에 대 한 누락 된 경우 도메인 컨트롤러에 대 한 준비 전환 상태에서 start 상태에서 준비 된 상태 마이그레이션 지연 됨. 이 경우 사용할 수 있습니다는 **dfsrmig** 명령에 **/createGlobalObjects** 설정을 수동으로 만드는 옵션을 합니다. **참고:** 읽기 전용 도메인 컨트롤러에 대 한 DFS 복제 서비스에 대 한 전역 AD DS 설정을 PDC 에뮬레이터에서 만들어지므로 이러한 설정은 필요가 복제 읽기 전용 도메인 컨트롤러에 DFS 복제 서비스 전에 PDC 에뮬레이터에서에 읽기 전용 도메인 컨트롤러에는 이러한 설정을 사용할 수 있습니다. 이 복제는 활성 irectory 복제 대기 시간으로 인해 발생 하는 데 시간이 걸릴 수 있습니다.|
|/deleteRoNtfrsMember [<read_only_domain_controller_name>]|지정 된 읽기 전용 도메인 컨트롤러에 해당 하는 FRS 복제에 대 한 전역 AD DS 설정을 삭제 하거나 없는 값을 지정 하는 경우 모든 읽기 전용 도메인 컨트롤러에 대 한 FRS 복제에 대 한 전역 AD DS 설정을 삭제 *read_only_ domain_controller_name*합니다.<br /><br />DFS 복제 서비스는 자동으로 이러한 AD DS 설정을 제거 상태로 Redirected 상태에서 마이그레이션하는 동안 삭제 하기 때문에 일반적인 마이그레이션 과정에서이 옵션을 사용할 필요가 없습니다. 읽기 전용 도메인 컨트롤러는 AD DS에서 이러한 설정을 삭제할 수 없으므로, PDC 에뮬레이터에는이 작업을 수행 하 고 변경 내용을 복제 읽기 전용 도메인 컨트롤러에 active directory 복제에 적용 된 대기 시간 후 합니다.<br /><br />자동 삭제 읽기 전용 도메인 컨트롤러에 실패 하 고 제거 상태로 Redirected 상태에서 마이그레이션하는 동안 긴 ime에 대 한 읽기 전용 도메인 컨트롤러를 중지 하는 경우에 AD DS 설정을 수동으로 삭제 하려면이 옵션을 사용 합니다.|
|/deleteRoDfsrMember [<read_only_domain_controller_name>]|지정 된 읽기 전용 도메인 컨트롤러에 해당 하는 DFS 복제에 대 한 전역 AD DS 설정을 삭제 하거나 없는 값을 지정 하는 경우 모든 읽기 전용 도메인 컨트롤러에 대 한 DFS 복제에 대 한 전역 AD DS 설정을 삭제 *read_only_ domain_controller_name*합니다.<br /><br />자동 삭제 읽기 전용 도메인 컨트롤러에 실패 한 읽기 전용 도메인 컨트롤러를 중지 하는 경우에 AD DS 설정을 수동으로 삭제 하려면이 옵션을 사용 하 여 롤백할 때 마이그레이션을 준비 된 상태에서 start 상태 시간입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다. 실행 중에 해당 **dfsrmig** 옵션 없이 합니다.|
## <a name="remarks"></a>설명
-   dfsrmig.exe, DFS 복제 서비스에 대 한 마이그레이션 도구는 DFS 복제 서비스를 사용 하 여 설치 됩니다.
    새 Windows Server 2008 서버에 대 한 Dcpromo.exe 설치 하 고 컴퓨터를 도메인 컨트롤러로 수준을 올릴 때 DFS 복제 서비스를 시작 합니다. Windows Server 2003에서 Windows Server 2008에서는 업그레이드 프로세스 설치 하는 서버를 업그레이드 및 DFS 복제 서비스를 시작 합니다. DFS 복제 서비스를 설치 및 시작 DFS 복제 역할 서비스를 설치할 필요가 없습니다.
-   합니다 **dfsrmig** 에서 작동 하는 도메인 컨트롤러에서 FRS에서 DFS 복제 SYSvol 마이그레이션 가능만 도구는 Windows Server 2008 도메인 기능 수준에서 실행 되는 도메인 컨트롤러에만 지원 합니다  Windows Server 2008 도메인 기능 수준입니다.
-   실행할 수는 **dfsrmig** 만들거나 AD DS를 조작 하는 작업 하지만 모든 도메인 컨트롤러에서 명령을 개체 (읽기 전용 도메인 컨트롤러)에 없는 읽기 / 쓰기 가능 도메인 컨트롤러에만 허용 됩니다.
-   실행 중인 **dfsrmig** 옵션 없이 명령 프롬프트에서 도움말을 표시 합니다.
## <a name="BKMK_examples"></a>예제
준비 전역 마이그레이션 상태를 설정 하려면 (**1**)를 마이그레이션 또는 형식 준비 된 상태에서 롤백을 시작 합니다.
```
dfsrmig /SetGlobalState 1
```
시작 하려면 글로벌 마이그레이션 상태를 설정 하려면 (**0**) 형식 시작 상태로 롤백 시작:
```
dfsrmig /SetGlobalState 0
```
전역 마이그레이션 상태를 표시 하려면 다음을 입력 합니다.
```
dfsrmig /GetGlobalState
```
일반적인 출력을 보여 주는이 예제는 **dfsrmig /GetGlobalState** 명령입니다.
```
Current DFSR global state:  Prepared 
Succeeded.
```
모든 도메인 컨트롤러에서 로컬 마이그레이션 상태 전역 마이그레이션 상태 및 로컬 상태 전역 상태가 일치 하지 않는 모든 도메인 컨트롤러에 대 한 로컬 마이그레이션 상태를 일치 하는 여부에 대 한 정보를 표시 하려면 다음을 입력 합니다.
```
dfsrmig /GetMigrationState
```
일반적인 출력을 보여 주는이 예제는 **dfsrmig /GetMigrationState** 모든 도메인 컨트롤러에서 로컬 마이그레이션 상태에는 전역 마이그레이션 상태와 일치 하는 경우 명령입니다.
```
All Domain Controllers have migrated successfully to Global state ( Prepared ).
Migration has reached a consistent state on all Domain Controllers.
Succeeded.
```
일반적인 출력을 보여 주는이 예제는 **dfsrmig /GetMigrationState** 일부 도메인 컨트롤러에서 로컬 마이그레이션 상태 전역 마이그레이션 상태를 일치 하지 않을 때 명령입니다.
```
The following Domain Controllers are not in sync with Global state ( Prepared ):
Domain Controller (Local Migration State)   DC type
=========
CONTOSO-DC2 ( start )   ReadOnly DC
CONTOSO-DC3 ( Preparing )   Writable DC
Migration has not yet reached a consistent state on all domain controllers
State information might be stale due to AD latency.
```
여기서 해당 설정이 만들어지지 않은 자동으로 마이그레이션하는 동안 도메인 컨트롤러에서 AD DS의 DFS 복제를 사용 하 여 전역 개체 및 설정을 만들거나 이러한 설정이 없는 경우 입력:
```
dfsrmig /createGlobalObjects
```
이러한 설정이 마이그레이션 프로세스에 의해 자동으로 삭제 삭제 되지 않은 경우 contoso-d c 2 라는 읽기 전용 도메인 컨트롤러에 대 한 FRS 복제에 대 한 전역 AD DS 설정을 삭제 하려면 다음을 입력 합니다.
```
dfsrmig /deleteRoNtfrsMember contoso-dc2
```
마이그레이션 프로세스에서 이러한 설정을 자동으로 삭제 되지 않은 경우 모든 읽기 전용 도메인 컨트롤러에 대 한 FRS 복제에 대 한 전역 AD DS 설정을 삭제 하려면 다음을 입력 합니다.
```
dfsrmig /deleteRoNtfrsMember
```
마이그레이션 프로세스에서 이러한 설정을 자동으로 삭제 되지 않은 경우 contoso-d c 2 라는 읽기 전용 도메인 컨트롤러에 대 한 DFS 복제에 대 한 전역 AD DS 설정을 삭제 하려면 다음을 입력 합니다.
```
dfsrmig /deleteRoDfsrMember contoso-dc2
```
마이그레이션 프로세스에서 이러한 설정을 자동으로 삭제 되지 않은 경우 모든 읽기 전용 도메인 컨트롤러에 대 한 DFS 복제에 대 한 전역 AD DS 설정을 삭제 하려면 다음을 입력 합니다.
```
dfsrmig /deleteRoDfsrMember
```
## <a name="additional-references"></a>추가 참조
[명령줄 구문 키](https://go.microsoft.com/fwlink/?LinkId=122056)

[SYSvol 마이그레이션 시리즈: 2 부 dfsrmig.exe: SYSvol 마이그레이션 도구](https://go.microsoft.com/fwlink/?LinkID=121757)
