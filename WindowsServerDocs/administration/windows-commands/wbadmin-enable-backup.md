---
title: wbadmin 백업 사용
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0e57f8a-70fa-4c60-9754-e762e8ad8772
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d30136f7eb3ea48b8d9b0a740eb5a77e981ae3f0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362383"
---
# <a name="wbadmin-enable-backup"></a>wbadmin 백업 사용



매일 백업 일정을 만들고 사용 하도록 설정 하거나 기존 백업 일정을 수정 합니다. 매개 변수를 지정 하지 않으면 현재 예약 된 백업 설정이 표시 됩니다.

일별 백업 일정을 구성 하거나 수정 하려면 **Administrators** 또는 **backup Operators** 그룹의 구성원 이어야 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트 마우스를 열려면 **Command Prompt** 클릭 하 고 **관리자 권한으로 실행**.)

이 명령을 사용 하는 방법의 예제를 보려면 [예제](#BKMK_examples)합니다.

## <a name="syntax"></a>구문

Windows Server 2008 구문:
```
wbadmin enable backup
[-addtarget:<BackupTargetDisk>]
[-removetarget:<BackupTargetDisk>]
[-schedule:<TimeToRunBackup>]
[-include:<VolumesToInclude>]
[-allCritical]
[-quiet]
```
Windows Server 2008 r 2의 구문:
```
wbadmin enable backup
[-addtarget:<BackupTarget>]
[-removetarget:<BackupTarget>]
[-schedule:<TimeToRunBackup>]
[-include:<VolumesToInclude>]
[-nonRecurseInclude:<ItemsToInclude>]
[-exclude:<ItemsToExclude>]
[-nonRecurseExclude:<ItemsToExclude>][-systemState]
[-allCritical]
[-vssFull | -vssCopy]
[-user:<UserName>]
[-password:<Password>]
[-quiet]
```
Windows Server 2012 및 Windows Server 2012 R2 구문:
```
wbadmin enable backup
[-addtarget:<BackupTarget>]
[-removetarget:<BackupTarget>]
[-schedule:<TimeToRunBackup>]
[-include:<VolumesToInclude>]
[-nonRecurseInclude:<ItemsToInclude>]
[-exclude:<ItemsToExclude>]
[-nonRecurseExclude:<ItemsToExclude>][-systemState]
[-hyperv:<HyperVComponentsToExclude>]
[-allCritical]
[-systemState] 
[-vssFull | -vssCopy]
[-user:<UserName>]
[-password:<Password>]
[-quiet] 
[-allowDeleteOldBackups]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-addtarget|Windows Server 2008의 경우 백업에 대 한 저장소 위치를 지정 합니다. 백업의 대상을 디스크 식별자로 지정 해야 합니다 (설명 참조). 디스크는 사용 하기 전에 포맷 되며, 해당 디스크의 기존 데이터는 영구적으로 삭제 됩니다.</br>Windows Server 2008 R2 이상 버전의 경우 백업에 대 한 저장소 위치를 지정 합니다. 에서는 위치를 원격 공유\\폴더 (\\\<servername >\<sharename >\)의 디스크, 볼륨 또는 UNC (범용 명명 규칙) 경로로 지정 해야 합니다. 기본적으로 백업은 다음 위치에 저장 \\됩니다: \\ <servername> \<sharename > \WindowsImageBackup\<ComputerBackedUp >\. 디스크를 지정 하는 경우 디스크를 사용 하기 전에 형식이 지정 되 고, 해당 디스크의 기존 데이터는 영구적으로 삭제 됩니다. 공유 폴더를 지정 하는 경우에는 위치를 더 추가할 수 없습니다. 한 번에 하나의 공유 폴더만 저장소 위치로 지정할 수 있습니다.</br>중요: 원격 공유 폴더에 백업을 저장 하는 경우 동일한 폴더를 사용 하 여 동일한 컴퓨터를 다시 백업 하면 해당 백업을 덮어쓰게 됩니다. 또한 백업 작업이 실패 하는 경우 얻게 될 수 있습니다 백업이 하나도 최신 백업을 사용할 수 없습니다. 하지만 이전 백업을 덮어쓰게 됩니다. 백업을 구성 하는 원격 공유 폴더에 하위 폴더를 만들어서이 방지할 수 있습니다. 이 작업을 수행 하는 경우 하위 폴더에는 부모 폴더의 두 배 공간이 필요 합니다.</br>단일 명령에는 위치를 하나만 지정할 수 있습니다. 명령을 다시 실행 하 여 여러 볼륨 및 디스크 백업 저장소 위치를 추가할 수 있습니다.|
|-removetarget|기존 백업 일정에서 제거 하려는 저장소 위치를 지정 합니다. 위치를 디스크 식별자로 지정 해야 합니다 (설명 참조).|
|-일정|백업을 만들 시간을 지정 합니다. HH: MM 형식으로, 쉼표로 구분 되어 있습니다.|
|-포함|Windows Server 2008의 경우 백업에 포함할 볼륨 드라이브 문자, 볼륨 탑재 지점이 나 GUID 기반 볼륨 이름을 쉼표로 구분한 목록을 지정 합니다.</br>Windows Server 2008 R2and 나중에 백업에 포함할 쉼표로 구분 된 항목 목록을 지정 합니다. 여러 파일, 폴더 또는 볼륨을 포함할 수 있습니다. 볼륨 드라이브 문자, 볼륨 탑재 지점이 나 GUID 기반 볼륨 이름을 사용 하 여 볼륨 경로를 지정할 수 있습니다. GUID 기반 볼륨 이름을 사용 하는 경우 백슬래시 ()\)로 끝나야 합니다. 파일 경로를 지정할 때 파일 이름에 와일드 카드 문자 (*)를 사용할 수 있습니다.|
|-nonRecurseInclude|Windows Server 2008 R2 이상에서는 백업에 포함할 항목의 비재귀적 및 쉼표로 구분 된 목록을 지정 합니다. 여러 파일, 폴더 또는 볼륨을 포함할 수 있습니다. 볼륨 드라이브 문자, 볼륨 탑재 지점이 나 GUID 기반 볼륨 이름을 사용 하 여 볼륨 경로를 지정할 수 있습니다. GUID 기반 볼륨 이름을 사용 하는 경우 백슬래시 ()\)로 끝나야 합니다. 파일 경로를 지정할 때 파일 이름에 와일드 카드 문자 (*)를 사용할 수 있습니다. -BackupTarget 매개 변수를 사용 하는 경우에만 사용 해야 합니다.|
|-제외|Windows Server 2008 R2 이상에서는 백업에서 제외할 항목의 쉼표로 구분 된 목록을 지정 합니다. 파일, 폴더 또는 볼륨을 제외할 수 있습니다. 볼륨 드라이브 문자, 볼륨 탑재 지점이 나 GUID 기반 볼륨 이름을 사용 하 여 볼륨 경로를 지정할 수 있습니다. GUID 기반 볼륨 이름을 사용 하는 경우 백슬래시 ()\)로 끝나야 합니다. 파일 경로를 지정할 때 파일 이름에 와일드 카드 문자 (*)를 사용할 수 있습니다.|
|-nonRecurseExclude|Windows Server 2008 R2 이상에서는 백업에서 제외할 항목의 비재귀적, 쉼표로 구분 된 목록을 지정 합니다. 파일, 폴더 또는 볼륨을 제외할 수 있습니다. 볼륨 드라이브 문자, 볼륨 탑재 지점이 나 GUID 기반 볼륨 이름을 사용 하 여 볼륨 경로를 지정할 수 있습니다. GUID 기반 볼륨 이름을 사용 하는 경우 백슬래시 ()\)로 끝나야 합니다. 파일 경로를 지정할 때 파일 이름에 와일드 카드 문자 (*)를 사용할 수 있습니다.|
|-hyperv|백업에 포함 될 구성 요소에 대 한 쉼표로 구분 된 목록을 지정 합니다. 식별자는 구성 요소 이름 또는 중괄호를 포함 하거나 포함 하지 않는 구성 요소 GUID 일 수 있습니다.|
|-systemState|Windows ° 7 및 Windows Server 2008 R2 이상에서는 **-include** 매개 변수를 사용 하 여 지정한 다른 항목과 함께 시스템 상태를 포함 하는 백업을 만듭니다. 시스템 상태는 부팅 파일 (Boot.ini, NDTLDR, NTDetect.com), COM 설정을 포함 하는 Windows 레지스트리, SYSVOL (그룹 정책 및 로그온 스크립트), Active Directory 및 NTDS를 포함 합니다. 도메인 컨트롤러의 DIT 및 인증서 서비스가 설치 된 경우 인증서 저장소입니다. 서버에 설치 된 웹 서버 역할을 하는 경우 IIS 메타 디렉터리 포함 됩니다. 서버가 클러스터의 일부인 경우에도 클러스터 서비스 정보가 포함 됩니다.|
|-allCritical|모든 중요 한 볼륨 (운영 체제의 상태를 포함 하는 볼륨)는 백업에 포함 되도록 지정 합니다. 이 매개 변수는 전체 시스템 또는 시스템 상태 복구에 대 한 백업을 만드는 경우에 유용 합니다. -BackupTarget이 지정 된 경우에만 사용 해야 합니다. 그렇지 않으면 명령이 실패 합니다. 와 함께 사용할 수는 **-포함** 옵션입니다.</br>팁: 중요 한 볼륨 백업에 대 한 대상 볼륨은 로컬 드라이브 일 수 있지만 백업에 포함 된 볼륨이 될 수는 없습니다.|
|-vssFull|Windows Server 2008 R2 이상에서는 VSS (볼륨 섀도 복사본 서비스)를 사용 하 여 전체 백업을 수행 합니다. 모든 파일이 백업, 각 파일의 기록 백업 된 것을 이전 백업의 로그 문자열이 잘릴 수를 반영 하도록 업데이트 됩니다. 이 매개 변수를 사용 하지 않는 경우 wbadmin start backup은 복사 백업을 만들지만 백업 중인 파일의 기록은 업데이트 되지 않습니다.</br>주의: Windows Server 백업 이외의 제품을 사용 하 여 현재 백업에 포함 된 볼륨에 있는 응용 프로그램을 백업 하는 경우에는이 매개 변수를 사용 하지 마십시오. 이렇게 하면 백업할 데이터의 크기를 결정 하는 데 의존 하 고 있는 기록 및 전체 백업을 수행할 수 있으므로 다른 백업 제품에서 만드는 증분, 차등 또는 다른 유형의 백업이 손상 될 수 있습니다. 시간이.|
|-vssCopy|Windows Server 2008 R2 이상에서는 VSS를 사용 하 여 복사 백업을 수행 합니다. 모든 파일을 백업할 수 있지만 응용 프로그램 로그 파일 뿐 아니라는 대 한 모든 정보는 파일 변경, 삭제 및 온 위치를 유지할 백업 되는 파일의 기록을 업데이트 되지 않습니다. 이 백업 유형을 사용 해도이 복사 백업에 독립적으로 발생할 수 있는 증분 및 차등 백업의 시퀀스에는 영향을 주지 않습니다. 기본값입니다.</br>경고: 증분 또는 차등 백업 또는 복원에는 복사 백업을 사용할 수 없습니다.|
|-사용자|Windows Server 2008 R2 이상에서는 백업 저장소 대상에 대 한 쓰기 권한이 있는 사용자 (원격 공유 폴더인 경우)를 지정 합니다. 사용자는 백업 하는 컴퓨터에서 Administrators 그룹 또는 Backup Operators 그룹의 구성원 이어야 합니다.|
|-암호|Windows Server 2008 R2 이상에서는-user 매개 변수에서 제공 하는 사용자 이름에 대 한 암호를 지정 합니다.|
|-quiet|사용자에 게 하위 명령 프롬프트 없이 실행 됩니다.|
|-allowDeleteOldBackups|컴퓨터를 업그레이드 하기 전에 수행 된 모든 백업을 덮어씁니다.|

## <a name="remarks"></a>설명

디스크에 대 한 디스크 식별자 값을 보려면 **wbadmin get disks**를 입력 합니다.

## <a name="BKMK_examples"></a>예와

다음 예에서는 다양 한 백업 시나리오에서 **wbadmin enable backup** 명령을 사용 하는 방법을 보여 줍니다.

시나리오 #1
- 하드 디스크 드라이브의 백업 예약 e:, d:\mountpoint 지점 및 \\ \\? \Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
- 디스크 디스크가에 파일을 저장 합니다.
- 매일 오전 9:00에 백업을 실행 합니다. 오후 6시 사이로
  ```
  wbadmin enable backup -addtarget:DiskID -schedule:09:00,18:00 -include:e:,d:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
  ```
  시나리오 #2
- 네트워크 위치로 \\ \\d:\documents 폴더의 백업 예약 backupshare\backup1
- 도메인 CONTOSOEAST의 구성원이 고 네트워크 공유에 대 한 액세스를 인증 하는 백업 관리자 Aaren (aekel)에 대 한 네트워크 자격 증명을 사용 합니다. Aaren 암호는 *$3Hm9 ^ 5lp*입니다.
- 매일 오전 12:00에 백업을 실행 합니다. 및 오후 7:00
  ```
  wbadmin enable backup –addtarget:\\backupshare\backup1 –include: d:\documents –user:CONTOSOEAST\aekel –password:$3hM9^5lp –schedule:00:00,19:00
  ```
  시나리오 #3
- 볼륨 t: 및 폴더 d:\documents의 백업을 h:으로 예약 하 고 d:\documents\~폴더를 제외 합니다.
- 볼륨 섀도 복사본 서비스를 사용 하 여 전체 백업을 수행 합니다.
- 매일 오전 1:00에 백업을 실행 합니다.
  ```
  wbadmin enable backup –addtarget:H: –include T:,D:\documents –exclude D:\documents\~tmp –vssfull –schedule:01:00
  ```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)