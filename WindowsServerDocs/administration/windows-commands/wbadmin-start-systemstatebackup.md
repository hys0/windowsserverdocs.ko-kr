---
title: wbadmin 시작 systemstatebackup
description: 로컬 컴퓨터의 시스템 상태 백업을 만들고 지정 된 위치에 저장 하는 wbadmin start systemstatebackup에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 998366c1-0a64-45e6-9ed3-4c3f5b8406f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c4ca390d910a5a38919d60421091264aa56de33
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725908"
---
# <a name="wbadmin-start-systemstatebackup"></a>wbadmin 시작 systemstatebackup



로컬 컴퓨터의 시스템 상태 백업을 만들어 지정 된 위치에 저장 합니다.

> [!NOTE]
> Windows Server 백업 않습니다 백업이 나 시스템 상태 백업 또는 시스템 상태 복구의 일부로 레지스트리 사용자 하이브 (HKEY_CURRENT_USER)를 복구 합니다.

이 하위 명령으로 시스템 상태 백업을 수행 하려면 **Backup Operators** 그룹 또는 **Administrators** 그룹의 구성원 이거나 적절 한 권한을 위임 받아야 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트를 열려면 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.)

## <a name="syntax"></a>구문

```
wbadmin start systemstatebackup
-backupTarget:<VolumeName>
[-quiet]
```

### <a name="parameters"></a>매개 변수

|   매개 변수   |                                                                                                                                                                                                                      설명                                                                                                                                                                                                                      |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -backupTarget | 백업을 저장할 위치를 지정 합니다. 저장소 위치에는 드라이브 문자 또는 guid 기반 볼륨 형식 ( \\ \\? \Volume{*guid*} 형식)이 필요 합니다.</br>Windows Server 2008를 실행 하는 컴퓨터에서는 공유 네트워크 폴더에 대 한 시스템 상태 백업이 지원 되지 않습니다. 서버에서 Windows server 2008 R2 이상을 실행 하는 경우에는 명령줄 **:\\\\servername\sharedFolder\\ ** 를 사용 하 여 시스템 상태 백업을 저장할 수 있습니다. |
|    -quiet     |                                                                                                                                                                                                   사용자에 게 하위 명령 프롬프트 없이 실행 됩니다.                                                                                                                                                                                                    |

## <a name="remarks"></a>설명

시스템 상태 파일을 포함 하는 볼륨에 시스템 상태 백업을 저장 하는 방법에 대 한 자세한 내용은 Microsoft 기술 자료 문서 944530 () ([https://go.microsoft.com/fwlink/?LinkId=110439](https://go.microsoft.com/fwlink/?LinkId=110439)영문)을 참조 하십시오.

## <a name="examples"></a>예

시스템 상태 백업을 만들고 볼륨 f에 저장 하려면 다음을 입력 합니다.
```
wbadmin start systemstatebackup -backupTarget:f:
```

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBBackup](https://technet.microsoft.com/library/jj902459.aspx) cmdlet