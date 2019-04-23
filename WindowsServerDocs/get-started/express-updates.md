---
title: 2018 년 11 월에 대 한 다시 사용 하도록 설정 하는 Windows Server 2016에 대 한 업데이트를 express 업데이트
description: Windows Server 2016에서 Express 업데이트에 대 한 정보를 제공합니다.
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.openlocfilehash: c48979440ab7c5cfa86aa1287b354a1e43692f48
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867444"
---
# <a name="express-updates-for-windows-server-2016-re-enabled-for-november-2018-update"></a>2018 년 11 월에 대 한 다시 사용 하도록 설정 하는 Windows Server 2016에 대 한 업데이트를 express 업데이트

>Joel Frauenheim 여

>적용 대상: Windows Server 2016

시작 2018 년 11 월 13 일 화요일의 업데이트, Windows를 다시 게시할 Express 업데이트 Windows Server 2016에 대 한 합니다. Windows Server 2016에 대 한 빠른 업데이트를 올바르게 설치할 업데이트를 유지 하는 중요 한 문제를 찾을 수 후 2017 년 중반부터에서 중지 되었습니다. 업데이트 팀 보수적인 접근 방법은 대부분의 고객은 2017 년 11 월 14 일 업데이트 해야 하도록 Express 패키지를 게시 하는 데 걸린 2017 년 11 월에에서는 문제가 수정 되어 있지만 ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) 해당 서버에 설치 환경 및 되지 문제가 영향을 받을 수 있습니다.

WSUS 및 System Center Configuration Manager (SCCM)에 대 한 시스템 관리자가 2018 년 11 월에에서 다시 한 번 표시 될 Windows Server 2016 업데이트에 대 한 두 개의 패키지 유의 해야 합니다: 전체 업데이트 및 Express 업데이트 합니다. 오프 되었는지 확인 하려면 장치는 2017 년 11 월 14 일 이후 전체 업데이트 해야 해당 서버 환경에 대 한 Express를 사용 하려면 시스템 관리자 ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) Express 업데이트를 올바르게 설치 되도록 합니다. 2017 년 11 월 14 일 업데이트 이후에 업데이트 되지 않은 모든 장치 ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) Express 업데이트 하려고 하는 경우 대역폭과 CPU 리소스가 무한 루프를 사용 하는 반복 된 오류가 표시 됩니다.  해당 상태에 대 한 업데이트 관리 Express 업데이트 푸시를 중지 하 고 오류 루프를 중지 하려면 최근 전체 업데이트를 푸시 하려면 시스템 관리자에 대 한 것입니다.

2018 년 11 월 13 일을 사용 하 여 Express 업데이트 고객 관리 시스템 및 Windows Server 2016 끝점 간의 패키지 크기를 즉시 감소를 표시 됩니다.  