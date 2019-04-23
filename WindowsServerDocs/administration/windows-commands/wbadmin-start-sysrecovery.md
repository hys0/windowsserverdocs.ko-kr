---
title: wbadmin 시작 sysrecovery
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95b8232f-7c42-452b-838e-15b0cf6faebe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e8e0ff114d09d70b9e50e8c4ea6af6330c74128c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847164"
---
# <a name="wbadmin-start-sysrecovery"></a>wbadmin 시작 sysrecovery



지정 된 매개 변수를 사용 하 여 (bare metal recovery) 시스템에서 복구를 수행 합니다.

> [!NOTE]
> 이 하위 명령은 Windows 복구 환경 에서만에서 실행할 수 있습니다 및 기본 사용법 텍스트에 나열 되지 않습니다 **Wbadmin**합니다. 자세한 내용은 [Windows 복구 환경 (Windows RE) 개요](https://technet.microsoft.com/library/hh825173.aspx)합니다.

이 하위 명령 사용 하 여 시스템 복구를 수행 하려면의 구성원 이어야 합니다 **Backup Operators** 그룹 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다.

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

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-버전|MM/DD/YYYY에서 복구 하려면 백업에 대 한 버전 식별자를 지정 합니다-hh: mm 형식입니다. 버전 식별자를 모르는 경우 입력 **wbadmin 버전 가져오기**합니다.|
|-backupTarget|복구 하려는 백업을 포함 하는 저장소 위치를 지정 합니다. 이 매개 변수는 저장소 위치는이 컴퓨터의 백업을 일반적으로 저장 된 위치에서 다른 경우에 유용 합니다.|
|-컴퓨터|복구 하려는 컴퓨터의 이름을 지정 합니다. 이 매개 변수 같은 위치에 여러 대의 컴퓨터 백업 된 경우에 유용 합니다. 경우에 사용 해야는 **-backupTarget** 매개 변수를 지정 합니다.|
|-restoreAllVolumes|선택한 백업에서 모든 볼륨을 복구합니다. 이 매개 변수를 지정 하지 않으면 중요 한 볼륨 (시스템 상태 및 운영 체제 구성 요소를 포함 하는 볼륨)이 복구 됩니다. 이 매개 변수를 시스템 복구 하는 동안 중요 하지 않은 볼륨을 복구 해야 하는 경우에 유용 합니다.|
|-recreateDisks|디스크 구성의 백업이 생성 될 때 존재 하는 상태로 복구 합니다.</br>경고: 이 매개 변수는 호스트 운영 체제 구성 요소에 해당 볼륨의 모든 데이터를 삭제합니다. 데이터 볼륨에서 데이터를 삭제할 수도 있습니다.|
|-excludeDisks|지정 된 경우에 유효 합니다 **-recreateDisks** 매개 변수 및 디스크 식별자의 쉼표로 구분 된 목록으로 입력 해야 합니다 (출력에 나열 된 **wbadmin get 디스크**). 제외 된 디스크 분할 되지 않거나 서식이 지정 됩니다. 이 매개 변수는 복구 작업 중에 수정 하지 않으려면 디스크에서 데이터를 유지 하는 데 도움이 됩니다.|
|-skipBadClusterCheck|잘못 된 클러스터 정보에 대 한 복구 디스크 검사를 생략 합니다. 하드웨어 또는 대체 서버를 복원 하는 경우이 매개 변수를 사용 하지 않는 것이 좋습니다. 수동으로 실행할 수 있습니다 **chkdsk/b** 에 복구 디스크 언제 든 지 잘못 된 클러스터에 대 한이 확인 하 고 다음 파일 시스템 정보를 적절 하 게 업데이트 합니다.</br>경고: 실행할 때 까지는 **chkdsk** 설명 했 듯이, 잘못 된 클러스터 복구 된 시스템에 보고 되지 않을 수 있습니다 정확 하 게 합니다.|
|-quiet|사용자에 게 명령 프롬프트 없이 실행 됩니다.|

## <a name="BKMK_examples"></a>예제

오전 9 시 2013 년 3 월 31 일에 실행 된 백업에서 정보를 복구 하려면 드라이브 d: 이며 형식에 있습니다.
```
wbadmin start sysrecovery -version:03/31/2013-09:00 -backupTarget:d:
```
오전 9 시 2013 년 4 월 30에서 실행 된 백업에서 정보를 복구 하려면 공유 폴더에 있는 \\ \\servername\shared: server01를 입력 합니다.
```
wbadmin start sysrecovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get-WBBareMetalRecovery](https://technet.microsoft.com/library/jj902461.aspx) cmdlet