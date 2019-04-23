---
title: 이벤트 로깅
description: Windows Admin Center (프로젝트 브라 티)에서 이벤트 로깅
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d91b92cb3bba99ae4aa96a96650a251a6df4cea5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849304"
---
# <a name="use-event-logging-in-windows-admin-center-to-gain-insight-into-management-activities-and-track-gateway-usage"></a>Windows Admin Center 이벤트 로그를 사용 하 여 관리 활동 및 추적 게이트웨이 사용량을 파악할 수

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 환경의 서버에서 수행 하 고 관리 작업을 볼 수 있도록 뿐만 아니라 Windows Admin Center 문제를 해결 하는 데 이벤트 로그를 씁니다.

## <a name="gain-insight-into-management-activities-in-your-environment-through-user-action-logging"></a>사용자 작업 로깅을 통해 사용자 환경에서 관리 활동에 대 한 정보 얻기

Windows Admin Center 로깅 작업을 수행한 사용자 환경에 있는 서버의 관리 작업에 대 한 정보를 제공 합니다 **Microsoft ServerManagementExperience** 관리 되는 이벤트 로그에 이벤트 채널 서버에서 원본 SMEGateway EventID 4000와 합니다. 사용자에 대 한 읽기 전용 서버에 액세스 하는 경우 기록 된 이벤트를 표시 하지 않습니다 Windows Admin Center 관리 서버에 대 한 작업을 기록 합니다.

기록된 된 이벤트에는 다음 정보가 포함 됩니다.

| Key           | 값                                                                                              |
|---------------|----------------------------------------------------------------------------------------------------|
| PowerShell    | 작업을 PowerShell 스크립트를 실행 하는 경우 서버에서 실행 된 PowerShell 스크립트 이름 |
| CIM           | 작업에 CIM 호출을 실행 하는 경우 서버에서 실행 된 CIM 호출                        |
| 모듈        | 도구 (또는 모듈) 작업이 실행 된 위치                                                     |
| 게이트웨이       | 작업을 실행할 Windows Admin Center 게이트웨이 컴퓨터의 이름                     |
| UserOnGateway | Windows Admin Center 게이트웨이에 액세스 하 고 작업을 실행 하는 데 사용 하는 사용자 이름                    |
| UserOnTarget  | UserOnGateway (즉, 자격 증명 "으로 관리"를 사용 하 여 서버를 사용 하 여 액세스 사용자)와 다른 경우 대상 관리 서버에 액세스 하는 데 사용 하는 사용자 이름 |
| 위임    | 부울: 대상 관리 되는 경우 게이트웨이 신뢰 하는 서버 및 사용자의 클라이언트 컴퓨터에서 위임 된 자격 증명             |
| LAPS          | 부울: 사용자가 서버를 통해 액세스 하는 경우 [LAPS](https://technet.microsoft.com/mt227395.aspx) 자격 증명                          |
| 파일          | 작업이 파일을 업로드 하는 경우 업로드 된 파일의 이름                                |

## <a name="learn-about-windows-admin-center-activity-with-event-logging"></a>이벤트 로깅 사용 하 여 Windows Admin Center 활동에 알아봅니다

Windows Admin Center 문제 해결 및 사용량 메트릭을 볼 수 있도록 게이트웨이 컴퓨터의 이벤트 채널에 게이트웨이 활동을 기록 합니다. 이러한 이벤트에 기록 되는 **Microsoft ServerManagementExperience** 이벤트 채널입니다.

[Windows Admin Center 문제 해결에 대해 알아봅니다.](troubleshooting.md)
