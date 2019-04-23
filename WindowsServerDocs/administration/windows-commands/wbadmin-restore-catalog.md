---
title: wbadmin 복원 카탈로그
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce1e24a0-821d-4353-b09d-8f82c5c4ad56
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5876a44b178025baac7ee5901cdc32c1b5d33dad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851714"
---
# <a name="wbadmin-restore-catalog"></a>wbadmin 복원 카탈로그



사용자가 지정한 저장소 위치에서 로컬 컴퓨터에 대 한 백업 카탈로그를 복구 합니다.

이 하위 명령으로 백업 카탈로그를 복구 하려면의 구성원 이어야는 **백업 운영자** 그룹 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트 마우스를 열려면 **Command Prompt**, 를 클릭 하 고 **관리자 권한으로 실행**.)

이 명령을 사용 하는 방법의 예제를 보려면 [예제](#BKMK_examples)합니다.

## <a name="syntax"></a>구문

```
wbadmin restore catalog
-backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>}
[-machine:<BackupMachineName>]
[-quiet]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-backupTarget|당시에 지점 백업을 만든 후에 시스템의 백업 카탈로그의 위치를 지정 합니다.|
|-컴퓨터|에 대 한 백업 카탈로그 복구 하려고 하는 컴퓨터의 이름을 지정 합니다. 여러 컴퓨터에 대 한 백업이 동일한 위치에 저장 된 경우 사용 합니다. 경우에 사용 해야 **-backupTarget** 지정 됩니다.|
|-quiet|사용자에 게 하위 명령 프롬프트 없이 실행 됩니다.|

## <a name="remarks"></a>설명

백업을 저장할 위치 (예: 디스크, DVD 또는 원격 공유 폴더) 손상 되거나 손실 된 경우 백업 카탈로그 복원를 사용 하 여 사용할 수 없습니다 **wbadmin 카탈로그를 삭제** 손상된 된 카탈로그를 삭제 합니다. 이 경우 만들어야 새 백업을 백업 카탈로그를 삭제 합니다.

## <a name="BKMK_examples"></a>예제

D: 디스크에 저장 된 백업에서 카탈로그를 복원 하려면 다음을 입력 합니다.
```
wbadmin restore catalog -backupTarget:d
```
공유 폴더에 저장 된 백업에서 카탈로그를 복원 하려면 \\ \\servername\share server01 유형입니다.
```
wbadmin restore catalog -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [복원 WBCatalog](https://technet.microsoft.com/library/jj902437.aspx) cmdlet