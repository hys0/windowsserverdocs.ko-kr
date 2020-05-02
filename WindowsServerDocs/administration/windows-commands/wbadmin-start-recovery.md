---
title: wbadmin 복구 시작
description: 지정한 매개 변수에 따라 복구 작업을 실행 하는 wbadmin start recovery에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 52381316-a0fa-459f-b6a6-01e31fb21612
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ec116bb69dd70cb58f6cb71ccf9ccfa04dea2e54
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725883"
---
# <a name="wbadmin-start-recovery"></a>wbadmin 복구 시작

사용자가 지정한 매개 변수에 따라 복구 작업을 실행 합니다.

이 하위 명령으로 복구를 수행 하려면의 구성원 이어야는 **Backup Operators** 그룹 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. 관리자 권한 명령 프롬프트를 열려면 **시작**을 클릭 하 고 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.

## <a name="syntax"></a>구문

```
wbadmin start recovery
-version:<VersionIdentifier>
-items:{<VolumesToRecover> | <AppsToRecover> | <FilesOrFoldersToRecover>}
-itemtype:{Volume | App | File}
[-backupTarget:{<VolumeHostingBackup> | <NetworkShareHostingBackup>}]
[-machine:<BackupMachineName>]
[-recoveryTarget:{<TargetVolumeForRecovery> | <TargetPathForRecovery>}]
[-recursive]
[-overwrite:{Overwrite | CreateCopy | Skip}]
[-notRestoreAcl]
[-skipBadClusterCheck]
[-noRollForward]
[-quiet]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-version|MM/DD/YYYY에서 복구 하려면 백업 버전 식별자를 지정 합니다-hh: mm 형식입니다. 버전 식별자를 모르는 경우 입력 **wbadmin 버전 가져오기**합니다.|
|-항목|볼륨, 애플리케이션, 파일 또는 폴더를 복구 하는 쉼표로 구분 된 목록을 지정 합니다.</br>- **-Itemtype** 는 **볼륨**, 단일 볼륨에만 지정할 수 있습니다-볼륨 드라이브 문자, 볼륨 탑재 지점 또는 GUID 기반의 볼륨 이름을 제공 하 여 합니다.</br>- **-Itemtype** 은 **앱**, 만 단일 애플리케이션을 지정할 수 있습니다. 복구 하려면 Windows Server 백업 애플리케이션 등록 있어야 합니다. 값을 사용할 수도 있습니다 **ADIFM** Active Directory 설치를 복구할 수 있습니다. 자세한 내용은의 설명 부분을 참조 하십시오.</br>- **-Itemtype** 은 **파일**, 파일 또는 폴더를 지정할 수 있습니다 하지만 동일한 볼륨의 일부가 겠지요 및 동일한 상위 폴더 아래에서 사용할 수 있어야 합니다.|
|-itemtype|복구 하는 항목의 유형을 지정 합니다. 해야 **볼륨**, **앱**, 또는 **파일**합니다.|
|-backupTarget|복구하려는 백업을 포함하는 스토리지 위치를 지정합니다. 이 매개 변수는 위치는이 컴퓨터의 백업을 일반적으로 저장 된 위치에서 다른 경우에 유용 합니다.|
|-컴퓨터|복구에 대 한 백업 하려는 컴퓨터의 이름을 지정 합니다. 이 매개 변수 같은 위치에 여러 대의 컴퓨터 백업 된 경우에 유용 합니다. 것이 때 사용 되는 **-backupTarget** 매개 변수를 지정 합니다.|
|-recoveryTarget|복원 하려면 위치를 지정 합니다. 이 매개 변수는이 위치에 백업 했던 위치와 다른 경우에 유용 합니다. 볼륨, 파일 또는 애플리케이션의 복원 데도 수 있습니다. 볼륨을 복원 하는 경우에 대체 볼륨의 볼륨 드라이브 문자를 지정할 수 있습니다. 파일 또는 애플리케이션을 복원 하는 경우 대체 복구 위치를 지정할 수 있습니다.|
|재귀적|파일을 복구 하는 경우에 유효 합니다. 지정된 된 폴더에 종속 된 모든 파일 및 폴더의 파일을 복구합니다. 기본적으로 지정된 된 폴더에 직접 상주 하는 파일에만 복구 됩니다.|
|-덮어쓰기|파일을 복구 하는 경우에 유효 합니다. 이미 복구 중인 파일이 동일한 위치에 있는 경우 수행할 동작을 지정 합니다.</br>-   **Skip** 을 사용 하면 Windows Server 백업는 기존 파일을 건너뛰고 다음 파일의 복구를 계속 합니다.</br>-   **CreateCopy** 를 설정 하면 기존 파일이 수정 되지 않도록 Windows Server 백업가 기존 파일의 복사본을 만듭니다.</br>-   **Overwrite** 를 사용 하면 기존 파일을 백업에서 파일로 덮어쓰는 Windows Server 백업 발생 합니다.|
|-notRestoreAcl|파일을 복구 하는 경우에 유효 합니다. 백업에서 복구 되 고 파일의 보안 액세스 제어 목록 (Acl)을 복원 하지 하도록 지정 합니다. 기본적으로 보안 Acl이 복원 됩니다 (기본값은 **true)** 합니다. 이 매개 변수를 사용 하는 경우 파일을 복원한 위치에서 복원된 된 파일에 대 한 Acl은 상속 됩니다.|
|-skipBadClusterCheck|볼륨을 복구 하는 경우에 유효 합니다. 잘못 된 클러스터 정보에 대 한 복구 하는 디스크 검사를 생략 합니다. 하드웨어 또는 대체 서버 복구 하는 경우에이 매개 변수를 사용 하지 않는 것이 좋습니다. 명령을 수동으로 실행 **chkdsk/b** 언제 든 지 잘못 된 클러스터에 대 한이 확인 한 다음 파일 시스템 정보를 적절 하 게 업데이트를이 디스크에 있습니다.</br>중요: 를 실행할 때까지 **chkdsk** 설명 된 대로, 복구 된 시스템에 보고 된 잘못 된 클러스터 되지 않을 수 있습니다 정확 하 게 합니다.|
|-noRollForward|애플리케이션을 복구 하는 경우에 유효 합니다. 백업에서 최신 버전을 선택한 경우 애플리케이션의 이전 지정 시간 복구를 허용 합니다. 최신, 이전 지정 시간 복구 되지 않는 애플리케이션의 다른 버전에 대 한 기본 작업 수행 됩니다.|
|-quiet|사용자에 게 하위 명령 프롬프트 없이 실행 됩니다.|

## <a name="remarks"></a>설명

-   사용 하 여 특정 백업 버전에서 복구에 사용할 수 있는 항목의 목록을 보려면 **wbadmin 항목을 가져와**합니다. 백업 시 볼륨 탑재 지점 또는 드라이브 문자가 없는, 하는 경우이 하위 명령에서 볼륨을 복구에 사용 해야 하는 GUID 기반 볼륨 이름을 반환 합니다.
-   때는 **-itemtype** 은 **앱**, 의 값을 사용할 수 있습니다 **ADIFM** 에 대 한 **-항목** Active Directory 도메인 서비스에 필요한 모든 관련된 데이터를 복구 작업을 미디어에서 설치를 수행 하려면. **ADIFM** Active Directory 데이터베이스, 레지스트리 및 SYSVOL 상태의 복사본을 만들고 지정 된 위치에 해당이 정보를 저장 한 다음 **-recoveryTarget**합니다. 이 매개 변수를 사용 하 여 경우에만 **-recoveryTarget** 지정 됩니다.

>     [!NOTE]
>     Before using **wbadmin** to perform an install from media operation, you should consider using the **ntdsutil** command because **ntdsutil** only copies the minimum amount of data needed, and it uses a more secure data transport method.

## <a name="examples"></a>예

2013 년 3 월 31, 오전 9시, d: 볼륨의 사용에서 백업 복구를 실행 하려면 다음을 입력 합니다.
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume -items:d:
```
년 3 월 31, 2013에서 오전 9시, 레지스트리, 수행 된 백업 d 드라이브에 복구를 실행 하려면 다음을 입력 합니다.
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:App -items:Registry -recoverytarget:d:\
```
년 3 월 31, 2013에서 오전 9시, d:\folder 및 d:\folder, 하위 폴더에 수행 된 백업 복구를 실행 하려면 다음을 입력 합니다.
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:File -items:d:\folder -recursive
```
2013 년 3 월 31 일 오전 \\ \\9:00에 생성 된 백업 복구를 실행 하려면 \Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\, 형식:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume 
-items:\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
```
2013 년 4 월 30 일 오전 9:00에 생성 된 공유 폴더 \\ \\servername\share의 백업 복구를 실행 하려면 다음을 입력 합니다.
```
wbadmin start recovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [시작 WBFileRecovery](https://technet.microsoft.com/library/jj902457.aspx) cmdlet
-   [시작 WBHyperVRecovery](https://technet.microsoft.com/library/jj902463.aspx) cmdlet
-   [시작 WBSystemStateRecovery](https://technet.microsoft.com/library/jj902449.aspx) cmdlet
-   [시작 WBVolumeRecovery](https://technet.microsoft.com/library/jj902470.aspx) cmdlet