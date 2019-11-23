---
title: wbadmin get 버전
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b986acc4-d083-4d32-9434-862314ed5e97
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b7ba0749c8ef347e27590bde4eed7bbcf25af7e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362365"
---
# <a name="wbadmin-get-versions"></a>wbadmin get 버전



로컬 컴퓨터 또는 다른 컴퓨터에 저장 되어 있는 사용 가능한 백업에 대 한 세부 정보를 나열 합니다. 이 하위 매개 변수 없이 사용 되 면 해당 백업을 사용할 수 없는 경우에 로컬 컴퓨터의 모든 백업을 나열 합니다. 백업에 제공 되는 세부 백업 시간, 백업 저장소 위치, 버전 식별자를 포함 (에 필요한는 **wbadmin 항목을 가져올** 하위 명령 및 복구를 수행), 및 유형의 복구를 수행할 수 있습니다.

이 하위 명령을 사용 하 여 사용 가능한 백업에 대 한 세부 정보를 가져오려면의 구성원 이어야는 **Backup Operators** 그룹 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트를 열려면 **Command Prompt** 클릭 하 고 **관리자 권한으로 실행**.)

이 명령을 사용 하는 방법의 예제를 보려면 [예제](#BKMK_examples)합니다.

## <a name="syntax"></a>구문

```
wbadmin get versions
[-backupTarget:{<BackupTargetLocation> | <NetworkSharePath>}]
[-machine:BackupMachineName]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-backupTarget|백업에 대 한 세부 정보를 포함 하는 저장소 위치를 지정 합니다. 해당 대상 위치에 저장 된 백업 목록에 사용 됩니다. 백업 대상 위치는 로컬로 연결 된 디스크 드라이브, 볼륨, 원격 공유 폴더, DVD 드라이브와 같은 이동식 미디어 또는 기타 광학 미디어 될 수 있습니다. 경우 **wbadmin 버전 가져오기** 실행 백업을 만든 동일한 컴퓨터에서이 매개 변수가 필요 하지 않습니다. 그러나 다른 컴퓨터에서 만든 백업에 대 한 정보를 가져오려면이 매개 변수가 필요 합니다.|
|-컴퓨터|컴퓨터에 대 한 백업 세부 정보를 지정 합니다. 여러 컴퓨터의 백업이 동일한 위치에 저장 되는 경우 사용 합니다. 경우에 사용 해야 **-backupTarget** 지정 됩니다.|

## <a name="remarks"></a>설명

특정 백업에서 복구에 사용할 수 있는 목록 항목을 사용 하 여 **wbadmin 항목을 가져와**합니다.

## <a name="BKMK_examples"></a>예와

H 볼륨에 저장 되어 있는 사용 가능한 백업 목록을 보려면 다음을 입력 합니다.
```
wbadmin get versions -backupTarget:h:
```
원격 공유 폴더 \\\\servername\share에 저장 된 사용 가능한 백업 목록을 보려면 컴퓨터 server01에 대해 다음을 입력 합니다.
```
wbadmin get versions -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get WBBackupTarget](https://technet.microsoft.com/library/jj902447.aspx) cmdlet