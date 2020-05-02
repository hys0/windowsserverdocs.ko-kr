---
title: wbadmin delete systemstatebackup
description: 지정 된 시스템 상태 백업을 삭제 하는 wbadmin delete systemstatebackup에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 707d37cb-448d-4542-b6ac-1fc89e749788
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 12d8ba6ff24e338c6afa5556d7a60e2157156acc
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720205"
---
# <a name="wbadmin-delete-systemstatebackup"></a>wbadmin delete systemstatebackup



지정 하는 시스템 상태 백업을 삭제 합니다. 지정한 볼륨의 백업을 로컬 서버의 시스템 상태 백업이 아닌 다른 들어 있을 경우 이러한 백업은 삭제 되지 않습니다.

> [!NOTE]
> Windows Server 백업 않습니다 백업이 나 시스템 상태 백업 또는 시스템 상태 복구의 일부로 레지스트리 사용자 하이브 (HKEY_CURRENT_USER)를 복구 합니다.

이 하위 명령 사용 하 여 시스템 상태 백업을 삭제 하려면의 구성원 이어야는 **백업 운영자** 그룹 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트를 열려면 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.)



## <a name="syntax"></a>구문

```
wbadmin delete systemstatebackup
{-keepVersions:<NumberofCopies> | -version:<VersionIdentifier> | -deleteOldest}
[-backupTarget:<VolumeName>]
[-machine:<BackupMachineName>]
[-quiet]
```

> [!IMPORTANT]
> 이러한 매개 변수 중 하나만 지정 해야 합니다: **-keepVersions**, **-버전**, 또는 **-deleteOldest**합니다.

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-keepVersions|변경 하지 않으려면 최신 시스템 상태 백업의 수를 지정 합니다. 값은 양의 정수여야 합니다. 매개 변수 값은 **-keepVersions: 0** 모든 시스템 상태 백업을 삭제 합니다.|
|-version|MM/DD/YYYY에서 백업 버전 식별자를 지정 합니다.-hh: mm 형식입니다. 버전 식별자를 모르는 경우 입력 **wbadmin 버전 가져오기**합니다.</br>이 명령을 사용 하 여 단독으로 시스템 상태 백업 되는 버전을 삭제할 수 있습니다. 사용 하 여 **wbadmin 항목을 가져와** 버전 형식을 볼 수 있습니다.|
|-deleteOldest|가장 오래 된 시스템 상태 백업을 삭제합니다.|
|-backupTarget|삭제하려는 백업 스토리지 위치를 지정합니다. 디스크 백업에 대한 스토리지 위치는 드라이브 문자, 탑재 지점 또는 GUID 기반 볼륨 경로일 수 있습니다. 이 값만 로컬 컴퓨터의 하지 않은 백업 찾기 위한 지정 해야 합니다. 로컬 컴퓨터에 대 한 백업에 대 한 정보는 로컬 컴퓨터에서 백업 카탈로그에서 사용할 수 있습니다.|
|-컴퓨터|해당 시스템 상태 백업을 삭제 하려면 컴퓨터를 지정 합니다. 여러 컴퓨터에 동일한 위치에 백업 된 경우 유용 합니다. 경우에 사용 해야는 **-backupTarget** 매개 변수를 지정 합니다.|
|-quiet|사용자에 게 하위 명령 프롬프트 없이 실행 됩니다.|

## <a name="examples"></a>예

2013 년 3 월 31 일 오전 10시 생성 하 여 시스템 상태 백업을 삭제 하려면 다음을 입력 합니다.
```
wbadmin delete systemstatebackup -version:03/31/2013-10:00
```
최근 3 개를 제외한 모든 시스템 상태 백업을 삭제 하려면 다음을 입력 합니다.
```
wbadmin delete systemstatebackup -keepVersions:3
```
디스크 f에 저장 하 여 가장 오래 된 시스템 상태 백업을 삭제 하려면 다음을 입력 합니다.
```
wbadmin delete systemstatebackup -backupTarget:f -deleteOldest
```

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)