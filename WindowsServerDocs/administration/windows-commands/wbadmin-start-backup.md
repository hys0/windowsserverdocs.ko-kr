---
title: wbadmin 백업 시작
description: 지정 된 매개 변수를 사용 하 여 백업을 만드는 wbadmin start backup에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 56f3e752-d99a-4c3d-8e97-10303c37dd78
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: afce1cd70f5481410071ff48d427be73b178744a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829656"
---
# <a name="wbadmin-start-backup"></a>wbadmin 백업 시작



지정 된 매개 변수를 사용 하 여 데이터베이스 백업을 만듭니다. 매개 변수는 지정한 예약된 된 매일 백업을 만든 경우이 하위 명령 백업이 예약 된 백업에 대 한 설정을 사용 하 여 만들어집니다. 매개 변수를 지정 하는 경우 볼륨 섀도 복사본 서비스 (VSS) 복사본 백업을 만들고 백업 되 고 있는 파일의 기록을 업데이트 되지 않습니다.

이 하위 명령으로 일회성 백업을 만들려면의 구성원 이어야는 **백업 운영자** 그룹 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트 마우스를 열려면 **Command Prompt** 클릭 하 고 **관리자 권한으로 실행**.)

이 명령을 사용 하는 방법의 예제를 보려면 [예제](#BKMK_examples)합니다.

## <a name="syntax"></a>구문

Windows ° Vista 및 Windows Server 2008에 대 한 구문:
```
wbadmin start backup
[-backupTarget:{<BackupTargetLocation> | <TargetNetworkShare>}]
[-include:<VolumesToInclude>]
[-allCritical]
[-noVerify]
[-user:<UserName>]
[-password:<Password>]
[-noinheritAcl]
[-vssFull]
[-quiet]
```
Windows ° 7 및 Windows Server 2008 R2 이상에 대 한 구문:
```
Wbadmin start backup
[-backupTarget:{<BackupTargetLocation> | <TargetNetworkShare>}]
[-include:<ItemsToInclude>]
[-nonRecurseInclude:<ItemsToInclude>]
[-exclude:<ItemsToExclude>]
[-nonRecurseExclude:<ItemsToExclude>]
[-allCritical]
[-systemState]
[-noVerify]
[-user:<UserName>]
[-password:<Password>]
[-noInheritAcl]
[-vssFull | -vssCopy] 
[-quiet]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-backupTarget|이 백업에 대 한 스토리지 위치를 지정합니다. 하드 디스크 드라이브 문자 (f:), \\\\형식의 볼륨 GUID 기반 경로,\\볼륨 {GUID} 또는 원격 공유 폴더에 대 한 UNC (범용 명명 규칙) 경로 (\\\\\<servername >\\\<sharename >\\)를 요구 합니다. 기본적으로 백업은: \\\\\<servername >\\\<sharename >\\**WindowsImageBackup**\\\<ComputerBackedUp >\\에 저장 됩니다.</br>중요: 백업을 원격 공유 폴더에 저장 하는 경우 동일한 폴더를 사용 하 여 동일한 컴퓨터를 다시 백업 하면 해당 백업을 덮어쓰게 됩니다. 또한 백업 작업이 실패 하는 경우 얻게 될 수 있습니다 백업이 하나도 최신 백업을 사용할 수 없습니다. 하지만 이전 백업을 덮어쓰게 됩니다. 백업을 구성 하는 원격 공유 폴더에 하위 폴더를 만들어서이 방지할 수 있습니다. 이렇게 하면 하위 폴더는 부모 폴더와 두 배의 공간이 필요 합니다.|
|-포함|Windows ° Vista 및 Windows Server 2008의 경우 백업에 포함할 볼륨 드라이브 문자, 볼륨 탑재 지점의 GUID 기반 볼륨 이름 또는 쉼표로 구분 된 목록을 지정 합니다. 이 매개 변수를 사용할 경우에만 **-backupTarget** 매개 변수를 사용 합니다.</br>Windows ° 7 및 Windows Server 2008 R2 이상에서는 백업에 포함할 항목의 쉼표로 구분 된 목록을 지정 합니다. 여러 파일, 폴더 또는 볼륨을 포함할 수 있습니다. 볼륨 드라이브 문자, 볼륨 탑재 지점이 나 GUID 기반 볼륨 이름을 사용 하 여 볼륨 경로를 지정할 수 있습니다. 종료 백슬래시를 삽입 하면 GUID 기반의 볼륨 이름을 사용 하는 경우 (\\). 와일드 카드 문자를 사용할 수 있습니다 (\*) 파일에 대 한 경로 지정 하는 경우 파일 이름에 있습니다. 사용할 경우에만 **-backupTarget** 매개 변수를 사용 합니다.|
|-제외|Windows ° 7 및 Windows Server 2008 R2 이상에서는 백업에서 제외할 항목의 쉼표로 구분 된 목록을 지정 합니다. 파일, 폴더 또는 볼륨을 제외할 수 있습니다. 볼륨 드라이브 문자, 볼륨 탑재 지점이 나 GUID 기반 볼륨 이름을 사용 하 여 볼륨 경로를 지정할 수 있습니다. 종료 백슬래시를 삽입 하면 GUID 기반의 볼륨 이름을 사용 하는 경우 (\\). 와일드 카드 문자를 사용할 수 있습니다 (\*) 파일에 대 한 경로 지정 하는 경우 파일 이름에 있습니다. 사용할 경우에만 **-backupTarget** 매개 변수를 사용 합니다.|
|-nonRecurseInclude|Windows ° 7 및 Windows Server 2008 R2 이상 버전의 경우 백업에 포함할 비재귀적, 쉼표로 구분 된 항목 목록을 지정 합니다. 여러 파일, 폴더 또는 볼륨을 포함할 수 있습니다. 볼륨 드라이브 문자, 볼륨 탑재 지점이 나 GUID 기반 볼륨 이름을 사용 하 여 볼륨 경로를 지정할 수 있습니다. 종료 백슬래시를 삽입 하면 GUID 기반의 볼륨 이름을 사용 하는 경우 (\\). 와일드 카드 문자를 사용할 수 있습니다 (\*) 파일에 대 한 경로 지정 하는 경우 파일 이름에 있습니다. 사용할 경우에만 **-backupTarget** 매개 변수를 사용 합니다.|
|-nonRecurseExclude|Windows ° 7 및 Windows Server 2008 R2 이상 버전의 경우 백업에서 제외할 항목의 쉼표로 구분 된 목록을 지정 합니다. 파일, 폴더 또는 볼륨을 제외할 수 있습니다. 볼륨 드라이브 문자, 볼륨 탑재 지점이 나 GUID 기반 볼륨 이름을 사용 하 여 볼륨 경로를 지정할 수 있습니다. 종료 백슬래시를 삽입 하면 GUID 기반의 볼륨 이름을 사용 하는 경우 (\\). 와일드 카드 문자를 사용할 수 있습니다 (\*) 파일에 대 한 경로 지정 하는 경우 파일 이름에 있습니다. 사용할 경우에만 **-backupTarget** 매개 변수를 사용 합니다.|
|-allCritical|모든 중요 한 볼륨 (운영 체제의 상태를 포함 하는 볼륨)는 백업에 포함 되도록 지정 합니다. 이 매개 변수는 완전 복구에 대 한 백업을 만드는 경우에 유용 합니다. 사용할 경우에만 **-backupTarget** 가 지정 하 고, 그렇지 않으면 명령이 실패 합니다. 와 함께 사용할 수는 **-포함** 옵션입니다.</br>팁: 중요 한 볼륨 백업의 대상 볼륨은 로컬 드라이브 일 수 있지만 백업에 포함 된 볼륨에는 사용할 수 없습니다.|
|-systemState|Windows ° 7 및 Windows Server 2008 R2 이상에서는 **-include** 매개 변수를 사용 하 여 지정한 다른 항목과 함께 시스템 상태를 포함 하는 백업을 만듭니다. 시스템 상태 (그룹 정책 및 로그온 스크립트) SYSVOL, Active Directory 및 NTDS COM 설정을 포함 하 여 Windows 레지스트리 부팅 파일 (Boot.ini, NDTLDR, NTDetect.com)를 포함 합니다. 도메인 컨트롤러에서 DIT 및 인증서를 저장 하는 인증서 서비스가 설치 된 경우. 서버에 설치 된 웹 서버 역할을 하는 경우 IIS 메타 디렉터리 포함 됩니다. 서버 클러스터의 일부 이면 클러스터 서비스 정보가 포함 됩니다.|
|-noVerify|이동식 미디어 (예: DVD)에 저장 되는 백업 오류에 대 한 확인 되지 않습니다 지정 합니다. 이 매개 변수를 사용 하지 않는 경우 이동식 미디어에 저장 되는 백업 오류에 대 한 확인 됩니다.|
|-사용자|백업을 원격 공유 폴더에 저장 되는 경우에 폴더에 쓰기 권한이 있는 사용자 이름을 지정 합니다.|
|-password|매개 변수에서 제공 되는 사용자 이름에 대 한 암호를 지정 **-사용자**합니다.|
|-noInheritAcl|는 **-user** 및 **-password** 매개 변수에서 제공 하는 자격 증명에 해당 하는 ACL (액세스 제어 목록) 권한을 적용 하 여 \\\<servername >\\\<sharename >\\WindowsImageBackup\\\<ComputerBackedUp >\\ (백업이 포함 된 폴더)를 \\합니다. 백업에 액세스 하 나중에 이러한 자격 증명을 사용 하거나 해야 Administrators 그룹 또는 공유 폴더를 사용 하 여 컴퓨터에서 Backup Operators 그룹의 구성원 이어야 합니다. **-NoInheritAcl** 을 사용 하지 않는 경우 원격 공유 폴더의 ACL 권한은 기본적으로 \\\<ComputerBackedUp > 폴더에 적용 되므로 원격 공유 폴더에 액세스할 수 있는 모든 사용자가 백업에 액세스할 수 있습니다.|
|-vssFull|전체 백업 볼륨 섀도 복사본 서비스 (VSS)를 사용 하 여 수행 합니다. 모든 파일이 백업, 각 파일의 기록 백업 된 것을 이전 백업의 로그 문자열이 잘릴 수를 반영 하도록 업데이트 됩니다. 이 매개 변수를 사용 하지 않는 경우 **wbadmin 백업 시작** 이유로 복사 백업 하지만 기록 파일 백업 되는 업데이트 되지 않습니다.</br>주의: Windows Server 백업 이외의 제품을 사용 하 여 현재 백업에 포함 된 볼륨에 있는 응용 프로그램을 백업 하는 경우에는이 매개 변수를 사용 하지 마십시오. 이렇게 하면 백업 하는 데 필요한 데이터의 양을 결정 하는 데 의존 하는 기록이 있으므로 다른 백업 제품에서 만드는 증분, 차등 또는 기타 유형의 백업이 중단 될 수 있으며,이로 인해 전체 백업을 불필요 하 게 수행할 수 있습니다.|
|-vssCopy|Windows 7 및 Windows Server 2008 R2 이상에서는 VSS를 사용 하 여 복사 백업을 수행 합니다. 모든 파일을 백업할 수 있지만 애플리케이션 로그 파일 뿐 아니라는 대 한 모든 정보는 파일 변경, 삭제 및 온 위치를 유지할 백업 되는 파일의 기록을 업데이트 되지 않습니다. 이 백업 유형을 사용 해도이 복사 백업에 독립적으로 발생할 수 있는 증분 및 차등 백업의 시퀀스에는 영향을 주지 않습니다. 기본값입니다.</br>경고: 증분 또는 차등 백업 또는 복원에는 복사 백업을 사용할 수 없습니다.|
|-quiet|사용자에 게 하위 명령 프롬프트 없이 실행 됩니다.|

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예에서는 다양 한 백업 시나리오에서 **wbadmin start backup** 명령을 사용 하는 방법을 보여 줍니다.

시나리오 #1
- 볼륨 e:, d:\\탑재 및 \\\\의 백업을 만듭니다.\\볼륨 {cc566d14-4410-11d9-9d93-806e6f6e6963}
- F: 볼륨에 백업을 저장합니다
  ```
  wbadmin start backup -backupTarget:f: -include:e:,d:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
  ```
  시나리오 #2
- *F:\\folder1* 및 *h:\\folder2* 를 볼륨 *d:* 에 백업 합니다.
- 시스템 상태 백업
- 복사 백업 정상적으로 예약 된 차등 백업에 영향을 받지 않도록 확인 하십시오.
  ```
  wbadmin start backup –backupTarget:d: -include:g\folder1,h:\folder2 –systemstate -vsscopy
  ```
  시나리오 #3
- 비 재귀적으로 백업 되어야 하는 *d:\\folder1* 의 일회성 백업을 수행 합니다.
- 네트워크 위치에 폴더를 백업 *\\\\backupshare\\백업 1*
- 멤버에 대 한 백업에 대 한 액세스를 제한 된 **관리자** 또는 **백업 운영자** 그룹입니다.
  ```
  wbadmin start backup –backupTarget: \\backupshare\backup1 -noinheritacl -nonrecurseinclude:d:\folder1
  ```

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
