---
title: Windows Server 백업 명령 참조
description: 백업 명령 참조에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 03de0a65-21f0-4dd7-a3ae-251c98bbf6eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 32dfcc619fd12f4ac2e409fe8119bfa5dca225a7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936249"
---
# <a name="windows-server-backup-command-reference"></a>Windows Server 백업 명령 참조



다음 하위 명령에 대 한 **wbadmin** 명령 프롬프트에서 백업 및 복구 기능을 제공 합니다.

백업 일정을 구성 하려면의 구성원 이어야는 **관리자** 그룹입니다. 이 명령 사용 하 여 다른 모든 작업을 수행 하려면의 구성원 이어야는 **Backup Operators** 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다.

실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. 관리자 권한 명령 프롬프트를 열려면 **시작**을 클릭 하 고 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.

|하위 명령|설명|
|----------|-----------|
|[Wbadmin enable backup](wbadmin-enable-backup.md)|구성 하 고 일별 백업 일정을 활성화 합니다.|
|[Wbadmin disable backup](wbadmin-disable-backup.md)|매일 백업을 사용 하지 않습니다.|
|[Wbadmin start backup](wbadmin-start-backup.md)|일회성 백업을 실행합니다. 매개 변수 없이 사용 하는 경우에 일별 백업 일정의 설정을 사용 합니다.|
|[Wbadmin stop job](wbadmin-stop-job.md)|현재 실행 중인 백업이 나 복구 작업을 중지 합니다.|
|[Wbadmin get versions](wbadmin-get-versions.md)|로컬 컴퓨터에서 복구 가능한 백업의 세부 정보를 나열 하거나 다른 컴퓨터에서 다른 위치를 지정 합니다.|
|[Wbadmin get items](wbadmin-get-items.md)|특정 백업에 포함 된 항목을 나열 합니다.|
|[Wbadmin start recovery](wbadmin-start-recovery.md)|볼륨, 애플리케이션, 파일 또는 지정 된 폴더의 복구를 실행 합니다.|
|[Wbadmin get status](wbadmin-get-status.md)|현재 실행 중인 백업이 나 복구 작업의 상태를 보여 줍니다.|
|[Wbadmin get disks](wbadmin-get-disks.md)|현재 온라인 상태의 디스크를 나열 합니다.|
|[Wbadmin start systemstaterecovery](wbadmin-start-systemstaterecovery.md)|시스템 상태 복구를 실행합니다.|
|[Wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md)|시스템 상태 백업을 실행합니다.|
|[Wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)|하나 이상의 시스템 상태 백업을 삭제합니다.|
|[Wbadmin start sysrecovery](wbadmin-start-sysrecovery.md)|전체 시스템 (최소한 모든 볼륨 운영 체제의 상태를 포함 하는)의 복구를 실행 합니다. 이 하위 명령은 Windows 복구 환경을 사용 하는 경우에 사용할 수만 있습니다.|
|[Wbadmin restore catalog](wbadmin-restore-catalog.md)|로컬 컴퓨터의 백업 카탈로그가 손상된 경우에 지정된 스토리지 위치에서 백업 카탈로그를 복구합니다.|
|[Wbadmin delete catalog](wbadmin-delete-catalog.md)|로컬 컴퓨터에서 백업 카탈로그를 삭제합니다. 이 컴퓨터에 백업 카탈로그 손상 되 고 카탈로그를 복원 하는 데 사용할 수 있는 다른 위치에 저장 된 백업이 있는 경우에이 명령을 사용 합니다.|