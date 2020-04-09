---
title: wbadmin 시작 systemstaterecovery
description: 사용자가 지정한 백업에서 시스템 상태 복구를 수행 하는 wbadmin start systemstaterecovery에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 208b1be9-3452-4aba-bb49-46bc587fca96
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 581ad6fe3591e549c3f89e4c95d2f8ab0cde059c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829496"
---
# <a name="wbadmin-start-systemstaterecovery"></a>wbadmin 시작 systemstaterecovery



지정한 백업에서 특정 위치로 시스템 상태 복구를 수행 합니다.

> [!NOTE]
> Windows Server 백업 않습니다 백업이 나 시스템 상태 백업 또는 시스템 상태 복구의 일부로 레지스트리 사용자 하이브 (HKEY_CURRENT_USER)를 복구 합니다.

이 하위 명령으로 시스템 상태 복구를 수행 하려면 **Backup Operators** 그룹 또는 **Administrators** 그룹의 구성원 이거나 적절 한 권한을 위임 받아야 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트 마우스를 열려면 **Command Prompt**, 를 클릭 하 고 **관리자 권한으로 실행**.)

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

Windows Server 2008 구문:
```
wbadmin start systemstaterecovery
-version:<VersionIdentifier>
-showsummary
[-backupTarget:{<BackupDestinationVolume> | <NetworkSharePath>}]
[-machine:<BackupMachineName>]
[-recoveryTarget:<TargetPathForRecovery>]
[-authsysvol]
[-quiet]
```
Windows Server 2008 R2 이상에 대 한 구문:
```
wbadmin start systemstaterecovery
-version:<VersionIdentifier>
-showsummary
[-backupTarget:{<BackupDestinationVolume> | <NetworkSharePath>}]
[-machine:<BackupMachineName>]
[-recoveryTarget:<TargetPathForRecovery>]
[-authsysvol]
[-autoReboot]
[-quiet]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-버전|복원할 백업에 대 한 버전 식별자를 MM/DD/YYYY-HH: MM 형식으로 지정 합니다. 버전 식별자를 모르는 경우 입력 **wbadmin 버전 가져오기**합니다.|
|-showsummary|작업을 완료 하기 위해 다시 시작 해야 하는 마지막 시스템 상태 복구의 요약 정보를 보고 합니다. 이 매개 변수는 다른 매개 변수와 함께 사용할 수 없습니다.|
|-backupTarget|복구 하려는 백업이 포함 된 저장소 위치를 지정 합니다. 이 매개 변수는 저장소 위치가이 컴퓨터의 백업이 일반적으로 저장 되는 위치와 다른 경우에 유용 합니다.|
|-컴퓨터|복구 하려는 컴퓨터의 이름을 지정 합니다. 이 매개 변수 같은 위치에 여러 대의 컴퓨터 백업 된 경우에 유용 합니다. 경우에 사용 해야는 **-backupTarget** 매개 변수를 지정 합니다.|
|-recoveryTarget|복원할 디렉터리를 지정 합니다. 이 매개 변수는 백업이 대체 위치로 복원 되는 경우에 유용 합니다.|
|-authsysvol|사용 되는 경우 SYSVOL (시스템 볼륨 공유 디렉터리)의 정식 복원을 수행 합니다.|
|-autoReboot|시스템 상태 복구 작업이 끝날 때 시스템을 다시 시작 하도록 지정 합니다. 이 매개 변수는 원래 위치로 복구 하는 경우에만 유효 합니다. 복구 작업 후에 단계를 수행 해야 하는 경우에는이 매개 변수를 사용 하지 않는 것이 좋습니다.|
|-quiet|사용자에 게 하위 명령 프롬프트 없이 실행 됩니다.|

## <a name="examples"></a><a name=BKMK_examples></a>예와

- 03/31/2013에서 오전 9:00에 백업 시스템 상태 복구를 수행 하려면 다음을 입력 합니다.  
  ```
  wbadmin start systemstaterecovery -version:03/31/2013-09:00
  ```  
- 04/30/2013에서 오전 9:00에 백업 시스템 상태 복구를 수행 하려면 server01에 대 한 공유 리소스 \\\\servername\share에 저장 된 다음을 입력 합니다.  
  ```
  wbadmin start systemstaterecovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
  ```

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [시작 WBSystemStateRecovery](https://technet.microsoft.com/library/jj902449.aspx) cmdlet