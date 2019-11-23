---
title: wbadmin get 항목
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27d08ce3-6e06-4260-b264-fc1bde132d09
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c3cc532381321655bbd3d5549b3c9b1896b9280
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362408"
---
# <a name="wbadmin-get-items"></a>wbadmin get 항목



특정 백업에 포함 된 항목을 나열 합니다.

이 하위 명령을 사용 하려면의 구성원 이어야는 **Backup Operators** 그룹 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트 마우스를 열려면 **Command Prompt** 클릭 하 고 **관리자 권한으로 실행**.)

이 명령을 사용 하는 방법의 예제를 보려면 [예제](#BKMK_examples)합니다.

## <a name="syntax"></a>구문

```
wbadmin get items
-version:<VersionIdentifier>
[-backupTarget:{<BackupDestinationVolume> | <NetworkSharePath>}]
[-machine:<BackupMachineName>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-버전|MM/DD/YYYY에서 백업 버전을 지정 합니다.-hh: mm 형식입니다. 버전 정보를 모르는 경우 입력 **wbadmin 버전 가져오기**합니다.|
|-backupTarget|세부 정보 하려는 백업을 포함 하는 저장소 위치를 지정 합니다. 해당 대상 위치에 저장 된 백업 목록에 사용 됩니다. 백업 대상 위치는 로컬로 연결 된 디스크 드라이브 또는 원격 공유 폴더 될 수 있습니다. 경우 **wbadmin 항목을 가져와**실행 백업을 만든 동일한 컴퓨터에서이 매개 변수가 필요 하지 않습니다. 그러나 다른 컴퓨터에서 만든 백업에 대 한 정보를 가져오려면이 매개 변수가 필요 합니다.|
|-컴퓨터|에 대 한 정보를 백업 하는 컴퓨터의 이름을 지정 합니다. 여러 대의 컴퓨터는 같은 위치에 백업 하는 경우 유용 합니다. 경우에 사용 해야 **-backupTarget** 지정 됩니다.|

## <a name="BKMK_examples"></a>예와

항목을 나열 하려면 형식 오전 9 시에 2013 년 3 월 31 일에 실행 된 백업에서:
```
wbadmin get items -version:03/31/2013-09:00
```
항목을 나열 하려면 백업에서 오전 9시 2013 년 4 월 30 일에 실행 된 server01의 \\\\servername\share에 저장 하 고 다음을 입력 합니다.
```
wbadmin get items -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get WBBackupSet](https://technet.microsoft.com/library/jj902473.aspx) cmdlet