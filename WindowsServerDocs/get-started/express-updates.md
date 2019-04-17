---
title: Express 업데이트 2018 년 11 월에 다시 사용 하도록 설정 하는 Windows Server 2016에 대 한 업데이트
description: Windows Server 2016의 Express 업데이트에 대 한 정보를 제공합니다.
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.openlocfilehash: c48979440ab7c5cfa86aa1287b354a1e43692f48
ms.sourcegitcommit: 23e0a68e21985d709e029e7771d3c52d6815bcb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "6507858"
---
# Express 업데이트 2018 년 11 월에 다시 사용 하도록 설정 하는 Windows Server 2016에 대 한 업데이트

>Joel Frauenheim 하 여

>적용 대상: WindowsServer 2016

시작 2018 년 11 월 13 일을 사용 하 여 업데이트 화요일, Windows가 다시 게시 Express 업데이트 Windows Server 2016에 대 한 합니다. Windows Server 2016에 대 한 빠른 업데이트 후 올바르게 설치에서 업데이트를 유지 하는 중요 한 문제를 찾을 수 2017 중간에 중지 합니다. 업데이트 팀 때 보수적으로 접근 대부분의 고객은 2017 년 11 월 14 일 업데이트 ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953))가 서버 환경에 설치 하 고 되지 익스프레스 패키지를 게시 하는 데 걸린 문제는 2017 년 11 월에서에서 해결 되었습니다, 동안 문제에 영향을 받는 합니다.

WSUS 및 System Center Configuration Manager (SCCM)에 대 한 시스템 관리자가는 2018 년 11 월에에서는 한 번 다시 표시 Windows Server 2016 업데이트에 대 한 두 개의 패키지 주의 해야 할: 전체 업데이트 및 Express 업데이트 합니다. 자신의 서버 환경에 대 한 Express를 사용 하려는 시스템 관리자가 있는지 확인 하려면 장치는 2017 년 11 월 14, ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) Express 업데이트 올바르게 설치 되도록 이후 전체 업데이트 해야 합니다. 2017 년 11 월 14 일 업데이트 ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) 볼 수 있으므로 업데이트 되지 않은 모든 장치 Express 업데이트 시도 하는 경우 대역폭 및 무한 루프에서 CPU 리소스를 소비 하는 오류를 반복 합니다.  Express 업데이트를 푸시 중지 오류 루프를 중지할 최근 전체 업데이트를 푸시 하려면 시스템 관리자가 해당 상태에 대 한 수정이 됩니다.

2018 년 11 월 13 일을 사용 하 여 Express 업데이트 고객 관리 시스템 및 Windows Server 2016 끝점 간에 패키지 크기 감소는 즉시 표시 됩니다.  