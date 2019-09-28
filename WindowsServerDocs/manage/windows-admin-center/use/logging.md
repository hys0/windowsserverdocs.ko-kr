---
title: 이벤트 로깅
description: Windows 관리 센터에서 이벤트 로깅 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 012c2229fb29aa711d9887f28859e09bcf71c14a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356874"
---
# <a name="use-event-logging-in-windows-admin-center-to-gain-insight-into-management-activities-and-track-gateway-usage"></a>Windows 관리 센터에서 이벤트 로깅을 사용 하 여 관리 활동에 대 한 통찰력 확보 및 게이트웨이 사용 추적

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows 관리 센터는 이벤트 로그를 기록 하 여 사용자 환경의 서버에서 수행 되는 관리 작업 뿐 아니라 Windows 관리 센터 문제를 해결 하는 데 도움을 줍니다.

## <a name="gain-insight-into-management-activities-in-your-environment-through-user-action-logging"></a>사용자 작업 로깅을 통해 사용자 환경에서 관리 활동에 대 한 통찰력 얻기

Windows 관리 센터는 관리 되는 서버의 이벤트 로그에 있는 **Microsoft ServerManagementExperience** 이벤트 채널에 작업을 기록 하 여 사용자 환경의 서버에서 수행 되는 관리 작업에 대 4000 한 통찰력을 제공 합니다. 및 원본 SMEGateway. Windows 관리 센터는 관리 되는 서버에 대 한 작업만 로깅합니다. 따라서 사용자가 읽기 전용으로 서버에 액세스 하는 경우 기록 되는 이벤트는 표시 되지 않습니다.

기록 된 이벤트에는 다음 정보가 포함 됩니다.

| Key           | 값                                                                                              |
|---------------|----------------------------------------------------------------------------------------------------|
| PowerShell    | 작업에서 PowerShell 스크립트를 실행 한 경우 서버에서 실행 된 PowerShell 스크립트 이름 |
| CIM           | 작업에서 CIM 호출을 실행 한 경우 서버에서 실행 된 CIM 호출                        |
| 모듈        | 작업이 실행 된 도구 (또는 모듈)                                                     |
| 게이트웨이       | 작업이 실행 된 Windows 관리 센터 게이트웨이 컴퓨터의 이름입니다.                     |
| UserOnGateway | Windows 관리 센터 게이트웨이에 액세스 하 고 작업을 실행 하는 데 사용 되는 사용자 이름입니다.                    |
| UserOnTarget  | UserOnGateway와 다른 경우 (예: "다른 이름으로 관리" 자격 증명을 사용 하 여 서버를 사용 하 여 액세스 한 사용자) 대상 관리 되는 서버에 액세스 하는 데 사용 되는 사용자 이름 |
| 위임    | 부울: 대상 관리 서버가 게이트웨이를 신뢰 하 고 자격 증명이 사용자의 클라이언트 컴퓨터에서 위임 된 경우             |
| LAPS          | 부울: 사용자가 [LAPS](https://technet.microsoft.com/mt227395.aspx) 자격 증명을 사용 하 여 서버에 액세스 한 경우                          |
| 파일          | 파일이 업로드 된 경우 업로드 된 파일의 이름입니다.                                |

## <a name="learn-about-windows-admin-center-activity-with-event-logging"></a>이벤트 로깅을 사용 하 여 Windows 관리 센터 작업에 대 한 자세한 정보

Windows 관리 센터는 게이트웨이 컴퓨터의 이벤트 채널에 게이트웨이 작업을 기록 하 여 문제를 해결 하 고 사용량에 대 한 메트릭을 볼 수 있도록 합니다. 이러한 이벤트는 **Microsoft ServerManagementExperience** 이벤트 채널에 기록 됩니다.

[Windows 관리 센터 문제 해결에 대해 자세히 알아보세요.](troubleshooting.md)
