---
title: wbadmin 시작 sysrecovery
description: 사용자가 지정한 매개 변수를 사용 하 여 시스템 복구 (완전 복구)를 수행 하는 wbadmin start sysrecovery에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 95b8232f-7c42-452b-838e-15b0cf6faebe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e0f1f79f35678b5c4a50022adf3413f3de217a7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829596"
---
# <a name="wbadmin-start-sysrecovery"></a>wbadmin 시작 sysrecovery



지정한 매개 변수를 사용 하 여 시스템 복구 (완전 복구)를 수행 합니다.

> [!NOTE]
> 이 하위 명령은 Windows 복구 환경 에서만 실행할 수 있으며, 기본적으로 **Wbadmin**의 사용 현황 텍스트에 나열 되지 않습니다. 자세한 내용은 windows [RE (Windows 복구 환경) 개요](https://technet.microsoft.com/library/hh825173.aspx)를 참조 하세요.

이 하위 명령으로 시스템 복구를 수행 하려면 **Backup Operators** 그룹 또는 **Administrators** 그룹의 구성원 이거나 적절 한 권한을 위임 받아야 합니다.

이 명령을 사용 하는 방법의 예제를 보려면 [예제](#BKMK_examples)합니다.

## <a name="syntax"></a>구문

```
wbadmin start sysrecovery
-version:<VersionIdentifier>
-backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>}
[-machine:<BackupMachineName>]
[-restoreAllVolumes]
[-recreateDisks]
[-excludeDisks]
[-skipBadClusterCheck]
[-quiet]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-버전|복원할 백업에 대 한 버전 식별자를 MM/DD/YYYY-HH: MM 형식으로 지정 합니다. 버전 식별자를 모르는 경우 입력 **wbadmin 버전 가져오기**합니다.|
|-backupTarget|복구 하려는 백업이 포함 된 저장소 위치를 지정 합니다. 이 매개 변수는 저장소 위치가이 컴퓨터의 백업이 일반적으로 저장 되는 위치와 다른 경우에 유용 합니다.|
|-컴퓨터|복구 하려는 컴퓨터의 이름을 지정 합니다. 이 매개 변수 같은 위치에 여러 대의 컴퓨터 백업 된 경우에 유용 합니다. 경우에 사용 해야는 **-backupTarget** 매개 변수를 지정 합니다.|
|-restoreAllVolumes|선택한 백업에서 모든 볼륨을 복구 합니다. 이 매개 변수를 지정 하지 않으면 중요 한 볼륨 (시스템 상태 및 운영 체제 구성 요소가 포함 된 볼륨)만 복구 됩니다. 이 매개 변수는 시스템 복구 중 중요 하지 않은 볼륨을 복구 해야 하는 경우에 유용 합니다.|
|-recreateDisks|백업을 만들 때 있었던 상태로 디스크 구성을 복구 합니다.</br>경고:이 매개 변수는 운영 체제 구성 요소를 호스트 하는 볼륨의 모든 데이터를 삭제 합니다. 데이터 볼륨에서 데이터를 삭제할 수도 있습니다.|
|-excludeDisks|**-RecreateDisks** 매개 변수를 사용 하 여 지정 된 경우에만 유효 하며, **wbadmin get disks**의 출력에 나열 된 것과 같이 쉼표로 구분 된 디스크 식별자 목록으로 입력 해야 합니다. 제외 된 디스크는 분할 되거나 형식이 지정 되지 않습니다. 이 매개 변수는 복구 작업을 수행 하는 동안 수정 하지 않으려는 디스크의 데이터를 유지 하는 데 도움이 됩니다.|
|-skipBadClusterCheck|복구 디스크에서 잘못 된 클러스터 정보를 확인 하는 것을 건너뜁니다. 대체 서버 또는 하드웨어로 복원 하는 경우에는이 매개 변수를 사용 하지 않는 것이 좋습니다. 언제 든 지 복구 디스크에서 수동으로 **chkdsk/b** 를 실행 하 여 잘못 된 클러스터를 확인 한 다음 파일 시스템 정보를 적절 하 게 업데이트할 수 있습니다.</br>경고: 설명 된 대로 **chkdsk** 를 실행할 때까지 복구 된 시스템에 보고 된 잘못 된 클러스터는 정확 하지 않을 수 있습니다.|
|-quiet|사용자에 게 프롬프트를 표시 하지 않고 명령을 실행 합니다.|

## <a name="examples"></a><a name=BKMK_examples></a>예와

2013 년 3 월 31 일 오전 9:00에 실행 된 백업에서 정보 복구를 시작 하려면 다음을 입력 합니다.
```
wbadmin start sysrecovery -version:03/31/2013-09:00 -backupTarget:d:
```
2013 년 4 월 30 일 오전 9:00에 실행 된 백업에서 정보 복구를 시작 하려면 servername\shared: \\: server01에 있는 공유 폴더 \\에 다음을 입력 합니다.
```
wbadmin start sysrecovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBBareMetalRecovery](https://technet.microsoft.com/library/jj902461.aspx) cmdlet