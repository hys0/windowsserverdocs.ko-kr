---
title: Windows 관리 센터 SDK 사례 연구-Fujitsu
description: Windows 관리 센터 SDK 사례 연구-Fujitsu
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 6d916920b187dd3c637644a0f40ae9f9cca72b66
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "2052377"
---
# <a name="fujitsu-serverview-health-and-raid-extensions"></a>Fujitsu ServerView 상태 및 RAID 확장

## <a name="bringing-end-to-end-visibility-from-operating-system-to-hardware-into-windows-admin-center"></a>Windows 관리 센터에 끝-표시 유형, 하드웨어, 운영 체제에서로 가져오기

Fujitsu는 표기할 때 앞쪽 일본어 정보 및 통신 기술 회사 및 [PRIMERGY](http://www.fujitsu.com/fts/products/computing/servers/primergy/) 및 [PRIMEQUEST](http://www.fujitsu.com/fts/products/computing/servers/mission-critical/) 서버 제품의 제조업체는 합니다. [Fujitsu ServerView 관리 제품군을 사용](http://www.fujitsu.com/fts/products/computing/servers/primergy/management/) 하는 포괄적인 도구 집합을 제공 서버에 대 한 하드웨어 관리를 위한 CIM 및 PowerShell 인터페이스를 제공 하는 서버쪽 에이전트를 포함 하 여 수명 주기 관리 합니다.

Fujitsu 쉽게 서버쪽 에이전트와 통신할 수 있는 CIM 및 PowerShell 인터페이스를 제공 하는 대로 Windows 관리 센터와 통합할 수 있을 것입니다. Fujitsu에서 개발팀 쉽게 에이전트에 게 익숙한 시점의 CIM 통화를 구현 하 고 사용할 수 있는 UI 구성 요소를 사용 하 여 Windows 관리 센터 내에서 정보를 시각화 하는 작업을 수 있었습니다.

![Fujitsu 확장-상태 트리 보기](../../media/extend-case-study-fujitsu/health-tree.png)

HTML 코드를 단순히 몇 줄 더 추가 힘든 추가 하드웨어 정보를 노출 하는 UI 추가 (영문) 및 하드웨어 구성 요소에 대 한 요약 보기를 표시 하는 단일 도구에서 확장을 신속 하 게 수 있었던 후 Windows 관리 센터 SDK에 익숙한, 팀에서 변경 되었습니다. 상태, 시스템 이벤트 로그, 드라이버 모니터에 대 한 상세 보기에는 프로세서, 메모리, 팬, 전원 공급 장치, 온도 및 전압, 보기 및 RAID 관리를 위한 추가 도구인도 분리 합니다. 눈금 및 세부 정보 창 컨트롤을 트리 같은 SDK에서 사용할 수 있는 UI 컨트롤을 사용 하 여, 신속 하 게 UI를 구성 하 고도 Windows 관리 센터의 나머지 기능과 매우 유사 표시 및 상호작용 디자인을 달성 하는 팀을 사용 하도록 설정 합니다.

![Fujitsu 확장-RAID 트리 보기](../../media/extend-case-study-fujitsu/raid-tree.png)

![Fujitsu 확장-RAID 볼륨 보기](../../media/extend-case-study-fujitsu/raid-volumes.png)

Fujitsu 및 Windows 관리 센터 팀 간 파트너 관계 명확 하 게 값이 표시의 통합 Windows 관리 센터 내에서 서버 역할 및 서비스, 운영 체제 및 하드웨어 관리에 대 한 끝-한 정보를 포함 하는 고객을 사용 하도록 설정 .