---
title: Windows 관리 센터 SDK 사례 연구-Fujitsu
description: Windows 관리 센터 SDK 사례 연구-Fujitsu
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 9acfa873e4ce7d3e91a23abff726836f0e11ce59
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357223"
---
# <a name="fujitsu-serverview-health-and-raid-extensions"></a>Fujitsu ServerView 상태 및 RAID 확장

## <a name="bringing-end-to-end-visibility-from-operating-system-to-hardware-into-windows-admin-center"></a>운영 체제에서 하드웨어로, Windows 관리 센터에 종단 간 표시 유형

Fujitsu는 선도적인 일본 정보 및 통신 기술 회사와 [PRIMERGY](http://www.fujitsu.com/fts/products/computing/servers/primergy/) 및 [PRIMEQUEST](http://www.fujitsu.com/fts/products/computing/servers/mission-critical/) server 제품의 제조업체입니다. [Fujitsu ServerView 관리 도구 모음은](http://www.fujitsu.com/fts/products/computing/servers/primergy/management/) 하드웨어 관리용 CIM 및 PowerShell 인터페이스를 제공 하는 서버 수명 주기 관리를 위한 포괄적인 도구 집합을 제공 합니다.

Fujitsu는 서버 쪽 에이전트와 통신할 수 있는 CIM 및 PowerShell 인터페이스를 제공 하는 Windows 관리 센터와 쉽게 통합할 수 있는 기회를 살펴보았습니다. Fujitsu의 개발 팀은 사용 가능한 UI 구성 요소를 사용 하 여 Windows 관리 센터 내의 정보를 시각화 하 고 에이전트에 익숙한 CIM 호출을 쉽게 구현할 수 있었습니다.

![Fujitsu 확장-상태 트리 뷰](../../media/extend-case-study-fujitsu/health-tree.png)

Windows 관리 센터 SDK에 대해 잘 알고 있는 경우 추가 하드웨어 정보를 노출 하는 UI를 추가 하는 것은 종종 몇 줄의 HTML 코드 이며, 단일 도구에서 신속 하 게 확장 하 여 하드웨어 구성 요소에 대 한 요약 보기를 표시할 수 있었습니다. 상태, 시스템 이벤트 로그에 대 한 상세 보기, 드라이버 모니터, 프로세서, 메모리, 팬, 전원 공급 장치, 온도 및 전압 및 RAID 관리용 추가 도구에 대 한 별도의 보기입니다. 트리, 그리드 및 세부 정보 창 컨트롤과 같은 SDK에서 제공 되는 UI 컨트롤을 사용 하면 팀에서 UI를 신속 하 게 작성 하 고 Windows 관리 센터의 나머지 부분과 매우 유사한 시각적 및 상호 작용 디자인을 구현할 수 있습니다.

![Fujitsu 확장-RAID 트리 보기](../../media/extend-case-study-fujitsu/raid-tree.png)

![Fujitsu 확장-RAID 볼륨 보기](../../media/extend-case-study-fujitsu/raid-volumes.png)

Fujitsu와 Windows 관리 센터 팀 간의 파트너 관계는 Windows 관리 센터 내에서 통합의 가치를 명확 하 게 보여 주며, 고객이 서버 역할 및 서비스, 운영 체제 및 하드웨어 관리에 대 한 종단 간 통찰력을 가질 수 있도록 합니다. .