---
title: 이벤트 로깅
description: Windows 관리 센터 (프로젝트 브라 티)에서 이벤트 로깅
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d91b92cb3bba99ae4aa96a96650a251a6df4cea5
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "2074344"
---
# <a name="use-event-logging-in-windows-admin-center-to-gain-insight-into-management-activities-and-track-gateway-usage"></a>Windows 관리 센터에 로그인 하는 이벤트를 사용 하 여 관리 작업 및 추적 게이트웨이 사용에 대 한 통찰력 확보 합니다.

>적용 대상: Windows 관리 센터, Windows 관리 센터 미리 보기

Windows 관리 센터 환경에서 서버에서 수행 되는 관리 작업을 볼 수 있도록 뿐만아니라 모든 Windows 관리 센터 문제를 해결 하는데 도움이 되는 이벤트 로그에 씁니다.

## <a name="gain-insight-into-management-activities-in-your-environment-through-user-action-logging"></a>사용자 작업 로깅을 통해 환경에서 관리 작업에 대 한 통찰력을 확보 합니다.

Windows 관리 센터 EventID 4000와 관리 되는 서버의 이벤트 로그에 **Microsoft ServerManagementExperience** 이벤트 채널에 로깅 동작 하 여 사용자 환경에 서버에서 수행 되는 관리 작업에 대 한 정보를 제공 합니다. 및 SMEGateway 원본입니다. Windows 관리 센터 하므로 사용자가 읽기 전용 목적을 위해 서버를 액세스 하는 경우 기록 되는 이벤트를 볼 수 없습니다만 관리 되는 서버에 대 한 작업을 기록 합니다.

로그에 이벤트가 기록된에 다음 정보가 포함 됩니다.

| 키           | 값                                                                                              |
|---------------|----------------------------------------------------------------------------------------------------|
| PowerShell    | 작업 PowerShell 스크립트를 실행 하는 경우 서버에서 실행 된 PowerShell 스크립트 이름 |
| CIM           | 작업 CIM 호출을 실행 하는 경우 서버에서 실행 된 CIM 통화                        |
| 모듈        | 도구 (또는 모듈) 작업이 실행 된 포리스트의                                                     |
| 게이트웨이       | 작업이 실행 된 포리스트의 Windows 관리 센터 게이트웨이 컴퓨터의 이름                     |
| UserOnGateway | Windows 관리 센터 게이트웨이 액세스 하 고 작업을 실행 하는 데 사용 하는 사용자 이름                    |
| UserOnTarget  | UserOnGateway (즉, 사용자의 자격 증명 "다른 사람으로 관리"를 사용 하 여 서버를 사용 하 여 액세스)에서 다른 경우에 관리 되는 대상 서버에 액세스 하는 데 사용 하는 사용자 이름 |
| 위임    | 부울: 대상 관리 하는 경우 게이트웨이 신뢰 하는 서버 및 사용자의 클라이언트 컴퓨터에서 자격 증명 위임             |
| 랩          | 부울: 사용자 [랩](https://technet.microsoft.com/mt227395.aspx) 자격 증명을 사용 하 여 해당 서버에 액세스 하는 경우                          |
| 파일          | 작업 파일 업로드 한 경우 업로드 된 파일의 이름                                |

## <a name="learn-about-windows-admin-center-activity-with-event-logging"></a>이벤트 로깅 사용 하 여 Windows 관리 센터 활동에 대 한 설명

Windows 관리 센터 문제를 해결 하 고 사용 현황에 대 메트릭을 볼 수 있도록 게이트웨이 컴퓨터에서 이벤트 채널에 게이트웨이 작업을 기록 합니다. 이러한 이벤트는 **Microsoft ServerManagementExperience** 이벤트 채널에 기록 됩니다.

[Windows 관리 센터의 문제를 해결 하는 방법에 대 한 자세한 내용은.](troubleshooting.md)
