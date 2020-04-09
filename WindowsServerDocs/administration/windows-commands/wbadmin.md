---
title: wbadmin
description: 명령 프롬프트에서 운영 체제, 볼륨, 파일, 폴더 및 응용 프로그램을 백업 하 고 복원할 수 있는 wbadmin의 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b0b3f32-d21f-4861-84bb-b2eadbf1e7b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ca9bdc54cd77f11239d0a61cf052e7b12b02b22
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829476"
---
# <a name="wbadmin"></a>wbadmin



백업 및 명령 프롬프트에서 운영 체제, 볼륨, 파일, 폴더 및 애플리케이션을 복원할 수 있습니다.

정기적으로 예약 된 백업을 구성 하려면의 구성원 이어야는 **관리자** 그룹입니다. 이 명령 사용 하 여 다른 모든 작업을 수행 하려면의 구성원 이어야는 **Backup Operators** 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다.

실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트를 열려면 마우스 오른쪽 단추로 클릭 **Command Prompt**, 를 클릭 하 고 **관리자 권한으로 실행**.)

## <a name="subcommands"></a>하위 명령

|하위 명령|설명|
|----------|-----------|
|[Wbadmin enable backup](wbadmin-enable-backup.md)|구성 하 고 정기적으로 예약 된 백업을 사용 하도록 설정 합니다.|
|[Wbadmin disable backup](wbadmin-disable-backup.md)|매일 백업을 사용 하지 않습니다.|
|[Wbadmin start backup](wbadmin-start-backup.md)|일회성 백업을 실행합니다. 매개 변수 없이 사용 하는 경우에 일별 백업 일정의 설정을 사용 합니다.|
|[Wbadmin stop job](wbadmin-stop-job.md)|현재 실행 중인 백업이 나 복구 작업을 중지 합니다.|
|[Wbadmin get versions](wbadmin-get-versions.md)|로컬 컴퓨터에서 복구 가능한 백업의 세부 정보를 나열 하거나 다른 컴퓨터에서 다른 위치를 지정 합니다.|
|[Wbadmin get items](wbadmin-get-items.md)|백업에 포함 된 항목을 나열 합니다.|
|[Wbadmin start recovery](wbadmin-start-recovery.md)|볼륨, 애플리케이션, 파일 또는 지정 된 폴더의 복구를 실행 합니다.|
|[Wbadmin get status](wbadmin-get-status.md)|현재 실행 중인 백업이 나 복구 작업의 상태를 보여 줍니다.|
|[Wbadmin get disks](wbadmin-get-disks.md)|현재 온라인 상태의 디스크를 나열 합니다.|
|[Wbadmin start systemstaterecovery](wbadmin-start-systemstaterecovery.md)|시스템 상태 복구를 실행합니다.|
|[Wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md)|시스템 상태 백업을 실행합니다.|
|[Wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)|하나 이상의 시스템 상태 백업을 삭제합니다.|
|[Wbadmin start sysrecovery](wbadmin-start-sysrecovery.md)|전체 시스템 (최소한 모든 볼륨 운영 체제의 상태를 포함 하는)의 복구를 실행 합니다. 이 하위 명령은 Windows 복구 환경을 사용 하는 경우에 사용할 수만 있습니다.|
|[Wbadmin restore catalog](wbadmin-restore-catalog.md)|백업 카탈로그는 로컬 컴퓨터에 손상 된 경우에서 지정 된 스토리지 위치에서 백업 카탈로그를 복구 합니다.|
|[Wbadmin delete catalog](wbadmin-delete-catalog.md)|로컬 컴퓨터에서 백업 카탈로그를 삭제합니다. 이 컴퓨터에 백업 카탈로그 손상 되 고 카탈로그를 복원 하는 데 사용할 수 있는 다른 위치에 저장 된 백업이 있는 경우에이 하위 명령을 사용 합니다.|

## <a name="additional-references"></a>추가 참조

-   [백업 및 복구](https://go.microsoft.com/fwlink/?LinkID=195054)
-   [Windows PowerShell의 Windows Server 백업 Cmdlet](https://technet.microsoft.com/library/jj902428.aspx)