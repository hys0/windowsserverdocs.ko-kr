---
title: Windows Admin Center SDK 사례 연구-Fujitsu
description: Windows Admin Center SDK 사례 연구-Fujitsu
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 6d916920b187dd3c637644a0f40ae9f9cca72b66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814994"
---
# <a name="fujitsu-serverview-health-and-raid-extensions"></a>Fujitsu ServerView 상태 및 RAID 확장

## <a name="bringing-end-to-end-visibility-from-operating-system-to-hardware-into-windows-admin-center"></a>상태로 만들기 엔드-투-엔드 가시성, 하드웨어, 운영 체제에서 Windows Admin Center

Fujitsu은 선행 일본어 정보 및 통신 기술 업체 및 제조업체 [PRIMERGY](http://www.fujitsu.com/fts/products/computing/servers/primergy/) 하 고 [PRIMEQUEST](http://www.fujitsu.com/fts/products/computing/servers/mission-critical/) 서버 제품입니다. 합니다 [Fujitsu ServerView management](http://www.fujitsu.com/fts/products/computing/servers/primergy/management/) 하드웨어 관리에 대 한 CIM 및 PowerShell 인터페이스를 제공 하는 서버 쪽 에이전트를 포함 하는 수명 주기 관리 서버를 위한 포괄적인 도구 집합을 제공 합니다.

Fujitsu 서버 쪽 에이전트와 통신할 수 있는 CIM 및 PowerShell 인터페이스를 제공 하는 대로 Windows Admin Center 쉽게 통합할 수를 확인 합니다. Fujitsu의 개발 팀 손쉽게 에이전트에 익숙하지 않은 CIM 호출을 구현 하 고 사용 가능한 UI 구성 요소를 사용 하 여 Windows Admin Center 내에서 정보를 시각화 하는 데 수 있었습니다.

![Fujitsu 확장-상태 트리 뷰](../../media/extend-case-study-fujitsu/health-tree.png)

팀 Windows Admin Center SDK를 사용 하 여 친숙 한 년이 되 면 추가 하드웨어 정보를 노출 하는 UI를 추가 합니다. 종종 HTML 코드를 단순히 몇 줄 더 추가 되었으며 하드웨어 구성 요소에 대 한 요약 보기를 표시 하는 단일 도구에서 확장 하 고 신속 하 게 할 것 상태를 시스템 이벤트 로그와 드라이버 모니터에 대 한 자세한 보기에는 프로세서, 메모리, 팬, 전원 공급 장치, 온도 및 전압, 뷰 및 RAID 관리를 위한 추가 도구도 구분 합니다. 표 및 세부 정보 창 컨트롤을 트리 등 SDK의 사용 가능한 UI 컨트롤을 사용 하 여, 팀을 신속 하 게 UI를 빌드하고 Windows Admin Center 나머지와 매우 비슷합니다는 시각적 개체와 상호 작용 디자인을 얻을 수도 사용 하도록 설정 합니다.

![Fujitsu 확장-RAID 트리 뷰](../../media/extend-case-study-fujitsu/raid-tree.png)

![Fujitsu 확장-RAID 볼륨 보기](../../media/extend-case-study-fujitsu/raid-volumes.png)

Fujitsu와 Windows Admin Center 팀 간의 파트너 관계가 명확 하 게 값을 보여 줍니다 통합 Windows Admin Center 내에서 서버 역할과 서비스, 운영 체제 및 하드웨어 관리 엔드-투-엔드 파악 하도록 고객에 게 사용 하도록 설정 .